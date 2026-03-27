# Unit 7: Game Systems & Enemies

## Unit Overview

**Duration:** Days 25-28 (4 days)
**Key Concepts:** Health systems, enemy AI, game state management, scoring, win/lose conditions
**Big Idea:** Games are made of interconnected systems. Health systems manage entity state, AI makes enemies feel intelligent, game managers coordinate everything.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Design and implement modular health/damage systems
- [ ] Create enemy AI with state machines (Patrol, Chase, Attack)
- [ ] Use Vector3.Distance() to detect proximity
- [ ] Implement NavMesh for intelligent pathfinding (navigation mesh)
- [ ] Create a GameManager singleton for global game state
- [ ] Track score, high score, and player statistics
- [ ] Implement win/lose/pause conditions
- [ ] Manage game time with Time.timeScale
- [ ] Design game state flow (Play, Paused, GameOver, Win)
- [ ] Create effective enemy behaviors that feel alive

---

## Day-by-Day Content

### Day 25: Health Components & Modular Design

#### Key Concepts
- **Health System:** Tracks entity health and handles damage
- **Modular Design:** Breaking code into independent, reusable components
- **Damage Method:** Public method for taking damage
- **Death Handler:** Cleanup and effects when health reaches 0
- **Damage Types:** Different damage sources (weapon, hazard, poison)
- **Knockback:** Pushing entity away on impact
- **Invulnerability Frames:** Temporary immunity to damage

#### Content
A health system is essential for games with enemies and damage. Instead of each script handling damage independently, create a reusable Health component.

**Health Component Benefits:**
- Consistency: All entities with health behave the same way
- Reusability: Add to player, enemies, destructible objects
- Maintainability: Changes to health logic happen in one place

**Modular Design Pattern:**
Instead of one big script doing everything:
- Create a Health component (handles damage, death)
- Create an Enemy component (handles AI)
- Create a Weapon component (handles attacks)
- Create a GameManager component (coordinates everything)

Each component is independent and can be reused.

#### Annotated Code Example

```csharp
using UnityEngine;

// Reusable health component
public class Health : MonoBehaviour
{
    [Header("Health Settings")]
    public int maxHealth = 100;
    public int currentHealth;

    [Header("Damage Settings")]
    public float invulnerabilityDuration = 0.2f;
    private float invulnerabilityTimer = 0f;

    [Header("References")]
    public GameObject deathEffectPrefab;
    public AudioClip damageSound;
    public AudioClip deathSound;

    // Events for other systems to listen to
    public delegate void HealthChangedEvent(int newHealth);
    public event HealthChangedEvent OnHealthChanged;

    void Start()
    {
        currentHealth = maxHealth;
        OnHealthChanged?.Invoke(currentHealth);
    }

    void Update()
    {
        // Decrease invulnerability timer
        if (invulnerabilityTimer > 0)
        {
            invulnerabilityTimer -= Time.deltaTime;
        }
    }

    // Public method for taking damage
    public void TakeDamage(int damageAmount)
    {
        // Don't take damage if invulnerable
        if (invulnerabilityTimer > 0)
        {
            Debug.Log("Invulnerable! Ignoring damage.");
            return;
        }

        currentHealth -= damageAmount;
        invulnerabilityTimer = invulnerabilityDuration;

        Debug.Log(gameObject.name + " took " + damageAmount + " damage. Health: " + currentHealth);

        // Clamp health to 0
        if (currentHealth < 0)
            currentHealth = 0;

        // Invoke event so UI and other systems update
        OnHealthChanged?.Invoke(currentHealth);

        // Play damage sound
        if (damageSound != null)
        {
            AudioSource.PlayClipAtPoint(damageSound, transform.position);
        }

        // Check if dead
        if (currentHealth <= 0)
        {
            Die();
        }
    }

    public void Heal(int healAmount)
    {
        currentHealth += healAmount;
        if (currentHealth > maxHealth)
            currentHealth = maxHealth;

        Debug.Log("Healed " + healAmount + " health. Current: " + currentHealth);
        OnHealthChanged?.Invoke(currentHealth);
    }

    void Die()
    {
        Debug.Log(gameObject.name + " died!");

        // Play death effect
        if (deathEffectPrefab != null)
        {
            Instantiate(deathEffectPrefab, transform.position, Quaternion.identity);
        }

        // Play death sound
        if (deathSound != null)
        {
            AudioSource.PlayClipAtPoint(deathSound, transform.position);
        }

        // Notify other systems
        GetComponent<IDeathHandler>()?.OnDeath();

        // Remove from scene
        Destroy(gameObject);
    }

    public bool IsAlive()
    {
        return currentHealth > 0;
    }

    public float GetHealthPercent()
    {
        return (float)currentHealth / maxHealth;
    }
}

// Interface for death handling
public interface IDeathHandler
{
    void OnDeath();
}

// Example: Enemy that implements IDeathHandler
public class Enemy : MonoBehaviour, IDeathHandler
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();
    }

    public void OnDeath()
    {
        Debug.Log("Enemy died! Award points.");
        GameManager.instance.AddScore(100);
    }
}
```

