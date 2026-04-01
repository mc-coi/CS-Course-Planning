# Unit 5 Answer Key: Game Design Principles & UI

Comprehensive answer key for all 15 practice problems covering game design, UI systems, persistence, and audio.

---

## Problem 1: MDA Analysis

### Solution

**Game: Flappy Bird**

**Mechanic:** Press Space → Bird jumps

**Dynamics:**
- Player learns timing to avoid obstacles
- Decision-making becomes rapid and reactive
- Muscle memory develops through repetition
- Anticipation builds as gaps approach

**Aesthetics:**
- Tension (fear of hitting pipes)
- Rapid decision-making urgency
- Satisfaction on passing pipe
- Frustration on failure

### What Success Looks Like
Student identifies mechanic, emergent dynamics, and emotional responses clearly. Explains how simple mechanic creates complex player experience.

### Common Mistakes
- Confusing mechanics with dynamics
- Generic descriptions ("fun", "challenging" without specifics)
- Not explaining cause and effect

---

## Problem 2: Flow State

### Solution

**Issue:** Level 1 easy, Level 5 impossible. No progression curve.

**Solution:** Add intermediate difficulty levels with gradual increase.

- Level 1: Easy (learn basics)
- Level 2: Easy-Medium (master basics)
- Level 3: Medium (introduce new mechanic)
- Level 4: Medium-Hard (new mechanic gets harder)
- Level 5: Hard (master everything)

Alternatively: Redesign Level 5 to introduce its new mechanic gradually before hard challenges.

### What Success Looks Like
Student understands flow state (challenge slightly exceeding skill). Provides reasonable difficulty progression. Each level teaches something new.

### Common Mistakes
- Sudden difficulty spikes
- Repeating same challenge (no learning)
- Not tutorializing new mechanics before hard use

---

## Problem 3: Level Design Loop

### Solution

**Safe Zone:** Open platform with no enemies. Player can practice dashing left/right freely. Tutorial label says "Press SPACE to dash."

**Challenge Zone:** Series of moving platforms separated by gaps. Player must dash across gaps to progress. One slow enemy walks back and forth to add mild pressure.

**Reward Zone:** Final platform with glowing exit. Simple jump+dash required. Enemy defeated, clear path to goal.

### What Success Looks Like
Three distinct zones with clear progression. Safe zone teaches, challenge zone applies learning, reward zone feels accomplishment.

