# Day 13: Main Menu & Scene Management

**Learning Target:** I can build a functional main menu and load scenes from buttons.

---

## Key Concepts

**Scene Management**: Switch between menu, gameplay, and other scenes using `SceneManager`.

**Menu Flow**: Main Menu → Gameplay Scene, or Pause Menu (overlay) → Resume/Quit.

**Button Actions**: Buttons call scene loading methods.

**Async Loading**: Load scenes in background without freezing game.

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;

public class MainMenuManager : MonoBehaviour
{
    public Button playButton;
    public Button settingsButton;
    public Button quitButton;

    private void Start()
    {
        playButton.onClick.AddListener(OnPlayClicked);
        settingsButton.onClick.AddListener(OnSettingsClicked);
        quitButton.onClick.AddListener(OnQuitClicked);
    }

    public void OnPlayClicked()
    {
        // Load the gameplay scene by name
        SceneManager.LoadScene("GameScene");
    }

    public void OnSettingsClicked()
    {
        // Load settings as additive (on top of menu)
        SceneManager.LoadScene("Settings", LoadSceneMode.Additive);
    }

    public void OnQuitClicked()
    {
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }

    public void BackToMenu()
    {
        SceneManager.LoadScene("MainMenu");
    }
}
```

---

## Unity Setup Steps

1. **Setup Scenes**:
   - Create "MainMenu" scene with buttons
   - Create "GameScene" with game objects
   - Save both

2. **Add to Build Settings**:
   - File → Build Settings
   - Drag MainMenu into Scenes to Build (Index 0)
   - Drag GameScene (Index 1)
   - Verify order

3. **Create Main Menu**:
   - Canvas with buttons: Play, Settings, Quit
   - Attach MainMenuManager script
   - Hook buttons to methods

4. **Test Scene Loading**:
   - Play MainMenu scene
   - Click Play button
   - Should load GameScene

5. **Optional: Loading Screen**:
   - Add a loading screen scene with progress bar
   - Use async loading to show progress

---

## Guided Practice

1. **Build Main Menu**:
   - Create Play, Settings, Quit buttons
   - Hook to SceneManager methods
   - Test in Play mode

2. **Scene Transitions**:
   - From GameScene, add a "Return to Menu" button
   - Loading screen in between transitions

3. **Fade Effect**:
   - Add a black panel that fades in/out during transitions
   - Smooth visual effect, not jarring cut

---

## Practice Problems

**Beginner:**
Create a simple main menu with Play and Quit buttons that actually load a game scene or quit.

**Intermediate:**
Build a complete menu flow: Main → Settings → Audio (submenu) → Back to Settings → Back to Main.

**Challenge:**
Implement an async scene loader that shows a loading progress bar while the scene loads in background.

<details><summary>💡 Hints</summary>
- Beginner: Use `SceneManager.LoadScene()` with scene name
- Intermediate: Use additive loading, track menu stack
- Challenge: Use `AsyncOperation` and `isDone` property to track progress
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public void Play() => SceneManager.LoadScene("GameScene");
public void Quit() => Application.Quit();
```

**Intermediate:**
```csharp
private Stack<string> menuStack = new Stack<string>();

public void OpenMenu(string menuName)
{
    menuStack.Push(menuName);
    SceneManager.LoadScene(menuName, LoadSceneMode.Additive);
}

public void BackToMenu()
{
    string current = menuStack.Pop();
    SceneManager.UnloadSceneAsync(current);
    if (menuStack.Count > 0)
        SceneManager.LoadScene(menuStack.Peek(), LoadSceneMode.Additive);
}
```

**Challenge:**
```csharp
public void LoadSceneAsync(string sceneName)
{
    StartCoroutine(LoadAsyncCoroutine(sceneName));
}

IEnumerator LoadAsyncCoroutine(string sceneName)
{
    AsyncOperation asyncOp = SceneManager.LoadSceneAsync(sceneName);
    while (!asyncOp.isDone)
    {
        float progress = asyncOp.progress;
        progressBar.value = progress;
        yield return null;
    }
}
```
</details>