---

### Day 26: Enemy AI State Machine

#### Key Concepts
- **AI State Machine:** Enemies cycle through behaviors (Patrol, Chase, Attack)
- **Patrol State:** Moving along a fixed path
- **Chase State:** Following the player when nearby
- **Attack State:** Attacking when in range
- **Detection Range:** Distance at which enemy notices player
- **Attack Range:** Distance at which enemy can attack
- **Cooldown:** Time between attacks
- **Vector3.Distance():** Calculating distance between two positions

#### Content
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

#### Annotated Code Example

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

---

### Day 27: GameManager Singleton & Scoring

#### Key Concepts
- **Singleton Pattern:** Only one instance of a class exists globally
- **GameManager:** Central manager for game state, score, lives
- **Static Instance:** A public static variable for global access
- **DontDestroyOnLoad():** Keeps GameManager across scene loads
- **Score Tracking:** Keeping track of player score and high score
- **Game Statistics:** Health, ammo, lives, level progress
- **Pause State:** Freezing gameplay without reloading

#### Content
The GameManager is a singleton—a single instance accessible from anywhere in the game.

**Singleton Pattern:**
```csharp
public static GameManager instance { get; private set; }

void Awake()
{
    if (instance == null)
        instance = this;
    else
        Destroy(gameObject);
}
```

**Why Singleton?**
- Accessible globally: `GameManager.instance.AddScore(10);`
- Only one exists: No duplicate managers
- Persists across scenes: `DontDestroyOnLoad(gameObject);`

#### Annotated Code Example

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    // Singleton instance
    public static GameManager instance { get; private set; }

    [Header("Game State")]
    public int score = 0;
    public int highScore = 0;
    public int health = 100;
    public int level = 1;
    public bool isPaused = false;

    [Header("Game Progress")]
    private int enemiesDefeated = 0;
    private int itemsCollected = 0;

    void Awake()
    {
        // Implement singleton pattern
        if (instance == null)
        {
            instance = this;
            DontDestroyOnLoad(gameObject);  // Persist across scenes
        }
        else
        {
            Destroy(gameObject);  // Destroy duplicate
        }
    }

    void Start()
    {
        // Load high score from PlayerPrefs
        highScore = PlayerPrefs.GetInt("HighScore", 0);
        Debug.Log("High Score: " + highScore);
    }

    void Update()
    {
        // Pause toggle (ESC key)
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            TogglePause();
        }
    }

    // Score management
    public void AddScore(int points)
    {
        score += points;
        Debug.Log("Score: " + score);

        // Check for new high score
        if (score > highScore)
        {
            highScore = score;
            PlayerPrefs.SetInt("HighScore", highScore);
            Debug.Log("New High Score: " + highScore);
        }
    }

    public void ResetScore()
    {
        score = 0;
    }

    // Health management
    public void SetHealth(int newHealth)
    {
        health = newHealth;
        if (health <= 0)
        {
            GameOver();
        }
    }

    // Game state management
    public void TogglePause()
    {
        isPaused = !isPaused;
        Time.timeScale = isPaused ? 0f : 1f;  // 0 = paused, 1 = normal speed
        Debug.Log(isPaused ? "Paused" : "Resumed");
    }

    public void GameOver()
    {
        Debug.Log("Game Over! Final Score: " + score);
        isPaused = true;
        Time.timeScale = 0f;
        SceneManager.LoadScene("GameOverScene");
    }

    public void Win()
    {
        Debug.Log("You Win! Score: " + score);
        isPaused = true;
        Time.timeScale = 0f;
        SceneManager.LoadScene("WinScene");
    }

    public void LoadScene(string sceneName)
    {
        Time.timeScale = 1f;  // Resume before loading
        SceneManager.LoadScene(sceneName);
    }

    public void Quit()
    {
        Debug.Log("Quitting game");
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }
}

// Example usage in other scripts
public class CoinPickup : MonoBehaviour
{
    public int coinValue = 10;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            GameManager.instance.AddScore(coinValue);
            Destroy(gameObject);
        }
    }
}

