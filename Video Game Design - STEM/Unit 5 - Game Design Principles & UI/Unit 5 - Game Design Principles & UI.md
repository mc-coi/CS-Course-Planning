# Unit 5: Game Design Principles & UI

## Unit Overview

**Duration:** Days 17-20 (4 days)
**Key Concepts:** MDA framework, level design, UI systems, canvas, TextMeshPro, menus, scene management
**Big Idea:** Games need thoughtful design and clear communication. Level design teaches through play, UI provides feedback, and menus guide players through the experience.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Apply the MDA framework to analyze and design games
- [ ] Understand the core game loop and player motivation
- [ ] Design levels that teach through play (onboarding)
- [ ] Explain grayboxing and rapid prototyping
- [ ] Create Canvas and UI elements in scenes
- [ ] Use TextMeshPro for text rendering
- [ ] Implement UI anchoring and scaling for different resolutions
- [ ] Create menus with buttons that load scenes
- [ ] Use SceneManager to load and manage scenes
- [ ] Implement persistent data with PlayerPrefs
- [ ] Design effective UI feedback systems

---

## Day-by-Day Content

### Day 17: MDA Framework & Game Loop

#### Key Concepts
- **MDA Framework:** Mechanics (rules), Dynamics (interactions), Aesthetics (emotions)
- **Core Game Loop:** The repeating sequence of actions the player performs
- **Mechanics:** The rules and systems (jump, collect, defeat)
- **Dynamics:** How mechanics interact (increasing difficulty, chaining actions)
- **Aesthetics:** The emotional response (fun, tension, satisfaction)
- **Bartle Types:** Four player motivations (Achiever, Explorer, Socializer, Killer)
- **Player Motivation:** Why players play (challenge, exploration, story, competition)

#### Content
Every game can be analyzed through the MDA framework:

**Mechanics:** The rules. In Mario, you can jump, move, and collect coins.

**Dynamics:** How rules create interactions. Jumping over obstacles while collecting coins creates a rhythm. Enemies force you to dodge while collecting—increasing pressure.

**Aesthetics:** How interactions make players *feel*. The combination of jumping, collecting, and dodging creates tension and relief. Players feel accomplished when they beat a level.

**Core Game Loop:**
Every game has a repeating loop:
1. Player receives feedback (visual/audio)
2. Player makes decision (input)
3. Game responds (mechanics resolve)
4. Loop repeats

Example: In Pac-Man:
- See pellets and ghosts (feedback)
- Move with arrow keys (decision)
- Eat pellet, check if ghost touched you (mechanics)
- Repeat

**Bartle Types** describe player motivations:
- **Achiever:** Wants to overcome challenges, earn rewards, reach goals
- **Explorer:** Wants to discover secrets, understand systems, learn the world
- **Socializer:** Wants to interact with others, collaborate, tell stories
- **Killer:** Wants to compete, dominate, challenge other players

Different games appeal to different types. Many players exhibit multiple motivations.

#### Annotated Code Example

```csharp
using UnityEngine;

public class GameLoopManager : MonoBehaviour
{
    [System.Serializable]
    public class GameState
    {
        public int score = 0;
        public int health = 100;
        public int level = 1;
        public bool isPaused = false;
    }

    public GameState gameState = new GameState();

    // Simulating the core game loop:
    // 1. Feedback (UI update)
    // 2. Input (player decision)
    // 3. Resolution (mechanics)
    // 4. Repeat

    void Update()
    {
        if (gameState.isPaused)
            return;

        // Step 1: Provide feedback
        UpdateUI();

        // Step 2: Get player input
        HandleInput();

        // Step 3: Resolve mechanics
        UpdateGameMechanics();

        // Step 4: Repeat (Update() calls itself every frame)
    }

    void UpdateUI()
    {
        // Show current score, health, etc.
        Debug.Log($"Score: {gameState.score} | Health: {gameState.health} | Level: {gameState.level}");
    }

    void HandleInput()
    {
        // Player makes decisions
        if (Input.GetKeyDown(KeyCode.Space))
        {
            OnPlayerAction("Jump");
        }
    }

    void UpdateGameMechanics()
    {
        // Game responds to input
        // (Could damage player, collect items, etc.)
    }

    void OnPlayerAction(string action)
    {
        Debug.Log("Player performed: " + action);
        // Trigger feedback (particles, sounds, visual feedback)
    }

    public void AddScore(int points)
    {
        gameState.score += points;
    }

    public void TakeDamage(int damage)
    {
        gameState.health -= damage;
        if (gameState.health <= 0)
        {
            GameOver();
        }
    }

    void GameOver()
    {
        Debug.Log("Game Over! Final Score: " + gameState.score);
        gameState.isPaused = true;
    }
}
```

