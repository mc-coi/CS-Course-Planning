# Day 14: Pause Menu & Game Flow Control

**Learning Target:** I can implement a pause menu that freezes gameplay while allowing menu interaction.

---

## Key Concepts

**Time.timeScale**: Slows down or stops all physics/animations (set to 0 for pause).

**Pause Menu Overlay**: UI that appears on top of game without unloading the game scene.

**Input Handling**: Detect pause key (ESC) and toggle menu.

**Resume/Restart/MainMenu**: Buttons that change game state.

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class PauseManager : MonoBehaviour
{
    public static bool isPaused = false;
    public GameObject pauseMenuPanel;
    public Button resumeButton;
    public Button restartButton;
    public Button mainMenuButton;

    private void Start()
    {
        pauseMenuPanel.SetActive(false);
        resumeButton.onClick.AddListener(Resume);
        restartButton.onClick.AddListener(Restart);
        mainMenuButton.onClick.AddListener(GoToMainMenu);
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            if (isPaused)
                Resume();
            else
                Pause();
        }
    }

    public void Pause()
    {
        isPaused = true;
        Time.timeScale = 0f;  // FREEZE TIME
        pauseMenuPanel.SetActive(true);
    }

    public void Resume()
    {
        isPaused = false;
        Time.timeScale = 1f;  // UNFREEZE TIME
        pauseMenuPanel.SetActive(false);
    }

    public void Restart()
    {
        Time.timeScale = 1f;  // Don't forget to resume time!
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }

    public void GoToMainMenu()
    {
        Time.timeScale = 1f;  // IMPORTANT: Reset time before loading new scene
        SceneManager.LoadScene("MainMenu");
    }
}
```

---

## Unity Setup Steps

1. **Create Pause Menu Panel**:
   - In GameScene, right-click Canvas → UI → Panel
   - Set color to semi-transparent black
   - Name it "PauseMenuPanel"

2. **Add Buttons**:
   - Add Resume, Restart, MainMenu buttons to panel
   - Position them vertically in center

3. **Hide by Default**:
   - Select PauseMenuPanel
   - Uncheck the checkbox to disable it

4. **Attach Script**:
   - Create `PauseManager.cs`
   - Attach to a GameObject in the scene
   - In Inspector, assign:
     - pauseMenuPanel reference
     - Button references

5. **Test**:
   - Play scene
   - Press ESC to pause
   - Game should freeze, menu appears
   - Click Resume, game continues

---

## Guided Practice

1. **Basic Pause System**:
   - Implement pause/resume
   - Test that enemies freeze and resume smoothly
   - Verify time-based mechanics (animations, particles) freeze correctly

2. **Menu Persistence**:
   - Pause menu stays open until player resumes
   - Keyboard input (ESC) is still detected when paused
   - Can't interact with game behind menu

3. **Visual Feedback**:
   - Darken background when paused
   - Add a "PAUSED" label
   - Optional: Blur effect or animations for menu appearance

---

## Practice Problems

**Beginner:**
Create a pause menu that shows current playtime (even though time is frozen).

**Intermediate:**
Create a settings menu accessible from pause menu that can adjust volume and graphics quality.

**Challenge:**
Create a transition effect: When pausing, fade to black, show menu, then fade back in when resuming.

<details><summary>💡 Hints</summary>
- Beginner: Track elapsed time in a variable, pause doesn't prevent reading elapsed time
- Intermediate: Use Time.unscaledDeltaTime for UI animations that work during pause
- Challenge: Use a CanvasGroup with alpha fade during pause/resume
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
private float elapsedTime = 0;

void Update()
{
    if (!isPaused)
        elapsedTime += Time.deltaTime;
    
    playtimeText.text = $"Time: {elapsedTime:F0}s";
}
```

**Intermediate:**
```csharp
public void OpenSettings()
{
    settingsPanel.SetActive(true);
}

// Use Time.unscaledDeltaTime for sliders and buttons in pause menu
```

**Challenge:**
```csharp
IEnumerator FadeIn()
{
    CanvasGroup cg = pauseMenuPanel.GetComponent<CanvasGroup>();
    for (float t = 0; t < 0.5f; t += Time.unscaledDeltaTime)
    {
        cg.alpha = t / 0.5f;
        yield return null;
    }
}
```
</details>
