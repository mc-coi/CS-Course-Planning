# Day 7: Button Component & onClick Events

**Learning Target:** I can create interactive buttons and hook them to C# methods.

---

## Key Concepts

**Button Component**: Automatically handles UI interaction (hover, click, pressed states).

**onClick Event**: Fires when player clicks/taps the button. Can call multiple methods.

**Two Ways to Hook Buttons**:
1. **Inspector**: Drag object + select method in Editor (visual, no code needed)
2. **Script**: Use `button.onClick.AddListener()` to register methods programmatically

**Button States**: Automatic visual feedback:
- Normal: Default appearance
- Highlighted: Cursor hovering
- Pressed: Currently clicked
- Disabled: Grayed out

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;

public class ButtonManager : MonoBehaviour
{
    public Button playButton;
    public Button quitButton;

    private void Start()
    {
        // Method 1: Register listeners in code
        playButton.onClick.AddListener(OnPlayClicked);
        quitButton.onClick.AddListener(OnQuitClicked);
    }

    public void OnPlayClicked()
    {
        Debug.Log("Play button clicked!");
        // Start the game
    }

    public void OnQuitClicked()
    {
        Debug.Log("Quit button clicked!");
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }
}
```

---

## Unity Setup Steps

1. **Create Canvas with Buttons**:
   - Right-click Hierarchy → UI → Canvas
   - Right-click Canvas → UI → Button
   - Unity creates a Button with a TextMeshPro child

2. **Configure Button**:
   - In Inspector, Button component section
   - Click the circle next to "Normal Color" to set appearance
   - Navigation: "Automatic" (allows keyboard/gamepad control)

3. **Method A: Hook in Inspector**:
   - Select the Button
   - In Button component, find "On Click ()"
   - Click "+" to add a listener
   - Drag your script GameObject into the object field
   - Dropdown: Select your script class
   - Dropdown: Select the public method to call

4. **Method B: Hook in Code**:
   - Attach `ButtonManager.cs` script to a GameObject
   - Assign `playButton` reference in Inspector
   - Method is registered in `Start()`

5. **Test**:
   - Play the scene
   - Click the button
   - Check Console for debug output

---

## Guided Practice

1. **Create a Simple Menu**:
   - Canvas with 3 buttons: Start Game, Settings, Quit
   - Attach ButtonManager script
   - Hook each button to a different method
   - Test in Play mode

2. **Button Feedback**:
   - Change the button's "Highlighted Color" to yellow
   - Hover over button in Game view—does it change?

3. **Disable/Enable**:
   - Add a script that disables the "Settings" button
   - `settingsButton.interactable = false;`
   - Button should appear grayed out

---

## Practice Problems

**Beginner:**
Create a button that increments a counter and displays it in TextMeshPro text.

**Intermediate:**
Create two buttons: "Increase Volume" and "Decrease Volume." They should update a volume slider (or just log the current value).

**Challenge:**
Create a button that disables itself after being clicked, then re-enables itself after 5 seconds. Show a countdown timer on the button text.

<details><summary>💡 Hints</summary>
- Beginner: Use `GetComponent<TextMeshProUGUI>()` and `.text` property
- Intermediate: Create a public method that adjusts volume, call it from both buttons
- Challenge: Use a Coroutine and `button.interactable = false/true`
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public int counter = 0;
public TextMeshProUGUI counterText;

public void IncrementCounter()
{
    counter++;
    counterText.text = counter.ToString();
}
```

**Intermediate:**
```csharp
private float volume = 1f;

public void IncreaseVolume() { volume = Mathf.Min(1f, volume + 0.1f); UpdateUI(); }
public void DecreaseVolume() { volume = Mathf.Max(0f, volume - 0.1f); UpdateUI(); }

private void UpdateUI()
{
    Debug.Log($"Volume: {volume * 100}%");
}
```

**Challenge:**
```csharp
public void DisableTemporarily()
{
    button.interactable = false;
    StartCoroutine(EnableAfterDelay(5f));
}

IEnumerator EnableAfterDelay(float delay)
{
    for (float t = delay; t > 0; t -= Time.deltaTime)
    {
        button.GetComponentInChildren<TextMeshProUGUI>().text = $"Wait {t:F0}s";
        yield return null;
    }
    button.interactable = true;
    button.GetComponentInChildren<TextMeshProUGUI>().text = "Ready!";
}
```
</details>