---

### Day 18: Level Design & Grayboxing

#### Key Concepts
- **Level Design:** Creating challenges and teaching players through play
- **Onboarding:** Teaching mechanics early without tutorials
- **Grayboxing:** Using simple placeholder shapes to prototype level layouts
- **Pacing:** Varying difficulty to maintain engagement
- **Progression:** Gradually introducing new challenges
- **Learning Curve:** How quickly players master mechanics
- **Feedback:** Clear signals for what's allowed/forbidden
- **Safe Zone:** Area where players can practice without punishment

#### Content
Great level design teaches through play. Players learn by doing, not by reading.

**Teaching Through Play:**
- First level: Introduce jumping
- Second level: Combine jumping + obstacles
- Third level: Add enemies; avoid while jumping
- Fourth level: Combine all mechanics; increase pressure

Players learn by experiencing consequences. A hazard spike teaches "don't touch!" without explanation.

**Grayboxing:**
Grayboxing is building levels with placeholder geometry (gray cubes, boxes) before adding final art. This lets you:
- Test gameplay quickly
- Adjust difficulty and pacing
- Iterate without waiting for artists
- Focus on mechanics, not visuals

Create a level with:
1. A safe starting area
2. Introduce one mechanic
3. Practice zone
4. Challenge zone
5. Safe end area

**Pacing:**
Vary difficulty to maintain engagement:
- Easy section to relax
- Medium section to engage
- Hard section for challenge
- Easy section to celebrate victory

#### Annotated Code Example

```csharp
using UnityEngine;

public class LevelManager : MonoBehaviour
{
    [System.Serializable]
    public class LevelProgression
    {
        public int levelNumber = 1;
        public float baseEnemySpeed = 2f;
        public int numEnemies = 1;
        public float timeLimit = 60f;
    }

    public LevelProgression[] levels;
    private int currentLevelIndex = 0;

    void Start()
    {
        LoadLevel(0);
    }

    void LoadLevel(int index)
    {
        if (index >= levels.Length)
        {
            Debug.Log("All levels complete!");
            return;
        }

        currentLevelIndex = index;
        LevelProgression levelData = levels[index];

        Debug.Log($"Loading Level {levelData.levelNumber}");
        Debug.Log($"Difficulty: {levelData.baseEnemySpeed}x speed, {levelData.numEnemies} enemies");
        Debug.Log($"Time limit: {levelData.timeLimit} seconds");

        // Spawn enemies based on level difficulty
        SpawnEnemies(levelData.numEnemies, levelData.baseEnemySpeed);
    }

    void SpawnEnemies(int count, float speed)
    {
        for (int i = 0; i < count; i++)
        {
            Debug.Log($"Spawning enemy {i + 1} with speed {speed}");
            // In a real game, instantiate enemy prefab here
        }
    }

    public void CompleteLevel()
    {
        Debug.Log("Level complete!");
        if (currentLevelIndex < levels.Length - 1)
        {
            LoadLevel(currentLevelIndex + 1);
        }
        else
        {
            Debug.Log("Game complete!");
        }
    }

    // Graybox level structure:
    // 1. Safe starting zone (player learns controls)
    // 2. Tutorial zone (single mechanic practiced)
    // 3. Challenge zone (increased difficulty)
    // 4. Mastery zone (all mechanics combined)
    // 5. Safe ending zone (celebration)
}
```

---

### Day 19: Canvas & UI Elements

#### Key Concepts
- **Canvas:** Container for all UI elements (buttons, text, images)
- **Screen Space vs. World Space:** UI in screen (overlay) vs. in world (3D objects)
- **Anchors:** Reference points for UI positioning (corners, center, etc.)
- **Rect Transform:** Special transform for UI elements with width/height
- **TextMeshPro:** Professional text rendering for UI
- **Button:** Interactive element that triggers callbacks on click
- **Slider:** Draggable bar for values (volume, health bar, etc.)
- **Layout Groups:** Auto-arrange child UI elements
- **Image:** Display textures/colors as UI

