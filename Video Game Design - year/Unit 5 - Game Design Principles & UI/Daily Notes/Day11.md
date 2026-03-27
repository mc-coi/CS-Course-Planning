# Day 11: Score Systems & Displaying Dynamic Data

**Learning Target:** I can implement a score system and display it dynamically on screen.

---

## Key Concepts

**Static Score Manager**: Centralized score tracking accessible from any script.

**Updating Text at Runtime**: TextMeshPro updates when score changes.

**Score Formatting**: Display with separators (1,000,000) or suffixes (1.2M).

**Notifications**: Show "+100 points!" briefly when score increases.

---

## Code Example

```csharp
using UnityEngine;
using TMPro;

public class ScoreManager : MonoBehaviour
{
    public static ScoreManager instance;
    public static int score { get; private set; } = 0;

    private TextMeshProUGUI scoreDisplay;

    private void Awake()
    {
        if (instance != null && instance != this)
            Destroy(gameObject);
        else
            instance = this;
    }

    private void Start()
    {
        scoreDisplay = GetComponent<TextMeshProUGUI>();
        UpdateDisplay();
    }

    public static void AddScore(int points)
    {
        score += points;
        instance.UpdateDisplay();
        instance.ShowScorePopup(points);
    }

    private void UpdateDisplay()
    {
        // Format with commas: 1,000,000
        scoreDisplay.text = $"Score: {score.ToString("N0")}";
    }

    private void ShowScorePopup(int points)
    {
        // Create floating text showing "+{points}"
        Debug.Log($"+{points} points!");
    }
}
```

---

## Unity Setup Steps

1. **Create Score Display**:
   - Canvas → TextMeshPro Text
   - Position: Top-center
   - Text: "Score: 0"
   - Font size: 48

2. **Attach ScoreManager**:
   - Create `ScoreManager.cs`
   - Attach to the TextMeshPro GameObject
   - Set Singleton in Awake()

3. **Make it Persistent**:
   - Add `DontDestroyOnLoad(gameObject);` in Awake()
   - Score persists between scenes

4. **Test**:
   - Call `ScoreManager.AddScore(100)` from any script
   - Verify text updates

---

## Guided Practice

1. **Basic Score System**:
   - Create enemy that awards 10 points when defeated
   - Press Space to "defeat" enemy
   - Verify score updates with formatting (1,200 instead of 1200)

2. **Floating Text**:
   - When score increases, show "+10" briefly near center screen
   - Use TextMeshPro popup, fade out over 0.5 seconds

3. **High Score Tracking**:
   - Save high score to PlayerPrefs
   - Display "High Score: XXX" next to current score
   - Update only if current > high score

---

## Practice Problems

**Beginner:**
Create a script that multiplies score by 2x for 10 seconds (power-up effect).

**Intermediate:**
Implement combo system: Each enemy defeated within 2 seconds = 1.5x multiplier (stacks). Multiplier resets after 2 seconds without defeat.

**Challenge:**
Create an achie vement system: Award badges/points for milestones (Score 1000, Score 10000, etc.). Display notifications when earned.

<details><summary>💡 Hints</summary>
- Beginner: Use Coroutine, set multiplier flag, reset after delay
- Intermediate: Track time since last enemy defeated, increase multiplier each hit
- Challenge: Check conditions in UpdateDisplay(), show unlock popup
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
private float scoreMultiplier = 1f;

public static void AddScore(int points)
{
    score += Mathf.RoundToInt(points * instance.scoreMultiplier);
}

public void ApplyPowerUp(float multiplier, float duration)
{
    StartCoroutine(MultiplierCoroutine(multiplier, duration));
}

IEnumerator MultiplierCoroutine(float mult, float duration)
{
    scoreMultiplier = mult;
    yield return new WaitForSeconds(duration);
    scoreMultiplier = 1f;
}
```

**Intermediate:**
```csharp
private float comboMultiplier = 1f;
private float lastEnemyDefeatedTime = 0;

public static void OnEnemyDefeated()
{
    if (Time.time - instance.lastEnemyDefeatedTime < 2f)
        instance.comboMultiplier += 0.5f;
    else
        instance.comboMultiplier = 1f;
    
    instance.lastEnemyDefeatedTime = Time.time;
    AddScore(Mathf.RoundToInt(10 * instance.comboMultiplier));
}
```

**Challenge:**
```csharp
private void CheckAchievements()
{
    if (score >= 1000 && !achievementUnlocked1000)
    {
        UnlockAchievement("Score 1000");
        achievementUnlocked1000 = true;
    }
}
```
</details>
