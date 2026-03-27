# Day 10: Advanced Sliders & Progress Systems

**Learning Target:** I can create smooth, animated sliders and implement experience progress bars.

---

## Key Concepts

**Animated Value Changes**: Smoothly transition from old health to new health using `Lerp()` instead of instant updates.

**Progress Bars**: Similar to health bars but for XP, quest completion, or loading.

**Callbacks**: Use `onValueChanged` event to trigger effects (sounds, particle effects) when values change.

**Clamping**: Ensure values stay within min/max bounds.

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;

public class ExperienceBar : MonoBehaviour
{
    public Slider xpSlider;
    public TextMeshProUGUI levelText;
    
    private int currentLevel = 1;
    private int currentXP = 0;
    private int xpNeededForNextLevel = 100;
    private float lerpSpeed = 5f;
    private float targetSliderValue = 0;

    private void Start()
    {
        UpdateXPDisplay();
    }

    public void GainXP(int xpAmount)
    {
        currentXP += xpAmount;
        
        // Check for level up
        while (currentXP >= xpNeededForNextLevel)
        {
            currentXP -= xpNeededForNextLevel;
            LevelUp();
        }
        
        UpdateXPDisplay();
    }

    private void LevelUp()
    {
        currentLevel++;
        xpNeededForNextLevel = Mathf.RoundToInt(xpNeededForNextLevel * 1.1f);
        levelText.text = $"Level {currentLevel}";
        // Play level up effect
    }

    private void UpdateXPDisplay()
    {
        targetSliderValue = (float)currentXP / xpNeededForNextLevel;
        xpSlider.maxValue = 1f;
    }

    private void Update()
    {
        // Smoothly animate the slider
        xpSlider.value = Mathf.Lerp(xpSlider.value, targetSliderValue, lerpSpeed * Time.deltaTime);
    }
}
```

---

## Unity Setup Steps

1. **Create XP Bar UI**:
   - Canvas → Slider - Horizontal
   - Name it "XP Bar"

2. **Configure**:
   - Min Value: 0, Max Value: 1 (represents 0-100%)
   - Value: 0.5
   - Interactable: False

3. **Add Text Above**:
   - Create TextMeshPro text ("Level 1" → "Level 5")
   - Position above the slider

4. **Style**:
   - Fill color: Blue or gold (XP color)
   - Background: Gray
   - Make it responsive: Anchor to Top, Stretch Horizontal

5. **Attach Script**:
   - Create `ExperienceBar.cs`
   - Assign Slider reference in Inspector

---

## Guided Practice

1. **Build XP System**:
   - Implement GainXP() method
   - Test: Press Space to gain 20 XP
   - Verify level up triggers when reaching threshold

2. **Smooth Animation**:
   - Adjust `lerpSpeed` until the bar feels responsive but not instant
   - Does it feel game-like?

3. **Multiple Bars**:
   - Create Health, Stamina, and XP bars
   - Update all three simultaneously
   - Verify each has smooth animation

---

## Practice Problems

**Beginner:**
Create a simple "loading bar" that counts from 0 to 100% over 3 seconds.

**Intermediate:**
Create a quest progress bar that shows "1/5 items collected" and updates visually as player collects items.

**Challenge:**
Create a dual-layer progress bar: outer ring for overall quest, inner ring for current objective. Both animate independently.

<details><summary>💡 Hints</summary>
- Beginner: Use `yield return WaitForSeconds()` in a coroutine
- Intermediate: Track collected count, divide by total for percentage
- Challenge: Use two Slider components, or a custom shader that draws rings
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public IEnumerator LoadBar(Image fillImage)
{
    for (float t = 0; t < 3; t += Time.deltaTime)
    {
        fillImage.fillAmount = t / 3f;
        yield return null;
    }
    fillImage.fillAmount = 1f;
}
```

**Intermediate:**
```csharp
private int itemsCollected = 0;
private int itemsTotal = 5;

public void CollectItem()
{
    itemsCollected++;
    float progress = (float)itemsCollected / itemsTotal;
    questSlider.value = progress;
    questText.text = $"{itemsCollected}/{itemsTotal}";
}
```

**Challenge:**
```csharp
// Use two sliders, each with their own animation speed
// Outer: questProgress / totalQuests
// Inner: currentObjective / objectiveSteps
```
</details>