#### Content
Canvas is the foundation for all UI. Think of it as a 2D layer on top of the 3D world.

**Creating UI:**
1. Right-click in Hierarchy > UI > Button
2. Unity auto-creates a Canvas if needed
3. The Button becomes a child of Canvas
4. Adjust Anchors to position on screen

**Anchors:**
Anchors determine how UI scales with different screen sizes.
- Top-left anchor → top-left positioning
- Center anchor → center positioning
- Stretch → full-width/height

Use anchors to make UI responsive on different devices.

**TextMeshPro:**
Modern, high-quality text rendering. Better than legacy Text:
- Supports rich text tags (`<b>bold</b>`, `<color=red>text</color>`)
- Scales beautifully to any resolution
- Professional appearance

#### Annotated Code Example

```csharp
using UnityEngine;
using TMPro;
using UnityEngine.UI;

public class UIManager : MonoBehaviour
{
    [Header("Text Elements")]
    public TextMeshProUGUI scoreText;
    public TextMeshProUGUI healthText;
    public TextMeshProUGUI levelText;

    [Header("UI Elements")]
    public Slider healthBar;
    public Button pauseButton;
    public Button playButton;
    public Image damageOverlay;

    private int currentScore = 0;
    private int currentHealth = 100;
    private int maxHealth = 100;

    void Start()
    {
        // Set up button listeners
        pauseButton.onClick.AddListener(OnPauseClicked);
        playButton.onClick.AddListener(OnPlayClicked);

        // Initialize UI with starting values
        UpdateScoreDisplay();
        UpdateHealthDisplay();
    }

    void Update()
    {
        // Update health bar in real-time
        healthBar.value = (float)currentHealth / maxHealth;
    }

    // Called when score changes
    public void AddScore(int points)
    {
        currentScore += points;
        UpdateScoreDisplay();
    }

    void UpdateScoreDisplay()
    {
        // Use rich text tags for styling
        scoreText.text = $"<b>Score:</b> <color=yellow>{currentScore}</color>";
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        if (currentHealth < 0)
            currentHealth = 0;

        UpdateHealthDisplay();
        StartCoroutine(DamageFlash());
    }

    void UpdateHealthDisplay()
    {
        // Change color based on health state
        Color healthColor = currentHealth > 50 ? Color.green : Color.red;
        healthText.text = $"<color=#{ColorUtility.ToHtmlStringRGB(healthColor)}>Health: {currentHealth}/{maxHealth}</color>";

        healthBar.value = (float)currentHealth / maxHealth;
    }

    void OnPauseClicked()
    {
        Time.timeScale = 0f;  // Pause the game
        Debug.Log("Game paused");
    }

    void OnPlayClicked()
    {
        Time.timeScale = 1f;  // Resume the game
        Debug.Log("Game resumed");
    }

    System.Collections.IEnumerator DamageFlash()
    {
        // Flash red overlay when taking damage
        damageOverlay.color = new Color(1, 0, 0, 0.5f);
        yield return new WaitForSeconds(0.2f);
        damageOverlay.color = new Color(1, 0, 0, 0);
    }
}
```

---

### Day 20: Menus, Scene Management & Persistence

#### Key Concepts
- **Scene:** A level or menu screen in the game
- **SceneManager:** Loads, manages, and transitions between scenes
- **Additive Loading:** Loading a scene on top of another (for UI)
- **DontDestroyOnLoad():** Prevents object destruction when loading new scene
- **PlayerPrefs:** Persistent data storage (settings, high scores, etc.)
- **Menu Flow:** Start menu → Play menu → Game → Game Over menu
- **Button Navigation:** Connecting buttons to scene loading
- **Audio Persistence:** Music that plays across scenes

#### Content
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

#### Annotated Code Example

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

---

## Practice Problems

### Beginner Tier

**Problem 1:** Create a simple main menu with three buttons: Play, Settings, and Quit.

