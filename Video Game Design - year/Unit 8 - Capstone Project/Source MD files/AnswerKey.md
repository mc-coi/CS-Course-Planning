# Unit 8 Answer Key: Capstone Project

Answer key for all 15 sprint warm-up challenges. Use these to verify solutions or get hints when stuck.

---

## Challenge 1: Quick Movement Test (Unit 4 Review)

### Solution

```csharp
public class PlayerMovement : MonoBehaviour
{
    public float moveSpeed = 5f;
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");
        rb.velocity = new Vector2(moveInput * moveSpeed, rb.velocity.y);
    }
}
```

### What Success Looks Like
- Square moves left/right smoothly with arrow keys
- Movement frame-rate independent
- No vertical velocity affected

### Common Mistakes
- Using `transform.position +=` (ignores physics)
- Setting velocity.y to 0 (breaks gravity)
- Not multiplying by moveSpeed

---

## Challenge 2: Collision Count (Unit 3 Review)

### Solution

```csharp
public class PlayerHealth : MonoBehaviour
{
    private int coinsCollected = 0;

    void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.gameObject.CompareTag("Coin"))
        {
            coinsCollected++;
            Debug.Log("Coins: " + coinsCollected);
            Destroy(collision.gameObject);
        }
    }
}
```

### What Success Looks Like
- Console logs increment each pickup
- Coins disappear on collection
- Counter shows correct total

### Common Mistakes
- Using OnCollisionEnter2D instead of OnTriggerEnter2D
- Not checking tag (collects everything)
- Destroying wrong object

---

## Challenge 3: UI Text Update (Unit 5 Review)

### Solution

```csharp
using UnityEngine.UI;
using TMPro;

public class ScoreDisplay : MonoBehaviour
{
    public TextMeshProUGUI scoreText;
    private int score = 0;

    void Start()
    {
        scoreText = GetComponent<TextMeshProUGUI>();
    }

    public void AddScore(int points)
    {
        score += points;
        scoreText.text = $"Score: {score}";
    }
}
```

### What Success Looks Like
- Text updates immediately when AddScore() called
- Multiple calls accumulate correctly
- Display shows "Score: X" format

### Common Mistakes
- Using Text instead of TextMeshProUGUI
- Not updating text.text property
- Getting component wrong (crashes)

---

## Challenge 4: Particle Trigger (Unit 6 Review)

### Solution

```csharp
private ParticleSystem particles;

void Start()
{
    particles = GetComponent<ParticleSystem>();
    particles.Stop();
}

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        particles.Play();
    }
}
```

### What Success Looks Like
- Space key triggers particle emission
- Particles spawn and dissipate
- Console shows no errors

### Common Mistakes
- Using `particles.Play()` on wrong object
- Not stopping particles initially (can't restart)
- Forgetting GetComponent<ParticleSystem>()

---

## Challenge 5: Scene Loading (Unit 2 Review)

### Solution

```csharp
using UnityEngine.SceneManagement;
using UnityEngine.UI;

public class MenuManager : MonoBehaviour
{
    void Start()
    {
        Button startButton = GetComponent<Button>();
        startButton.onClick.AddListener(StartGame);
    }

    void StartGame()
    {
        SceneManager.LoadScene("Game");
    }
}
```

### What Success Looks Like
- Clicking "Start Game" loads Game scene
- Menu scene unloaded
- Game scene loaded successfully
- No errors about missing scenes

### Common Mistakes
- Scene name wrong (case-sensitive)
- Scene not in Build Settings
- Using wrong button reference

---

## Challenge 6: Coroutine Delay (Unit 7 Review)

### Solution

```csharp
public class DelayedAction : MonoBehaviour
{
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            StartCoroutine(WaitThenPrint());
        }
    }

    IEnumerator WaitThenPrint()
    {
        Debug.Log("Waiting...");
        yield return new WaitForSeconds(2f);
        Debug.Log("Done!");
    }
}
```

### What Success Looks Like
- "Waiting..." prints immediately
- 2 second delay
- "Done!" prints after delay
- Can be triggered multiple times

### Common Mistakes
- Using `yield return null;` (returns immediately)
- Forgetting time duration (syntax error)
- Not using IEnumerator return type

---

## Challenge 7: Singleton Access (Unit 8 Review)

### Solution

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    void Awake()
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

    public void EndGame()
    {
        Debug.Log("Game Over!");
    }
}

