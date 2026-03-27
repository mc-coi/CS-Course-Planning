# Day 26: Enemy AI State Machine

**Learning Target:** Create enemy AI with state machines (Patrol, Chase, Attack) that transition based on player proximity.

### Key Concepts

- **AI State Machine:** Enemies cycle through behaviors (Patrol, Chase, Attack)
- **Patrol State:** Moving along a fixed path
- **Chase State:** Following the player when nearby
- **Attack State:** Attacking when in range
- **Detection Range:** Distance at which enemy notices player
- **Attack Range:** Distance at which enemy can attack
- **Cooldown:** Time between attacks
- **Vector3.Distance():** Calculating distance between two positions

### Content

Good enemy AI feels natural and challenging. A state machine makes this organized:

**Patrol:** Enemy walks back and forth
**Chase:** When player is nearby, enemy follows
**Attack:** When in range, enemy attacks

Each state has its own logic and transition rules.

**Distance Calculation:**
```csharp
float distance = Vector3.Distance(enemyPos, playerPos);
if (distance < detectionRange)
    currentState = EnemyState.Chase;
```

**Attack Cooldown:**
```csharp
if (Time.time > lastAttackTime + attackCooldown)
{
    Attack();
    lastAttackTime = Time.time;
}
```

### Code Examples

```csharp
using UnityEngine;

public enum EnemyState { Patrol, Chase, Attack, Dead }

public class EnemyAI : MonoBehaviour
{
    [Header("State Settings")]
    public float detectionRange = 10f;
    public float attackRange = 2f;
    public float patrolSpeed = 2f;
    public float chaseSpeed = 4f;

    [Header("Attack Settings")]
    public int attackDamage = 10;
    public float attackCooldown = 1.5f;

    [Header("References")]
    public Transform player;
    private Health health;
    private Rigidbody rb;
    private float lastAttackTime = 0f;
    private EnemyState currentState = EnemyState.Patrol;
    private Vector3 patrolStartPos;
    private Vector3 patrolEndPos;
    private bool movingRight = true;

    void Start()
    {
        health = GetComponent<Health>();
        rb = GetComponent<Rigidbody>();
        patrolStartPos = transform.position;
        patrolEndPos = transform.position + Vector3.right * 5f;
    }

    void Update()
    {
        if (!health.IsAlive())
        {
            currentState = EnemyState.Dead;
            return;
        }

        // Calculate distance to player
        float distanceToPlayer = Vector3.Distance(transform.position, player.position);

        // State machine
        switch (currentState)
        {
            case EnemyState.Patrol:
                HandlePatrolState(distanceToPlayer);
                break;

            case EnemyState.Chase:
                HandleChaseState(distanceToPlayer);
                break;

            case EnemyState.Attack:
                HandleAttackState(distanceToPlayer);
                break;

            case EnemyState.Dead:
                break;
        }
    }

    void HandlePatrolState(float distanceToPlayer)
    {
        // Patrol back and forth
        Vector3 targetPos = movingRight ? patrolEndPos : patrolStartPos;
        transform.position = Vector3.MoveTowards(transform.position, targetPos, patrolSpeed * Time.deltaTime);

        // Switch direction at end of patrol
        if (Vector3.Distance(transform.position, targetPos) < 0.1f)
        {
            movingRight = !movingRight;
        }

        // Transition to chase if player detected
        if (distanceToPlayer < detectionRange)
        {
            currentState = EnemyState.Chase;
            Debug.Log("Enemy detected player!");
        }
    }

    void HandleChaseState(float distanceToPlayer)
    {
        // Chase player
        Vector3 directionToPlayer = (player.position - transform.position).normalized;
        transform.position += directionToPlayer * chaseSpeed * Time.deltaTime;

        // Transition to attack if in range
        if (distanceToPlayer < attackRange)
        {
            currentState = EnemyState.Attack;
            Debug.Log("Enemy in attack range!");
        }

        // Return to patrol if player lost
        if (distanceToPlayer > detectionRange * 1.5f)
        {
            currentState = EnemyState.Patrol;
            Debug.Log("Lost sight of player");
        }
    }

    void HandleAttackState(float distanceToPlayer)
    {
        // Stay facing player
        Vector3 directionToPlayer = (player.position - transform.position).normalized;
        transform.LookAt(player);

        // Attack if cooldown expired
        if (Time.time > lastAttackTime + attackCooldown)
        {
            Attack();
        }

        // Return to chase if player out of range
        if (distanceToPlayer > attackRange * 1.5f)
        {
            currentState = EnemyState.Chase;
        }
    }

    void Attack()
    {
        Debug.Log("Enemy attacking!");
        lastAttackTime = Time.time;

        // Check if player is in range and hit them
        if (Vector3.Distance(transform.position, player.position) < attackRange)
        {
            Health playerHealth = player.GetComponent<Health>();
            if (playerHealth != null)
            {
                playerHealth.TakeDamage(attackDamage);
            }
        }
    }
}
```

### Guided Practice

1. Create a script called `EnemyAI.cs` with a state machine
2. Set detectionRange = 10 and attackRange = 2 in the Inspector
3. Assign the player as a reference
4. Create patrol points (two positions the enemy walks between)
5. Test: Enemy should patrol until player gets within 10 units, then chase
6. Test: Enemy should attack when within 2 units
7. Verify state transitions in Debug.Log messages

### Practice Problems

**Problem 1 — Beginner:** Create an enemy that patrols back and forth between two points using Vector3.MoveTowards().

**Problem 2 — Intermediate:** Implement the three-state AI (Patrol, Chase, Attack) with proper distance checks and state transitions.

**Problem 3 — Challenge:** Add a "Stun" state where the enemy stops moving for 2 seconds after taking damage, then returns to their previous state.

<details>
<summary>Hints</summary>

**Problem 1:** Store patrol start/end positions. In Update(), move toward end position. When reached, switch direction.

**Problem 2:** Use enum for states. Calculate distance to player each frame. Transition states based on distance thresholds. See code example above.

**Problem 3:** Add a stunTimer field. In TakeDamage callback, set stunTimer = 2f. In Update, check if stunTimer > 0 and skip state logic.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
using UnityEngine;

public class PatrolEnemy : MonoBehaviour
{
    public float speed = 2f;
    private Vector3 startPos;
    private Vector3 endPos;
    private bool movingRight = true;

    void Start()
    {
        startPos = transform.position;
        endPos = transform.position + Vector3.right * 5f;
    }

    void Update()
    {
        Vector3 targetPos = movingRight ? endPos : startPos;
        transform.position = Vector3.MoveTowards(transform.position, targetPos, speed * Time.deltaTime);

        if (Vector3.Distance(transform.position, targetPos) < 0.1f)
        {
            movingRight = !movingRight;
        }
    }
}
```

**Problem 2:** See the EnemyAI class in the Code Examples section.

**Problem 3:** Add this to EnemyAI:
```csharp
private float stunTimer = 0f;

void Update()
{
    stunTimer -= Time.deltaTime;
    if (stunTimer > 0)
    {
        currentState = EnemyState.Stun;
        return;
    }
    // ... rest of state machine
}

// In TakeDamage callback:
stunTimer = 2f;
```

</details>
