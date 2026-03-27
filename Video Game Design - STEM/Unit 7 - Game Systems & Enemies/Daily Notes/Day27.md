# Day 27: GameManager Singleton & Scoring

**Learning Target:** Create a GameManager singleton for global game state, score tracking, and game statistics.

### Key Concepts

- **Singleton Pattern:** Only one instance of a class exists globally
- **GameManager:** Central manager for game state, score, lives
- **Static Instance:** A public static variable for global access
- **DontDestroyOnLoad():** Keeps GameManager across scene loads
- **Score Tracking:** Keeping track of player score and high score
- **Game Statistics:** Health, ammo, lives, level progress
- **Pause State:** Freezing gameplay without reloading

### Content

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

### Code Examples

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

### Guided Practice

1. Create a script called `GameManager.cs` with the singleton pattern
2. In Awake(), implement the singleton check
3. Call `DontDestroyOnLoad(gameObject)` so the manager persists
4. Add an AddScore() method that updates the score and checks for high score
5. Add a TogglePause() method that sets Time.timeScale to 0 or 1
6. Test: Create two scenes and verify GameManager persists when loading the second scene
7. Test: Press ESC to pause and verify Time.timeScale = 0

### Practice Problems

**Problem 1 — Beginner:** Create a GameManager singleton that tracks score and allows global access.

**Problem 2 — Intermediate:** Implement pause functionality using Time.timeScale and show/hide a pause menu.

**Problem 3 — Challenge:** Create a high score system that persists between game sessions using PlayerPrefs.

<details>
<summary>Hints</summary>

**Problem 1:** Implement singleton pattern with static instance. Use DontDestroyOnLoad(). Provide AddScore() method. See code example.

**Problem 2:** Set Time.timeScale = 0 to pause. Show pause UI. Resume with Time.timeScale = 1. Toggle with ESC key in Update().

**Problem 3:** Save high score: `PlayerPrefs.SetInt("HighScore", highScore)`. Load high score: `PlayerPrefs.GetInt("HighScore", 0)`. Call PlayerPrefs.Save() on mobile.

</details>

<details>
<summary>Sample Answers</summary>

See the Annotated Code Example above for the complete GameManager implementation with all required features.

Key points:
- Singleton check in Awake()
- DontDestroyOnLoad() for persistence
- AddScore() updates score and checks high score
- TogglePause() sets Time.timeScale
- PlayerPrefs for saving high score

</details>
