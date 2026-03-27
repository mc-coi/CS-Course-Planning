# Vocabulary & Quick Reference

## Key Terms

| Term | Definition |
|------|-----------|
| **Health Component** | Modular script managing entity damage and death |
| **State Machine** | System cycling through named states with transitions |
| **Patrol** | AI behavior of moving along a fixed path |
| **Chase** | AI behavior of following the player |
| **Attack** | AI behavior of attacking when in range |
| **Cooldown** | Time required between repeated actions |
| **GameManager** | Singleton managing global game state |
| **Singleton** | Design pattern where only one instance exists |
| **Win Condition** | Requirements to win the game |
| **Lose Condition** | Requirements to lose the game |
| **Game State** | Named state of the game (Playing, Paused, etc.) |
| **Time.timeScale** | Multiplier for game speed (0 = paused) |
| **Vector3.Distance()** | Calculates distance between two positions |

## Key Syntax

### Health & Damage Quick Reference

```csharp
// Health component usage
Health health = GetComponent<Health>();
health.TakeDamage(10);
health.Heal(20);
int percent = (int)(health.GetHealthPercent() * 100);

// Invulnerability
if (invulnerabilityTimer > 0)
    return;  // Ignore damage

invulnerabilityTimer = duration;
```

### Enemy AI Quick Reference

```csharp
// Distance calculation
float distance = Vector3.Distance(enemy.position, player.position);
if (distance < detectionRange)
    currentState = EnemyState.Chase;

// Direction to target
Vector3 direction = (player.position - enemy.position).normalized;
enemy.transform.position += direction * speed * Time.deltaTime;

// Attack cooldown
if (Time.time > lastAttackTime + attackCooldown)
{
    Attack();
    lastAttackTime = Time.time;
}
```

### GameManager Quick Reference

```csharp
// Singleton pattern
public static GameManager instance { get; private set; }

void Awake()
{
    if (instance == null)
        instance = this;
    else
        Destroy(gameObject);
}

// Persistent data
DontDestroyOnLoad(gameObject);

// Score
GameManager.instance.AddScore(100);
int score = GameManager.instance.score;
```

### Game State Quick Reference

```csharp
// Pause/Resume
Time.timeScale = 0f;    // Pause
Time.timeScale = 1f;    // Resume

// State transitions
switch (currentState)
{
    case GameState.Playing:
        // Update game logic
        break;
    case GameState.Paused:
        // Handle pause input
        break;
}

// Win/Lose
if (enemiesRemaining <= 0) Win();
if (health <= 0) Lose();
```

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Health goes negative | Not clamping health to 0 | Always use `if (health < 0) health = 0;` |
| Enemy attacks every frame | No attack cooldown | Use `Time.time > lastAttackTime + cooldown` to gate attacks |
| Distance check always fails | Not using Vector3.Distance correctly | Use `Distance(a, b)` - returns float distance |
| GameManager singleton creates duplicates | Not destroying duplicate in Awake | Always check if instance exists and Destroy() if it does |
| Game doesn't pause | Time.timeScale = 0 happens but game keeps running | Verify Time.deltaTime is 0 in paused state; check Update() vs FixedUpdate() |
| Enemy AI doesn't transition states | State logic is wrong or conditions never met | Add Debug.Log to state transitions to verify they're firing |
| Score doesn't persist between scenes | PlayerPrefs not saved to disk | Call PlayerPrefs.Save() after setting values (mobile requirement) |
| GameOver happens immediately | Losing condition always true | Check lose condition logic; should transition to GameOver state, not loop |
| Enemy ignores obstacles | No pathfinding, just moving toward player | Use NavMesh or raycast to check for obstacles before moving |
| Time.timeScale changes affect animations | Physics and animations both scale | Some animations need separate timing; consider alternatives to time scaling |