### Common Mistakes
- Safe zone too small (can't practice properly)
- Challenge zone not challenging enough (trivial)
- No clear progression between zones

---

## Problem 4: Canvas Setup

### Solution

- **Anchor Preset:** Top-Left
- **Pos X:** 10 (10 pixels from left edge)
- **Pos Y:** -10 (10 pixels from top edge, negative because down is negative)
- **Width:** 100, **Height:** 50

### What Success Looks Like
Button appears in top-left corner on all screen sizes. Position is consistent and readable. Responsive to different aspect ratios.

### Common Mistakes
- Forgetting that Y is negative at top of screen
- Using Center anchor for corner elements (wrong behavior)
- Not testing on multiple screen sizes

---

## Problem 5: TextMeshPro Formatting

### Solution

```csharp
text.text = "<color=gold><size=60><b>LEVEL UP!</b></size></color>";
```

### What Success Looks Like
Text displays as large, bold, gold-colored "LEVEL UP!" in scene.

### Common Mistakes
- Forgetting color tag brackets `<color=gold>`
- Using HTML hex instead of color name `<#FFD700>`
- Missing closing tags

---

## Problem 6: Button Interaction

### Solution

```csharp
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class ClickCounter : MonoBehaviour
{
    public Button clickButton;
    public TextMeshProUGUI counterText;
    private int count = 0;

    private void Start()
    {
        clickButton.onClick.AddListener(OnClick);
    }

    private void OnClick()
    {
        count++;
        counterText.text = $"Clicks: {count}";

        if (count >= 10)
            clickButton.interactable = false;
    }
}
```

### What Success Looks Like
- Click counter increments
- Text updates with current count
- Button disables after 10 clicks
- Button appears grayed out when disabled

### Common Mistakes
- Using Button.onClick in Inspector instead of AddListener in code
- Not checking count before disabling
- Forgetting to update text display

---

## Problem 7: Health Bar Animation

### Solution

```csharp
public void TakeDamage(float damage)
{
    currentHealth -= damage;
    currentHealth = Mathf.Max(0, currentHealth);
    StartCoroutine(AnimateHealth());
}

IEnumerator AnimateHealth()
{
    float targetValue = currentHealth / maxHealth;
    float duration = 0.5f;
    float elapsed = 0;

    while (elapsed < duration)
    {
        healthSlider.value = Mathf.Lerp(healthSlider.value, targetValue, elapsed / duration);
        elapsed += Time.deltaTime;
        yield return null;
    }
    healthSlider.value = targetValue;
}
```

### What Success Looks Like
- Health bar smoothly animates from current to new value
- Animation takes 0.5 seconds
- Final value precisely matches health

### Common Mistakes
- Not using coroutine (instant update, no animation)
- Lerp parameter wrong (animates incorrectly)
- Not clamping final value (overshoots)

---

## Problem 8: Score Formatting

### Solution

```csharp
scoreText.text = $"Score: {score:N0}";
// The ":N0" format specifier adds commas and no decimal places
```

**Examples:**
- 1000 → "Score: 1,000"
- 1000000 → "Score: 1,000,000"
- 1234567 → "Score: 1,234,567"

### What Success Looks Like
Large numbers display with comma separation. Readable and professional looking.

### Common Mistakes
- Using wrong format specifier (":F" gives decimals)
- Hardcoding commas (only works for specific values)
- Not using string interpolation

---

## Problem 9: PlayerPrefs High Score

### Solution

```csharp
private int highScore;

void Start()
{
    highScore = PlayerPrefs.GetInt("HighScore", 0);
    DisplayScores();
}

public void CheckHighScore(int newScore)
{
    if (newScore > highScore)
    {
        highScore = newScore;
        PlayerPrefs.SetInt("HighScore", highScore);
    }
    DisplayScores();
}

void DisplayScores()
{
    currentText.text = $"Current: {score}";
    highScoreText.text = $"High: {highScore}";
}
```

### What Success Looks Like
- High score persists between game sessions
- Only updates if new score higher
- Display shows both current and high score

### Common Mistakes
- Not calling PlayerPrefs.Save() (data doesn't persist)
- Overwriting high score with every score
- Not using default value (crashes if key missing)

---

## Problem 10: Pause Menu

### Solution

```csharp
public class PauseManager : MonoBehaviour
{
    public GameObject pauseMenu;
    public Button resumeButton;

    private void Start()
    {
        pauseMenu.SetActive(false);
        resumeButton.onClick.AddListener(Resume);
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            Time.timeScale = 0f;
            pauseMenu.SetActive(true);
        }
    }

    public void Resume()
    {
        Time.timeScale = 1f;
        pauseMenu.SetActive(false);
    }
}
```

### What Success Looks Like
- ESC pauses game (everything stops)
- Pause menu appears
- Resume button unpauses game
- Menu buttons work while paused (Time.timeScale doesn't affect UI)

### Common Mistakes
- Forgetting to set Time.timeScale back to 1f (game stays paused)
- Not setting pauseMenu inactive initially
- UI buttons don't work while paused (they also use deltaTime)

---

## Problem 11: Audio Manager Singleton

### Solution

```csharp
public static AudioManager instance;

private void Awake()
{
    if (instance != null && instance != this)
    {
        Destroy(gameObject);
    }
    else
    {
        instance = this;
        DontDestroyOnLoad(gameObject);
    }
}
```

### What Success Looks Like
- Only one AudioManager exists
- Persists between scene loads
- Accessible from anywhere via AudioManager.instance

### Common Mistakes
- Not checking if instance exists (multiple managers)
- Not calling DontDestroyOnLoad (destroyed on scene change)
- Destroying wrong object (destroys this instead of duplicate)

---

## Problem 12: Volume Control

### Solution

```csharp
public AudioSource audioSource;
public Slider volumeSlider;

void Start()
{
    float savedVolume = PlayerPrefs.GetFloat("Volume", 1f);
    volumeSlider.value = savedVolume;
    audioSource.volume = savedVolume;

    volumeSlider.onValueChanged.AddListener(SetVolume);
}

void SetVolume(float volume)
{
    audioSource.volume = volume;
    PlayerPrefs.SetFloat("Volume", volume);
}
```

### What Success Looks Like
- Slider controls audio volume in real-time
- Volume setting persists between sessions
- Starts with saved or default volume

### Common Mistakes
- Not setting slider initial value (resets on restart)
- Not adding listener to slider (manual changes don't work)
- Volume value outside 0-1 range (clipping/silence)

---

## Problem 13: Screen Shake

### Solution

```csharp
public IEnumerator ScreenShake(float intensity, float duration)
{
    Vector3 originalPos = transform.position;
    float elapsed = 0;

    while (elapsed < duration)
    {
        Vector3 randomOffset = Random.insideUnitSphere * intensity;
        transform.position = originalPos + randomOffset;

        elapsed += Time.deltaTime;
        intensity *= 0.95f; // Dampen over time
        yield return null;
    }

    transform.position = originalPos;
}
```

### What Success Looks Like
- Camera shakes violently at start
- Shake dampens smoothly over duration
- Returns to original position when complete

### Common Mistakes
- Intensity too high or too low (unnoticeable or painful)
- Not dampening (shake same intensity entire time)
- Not resetting position (camera stuck offset)

---

## Problem 14: Hit Flash Effect

### Solution

```csharp
public SpriteRenderer spriteRenderer;

public void OnHit()
{
    StartCoroutine(FlashWhite(0.1f));
    AudioManager.PlaySFX(hitSound);
}

IEnumerator FlashWhite(float duration)
{
    Color originalColor = spriteRenderer.color;
    spriteRenderer.color = Color.white;

    yield return new WaitForSeconds(duration);

    spriteRenderer.color = originalColor;
}
```

### What Success Looks Like
- Object briefly turns white on hit
- Returns to original color after duration
- Sound plays simultaneously

### Common Mistakes
- Not storing original color (can't restore properly)
- Duration too long (looks frozen)
- Not using WaitForSeconds (syncs incorrectly)

---

## Problem 15: Particle Effect on Click

### Solution

```csharp
public ParticleSystem clickParticles;
public AudioClip clickSound;

void Update()
{
    if (Input.GetMouseButtonDown(0))
    {
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(Input.mousePosition);

        ParticleSystem ps = Instantiate(clickParticles, mouseWorldPos, Quaternion.identity);
        Destroy(ps.gameObject, ps.main.duration);

        AudioManager.PlaySFX(clickSound);
    }
}
```

### What Success Looks Like
- Click spawns particle effect at mouse position
- Particles play and disappear after duration
- Sound plays simultaneously
- Effect doesn't persist in scene

### Common Mistakes
- Not setting Z depth (particles appear behind UI)
- Using fixed time instead of ps.main.duration (destroys too early)
- Not destroying particles (accumulate in scene)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | MDA Framework | Beginner |
| 2 | Flow State | Beginner |
| 3 | Level Design | Intermediate |
| 4 | Canvas Anchors | Beginner |
| 5 | TextMeshPro Tags | Beginner |
| 6 | Button Events | Intermediate |
| 7 | Slider Animation | Intermediate |
| 8 | Number Formatting | Beginner |
| 9 | PlayerPrefs | Intermediate |
| 10 | Time Control | Intermediate |
| 11 | Singleton Pattern | Intermediate |
| 12 | Audio Control | Intermediate |
| 13 | Screen Shake | Advanced |
| 14 | Hit Flash | Advanced |
| 15 | Particle Effects | Advanced |
