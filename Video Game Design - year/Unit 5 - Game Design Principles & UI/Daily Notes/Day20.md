# Day 20: Unit 5 Assessment

**Learning Target:** I can demonstrate mastery of game design principles and UI systems.

---

## Assessment Overview

This is your final assessment for Unit 5. It covers game design theory, UI implementation, audio integration, and game feel.

**Format:**
- 10 Multiple Choice questions (10 points)
- 5 Short Answer questions (10 points)
- 3 Coding Challenges (20 points)
- **Total: 40 points**

---

## Part A: Multiple Choice (1 point each)

1. In the MDA framework, which layer do designers directly control?
   - A) Mechanics B) Dynamics C) Aesthetics D) All equally

2. Flow state occurs when:
   - A) Challenge is too high B) Skill is too high C) Challenge matches skill D) Players are having fun

3. What does Time.timeScale = 0 do?
   - A) Pauses the game B) Slows time by half C) Resets time D) Disables physics

4. Which component displays text in modern Unity UI?
   - A) Text B) TextMeshPro C) Label D) Font

5. What does PlayOneShot() allow that Play() doesn't?
   - A) Looping sounds B) Overlapping sounds C) Higher volume D) Faster playback

6. RectTransform Anchor controls:
   - A) Size of element B) Parent transform C) Reference point on screen D) Rotation

7. PlayerPrefs can store:
   - A) Int, float, string B) Any data type C) Only strings D) Lists and arrays

8. A Slider component has:
   - A) Only a fill bar B) Value, min, max properties C) No visual feedback D) Fixed size

9. What's the purpose of a Particle System?
   - A) Physics simulation B) Camera effects C) Visual feedback effects D) Performance optimization

10. Screen shake is effective because:
    - A) It confuses players B) It emphasizes impact C) It hides lag D) It requires no scripting

---

## Part B: Short Answer (2 points each)

1. Explain the difference between a safe zone and a challenge zone in level design. Give one example of each.

2. Describe how you would implement a health bar that changes color from green to red as the player loses health.

3. What is a Singleton pattern? Why is it useful for an AudioManager?

4. How would you make button interactions feel responsive? List 3 specific techniques.

5. Explain why game feel (particles, sounds, screen shake) matters even in simple games.

---

## Part C: Coding Challenges (≈7 points each)

**Challenge 1: Pause Menu**
Create a PauseManager script that:
- Detects ESC key press
- Sets Time.timeScale to 0 to pause
- Shows a pause menu with Resume and Quit buttons
- Resumes time when Resume is clicked
- Returns to main menu when Quit is clicked

```csharp
// Your solution here
```

**Challenge 2: Dynamic Score Display**
Create a ScoreDisplay script that:
- Has a static AddScore(int points) method
- Updates TextMeshPro with formatted score (1,000,000 format)
- Shows a temporary "+100 points!" popup that fades out
- Persists high score to PlayerPrefs

```csharp
// Your solution here
```

**Challenge 3: Hit Feedback System**
Create a HitFeedback script that plays all together:
- Screen shake
- Object flash (white color)
- Sound effect
- Particle effect
- All triggered by a single OnHit() method

```csharp
// Your solution here
```

---

## Answer Key

### Part A Multiple Choice
1. A | 2. C | 3. A | 4. B | 5. B | 6. C | 7. A | 8. B | 9. C | 10. B

### Part B Short Answer

**1. Safe vs Challenge Zone:**
- Safe Zone: Player learns mechanic without risk. Example: "Jump over small gap with no enemies"
- Challenge Zone: Player uses mechanic under pressure. Example: "Jump over gaps while dodging enemies"

**2. Health Bar Color Change:**
```csharp
float healthPercent = currentHealth / maxHealth;
if (healthPercent > 0.66f) fillImage.color = Color.green;
else if (healthPercent > 0.33f) fillImage.color = Color.yellow;
else fillImage.color = Color.red;
```

**3. Singleton Pattern:**
- Pattern that ensures only one instance of a class exists
- Useful for AudioManager so all scripts access the same audio system
- Implemented with `if (instance != null) Destroy(this);` in Awake()