public class GameOverUI : MonoBehaviour
{
    void Start()
    {
        // Display final score and high score
        Debug.Log($"Final Score: {GameManager.instance.score}");
        Debug.Log($"High Score: {GameManager.instance.highScore}");
    }

    void Update()
    {
        // Press R to restart
        if (Input.GetKeyDown(KeyCode.R))
        {
            GameManager.instance.LoadScene("GameScene");
        }
    }
}
```

---

### Day 28: Game State & Complete Systems Integration

#### Key Concepts
- **Game State Enum:** Named states (Menu, Playing, Paused, GameOver, Win)
- **State Transitions:** Rules for moving between states
- **Time.timeScale:** Controls game speed (0 = paused)
- **Win Condition:** Requirements to win (defeat all enemies, reach goal)
- **Lose Condition:** Requirements to lose (health = 0, time = 0)
- **Game Flow:** Complete loop (Menu → Playing → Win/Lose → GameOver)

#### Content
A complete game manages multiple states and transitions between them.

**Game State Flow:**
```
Menu → Playing → (Paused) → GameOver/Win → Menu
```

**State Management:**
```csharp
public enum GameState { Menu, Playing, Paused, GameOver, Win }
private GameState currentState = GameState.Menu;

void Update()
{
    switch (currentState)
    {
        case GameState.Menu:
            // Handle menu input
            break;
        case GameState.Playing:
            // Update game logic
            break;
        case GameState.Paused:
            // Show pause menu, handle pause input
            break;
        // ... etc
    }
}
```

**Time.timeScale:**
- 0 = paused (all Delta Time = 0)
- 1 = normal speed
- 2 = fast forward
- Essential for pause functionality

#### Annotated Code Example

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public enum GameState { Menu, Playing, Paused, GameOver, Win }

public class GameController : MonoBehaviour
{
    [Header("State")]
    public GameState currentState = GameState.Playing;

    [Header("Win/Lose Conditions")]
    public int enemiesRemaining = 5;
    public float timeRemaining = 300f;
    private bool won = false;
    private bool lost = false;

    [Header("UI References")]
    public GameObject pauseMenuPanel;
    public GameObject gameOverPanel;
    public GameObject winPanel;

    void Start()
    {
        // Initialize UI (disable all except game UI)
        pauseMenuPanel.SetActive(false);
        gameOverPanel.SetActive(false);
        winPanel.SetActive(false);

        currentState = GameState.Playing;
        Time.timeScale = 1f;  // Ensure game is running
    }

    void Update()
    {
        if (currentState == GameState.Playing)
        {
            UpdateGameplay();
        }
        else if (currentState == GameState.Paused)
        {
            UpdatePausedState();
        }

        // Check win/lose conditions
        CheckGameConditions();
    }

    void UpdateGameplay()
    {
        // Update timer
        timeRemaining -= Time.deltaTime;
        if (timeRemaining <= 0)
        {
            lost = true;
        }

        // Pause input
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            Pause();
        }

        // Check win condition (all enemies defeated)
        if (enemiesRemaining <= 0)
        {
            won = true;
        }
    }

    void UpdatePausedState()
    {
        // Resume input
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            Resume();
        }

        // Quit input
        if (Input.GetKeyDown(KeyCode.Q))
        {
            LoadMainMenu();
        }
    }

    void CheckGameConditions()
    {
        if (won && currentState != GameState.Win)
        {
            Win();
        }

        if (lost && currentState != GameState.GameOver)
        {
            Lose();
        }
    }

    public void Pause()
    {
        if (currentState == GameState.Playing)
        {
            currentState = GameState.Paused;
            Time.timeScale = 0f;  // Freeze game
            pauseMenuPanel.SetActive(true);
            Debug.Log("Game Paused");
        }
    }

    public void Resume()
    {
        if (currentState == GameState.Paused)
        {
            currentState = GameState.Playing;
            Time.timeScale = 1f;  // Resume game
            pauseMenuPanel.SetActive(false);
            Debug.Log("Game Resumed");
        }
    }

    public void EnemyDefeated()
    {
        enemiesRemaining--;
        Debug.Log("Enemy defeated! Remaining: " + enemiesRemaining);
        GameManager.instance.AddScore(100);
    }

    void Win()
    {
        currentState = GameState.Win;
        Time.timeScale = 0f;
        winPanel.SetActive(true);
        Debug.Log("YOU WIN! Score: " + GameManager.instance.score);

        // Save high score
        int highScore = PlayerPrefs.GetInt("HighScore", 0);
        if (GameManager.instance.score > highScore)
        {
            PlayerPrefs.SetInt("HighScore", GameManager.instance.score);
        }
    }

    void Lose()
    {
        currentState = GameState.GameOver;
        Time.timeScale = 0f;
        gameOverPanel.SetActive(true);
        Debug.Log("GAME OVER. Final Score: " + GameManager.instance.score);
    }

    public void RestartGame()
    {
        Time.timeScale = 1f;
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }

    public void LoadMainMenu()
    {
        Time.timeScale = 1f;
        SceneManager.LoadScene("MainMenu");
    }
}

// Enemy notifies controller when defeated
public class Enemy : MonoBehaviour
{
    private Health health;
    private GameController gameController;

    void Start()
    {
        health = GetComponent<Health>();
        gameController = FindObjectOfType<GameController>();
    }

    void Update()
    {
        if (!health.IsAlive() && gameController != null)
        {
            gameController.EnemyDefeated();
        }
    }
}
```