<details>
<summary>Hint</summary>
Create a Canvas with three buttons. Add OnClick listeners that call different methods (LoadScene, ShowSettings, Quit).
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class SimpleMenu : MonoBehaviour
{
    public void PlayButtonClicked()
    {
        SceneManager.LoadScene("GameScene");
    }

    public void SettingsButtonClicked()
    {
        Debug.Log("Opening settings");
    }

    public void QuitButtonClicked()
    {
        Application.Quit();
    }
}
```
</details>

---

**Problem 2:** Display the player's score on a TextMeshProUGUI element and update it when they collect items.

<details>
<summary>Hint</summary>
Get the TextMeshProUGUI component. Update its text property whenever score changes.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;
using TMPro;

public class ScoreDisplay : MonoBehaviour
{
    public TextMeshProUGUI scoreText;
    private int score = 0;

    public void AddScore(int points)
    {
        score += points;
        scoreText.text = "Score: " + score;
    }
}
```
</details>

---

**Problem 3:** Create a slider that represents the player's health bar.

<details>
<summary>Hint</summary>
Create a Slider UI element. Set its value to currentHealth / maxHealth. Update it when player takes damage.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;
using UnityEngine.UI;

public class HealthBar : MonoBehaviour
{
    public Slider healthSlider;
    public int maxHealth = 100;
    private int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
        UpdateHealthBar();
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        if (currentHealth < 0)
            currentHealth = 0;
        UpdateHealthBar();
    }

    void UpdateHealthBar()
    {
        healthSlider.value = (float)currentHealth / maxHealth;
    }
}
```
</details>

---

### Intermediate Tier

**Problem 4:** Create a settings menu that saves player preferences (volume, difficulty) using PlayerPrefs.

<details>
<summary>Hint</summary>
Use PlayerPrefs.SetFloat() and PlayerPrefs.GetFloat(). Load saved values on startup.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;
using UnityEngine.UI;

public class SettingsManager : MonoBehaviour
{
    public Slider volumeSlider;
    public Dropdown difficultyDropdown;

    void Start()
    {
        // Load saved settings
        volumeSlider.value = PlayerPrefs.GetFloat("Volume", 0.5f);
        difficultyDropdown.value = PlayerPrefs.GetInt("Difficulty", 1);
    }

    public void OnVolumeChanged(float volume)
    {
        PlayerPrefs.SetFloat("Volume", volume);
    }

    public void OnDifficultyChanged(int difficulty)
    {
        PlayerPrefs.SetInt("Difficulty", difficulty);
    }
}
```
</details>

---

**Problem 5:** Design a complete game level that teaches a new mechanic through play without explicit tutorials.

<details>
<summary>Hint</summary>
Design the level progression: safe zone → introduce mechanic → practice zone → challenge zone → end. Use obstacles and hazards to teach.
</details>

<details>
<summary>Answer</summary>
This is a design task. Example:
1. Safe flat area (player learns movement)
2. Small jump gap (player learns jumping)
3. Multiple gaps (practice jumping)
4. Platform with hazard spike (player learns to avoid)
5. Combination: jump, collect coin, avoid spike (all mechanics)
6. Exit door

Each section teaches by experience, not instructions.
</details>

---

**Problem 6:** Create a game over screen that displays the final score and high score, with buttons to retry or return to menu.

<details>
<summary>Hint</summary>
Load the scene on game over. Display scores from PlayerPrefs. Create buttons that load appropriate scenes.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using TMPro;

public class GameOverScreen : MonoBehaviour
{
    public TextMeshProUGUI finalScoreText;
    public TextMeshProUGUI highScoreText;

    void Start()
    {
        int finalScore = PlayerPrefs.GetInt("FinalScore", 0);
        int highScore = PlayerPrefs.GetInt("HighScore", 0);

        finalScoreText.text = "Score: " + finalScore;
        highScoreText.text = "High Score: " + highScore;
    }

    public void RetryButtonClicked()
    {
        SceneManager.LoadScene("GameScene");
    }