// From any script:
public class Enemy : MonoBehaviour
{
    void OnDestroy()
    {
        GameManager.instance.EndGame();
    }
}
```

### What Success Looks Like
- "Game Over!" prints when enemy destroyed
- Only one GameManager exists
- Persists across scenes

### Common Mistakes
- Not checking if instance exists (multiple managers)
- Forgetting DontDestroyOnLoad
- Destroying wrong object

---

## Challenge 8: Rigidbody2D Forces (Unit 4 Review)

### Solution

```csharp
private Rigidbody2D rb;
public float jumpForce = 5f;

void Start()
{
    rb = GetComponent<Rigidbody2D>();
}

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
    }
}
```

### What Success Looks Like
- Space causes instant upward jump
- Player falls back due to gravity
- Jump feels responsive

### Common Mistakes
- Using ForceMode2D.Force instead of Impulse (slow acceleration)
- Not getting Rigidbody2D
- AddForce in wrong direction (wrong axis)

---

## Challenge 9: Tag Comparison (Unit 3 Review)

### Solution

```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    if (collision.gameObject.CompareTag("Enemy"))
    {
        Destroy(gameObject);
    }
}
```

### What Success Looks Like
- Player disappears on collision with enemy
- Tag must be set on enemy object
- No errors about missing tags

### Common Mistakes
- Tag name wrong or not set
- Using `==` instead of CompareTag
- Destroying wrong object (enemy instead of player)

---

## Challenge 10: PlayerPrefs Save/Load (Unit 8 Review)

### Solution

```csharp
public class HighScoreManager : MonoBehaviour
{
    void Start()
    {
        int highScore = PlayerPrefs.GetInt("HighScore", 0);
        Debug.Log("High Score: " + highScore);
    }

    public void SetHighScore(int newScore)
    {
        PlayerPrefs.SetInt("HighScore", newScore);
        PlayerPrefs.Save();
    }
}
```

### What Success Looks Like
- SetHighScore(100) saves score
- Close and reopen scene
- Console shows "High Score: 100"
- Data persists

### Common Mistakes
- Forgetting PlayerPrefs.Save() (doesn't persist)
- Not using default value (crashes if key missing)
- Using wrong data type (GetString vs GetInt)

---

## Challenge 11: AudioSource Play (Unit 6 Review)

### Solution

```csharp
private AudioSource audioSource;

void Start()
{
    audioSource = GetComponent<AudioSource>();
}

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        audioSource.Play();
    }
}
```

### What Success Looks Like
- Space key plays sound
- Audio clip assigned in Inspector
- Sound plays from start each time

### Common Mistakes
- AudioSource not in Inspector
- No audio clip assigned
- Using PlayOneShot instead of Play

---

## Challenge 12: Enemy AI Step (Unit 4 Review)

### Solution

```csharp
public class EnemyAI : MonoBehaviour
{
    public float moveSpeed = 2f;
    private float direction = 1f;
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        rb.velocity = new Vector2(direction * moveSpeed, rb.velocity.y);

        // Turn around at boundaries
        if (transform.position.x > 10f)
            direction = -1f;
        else if (transform.position.x < -10f)
            direction = 1f;
    }
}
```

### What Success Looks Like
- Enemy walks left/right continuously
- Turns around at boundaries (±10)
- Gravity still works (doesn't fly)

### Common Mistakes
- Not checking boundaries (enemy walks off)
- Velocity.y set to 0 (breaks gravity)
- Direction not changing (walks one way only)

---

## Challenge 13: 2D Sprite Flip (Unit 4 Review)

### Solution

```csharp
private SpriteRenderer spriteRenderer;

