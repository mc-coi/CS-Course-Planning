# Unit 5 Practice Problems

15 problems with solutions covering all Unit 5 concepts.

---

## Problem 1: MDA Analysis
**Difficulty: Beginner**

Analyze a simple game mechanic: "In Flappy Bird, pressing space makes the bird jump."

Identify:
- Mechanic
- Possible Dynamics
- Possible Aesthetics

<details><summary>Solution</summary>

**Mechanic**: Press Space → Bird jumps
**Dynamics**: Player learns timing, anticipates gaps, develops muscle memory
**Aesthetics**: Tension (fear of hitting pipes), rapid decision-making, urgency, satisfaction on passing a pipe

</details>

---

## Problem 2: Flow State
**Difficulty: Beginner**

You're designing a game. Level 1 is too easy, and Level 5 is impossible. How would you fix this?

<details><summary>Solution</summary>

Add intermediate levels with gradually increasing difficulty:
- Level 1: Easy (learn basics)
- Level 2: Easy-Medium (master basics)
- Level 3: Medium (introduce new mechanic)
- Level 4: Medium-Hard (new mechanic gets harder)
- Level 5: Hard (master everything)

Alternatively, redesign Level 5 to introduce its new mechanic gradually before the hard challenges.

</details>

---

## Problem 3: Level Design Loop
**Difficulty: Intermediate**

Design a 3-zone level that teaches the "dash" mechanic:
- Safe Zone: Learn dash
- Challenge Zone: Use dash
- Reward Zone: Victory

Write 2-3 sentences for each.

<details><summary>Solution</summary>

**Safe Zone**: Open platform with no enemies. Player can practice dashing left/right freely. A tutorial label says "Press SPACE to dash."

**Challenge Zone**: Series of moving platforms separated by gaps. Player must dash across gaps to progress. One slow enemy walks back and forth.

**Reward Zone**: Final platform with glowing exit. Simple jump+dash required. Enemy defeated, clear path to goal.

</details>

---

## Problem 4: Canvas Setup
**Difficulty: Beginner**

You create a UI button that should stick to the top-left corner on all screen sizes. What anchor and offset settings would you use?

<details><summary>Solution</summary>

- **Anchor Preset**: Top-Left
- **Pos X**: 10 (10px from left edge)
- **Pos Y**: -10 (10px from top edge)
- **Width**: 100, **Height**: 50

The negative Y is because top-left anchor measures downward as negative.

</details>

---

## Problem 5: TextMeshPro Formatting
**Difficulty: Beginner**

Write a C# line that displays: "LEVEL UP!" in large, bold, gold text.

<details><summary>Solution</summary>

```csharp
text.text = "<color=gold><size=60><b>LEVEL UP!</b></size></color>";
```

</details>

---

## Problem 6: Button Interaction
**Difficulty: Intermediate**

Write a script that:
- Detects when a button is clicked
- Increments a counter
- Updates TextMeshPro with the count
- Disables the button after 10 clicks

<details><summary>Solution</summary>

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

</details>

---

## Problem 7: Health Bar Animation
**Difficulty: Intermediate**

Write a script that smoothly animates a Slider from current health to new health when damage is taken.

<details><summary>Solution</summary>

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

</details>

---

## Problem 8: Score Formatting
**Difficulty: Beginner**

Write code that displays a score with commas: 1,000,000 instead of 1000000.

<details><summary>Solution</summary>

```csharp
scoreText.text = $"Score: {score:N0}";
// The ":N0" format specifier adds commas and no decimal places
```

</details>

---

## Problem 9: PlayerPrefs High Score
**Difficulty: Intermediate**

Write a script that:
- Saves high score to PlayerPrefs
- Loads it on startup
- Updates only if new score is higher
- Displays both current and high score

<details><summary>Solution</summary>

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

</details>

---

## Problem 10: Pause Menu
**Difficulty: Intermediate**

Write a script that:
- Pauses game when ESC is pressed (sets Time.timeScale = 0)
- Shows a pause menu
- Resumes when a button is clicked
- Allows pause menu buttons to work while paused

<details><summary>Solution</summary>

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

</details>

---

## Problem 11: Audio Manager Singleton
**Difficulty: Intermediate**

Write the Awake() method for an AudioManager Singleton that ensures only one instance exists and persists between scenes.

<details><summary>Solution</summary>

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

</details>

---

## Problem 12: Volume Control
**Difficulty: Intermediate**

Write a script that:
- Creates a slider for volume control
- Updates an AudioSource's volume in real-time
- Saves volume to PlayerPrefs
- Loads saved volume on startup

<details><summary>Solution</summary>

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

</details>

---

## Problem 13: Screen Shake
**Difficulty: Challenge**

Write a coroutine that shakes the camera for a given duration, with the shake dampening over time.

<details><summary>Solution</summary>

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

</details>

---

## Problem 14: Hit Flash Effect
**Difficulty: Challenge**

Write a script that flashes an object white briefly when hit, then returns to original color.

<details><summary>Solution</summary>

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

</details>

---

## Problem 15: Particle Effect on Click
**Difficulty: Challenge**

Write a script that:
- Spawns a particle effect at the mouse click position
- Destroys the particle after it finishes
- Plays a sound effect simultaneously

<details><summary>Solution</summary>

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

</details>

---

## Answer Summary

| Problem | Difficulty | Key Concept |
|---------|-----------|------------|
| 1 | Beginner | MDA Framework |
| 2 | Beginner | Flow State |
| 3 | Intermediate | Level Design |
| 4 | Beginner | Canvas Anchors |
| 5 | Beginner | TextMeshPro |
| 6 | Intermediate | Button Events |
| 7 | Intermediate | Slider Animation |
| 8 | Beginner | Number Formatting |
| 9 | Intermediate | PlayerPrefs |
| 10 | Intermediate | Time Control |
| 11 | Intermediate | Singleton |
| 12 | Intermediate | Audio Control |
| 13 | Challenge | Screen Shake |
| 14 | Challenge | Hit Flash |
| 15 | Challenge | Particle Effects |