    public void MenuButtonClicked()
    {
        SceneManager.LoadScene("MainMenu");
    }
}
```
</details>

---

### Challenge Tier

**Problem 7:** Create a complete multi-scene game with menu → gameplay → game over → menu loop. Include score persistence.

<details>
<summary>Hint</summary>
Create three scenes: MainMenu, GameScene, GameOverScene. Use SceneManager to transition. Use PlayerPrefs to save/load scores.
</details>

<details>
<summary>Answer</summary>
Combine the code examples from Day 20. Create three scenes and implement the transition logic.
</details>

---

**Problem 8:** Design and document a complete level using the graybox method, explaining how each section teaches mechanics progressively.

<details>
<summary>Hint</summary>
Create a document describing: Safe zone (learning), Tutorial zone (single mechanic), Challenge zone (multiple mechanics), Mastery zone (all combined), Boss/climax.
</details>

<details>
<summary>Answer</summary>
This is a design document task. Create detailed level layout descriptions with explanations of learning progression.
</details>

---

## Practice Bank (15 Problems)

1. **MDA Analysis:** Pick a game you know and analyze it through the MDA framework (mechanics, dynamics, aesthetics).

2. **Canvas Exploration:** Create a Canvas with 5+ different UI elements (buttons, sliders, text, images). Adjust anchors and test on different screen resolutions.

3. **TextMeshPro Formatting:** Create text with rich text tags: bold, colored, sized, and styled. Test different fonts.

4. **Button Network:** Create a menu with buttons that link to different panels/scenes. Implement proper transitions.

5. **Score System:** Implement a complete score system with display, save/load, and high score tracking.

6. **Health Bar UI:** Create both a number display (100/100) and a visual bar that empties as health decreases.

7. **Pause Menu:** Create a pause menu that freezes gameplay (Time.timeScale = 0) and unfreezes on resume.

8. **PlayerPrefs Practice:** Save 5+ different player settings and verify they persist across scenes.

9. **Scene Transitions:** Create smooth fade-in/fade-out transitions between scenes using CanvasGroup alpha.

10. **Level Design Document:** Write a one-page level design document for a platformer level, including difficulty progression.

11. **Tutorial Design:** Design an onboarding level that teaches one new mechanic at a time without text instructions.

12. **Difficulty Scaling:** Create a difficulty selection menu that changes gameplay parameters (enemy speed, time limit, etc.).

13. **Leaderboard Simulation:** Create a UI that displays top 5 scores, with current player highlighted.

14. **Responsive UI:** Design a UI that works correctly on mobile (portrait), tablet (landscape), and desktop resolutions.

15. **Game Loop Analysis:** Create a flowchart describing the core loop of your favorite game and identify feedback, input, resolution, and repetition.

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| UI elements don't appear | Canvas not in scene or element outside canvas bounds | Always create UI elements as children of Canvas |
| Buttons don't respond to clicks | OnClick event not set up or button disabled | Check button's InteractableToggle and OnClick list |
| TextMeshPro looks blurry | Font asset missing or resolution too low | Ensure TextMeshPro essential resources are imported |
| SceneManager.LoadScene freezes | Scene is very large or has lots of initialization | Use LoadSceneAsync for large scenes with loading screen |
| PlayerPrefs data doesn't save | Not calling PlayerPrefs.Save() (mobile only) or wrong key name | Use consistent key names; call Save() on mobile |
| UI scaling looks wrong on different resolutions | Incorrect anchor/pivot settings | Set anchors based on desired behavior (corners, stretch, etc.) |
| Game unpauses immediately after pause | Time.timeScale not properly managed | Ensure all pause state changes go through a single manager |
| Scene transitions are jarring | No fade or transition effect | Add fade-in/fade-out using CanvasGroup.alpha |
| High score doesn't persist | Forgot to save to PlayerPrefs on level complete | Always save high score when game ends |
| UI overlaps game objects | Canvas render mode is Screen Space (Overlay) | Use Screen Space (Camera) for layered UI |

---

## Assessment Prep: 10 Q&As

**Q1: Explain the MDA framework and give an example from a game.**
A: MDA = Mechanics (rules), Dynamics (interactions), Aesthetics (emotions). Example: Pac-Man's mechanic of eating pellets creates the dynamic of avoiding ghosts, which creates the aesthetic of suspense and relief.

**Q2: What is the core game loop?**
A: Feedback (see result) → Input (make decision) → Resolution (mechanics respond) → Repeat. Every game repeats this cycle.

**Q3: What is grayboxing and why is it useful?**
A: Using simple placeholder shapes (gray boxes) to prototype level layouts. It's useful for testing gameplay mechanics without waiting for final art.

**Q4: How do you create a responsive UI that works on different screen sizes?**
A: Use Anchors to position elements relative to screen edges. Use Layout Groups to auto-arrange child elements.

**Q5: What is TextMeshPro and how does it differ from legacy Text?**
A: TextMeshPro is modern, high-quality text rendering. It supports rich text tags, scales beautifully, and looks professional. Legacy Text is lower quality.

**Q6: How do you load a new scene and why would you use SceneManager?**
A: Use `SceneManager.LoadScene("SceneName");`. SceneManager organizes multiple scenes (menus, levels, etc.) and manages transitions.

**Q7: What does PlayerPrefs do and how do you use it?**
A: PlayerPrefs saves small amounts of persistent data (high scores, settings). Use `PlayerPrefs.SetInt("key", value);` to save and `PlayerPrefs.GetInt("key");` to load.

**Q8: How do you make a button load a new scene?**
A: Add an onClick listener to the button. In the callback, use `SceneManager.LoadScene("SceneName");`.

**Q9: Explain the difference between teaching through play and explicit tutorials.**
A: Teaching through play: level design forces players to learn by doing. Explicit tutorials: text/narration explains mechanics. Play teaches better because players learn by experience.

**Q10: What are Bartle Types and why do game designers care?**
A: Four player motivations: Achiever (challenge), Explorer (discovery), Socializer (interaction), Killer (competition). Designers create content for each type to appeal to diverse players.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **MDA** | Mechanics, Dynamics, Aesthetics (design framework) |
| **Mechanics** | Rules and systems of the game |
| **Dynamics** | How mechanics interact during play |
| **Aesthetics** | Emotional response players have |
| **Core Loop** | Repeating feedback-input-resolution cycle |
| **Grayboxing** | Using placeholder geometry to prototype |
| **Onboarding** | Teaching new players through early level design |
| **Canvas** | Container for all UI elements |
| **Anchor** | Reference point for UI positioning |
| **TextMeshPro** | Professional text rendering system |
| **Slider** | UI bar for numeric values |
| **Button** | Interactive UI element |
| **SceneManager** | Loads and manages scenes |
| **PlayerPrefs** | Persistent data storage |

### UI Quick Reference

```csharp
using TMPro;
using UnityEngine.UI;