---

## Practice Problems

### Beginner Tier

**Problem 1:** Create a Health component and attach it to an enemy. Make the enemy take damage on collision with the player.

<details>
<summary>Hint</summary>
Create Health.cs component. In OnCollisionEnter(), call TakeDamage(). Verify health decreases and enemy dies at 0 health.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 25 (Health class).
</details>

---

**Problem 2:** Implement a simple enemy that patrols back and forth along a fixed path.

<details>
<summary>Hint</summary>
Store patrol start/end positions. In Update(), move toward end position. When reached, switch direction.
</details>

<details>
<summary>Answer</summary>
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
</details>

---

**Problem 3:** Create a GameManager singleton that tracks score and allows global access.

<details>
<summary>Hint</summary>
Implement singleton pattern with static instance. Use DontDestroyOnLoad(). Provide AddScore() method.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 27 (GameManager class).
</details>

---

### Intermediate Tier

**Problem 4:** Create an enemy with a 3-state AI (Patrol, Chase, Attack) that transitions based on player distance.

<details>
<summary>Hint</summary>
Use enum for states. Calculate distance to player each frame. Transition states based on distance thresholds.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 26 (EnemyAI class).
</details>

---

**Problem 5:** Implement a pause system that freezes the game and shows a pause menu. Resume with ESC key.

