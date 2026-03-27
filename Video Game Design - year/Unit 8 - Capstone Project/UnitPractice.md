# Unit 8 Practice: Sprint Warm-Up Challenges

> Use these at the start of a work session to warm up, or when you're stuck and need to build momentum. Each challenge is 5–10 minutes and covers one key concept from Units 1–7. Pick one, solve it, then jump back to your capstone.

---

## Challenge 1: Quick Movement Test (Unit 4 Review)

**Goal:** Make a square move left and right with arrow keys at a steady speed.

**Setup:**
1. Create a 2D scene
2. Add a Sprite (white square, any size) to a gameObject called "Player"
3. Add a Rigidbody2D (Body Type: Dynamic, Gravity Scale: 0)

**Code:**
```csharp
public class PlayerMovement : MonoBehaviour {
    public float moveSpeed = 5f;
    private Rigidbody2D rb;

    void Start() {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update() {
        float moveInput = Input.GetAxis("Horizontal");
        // TODO: Apply moveInput * moveSpeed to the Rigidbody2D velocity
        // (Set x velocity; keep y velocity as is)
    }
}
```

**Challenge:** Make it work so arrow keys move the square smoothly.

**Bonus:** Add up/down movement with "Vertical" input.

---

## Challenge 2: Collision Count (Unit 3 Review)

**Goal:** Count how many times the player collides with "Coin" objects.

**Setup:**
1. In your scene, add 3 gameObjects with "Coin" tag and a CircleCollider2D (Is Trigger: true)
2. Add a script to the Player with a collision counter

**Code:**
```csharp
public class PlayerHealth : MonoBehaviour {
    private int coinsCollected = 0;

    void OnTriggerEnter2D(Collider2D collision) {
        if (collision.gameObject.CompareTag("Coin")) {
            coinsCollected++;
            Debug.Log("Coins: " + coinsCollected);
            Destroy(collision.gameObject); // Remove coin from scene
        }
    }
}
```

**Challenge:** Verify the coin count increases when you collide.

**Bonus:** Display the count on a UI Text element.

---

## Challenge 3: UI Text Update (Unit 5 Review)

**Goal:** Display a changing score on screen.

**Setup:**
1. Create a Canvas with a Text element (name it "ScoreText")
2. Set text to "Score: 0"

**Code (attach to Canvas or a UI Manager):**
```csharp
using UnityEngine.UI;

public class ScoreDisplay : MonoBehaviour {
    public Text scoreText;
    private int score = 0;

    void Start() {
        scoreText = GetComponent<Text>(); // or drag into Inspector
    }

    public void AddScore(int points) {
        score += points;
        // TODO: Update scoreText.text to show the new score
    }
}
```

**Challenge:** Call `AddScore(10)` from a button click and watch the text update.

**Bonus:** Make the text turn green when score > 50.

---

## Challenge 4: Particle Trigger (Unit 6 Review)

**Goal:** Play a particle effect when the player jumps.