// Text display and styling
TextMeshProUGUI text = GetComponent<TextMeshProUGUI>();
text.text = "Hello";
text.text = "<b>Bold</b> <i>Italic</i> <color=red>Red</color>";

// Button setup
Button button = GetComponent<Button>();
button.onClick.AddListener(() => Debug.Log("Clicked!"));

// Slider for values
Slider slider = GetComponent<Slider>();
slider.value = 0.5f;  // 0 to 1
slider.onValueChanged.AddListener((value) => Debug.Log(value));

// Anchoring UI
RectTransform rect = GetComponent<RectTransform>();
rect.anchorMin = Vector2.zero;  // Bottom-left
rect.anchorMax = Vector2.one;   // Top-right
```

### Scene Management Quick Reference

```csharp
using UnityEngine.SceneManagement;

// Load scene
SceneManager.LoadScene("SceneName");

// Load additive (on top of current)
SceneManager.LoadScene("UILayer", LoadSceneMode.Additive);

// Async load with progress
StartCoroutine(LoadSceneAsync("LargeScene"));

System.Collections.IEnumerator LoadSceneAsync(string sceneName)
{
    AsyncOperation async = SceneManager.LoadSceneAsync(sceneName);
    while (!async.isDone)
    {
        float progress = async.progress;
        yield return null;
    }
}

// DontDestroyOnLoad for persistent objects
DontDestroyOnLoad(gameObject);
```

### PlayerPrefs Quick Reference

```csharp
// Save data
PlayerPrefs.SetInt("HighScore", 1000);
PlayerPrefs.SetFloat("Volume", 0.8f);
PlayerPrefs.SetString("PlayerName", "Hero");

// Load data
int highScore = PlayerPrefs.GetInt("HighScore", 0);  // default: 0
float volume = PlayerPrefs.GetFloat("Volume", 0.5f);
string name = PlayerPrefs.GetString("PlayerName", "Player");

// Delete specific key
PlayerPrefs.DeleteKey("HighScore");

// Delete all
PlayerPrefs.DeleteAll();

// Force save (mobile)
PlayerPrefs.Save();
```

---

## Additional Resources

- **Level Design Fundamentals:** https://www.gamasutra.com
- **TextMeshPro Documentation:** https://docs.unity3d.com/Manual/TextMeshPro.html
- **SceneManager Reference:** https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html
- **UI Anchor Presets:** Window > 2D > UI Builder