<details>
<summary>Hint</summary>
Set Time.timeScale = 0 to pause. Show pause UI. Resume with Time.timeScale = 1.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class PauseManager : MonoBehaviour
{
    public GameObject pauseMenuUI;
    private bool isPaused = false;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            if (isPaused)
                Resume();
            else
                Pause();
        }
    }

    void Pause()
    {
        isPaused = true;
        Time.timeScale = 0f;
        pauseMenuUI.SetActive(true);
    }

    void Resume()
    {
        isPaused = false;
        Time.timeScale = 1f;
        pauseMenuUI.SetActive(false);
    }
}
```
</details>

---

**Problem 6:** Create a complete game with GameManager, player health, enemy AI, score system, and win condition.

<details>
<summary>Hint</summary>
Combine: GameManager singleton, Health component, Enemy AI, collision detection, scoring UI.
</details>

<details>
<summary>Answer</summary>
Combine code from Days 25, 26, and 27. Integrate into a complete scene.
</details>

---

### Challenge Tier

**Problem 7:** Design a complete multi-wave enemy system where waves get progressively harder, and the game tracks high score.

<details>
<summary>Hint</summary>
Create waves with increasing enemy count/difficulty. Spawn enemies between waves. Save high score when game ends.
</details>

<details>
<summary>Answer</summary>
Create a WaveManager that spawns enemy waves. Increase difficulty each wave. Track high score in GameManager.
</details>

---

**Problem 8:** Implement a full game state machine with Menu, Playing, Paused, and GameOver states with proper transitions.

<details>
<summary>Hint</summary>
Use GameState enum. In Update(), switch on state and handle transitions. Control Time.timeScale based on state.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 28 (GameController class).
</details>

---

## Practice Bank (15 Problems)

1. **Modular Health System:** Create a Health component and attach it to 3+ different entity types (player, enemy, destructible).

2. **Damage Types:** Implement different damage types (sword, fire, poison) that scale differently based on armor/resistance.

3. **Knockback Physics:** When hit, push the entity away from the hit source. Implement knockback knockback on damage.

4. **Invulnerability Frames:** Implement damage immunity after taking damage (visual blink effect + frame counter).

5. **Enemy Patrol AI:** Create a patrolling enemy with adjustable patrol points and speed.

6. **Enemy Detection:** Use raycasting to detect line-of-sight to the player. Only chase if visible.

7. **NavMesh Pathfinding:** Use Unity's NavMesh system for enemy pathfinding. Compare to manual movement.

8. **Attack Cooldown:** Implement cooldown between enemy attacks. Show cooldown timer visually.

9. **Weakness System:** Implement weaknesses (enemy weak to fire, strong to ice). Damage varies by element.

10. **Boss Enemy:** Create a boss enemy with multiple phases and special attacks.

11. **Loot Drop:** When enemy dies, randomly drop loot (health, coins, items).

12. **Difficulty Scaling:** Create difficulty settings that change enemy health, speed, and damage.

13. **Wave System:** Create waves of enemies with increasing difficulty. Track which wave the player is on.

14. **Time-Based Win Condition:** Implement a survival mode where player wins by lasting X minutes.

15. **Game State Flowchart:** Create a complete flowchart of your game's state transitions and document each state's behavior.

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Health goes negative | Not clamping health to 0 | Always use `if (health < 0) health = 0;` |
| Enemy attacks every frame | No attack cooldown | Use `Time.time > lastAttackTime + cooldown` to gate attacks |
| Distance check always fails | Not using Vector3.Distance correctly | Use `Distance(a, b)` not `(a - b).magnitude` (same thing, but clearer) |
| GameManager singleton creates duplicates | Not destroying duplicate in Awake | Always check if instance exists and Destroy() if it does |
| Game doesn't pause | Time.timeScale = 0 happens but game keeps running | Verify Time.deltaTime is 0 in paused state; check Update() vs FixedUpdate() |
| Enemy AI doesn't transition states | State logic is wrong or conditions never met | Add Debug.Log to state transitions to verify they're firing |
| Score doesn't persist between scenes | PlayerPrefs not saved to disk | Call PlayerPrefs.Save() after setting values (mobile requirement) |
| GameOver happens immediately | Losing condition always true | Check lose condition logic; should transition to GameOver state, not loop |
| Enemy ignores obstacles | No pathfinding, just moving toward player | Use NavMesh or raycast to check for obstacles before moving |
| Time.timeScale changes affect animations | Physics and animations both scale | Some animations need separate timing; consider alternatives to time scaling |

---

## Assessment Prep: 10 Q&As

**Q1: What is the singleton pattern and why use GameManager as a singleton?**
A: A singleton has only one instance globally accessible. GameManager is a singleton so you can access `GameManager.instance.AddScore()` from anywhere without storing references.

**Q2: Explain the health component design and why it's modular.**
A: Health component tracks damage independently. It's modular because you can attach it to any entity (player, enemy, destructible). Changes to health logic affect all entities.

**Q3: What is a state machine and how does enemy AI use it?**
A: A state machine cycles through named states (Patrol, Chase, Attack) with transition rules. Enemy AI uses states to organize behavior logically.

**Q4: How do you calculate distance between two objects?**
A: Use `Vector3.Distance(objectA.position, objectB.position);` which returns a float distance in units.

**Q5: What does Time.timeScale do and how is it used for pausing?**
A: Time.timeScale controls game speed. Setting it to 0 freezes the game (Time.deltaTime becomes 0). Set to 1 to resume.

**Q6: Explain the DontDestroyOnLoad() function.**
A: It prevents a GameObject from being destroyed when loading a new scene. Used for persistent managers like GameManager.

**Q7: How do you implement a win condition in a game?**
A: Define win criteria (e.g., `enemiesRemaining == 0`). Check each frame. When true, call Win() which displays win screen and saves high score.

**Q8: What is an attack cooldown and how do you implement it?**
A: Attack cooldown prevents attacking too frequently. Use `if (Time.time > lastAttackTime + cooldown)` to check if enough time passed since last attack.

**Q9: Describe the complete game state flow from menu to game over.**
A: Menu → Play (start game) → Gameplay → Pause (optional) → Resume → Win/Lose → Gameover → Menu

**Q10: How do you give feedback when an entity takes damage?**
A: Visual (sprite flash, screen shake), Audio (damage sound), Physical (knockback), UI (health bar decrease).

---

## Vocabulary & Quick Reference

### Key Terms

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

## Additional Resources

- **Health System Design:** https://www.gamasutra.com/blogs/
- **AI State Machines:** https://blog.unity.com/engine-platform/ai-in-games
- **NavMesh Documentation:** https://docs.unity3d.com/Manual/nav-NavigationSystem.html
- **Game State Management:** https://www.youtube.com/results?search_query=game+state+machine+unity

