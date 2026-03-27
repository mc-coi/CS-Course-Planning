# Day 11: Sprint 2 — UI Systems (HUD, Score, Health Bar)

**Session Goal:** Build a polished HUD with score display, health bar, and any other needed UI.

---

## Today's Focus

Today you level up your UI from placeholder text to a real HUD. A good HUD tells players exactly what they need to know without getting in the way.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up check-in.

**Minutes 5-45:** Build HUD elements: health bar, score text, lives display.

**Minutes 45-55:** Check HUD on different screen sizes (Game view → Free Aspect vs 16:9). Save.

---

## Technical Tips

```csharp
// Health bar using UI Slider
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class UIManager : MonoBehaviour
{
    public static UIManager instance;
    public Slider healthSlider;
    public TextMeshProUGUI scoreText;
    public TextMeshProUGUI livesText;

    void Awake()
    {
        if (instance == null) instance = this;
        else Destroy(gameObject);
    }

    public void SetMaxHealth(int max) { healthSlider.maxValue = max; healthSlider.value = max; }

    public void UpdateHealth(int current) { healthSlider.value = current; }

    public void UpdateScore(int score) { scoreText.text = "Score: " + score.ToString("D5"); }

    public void UpdateLives(int lives) { livesText.text = "Lives: " + lives; }
}

// Canvas setup: Create → UI → Canvas
// Set Canvas Scaler → Scale With Screen Size → 1920x1080 reference
// Add Slider for health bar, TextMeshPro for score/lives
```

---

## Reflection / Exit Ticket

1. Does your HUD clearly communicate player status (health, score)?
2. What HUD element would make the game feel more polished?

---

## Progress Checklist

- [ ] Health bar or hearts display showing current health
- [ ] Score counter updating in real time
- [ ] HUD looks clean at 16:9 aspect ratio
- [ ] UIManager hooked up to GameManager
- [ ] Scene saved and backed up
