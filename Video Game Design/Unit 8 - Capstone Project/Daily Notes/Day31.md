# Day 31: Systems Integration

**Learning Target:** Integrate multiple game systems so player, enemies, UI, and scoring all communicate properly.

### Key Concepts

- **Integration:** Connecting multiple systems (player, enemies, UI, scoring)
- **GetComponent:** Accessing other components on the same or different GameObjects
- **References:** Storing references to other GameManager, UI elements, etc.
- **Message Passing:** Systems communicating through method calls
- **Event System:** Loosely coupled communication using C# events
- **Dependency Injection:** Passing dependencies into components
- **Testing Integrated Systems:** Ensuring all systems work together

### Content

As games grow, many systems need to interact:
- Player shoots bullet
- Bullet hits enemy
- Enemy takes damage
- Enemy dies
- GameManager adds score
- UI updates score display

Each step requires communication between systems.

**Communication Methods:**
1. **Direct References:** Get component and call method
2. **Singletons:** Static GameManager instance
3. **Events:** Loosely coupled communication
4. **Messages:** Send messages between objects

**Integration Checklist:**
- [ ] Player controller communicates with animator
- [ ] Enemies receive damage and die
- [ ] Dying enemies reward points
- [ ] GameManager updates score
- [ ] UI reflects score changes
- [ ] Win/lose conditions are checked
- [ ] All systems work together

### Code Examples

```csharp
using UnityEngine;

// Integration example: Multiple systems working together

public class IntegratedGameManager : MonoBehaviour
{
    // INTEGRATION: Multiple systems communicating

    public static IntegratedGameManager instance { get; private set; }

    private int score = 0;
    private int enemiesDefeated = 0;
    private PlayerController player;
    private UIManager uiManager;

    void Awake()
    {
        instance = this;
    }

    void Start()
    {
        // Get references to other systems
        player = FindObjectOfType<PlayerController>();
        uiManager = FindObjectOfType<UIManager>();

        if (player == null)
            Debug.LogError("PlayerController not found!");
        if (uiManager == null)
            Debug.LogError("UIManager not found!");
    }

    void Update()
    {
        // Check win condition
        if (enemiesDefeated >= 5)
        {
            Win();
        }

        // Check lose condition
        if (player != null && !player.IsAlive())
        {
            Lose();
        }
    }

    // Called when enemy dies
    public void OnEnemyDefeated()
    {
        enemiesDefeated++;
        AddScore(100);
        Debug.Log("Enemy defeated! Total: " + enemiesDefeated);
    }

    // Called when player collects item
    public void OnItemCollected(int value)
    {
        AddScore(value);
    }

    // Central score management
    public void AddScore(int points)
    {
        score += points;

        // Notify UI to update
        if (uiManager != null)
        {
            uiManager.UpdateScoreDisplay(score);
        }

        Debug.Log("Score: " + score);
    }

    void Win()
    {
        Debug.Log("You Win! Score: " + score);
        // Transition to win scene
    }

    void Lose()
    {
        Debug.Log("Game Over. Final Score: " + score);
        // Transition to lose scene
    }
}

// Player system
public class PlayerController : MonoBehaviour
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();

        // Register health change event
        if (health != null)
        {
            health.OnHealthChanged += HandleHealthChanged;
        }
    }

    void HandleHealthChanged(int newHealth)
    {
        Debug.Log("Player health changed: " + newHealth);
    }

    public bool IsAlive()
    {
        return health != null && health.IsAlive();
    }
}

// Enemy system
public class EnemyController : MonoBehaviour
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();

        // Register death event
        if (health != null)
        {
            health.OnHealthChanged += CheckIfDead;
        }
    }

    void CheckIfDead(int newHealth)
    {
        if (newHealth <= 0)
        {
            // Notify GameManager
            IntegratedGameManager.instance.OnEnemyDefeated();
        }
    }
}

// UI system
public class UIManager : MonoBehaviour
{
    public TMPro.TextMeshProUGUI scoreText;

    public void UpdateScoreDisplay(int newScore)
    {
        if (scoreText != null)
        {
            scoreText.text = "Score: " + newScore;
        }
    }
}
```

### Guided Practice

1. Integrate player movement with a PlayerController script
2. Create an EnemyController that receives damage and dies
3. When enemy dies, notify GameManager
4. GameManager adds score and updates UI
5. Create a UIManager that displays score
6. Test: Enemy dies → score increases → UI updates
7. Verify all systems communicate properly

### Practice Problems

**Problem 1 — Beginner:** Create a simple integration where collecting a coin increases score and updates UI display.

**Problem 2 — Intermediate:** Integrate player, enemy, health, and scoring systems so enemies drop points when defeated.

**Problem 3 — Challenge:** Create a complete integration with player, enemies, UI, GameManager, and win/lose conditions working together.

<details>
<summary>Hints</summary>

**Problem 1:** Use GetComponent to access Health. Call AddScore() on GameManager when item is collected. Have UI listen to score changes.

**Problem 2:** Use events or direct references. When enemy health = 0, call GameManager.OnEnemyDefeated(). Have GameManager add score and notify UI.

**Problem 3:** See the IntegratedGameManager code example above for a complete integration pattern.

</details>

<details>
<summary>Sample Answers</summary>

See the Annotated Code Example above for the complete integration example with GameManager, PlayerController, EnemyController, and UIManager all working together.

Key integration points:
- GameManager singleton for central coordination
- Systems register with events (OnHealthChanged, etc.)
- GameManager notified of game events
- GameManager updates UI when score changes
- UI only updates through GameManager

</details>
