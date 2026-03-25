# Day 20: Menus, Scene Management & Persistence

**Learning Target:** Implement multi-scene game structure with menu transitions and persistent data storage using SceneManager and PlayerPrefs.

### Key Concepts

- **Scene:** A level or menu screen in the game
- **SceneManager:** Loads, manages, and transitions between scenes
- **Additive Loading:** Loading a scene on top of another (for UI)
- **DontDestroyOnLoad():** Prevents object destruction when loading new scene
- **PlayerPrefs:** Persistent data storage (settings, high scores, etc.)
- **Menu Flow:** Start menu → Play menu → Game → Game Over menu
- **Button Navigation:** Connecting buttons to scene loading
- **Audio Persistence:** Music that plays across scenes

### Content

Games are typically made of multiple scenes:
- Main Menu
- Settings Menu
- Game Level (multiple scenes)
- Game Over Menu
- Credits

Scenes are managed with SceneManager. Button clicks can load new scenes.

**SceneManager Basics:**
```csharp
// Load a scene by name
SceneManager.LoadScene("GameScene");

// Load additively (on top of current scene)
SceneManager.LoadScene("UILayer", LoadSceneMode.Additive);

// Unload a scene
SceneManager.UnloadSceneAsync("UILayer");
```

**PlayerPrefs:**
Saves small amounts of data (player name, high score, settings):
```csharp
PlayerPrefs.SetInt("HighScore", 1000);
int highScore = PlayerPrefs.GetInt("HighScore");
PlayerPrefs.DeleteKey("HighScore");
PlayerPrefs.Save();  // Force save (mobile)
```

### Code Examples

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using TMPro;

public class MenuManager : MonoBehaviour
{
    public TextMeshProUGUI highScoreText;

    void Start()
    {
        // Load and display high score
        int highScore = PlayerPrefs.GetInt("HighScore", 0);
        highScoreText.text = "High Score: " + highScore;
    }

    public void PlayButtonClicked()
    {
        Debug.Log("Loading game scene...");
        SceneManager.LoadScene("GameScene");
    }

    public void SettingsButtonClicked()
    {
        Debug.Log("Loading settings...");
        SceneManager.LoadScene("SettingsScene");
    }

    public void QuitButtonClicked()
    {
        Debug.Log("Quitting game");
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }
}

public class GameManager : MonoBehaviour
{
    private int currentScore = 0;
    private bool gameover = false;

    void Update()
    {
        if (gameover && Input.GetKeyDown(KeyCode.Return))
        {
            OnGameOver();
        }
    }

    public void AddScore(int points)
    {
        currentScore += points;
    }

    void OnGameOver()
    {
        gameover = true;

        // Save high score if current score is higher
        int highScore = PlayerPrefs.GetInt("HighScore", 0);
        if (currentScore > highScore)
        {
            PlayerPrefs.SetInt("HighScore", currentScore);
            Debug.Log("New high score: " + currentScore);
        }

        // Load game over scene after delay
        Invoke("LoadGameOverScene", 2f);
    }

    void LoadGameOverScene()
    {
        SceneManager.LoadScene("GameOverScene");
    }
}

public class GameOverManager : MonoBehaviour
{
    public TextMeshProUGUI finalScoreText;
    public TextMeshProUGUI highScoreText;

    void Start()
    {
        // Get scores from PlayerPrefs
        int finalScore = PlayerPrefs.GetInt("FinalScore", 0);
        int highScore = PlayerPrefs.GetInt("HighScore", 0);

        finalScoreText.text = "Final Score: " + finalScore;
        highScoreText.text = "High Score: " + highScore;
    }

    public void RetryButtonClicked()
    {
        SceneManager.LoadScene("GameScene");
    }

    public void MainMenuButtonClicked()
    {
        SceneManager.LoadScene("MainMenuScene");
    }
}

public class PersistentAudioManager : MonoBehaviour
{
    public static PersistentAudioManager instance;
    public AudioSource musicSource;

    void Awake()
    {
        // Singleton pattern: only one instance
        if (instance == null)
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }
}
```

### Guided Practice

**Activity:** Create a simple scene transition workflow

1. Create a "MainMenu" scene with a Play button
2. Create a "GameScene" scene with a simple game
3. Create a "GameOverScene" with Retry and Menu buttons
4. Wire buttons to load scenes using SceneManager

Test the flow: Menu → Game → Game Over → Menu/Retry

### Practice Problems

**Problem 1 — Beginner:** Create a main menu with 3 buttons (Play, Settings, Quit) that load appropriate scenes or quit.

**Problem 2 — Intermediate:** Implement high score persistence: save the score when the game ends, load it on the menu, display it on game over screen.

**Problem 3 — Challenge:** Create a complete multi-scene game structure with menu → gameplay → game over → menu loop, including score persistence and a pause menu.

<details>
<summary>Hints</summary>

**Problem 1:** Create buttons with OnClick listeners. In the listeners, call SceneManager.LoadScene() for Play/Settings, and Application.Quit() for Quit.

**Problem 2:** Use PlayerPrefs.SetInt() to save, PlayerPrefs.GetInt() to load. Save during OnGameOver(). Load during Start().

**Problem 3:** Combine code from MenuManager, GameManager, and GameOverManager examples. Create all necessary scenes in Build Settings.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
See MenuManager code example above.

**Problem 2:**
```csharp
// In GameManager.OnGameOver():
int highScore = PlayerPrefs.GetInt("HighScore", 0);
if (currentScore > highScore)
{
    PlayerPrefs.SetInt("HighScore", currentScore);
}

// In MenuManager.Start():
int highScore = PlayerPrefs.GetInt("HighScore", 0);
highScoreText.text = "High Score: " + highScore;
```

**Problem 3:**
Combine MenuManager, GameManager, and GameOverManager. Ensure all scenes are added to Build Settings (File > Build Settings). Wire all button OnClick events to the appropriate methods.

</details>