**4. Responsive Button Interactions:**
- Hover visual feedback (color change)
- Smooth animation when clicking
- Audio feedback (click sound)
- Disabled state when unavailable

**5. Why Game Feel Matters:**
- Makes actions feel impactful even in simple games
- Provides feedback that something happened
- Increases player satisfaction and engagement
- Professional polish vs. feeling unfinished

### Part C Coding Challenges

**Challenge 1: Pause Manager**
```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class PauseManager : MonoBehaviour
{
    public static bool isPaused = false;
    public GameObject pauseMenuPanel;
    public Button resumeButton;
    public Button quitButton;

    private void Start()
    {
        pauseMenuPanel.SetActive(false);
        resumeButton.onClick.AddListener(Resume);
        quitButton.onClick.AddListener(GoToMenu);
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
            if (isPaused) Resume(); else Pause();
    }

    void Pause()
    {
        isPaused = true;
        Time.timeScale = 0f;
        pauseMenuPanel.SetActive(true);
    }

    void Resume()
    {
        isPaused = false;
        Time.timeScale = 1f;
        pauseMenuPanel.SetActive(false);
    }

    void GoToMenu()
    {
        Time.timeScale = 1f;
        SceneManager.LoadScene("MainMenu");
    }
}
```

**Challenge 2: Score Display**
```csharp
using UnityEngine;
using TMPro;

public class ScoreDisplay : MonoBehaviour
{
    public static int score = 0;
    private TextMeshProUGUI scoreText;
    public TextMeshProUGUI popupTextPrefab;

    private void Start()
    {
        scoreText = GetComponent<TextMeshProUGUI>();
        LoadHighScore();
        UpdateDisplay();
    }

    public static void AddScore(int points)
    {
        score += points;
        instance.UpdateDisplay();
        instance.ShowPopup(points);
    }

    void UpdateDisplay()
    {
        scoreText.text = $"Score: {score:N0}";
        if (score > PlayerPrefs.GetInt("HighScore", 0))
            PlayerPrefs.SetInt("HighScore", score);
    }

    void ShowPopup(int points)
    {
        // Create and fade out "+{points}" text
    }

    void LoadHighScore()
    {
        // Optional: display high score
    }
}
```

**Challenge 3: Hit Feedback**
```csharp
using UnityEngine;

public class HitFeedback : MonoBehaviour
{
    public ParticleSystem hitParticles;
    public AudioClip hitSound;
    public SpriteRenderer spriteRenderer;
    public Transform cameraTransform;

    public void OnHit()
    {
        StartCoroutine(PlayFeedback());
    }

    IEnumerator PlayFeedback()
    {
        // Play all effects simultaneously
        ScreenShake(0.2f, 0.1f);
        FlashWhite(0.1f);
        PlaySound();
        PlayParticles();
        yield return null;
    }

    void ScreenShake(float intensity, float duration)
    {
        StartCoroutine(ShakeCoroutine(intensity, duration));
    }

    IEnumerator ShakeCoroutine(float intensity, float duration)
    {
        Vector3 original = cameraTransform.position;
        float elapsed = 0;
        while (elapsed < duration)
        {
            cameraTransform.position = original + (Vector3)Random.insideUnitCircle * intensity;
            elapsed += Time.deltaTime;
            yield return null;
        }
        cameraTransform.position = original;
    }

    void FlashWhite(float duration)
    {
        StartCoroutine(FlashCoroutine(duration));
    }

    IEnumerator FlashCoroutine(float duration)
    {
        Color orig = spriteRenderer.color;
        spriteRenderer.color = Color.white;
        yield return new WaitForSeconds(duration);
        spriteRenderer.color = orig;
    }

    void PlaySound()
    {
        AudioManager.PlaySFX(hitSound);
    }

    void PlayParticles()
    {
        Instantiate(hitParticles, transform.position, Quaternion.identity);
    }
}
```

---

## Reflection

After completing this assessment, reflect on:
1. What was the hardest concept? Why?
2. Which system (UI, audio, game feel) felt most natural to you?
3. What would you improve about your mini-project?
4. What's one advanced feature you'd like to add next?

Great work on Unit 5! You've built the foundation for professional game design and implementation.