**Setup:**
1. Add a Particle System to your Player (don't change defaults)
2. In the Player script, stop the particle system on Start

**Code:**
```csharp
private ParticleSystem particles;

void Start() {
    particles = GetComponent<ParticleSystem>();
    particles.Stop();
}

void Update() {
    if (Input.GetKeyDown(KeyCode.Space)) {
        // TODO: Play the particle system
    }
}
```

**Challenge:** Jump and see particles spawn.

**Bonus:** Disable looping and make particles one-shot.

---

## Challenge 5: Scene Loading (Unit 2 Review)

**Goal:** Load a new scene when a button is clicked.

**Setup:**
1. Create two scenes: "Menu" and "Game"
2. In Menu, add a Button that says "Start Game"
3. Add both to Build Settings (File → Build Settings)

**Code (attach to Button):**
```csharp
using UnityEngine.SceneManagement;
using UnityEngine.UI;

public class MenuManager : MonoBehaviour {
    void Start() {
        Button startButton = GetComponent<Button>();
        startButton.onClick.AddListener(StartGame);
    }

    void StartGame() {
        // TODO: Load the "Game" scene
    }
}
```

**Challenge:** Click the button and transition to the Game scene.

**Bonus:** Add a "Back to Menu" button in the Game scene.

---

## Challenge 6: Coroutine Delay (Unit 7 Review)

**Goal:** Wait 2 seconds, then do something.

**Setup:** Just a script with a public button or key press.

**Code:**
```csharp
public class DelayedAction : MonoBehaviour {
    void Update() {
        if (Input.GetKeyDown(KeyCode.Space)) {
            StartCoroutine(WaitThenPrint());
        }
    }

    IEnumerator WaitThenPrint() {
        Debug.Log("Waiting...");
        // TODO: Wait 2 seconds
        Debug.Log("Done!");
        yield break;
    }
}
```

**Challenge:** Press Space and verify the delay works.

**Bonus:** Use a coroutine to make an object fade out over 1 second.

---

## Challenge 7: Singleton Access (Unit 8 Review)

**Goal:** Access a GameManager from anywhere using the singleton pattern.

**Setup:** Create a GameManager gameObject with this script.

**Code:**
```csharp
public class GameManager : MonoBehaviour {
    public static GameManager instance;

    void Awake() {
        // TODO: Implement the singleton pattern
        // (Only one GameManager can exist; others are destroyed)
    }

    public void EndGame() {
        Debug.Log("Game Over!");
    }
}

// From any other script:
public class Enemy : MonoBehaviour {
    void OnDestroy() {
        GameManager.instance.EndGame();
    }
}
```

**Challenge:** Call `GameManager.instance.EndGame()` and verify the log prints.

**Bonus:** Prevent the GameManager from being destroyed when scenes load.

---

## Challenge 8: Rigidbody2D Forces (Unit 4 Review)

**Goal:** Apply an upward impulse to jump.

**Setup:** Player with Rigidbody2D (Dynamic, Gravity Scale: 1)

**Code:**
```csharp
private Rigidbody2D rb;
public float jumpForce = 5f;

void Start() {
    rb = GetComponent<Rigidbody2D>();
}

void Update() {
    if (Input.GetKeyDown(KeyCode.Space)) {
        // TODO: Apply an impulse upward using AddForce
        // Use ForceMode2D.Impulse
    }
}
```

**Challenge:** Press Space to jump.

**Bonus:** Only allow jumping if grounded (Raycast down or check collision).

---

## Challenge 9: Tag Comparison (Unit 3 Review)

**Goal:** Destroy the player if it hits an "Enemy" tag.

**Setup:** Player and one Enemy (both with colliders, one is "Enemy" tag)

**Code:**
```csharp
void OnCollisionEnter2D(Collision2D collision) {
    if (collision.gameObject.CompareTag("Enemy")) {
        // TODO: Destroy the player
        // Use Destroy(gameObject)
    }
}
```

**Challenge:** Collide with Enemy and watch the player disappear.

**Bonus:** Play a sound effect before destroying.

---

## Challenge 10: PlayerPrefs Save/Load (Unit 8 Review)

**Goal:** Save and load a high score.

**Setup:** Just a script in any scene.

**Code:**
```csharp
public class HighScoreManager : MonoBehaviour {
    void Start() {
        // TODO: Load the high score from PlayerPrefs
        // Default to 0 if it doesn't exist
        int highScore = 0; // Replace this line
        Debug.Log("High Score: " + highScore);
    }

    public void SetHighScore(int newScore) {
        // TODO: Save the new score and write to disk
    }
}

// Test: Call SetHighScore(100), close and reopen the scene, and the log should show 100
```

**Challenge:** Call `SetHighScore(100)`, close the scene, reopen, and verify the score persists.

**Bonus:** Add a "Reset" button that clears all saved data.

---

## Challenge 11: AudioSource Play (Unit 6 Review)

**Goal:** Play a sound effect when a button is clicked.

**Setup:** Player (or any object) with an AudioSource and an audio clip assigned

**Code:**
```csharp
private AudioSource audioSource;

void Start() {
    audioSource = GetComponent<AudioSource>();
}

void Update() {
    if (Input.GetKeyDown(KeyCode.Space)) {
        // TODO: Play the audio clip
    }
}
```

**Challenge:** Press Space and hear the sound.

**Bonus:** Make the volume randomize between 0.8 and 1.0 each time.

---

## Challenge 12: Enemy AI Step (Unit 4 Review)

**Goal:** Make an enemy patrol left and right.

**Setup:** Enemy sprite with Rigidbody2D (Dynamic, Gravity Scale: 0)

**Code:**
```csharp
public class EnemyAI : MonoBehaviour {
    public float moveSpeed = 2f;
    private float direction = 1f; // 1 = right, -1 = left
    private Rigidbody2D rb;

    void Start() {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update() {
        // TODO: Move the enemy at moveSpeed in the current direction
        // When it reaches a boundary (e.g., x > 10 or x < -10), flip direction
    }
}
```

**Challenge:** Watch the enemy patrol automatically.

**Bonus:** Add a ground check to make sure the enemy doesn't fly off.

---

## Challenge 13: 2D Sprite Flip (Unit 4 Review)

**Goal:** Flip the player sprite when moving left.

**Setup:** Player with a SpriteRenderer

**Code:**
```csharp
private SpriteRenderer spriteRenderer;

void Start() {
    spriteRenderer = GetComponent<SpriteRenderer>();
}

void Update() {
    float moveInput = Input.GetAxis("Horizontal");
    if (moveInput < 0) {
        spriteRenderer.flipX = true;
    } else if (moveInput > 0) {
        spriteRenderer.flipX = false;
    }
}
```

**Challenge:** Move left and the sprite flips.

**Bonus:** Only flip if the player is actually moving (avoid flickering).

---

## Challenge 14: Health System (Unit 5 Review)

**Goal:** Track player health and display it.

**Setup:** Player script and a UI Text for health display

**Code:**
```csharp
public class Player : MonoBehaviour {
    public int maxHealth = 3;
    private int currentHealth;
    public Text healthText;

    void Start() {
        currentHealth = maxHealth;
        UpdateHealthDisplay();
    }

    public void TakeDamage(int damage) {
        currentHealth -= damage;
        UpdateHealthDisplay();

        if (currentHealth <= 0) {
            Debug.Log("Player died!");
            Destroy(gameObject);
        }
    }

    void UpdateHealthDisplay() {
        // TODO: Update healthText to show "Health: currentHealth / maxHealth"
    }
}
```

**Challenge:** Call `TakeDamage(1)` and watch health decrease.

**Bonus:** Add a recovery item that heals 1 health.

---

## Challenge 15: Score Accumulator (Unit 5 Review)

**Goal:** Collect coins and accumulate a score; display the total.

**Setup:** Player, 5 coin prefabs (Trigger colliders, "Coin" tag), and a UI Text for score

**Code:**
```csharp
public class GameManager : MonoBehaviour {
    public static int score = 0;
    public Text scoreText;

    void Start() {
        score = 0;
        UpdateScore();
    }

    public static void AddPoints(int points) {
        score += points;
        // Call UpdateScore from here or from OnTriggerEnter
    }

    void UpdateScore() {
        scoreText.text = "Score: " + score;
    }
}

// In the coin script:
void OnTriggerEnter2D(Collider2D collision) {
    if (collision.CompareTag("Player")) {
        GameManager.AddPoints(10);
        Destroy(gameObject);
    }
}
```

**Challenge:** Collect all coins and watch the score reach 50.

**Bonus:** Spawn coins randomly and add a high score display.

---

## How to Use These

1. **Pick one challenge** that matches your current struggle.
2. **Set a timer for 10 minutes.**
3. **Implement the code**, following the TODO comments.
4. **Test it**, then move on.
5. **If stuck:** Check the ReferenceGuide or ask a classmate.

**Remember:** These aren't graded. They're just here to keep your skills sharp so your capstone goes smoothly. Have fun!
