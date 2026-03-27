# Day 28: Game State & Complete Systems Integration

**Learning Target:** Implement complete game state management with win/lose conditions and integrated systems.

### Key Concepts

- **Game State Enum:** Named states (Menu, Playing, Paused, GameOver, Win)
- **State Transitions:** Rules for moving between states
- **Time.timeScale:** Controls game speed (0 = paused)
- **Win Condition:** Requirements to win (defeat all enemies, reach goal)
- **Lose Condition:** Requirements to lose (health = 0, time = 0)
- **Game Flow:** Complete loop (Menu → Playing → Win/Lose → GameOver)

### Content

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

### Code Examples

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

### Guided Practice

1. Create a script called `GameController.cs` with a GameState enum
2. Define states: Menu, Playing, Paused, GameOver, Win
3. Implement the main state machine in Update()
4. Create win condition: When enemiesRemaining = 0
5. Create lose condition: When health = 0 or time = 0
6. Implement pause: ESC key sets Time.timeScale = 0 and shows pause menu
7. Test all state transitions and ensure Time.timeScale is properly managed

### Practice Problems

**Problem 1 — Beginner:** Implement a simple state machine with Playing and Paused states that toggle with ESC.

**Problem 2 — Intermediate:** Add win and lose conditions and transition to respective screens.

**Problem 3 — Challenge:** Create a complete game flow with Menu, Playing, Paused, Win, and GameOver states with proper transitions.

<details>
<summary>Hints</summary>

**Problem 1:** Use GameState enum. In Update(), check for ESC key. Toggle between Playing and Paused. Set Time.timeScale = 0 when paused, 1 when playing.

**Problem 2:** Add won and lost flags. Check conditions in Update(). Transition to Win() or Lose() when appropriate. Freeze time and show UI.

**Problem 3:** See GameController class in code examples. Implement all five states with proper transitions and Time.timeScale management.

</details>

<details>
<summary>Sample Answers</summary>

See the Annotated Code Example above for the complete GameController implementation.

Key implementation points:
- GameState enum with 5 states
- Switch statement for state logic
- Pause/Resume methods manage Time.timeScale
- Win/Lose check conditions each frame
- UI panels show/hide based on state

</details>
