# Day 19: Canvas & UI Elements

**Learning Target:** Create responsive UI elements using Canvas, TextMeshPro, and buttons that work across different screen sizes.

### Key Concepts

- **Canvas:** Container for all UI elements (buttons, text, images)
- **Screen Space vs. World Space:** UI in screen (overlay) vs. in world (3D objects)
- **Anchors:** Reference points for UI positioning (corners, center, etc.)
- **Rect Transform:** Special transform for UI elements with width/height
- **TextMeshPro:** Professional text rendering for UI
- **Button:** Interactive element that triggers callbacks on click
- **Slider:** Draggable bar for values (volume, health bar, etc.)
- **Layout Groups:** Auto-arrange child UI elements
- **Image:** Display textures/colors as UI

### Content

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

### Code Examples

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

### Guided Practice

**Activity:** Build a simple game HUD

Create a Canvas with:
1. **Score Display** — TextMeshPro showing current score (top-left corner)
2. **Health Bar** — Slider showing health (top-right corner)
3. **Pause Button** — Button in center-bottom

Make sure elements stay in correct positions when you resize the game view. Test on mobile portrait and desktop landscape aspect ratios.

### Practice Problems

**Problem 1 — Beginner:** Create a Canvas with a single TextMeshProUGUI element that displays "Game Over" in large text centered on screen.

**Problem 2 — Intermediate:** Create a health bar using a Slider that updates when the player takes damage.

**Problem 3 — Challenge:** Create a complete HUD with score (top-left), health bar (top-right), and pause button (bottom-center) that looks good on multiple screen sizes.

<details>
<summary>Hints</summary>

**Problem 1:** Use anchors to center the element. Set anchor to middle-center (the crosshair icon in RectTransform).

**Problem 2:** Get the Slider component. Set its value between 0-1 (current health / max health). Update it when damage is taken.

**Problem 3:** Use anchors appropriately for each element. Test by changing the Game window aspect ratio (top of Game panel).

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
- Create Canvas
- Right-click Canvas > TextMeshPro - Text
- Select the text element
- In RectTransform, set anchor to middle-center (the target icon)
- Change text to "Game Over"
- Increase font size in TextMeshPro component

**Problem 2:**
See UIManager code example above, specifically the UpdateHealthDisplay() and TakeDamage() methods.

**Problem 3:**
Combine multiple UI elements from the UIManager example:
- Score: anchor to top-left
- Health Bar: anchor to top-right
- Pause Button: anchor to bottom-center
- Test with different aspect ratios

</details>
