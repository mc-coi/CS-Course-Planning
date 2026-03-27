# Day 6: TextMeshPro & Dynamic Text

**Learning Target:** I can display and update text in UI using TextMeshPro.

---

## Key Concepts

**TextMeshPro (TMP)**: Modern text system that replaces legacy Text component.
- **Pros**: Sharper text, better performance, supports rich text formatting, emojis
- **Cons**: Requires TMP Essentials import (Unity does this automatically)

**Rich Text Tags**: Format text without code.
- `<b>bold</b>`, `<i>italic</i>`, `<color=red>red text</color>`
- `<size=50>large</size>`, `<sprite=0>` for icons

**Dynamic Updates**: Change text from C# script using `.text` property.

---

## Code Example

```csharp
using UnityEngine;
using TMPro;

public class ScoreDisplay : MonoBehaviour
{
    private TextMeshProUGUI scoreText;
    private int score = 0;

    private void Start()
    {
        scoreText = GetComponent<TextMeshProUGUI>();
        UpdateScoreDisplay();
    }

    public void AddScore(int points)
    {
        score += points;
        UpdateScoreDisplay();
    }

    private void UpdateScoreDisplay()
    {
        // Simple update
        scoreText.text = $"Score: {score}";
        
        // Or with rich text formatting
        scoreText.text = $"<color=yellow><b>Score: {score}</b></color>";
    }
}
```

---

## Unity Setup Steps

1. **Create Canvas** (if you don't have one):
   - Right-click Hierarchy → UI → Canvas

2. **Add TextMeshPro Text**:
   - Right-click Canvas → UI → Text - TextMeshPro
   - Unity imports TMP Essentials automatically (first time)

3. **Configure Text**:
   - In Inspector, find TextMeshPro component
   - Text: "Hello, World!"
   - Font: Select TMP_FontAsset (LiberationSans is default)
   - Size: 36
   - Alignment: Center

4. **Position it**:
   - RectTransform → Anchor Preset: Center
   - Width: 400, Height: 100

5. **Attach a script**:
   - Create `ScoreDisplay.cs`
   - Add `using TMPro;`
   - Get component: `GetComponent<TextMeshProUGUI>()`

---

## Guided Practice

1. **Create a Score Counter**:
   - Add TextMeshPro text to Canvas
   - Attach ScoreDisplay script
   - In Update, press Space to add 10 points
   - Verify score updates on screen

2. **Format with Rich Text**:
   - Modify the script to display: `"<color=lime><size=50>Score: {score}</size></color>"`
   - Does it look good?

3. **Timer Display**:
   - Create another TextMeshPro text
   - Attach a timer script that counts down from 60
   - Display: `"Time: {minutes}:{seconds:D2}"` (D2 = two digits with leading zero)

---

## Practice Problems

**Beginner:**
Write a script that displays the current FPS (frames per second) on screen using TextMeshPro.

**Intermediate:**
Create a feedback text that pops up when the player picks up an item, shows "+50 XP" in gold color, and fades out over 2 seconds.

**Challenge:**
Build a dialogue system where text appears letter-by-letter (typewriter effect) using a coroutine.

<details><summary>💡 Hints</summary>
- Beginner: Use `1f / Time.deltaTime` to calculate FPS
- Intermediate: Use `CanvasGroup.alpha` to fade. Use Coroutine with `WaitForSeconds`
- Challenge: Use `string.Substring(0, index)` in a loop with small delays
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
private TextMeshProUGUI fpsText;
private float fpsTimer = 0;

void Update()
{
    fpsTimer += Time.deltaTime;
    if (fpsTimer >= 0.5f)
    {
        int fps = Mathf.RoundToInt(1f / Time.deltaTime);
        fpsText.text = $"FPS: {fps}";
        fpsTimer = 0;
    }
}
```

**Intermediate:**
```csharp
public void ShowXPGain(int xp)
{
    tmpText.text = $"<color=gold>+{xp} XP</color>";
    StartCoroutine(FadeOut());
}

IEnumerator FadeOut()
{
    CanvasGroup cg = GetComponent<CanvasGroup>();
    for (float t = 2; t > 0; t -= Time.deltaTime)
    {
        cg.alpha = t / 2;
        yield return null;
    }
}
```

**Challenge:**
```csharp
public IEnumerator TypeWriter(string fullText, float delay = 0.05f)
{
    for (int i = 0; i <= fullText.Length; i++)
    {
        tmpText.text = fullText.Substring(0, i);
        yield return new WaitForSeconds(delay);
    }
}
```
</details>
