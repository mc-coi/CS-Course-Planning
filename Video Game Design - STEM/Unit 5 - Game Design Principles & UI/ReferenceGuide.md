# Vocabulary & Quick Reference

## Key Terms

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

## Key Syntax

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

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| UI elements don't appear | Canvas not in scene or element outside canvas bounds | Always create UI elements as children of Canvas |
| Buttons don't respond to clicks | OnClick event not set up or button disabled | Check button's Interactable Toggle and OnClick list |
| TextMeshPro looks blurry | Font asset missing or resolution too low | Ensure TextMeshPro essential resources are imported |
| SceneManager.LoadScene freezes | Scene is very large or has lots of initialization | Use LoadSceneAsync for large scenes with loading screen |
| PlayerPrefs data doesn't save | Not calling PlayerPrefs.Save() (mobile only) or wrong key name | Use consistent key names; call Save() on mobile |
| UI scaling looks wrong on different resolutions | Incorrect anchor/pivot settings | Set anchors based on desired behavior (corners, stretch, etc.) |
| Game unpauses immediately after pause | Time.timeScale not properly managed | Ensure all pause state changes go through a single manager |
| Scene transitions are jarring | No fade or transition effect | Add fade-in/fade-out using CanvasGroup.alpha |
| High score doesn't persist | Forgot to save to PlayerPrefs on level complete | Always save high score when game ends |
| UI overlaps game objects | Canvas render mode is Screen Space (Overlay) | Use Screen Space (Camera) for layered UI |