void Start()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
}

void Update()
{
    float moveInput = Input.GetAxis("Horizontal");
    if (moveInput < 0)
    {
        spriteRenderer.flipX = true;
    }
    else if (moveInput > 0)
    {
        spriteRenderer.flipX = false;
    }
}
```

### What Success Looks Like
- Sprite faces left when moving left
- Sprite faces right when moving right
- No flickering when idle

### Common Mistakes
- Flipping every frame (visible flickering)
- Logic inverted (flips wrong direction)
- Using only one condition (gets stuck one way)

---

## Challenge 14: Health System (Unit 5 Review)

### Solution

```csharp
public class Player : MonoBehaviour
{
    public int maxHealth = 3;
    private int currentHealth;
    public TextMeshProUGUI healthText;

    void Start()
    {
        currentHealth = maxHealth;
        UpdateHealthDisplay();
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        UpdateHealthDisplay();

        if (currentHealth <= 0)
        {
            Debug.Log("Player died!");
            Destroy(gameObject);
        }
    }

    void UpdateHealthDisplay()
    {
        healthText.text = $"Health: {currentHealth}/{maxHealth}";
    }
}
```

### What Success Looks Like
- Text shows "Health: 3/3" initially
- TakeDamage(1) → "Health: 2/3"
- At 0 health, player destroyed
- Text updates each damage

### Common Mistakes
- Not updating text
- Health going negative
- Destroying before display update

---

## Challenge 15: Score Accumulator (Unit 5 Review)

### Solution

```csharp
public class GameManager : MonoBehaviour
{
    public static int score = 0;
    public TextMeshProUGUI scoreText;

    void Start()
    {
        score = 0;
        UpdateScore();
    }

    public static void AddPoints(int points)
    {
        score += points;
        FindObjectOfType<GameManager>().UpdateScore();
    }

    void UpdateScore()
    {
        scoreText.text = "Score: " + score;
    }
}

// In coin script:
void OnTriggerEnter2D(Collider2D collision)
{
    if (collision.CompareTag("Player"))
    {
        GameManager.AddPoints(10);
        Destroy(gameObject);
    }
}
```

### What Success Looks Like
- Collect coin → score increases by 10
- Collect 5 coins → score = 50
- Text updates each collection
- Score persists for final display

### Common Mistakes
- Not calling UpdateScore() after adding points
- Static score not reset between games
- Multiple GameManager instances (scores stack)

---

## Summary Table

| Challenge | Unit | Concept | Time |
|-----------|------|---------|------|
| 1 | 4 | 2D Movement | 5 min |
| 2 | 3 | Collision Detection | 5 min |
| 3 | 5 | UI Text | 5 min |
| 4 | 6 | Particles | 5 min |
| 5 | 2 | Scene Loading | 5 min |
| 6 | 7 | Coroutines | 5 min |
| 7 | 8 | Singleton | 5 min |
| 8 | 4 | Physics Forces | 5 min |
| 9 | 3 | Tag Comparison | 5 min |
| 10 | 8 | Persistence | 5 min |
| 11 | 6 | Audio | 5 min |
| 12 | 4 | Enemy AI | 5 min |
| 13 | 4 | Sprite Flip | 5 min |
| 14 | 5 | Health Bar | 5 min |
| 15 | 5 | Score System | 5 min |

---

## How to Use These Solutions

1. **Attempt first:** Try solving without looking at answers
2. **Set timer:** 5-10 minutes per challenge
3. **Check solution:** Compare your approach
4. **Improve:** If stuck, review the "Common Mistakes" section
5. **Iterate:** Modify the solution (different values, more features)

## Testing Checklist

- [ ] Code compiles without errors
- [ ] Expected behavior works
- [ ] No console warnings/errors
- [ ] Tested multiple times
- [ ] Edge cases handled (empty, null, boundaries)

## Next Steps After Capstone

- Add more features to your capstone project
- Publish game to itch.io
- Optimize performance
- Polish UI and visual effects
- Add more levels or content
