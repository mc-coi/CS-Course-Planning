# Day 19: Physics Lab — Bouncing Ball Game

**Learning Target:** I can integrate multiple physics concepts into a complete game: bouncing, collision detection, scoring, and physics materials.

---

## Project Overview

Build a **Bouncing Ball Game** where:
1. Player controls a paddle to bounce a ball
2. Ball bounces off walls and paddle
3. Collects pickups for points
4. Falls off bottom = lose a life
5. Win by reaching target score

**Physics concepts used:**
- Rigidbody with velocity and forces
- Colliders (ball, paddle, walls, pickups)
- OnCollisionEnter for paddle detection
- OnTriggerEnter for pickups
- PhysicMaterial for bounce behavior
- Raycasting for ground detection

---

## Game Architecture

```
Game Scene
├── Ball (Sphere, Rigidbody, SphereCollider, PhysicMaterial)
├── Paddle (Cube, Rigidbody, BoxCollider)
├── Walls (4 Cubes, BoxColliders, Static Rigidbody)
├── Pickups (Spheres, SphereColliders, isTrigger)
└── GameManager (handles score, lives, win/lose)
```

---

## Code Example

```csharp
using UnityEngine;

public class BounceGameManager : MonoBehaviour
{
    public static int score = 0;
    public static int lives = 3;
    public int targetScore = 100;
    
    private bool gameOver = false;

    private void Start()
    {
        score = 0;
        lives = 3;
    }

    private void Update()
    {
        if (gameOver)
        {
            if (Input.GetKeyDown(KeyCode.Space))
            {
                UnityEngine.SceneManagement.SceneManager.LoadScene(UnityEngine.SceneManagement.SceneManager.GetActiveScene().name);
            }
        }
    }

    public void AddScore(int points)
    {
        score += points;
        Debug.Log("Score: " + score);

        if (score >= targetScore)
        {
            WinGame();
        }
    }

    public void LoseLife()
    {
        lives--;
        Debug.Log("Lives: " + lives);

        if (lives <= 0)
        {
            LoseGame();
        }
    }

    private void WinGame()
    {
        gameOver = true;
        Debug.Log("YOU WIN! Final score: " + score);
    }

    private void LoseGame()
    {
        gameOver = true;
        Debug.Log("GAME OVER! Final score: " + score);
    }

    public void OnGUI()
    {
        GUI.Label(new Rect(10, 10, 300, 30), "Score: " + score);
        GUI.Label(new Rect(10, 40, 300, 30), "Lives: " + lives);

        if (gameOver)
        {
            GUI.Label(new Rect(Screen.width / 2 - 100, Screen.height / 2, 200, 50), "Press SPACE to restart");
        }
    }
}

public class Ball : MonoBehaviour
{
    private Rigidbody rb;
    private float resetY = -5f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // Reset if ball falls off
        if (transform.position.y < resetY)
        {
            BounceGameManager.Instance.LoseLife();
            ResetBall();
        }
    }

    private void ResetBall()
    {
        transform.position = new Vector3(0, 5, 0);
        rb.velocity = Vector3.zero;
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Paddle"))
        {
            // Boost ball upward on paddle hit
            rb.velocity = new Vector3(rb.velocity.x, Mathf.Abs(rb.velocity.y), rb.velocity.z);
        }
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Pickup"))
        {
            BounceGameManager.Instance.AddScore(10);
            Destroy(other.gameObject);
        }
    }
}

public class Paddle : MonoBehaviour
{
    public float moveSpeed = 5f;

    private void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");
        transform.position += Vector3.right * moveInput * moveSpeed * Time.deltaTime;

        // Clamp paddle position
        transform.position = new Vector3(Mathf.Clamp(transform.position.x, -4, 4), transform.position.y, 0);
    }
}

public class Pickup : MonoBehaviour
{
    private void Start()
    {
        // Rotate slowly for visual feedback
        StartCoroutine(RotatePickup());
    }

    private System.Collections.IEnumerator RotatePickup()
    {
        while (true)
        {
            transform.Rotate(0, 3, 0);
            yield return null;
        }
    }
}
```

---

## Unity Setup Steps

1. **Create Game Scene** and add BounceGameManager (empty object with script)
2. **Create Ball:**
   - Sphere primitive
   - Rigidbody (not kinematic)
   - SphereCollider (default)
   - PhysicMaterial with bounciness = 0.9, friction = 0.1
   - Ball script

3. **Create Paddle:**
   - Cube scaled (4, 0.5, 1)
   - Position at Y = -3
   - Rigidbody (kinematic)
   - BoxCollider
   - Paddle script
   - Tag = "Paddle"

4. **Create Walls:**
   - 4 cubes (left, right, top, bottom)
   - Static Rigidbody
   - BoxColliders

5. **Create Pickups:**
   - Spawn 10 spheres around level
   - SphereCollider with isTrigger = true
   - Tag = "Pickup"

6. **Press Play:** Bounce ball with paddle, collect pickups

---

## Practice Problems

**Beginner:** Get the basic game running with paddle and ball bouncing.

**Intermediate:** Add 10 pickups and scoring system. Reach 100 points to win.

**Challenge:** Add power-ups: multi-ball, paddle size increase, slow-motion. Make game progressively harder.

<details><summary>💡 Hints</summary>
- Use PhysicMaterial to get bouncy behavior
- Paddle should be kinematic (moved by code, not physics)
- Pickups use triggers (isTrigger = true)
- Store game state in static variables (score, lives)
- OnGUI() can display HUD without canvas
</details>

<details><summary>✅ Full Game Code Snippet</summary>

```csharp
// BounceGameManager with singleton pattern
public class BounceGameManager : MonoBehaviour
{
    public static BounceGameManager Instance;

    private void Awake()
    {
        if (Instance == null)
            Instance = this;
        else
            Destroy(gameObject);
    }

    public void AddScore(int points) { /* ... */ }
    public void LoseLife() { /* ... */ }
}
```

</details>
