# Unit 6: 2D Game Development

## Unit Overview

**Duration:** Days 21-24 (4 days)
**Key Concepts:** 2D graphics, tilemaps, 2D physics, animation systems, prefabs
**Big Idea:** 2D games are powerful and accessible. Unity's 2D tools (Sprite Renderer, Tilemap, Animator, Rigidbody2D) make 2D development fast and fun.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Import and use 2D sprites in scenes
- [ ] Set up Sprite Renderer components with sorting orders
- [ ] Build levels using Tilemaps and Tile Palettes
- [ ] Create and configure Rigidbody2D components
- [ ] Use 2D colliders (BoxCollider2D, CircleCollider2D, PolygonCollider2D)
- [ ] Implement 2D movement using velocity and forces
- [ ] Create and configure animation clips with the Animator
- [ ] Use animation parameters (bool, float, trigger) for state control
- [ ] Create and instantiate prefabs
- [ ] Combine 2D systems into a complete mini-game

---

## Day-by-Day Content

### Day 21: Sprite Renderer & Tilemaps

#### Key Concepts
- **Sprite:** A 2D image used in 2D games
- **Sprite Renderer:** Component that displays a sprite on a GameObject
- **Texture Import Settings:** Determines how a sprite is processed (pixel perfect, compression, etc.)
- **Sorting Order:** Z-order of sprites (higher = in front)
- **Tilemap:** A grid of sprites used to build levels
- **Tile Palette:** A set of tiles available for painting
- **Tile:** Individual sprite in a tilemap
- **Isometric vs. Orthographic:** Different 2D perspectives

#### Content
Sprites are the foundation of 2D games. A Sprite Renderer displays a sprite on any GameObject.

**Setting Up Sprites:**
1. Import an image (PNG or JPG)
2. In the Inspector, set Texture Type to "Sprite (2D and UI)"
3. Click "Apply"
4. Drag the sprite onto a GameObject
5. A Sprite Renderer component is created automatically

**Sorting Order:**
When multiple sprites overlap, the one with higher Sorting Order appears in front.
- Background = 0
- Player = 5
- UI = 10

Organize your project with a consistent sorting order system.

**Tilemaps:**
Tilemaps are efficient for level design. Instead of placing 100 individual sprites, paint tiles on a grid.

**Creating a Tilemap:**
1. Right-click Hierarchy > 2D Object > Tilemap
2. In the Tile Palette, select a tile
3. Paint on the tilemap with the brush
4. Use the eraser to remove tiles

#### Annotated Code Example

```csharp
using UnityEngine;

public class SpriteManager : MonoBehaviour
{
    // Reference to the Sprite Renderer
    public SpriteRenderer spriteRenderer;
    public Sprite[] spriteFrames;  // Array of sprite images

    // Current sprite index for animation
    private int currentFrameIndex = 0;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();

        // Set initial sprite
        spriteRenderer.sprite = spriteFrames[0];

        // Set sorting order
        spriteRenderer.sortingOrder = 5;  // Player layer
    }

    // Switch to a different sprite
    public void SetSprite(int frameIndex)
    {
        if (frameIndex >= 0 && frameIndex < spriteFrames.Length)
        {
            spriteRenderer.sprite = spriteFrames[frameIndex];
            currentFrameIndex = frameIndex;
        }
    }

    // Flip sprite horizontally
    public void FlipSprite(bool faceRight)
    {
        spriteRenderer.flipX = !faceRight;
    }

    // Change sprite color (useful for hit feedback)
    public void SetSpriteColor(Color newColor)
    {
        spriteRenderer.color = newColor;
    }

    // Example: Flash white when taking damage
    public void DamageFlash()
    {
        spriteRenderer.color = Color.white;
        Invoke("ResetColor", 0.1f);
    }

    void ResetColor()
    {
        spriteRenderer.color = Color.white;  // or new Color(1, 1, 1, 1) for fully opaque white
    }
}

// Tilemap usage example
public class TilemapBuilder : MonoBehaviour
{
    // Tilemaps are created via the editor, not in code
    // But you can reference and modify them programmatically:

    public Tilemap tilemap;
    public TileBase emptyTile;

    void Start()
    {
        // Clear a tile at position
        tilemap.SetTile(new Vector3Int(5, 5, 0), null);
    }

    // Detect if there's a tile at a position
    public bool HasTileAt(Vector3Int gridPosition)
    {
        TileBase tile = tilemap.GetTile(gridPosition);
        return tile != null;
    }
}
```

---

### Day 22: 2D Movement with Rigidbody2D

#### Key Concepts
- **Rigidbody2D:** Physics component for 2D games
- **Velocity:** Speed and direction in 2D (x, y)
- **Gravity Scale:** How much gravity affects the object
- **Constraints:** Lock position or rotation axes
- **isGrounded Check:** Detecting if on the ground using raycasts or collisions
- **Collider2D:** 2D collision shape (BoxCollider2D, CircleCollider2D, etc.)
- **Direction Flipping:** Flipping sprite to face movement direction

#### Content
2D movement is simpler than 3D. Instead of position, we modify velocity.

**2D Rigidbody2D:**
- Mass, Gravity Scale, Drag work like 3D
- Body Type: Dynamic (affected by physics), Kinematic (moved by script), Static (immobile)
- Constraints: Lock X, Y, or Rotation to prevent unwanted movement

**2D Movement Approaches:**
1. **Direct Velocity:** `rb2d.velocity = new Vector2(speed, rb2d.velocity.y);`
2. **AddForce:** `rb2d.AddForce(new Vector2(force, 0), ForceMode2D.Force);`
3. **Translate:** `transform.Translate(speed * Time.deltaTime, 0);`

Direct velocity is simplest for platformers.

**Grounded Detection:**
Use a raycast or collider check below the player:
```csharp
RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.1f);
bool isGrounded = hit.collider != null;
```

#### Annotated Code Example

```csharp
using UnityEngine;

public class Player2D : MonoBehaviour
{
    [Header("Movement")]
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float groundDistance = 0.1f;
    public float groundDrag = 5f;
    public float airDrag = 1f;

    [Header("References")]
    private Rigidbody2D rb2d;
    private SpriteRenderer spriteRenderer;

    private bool isGrounded = false;
    private float horizontalInput = 0f;

    void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
        spriteRenderer = GetComponent<SpriteRenderer>();

        // Configure Rigidbody2D
        rb2d.gravityScale = 1f;
        rb2d.constraints = RigidbodyConstraints2D.FreezeRotation;
    }

    void Update()
    {
        // Get input
        horizontalInput = Input.GetAxis("Horizontal");

        // Check if grounded
        RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, groundDistance);
        isGrounded = hit.collider != null;

        // Jump
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }

        // Flip sprite based on direction
        if (horizontalInput > 0)
            spriteRenderer.flipX = false;
        else if (horizontalInput < 0)
            spriteRenderer.flipX = true;
    }

    void FixedUpdate()
    {
        // Apply movement
        rb2d.velocity = new Vector2(horizontalInput * moveSpeed, rb2d.velocity.y);

        // Apply drag
        rb2d.drag = isGrounded ? groundDrag : airDrag;
    }

    void Jump()
    {
        rb2d.velocity = new Vector2(rb2d.velocity.x, 0);
        rb2d.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        Debug.Log("Jumped!");
    }
}
```

---

### Day 23: Animation & Animator

#### Key Concepts
- **Animation Clip:** A sequence of sprites or keyframes
- **Animator:** Component that plays animations and manages states
- **Animation State:** A named animation (Idle, Run, Jump)
- **Transition:** Change from one animation to another
- **Condition:** Requirement for a transition to happen
- **Parameter:** Variables controlling animation (bool, int, float, trigger)
- **Blend Tree:** Smooth transitions between similar animations

#### Content
Animation brings 2D sprites to life. The Animator plays animation clips based on state.

**Creating Animations:**
1. Create folder for animation clips
2. Select multiple sprite frames
3. Drag them into the scene (Animator auto-creates)
4. Name the animation (e.g., "Idle", "Run", "Jump")
5. Adjust animation speed and loop settings

**Setting Up the Animator:**
1. Create an Animator Controller asset
2. Assign it to the Animator component
3. Create animation states by dragging in animation clips
4. Add transitions between states with conditions

**Animation Parameters:**
Use parameters to control which animation plays:
```csharp
animator.SetBool("IsRunning", true);        // Boolean parameter
animator.SetFloat("Speed", moveSpeed);      // Float parameter
animator.SetTrigger("Jump");                // Trigger (one-time)
animator.SetInteger("Direction", 1);       // Integer parameter
```

**Common Setup:**
```
Parameters: IsRunning (bool), IsJumping (bool)
States: Idle, Run, Jump, Fall
Transitions:
  Idle → Run (IsRunning = true)
  Run → Idle (IsRunning = false)
  Idle/Run → Jump (IsJumping = true)
  Jump → Fall (on animation complete)
  Fall → Idle (IsJumping = false)
```

#### Annotated Code Example

```csharp
using UnityEngine;

public class PlayerAnimator : MonoBehaviour
{
    private Animator animator;
    private Rigidbody2D rb2d;
    private float horizontalInput = 0f;
    private bool isJumping = false;

    void Start()
    {
        animator = GetComponent<Animator>();
        rb2d = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Get input
        horizontalInput = Input.GetAxis("Horizontal");

        // Determine if running
        bool isRunning = Mathf.Abs(horizontalInput) > 0.1f;

        // Update animator parameters
        animator.SetBool("IsRunning", isRunning);
        animator.SetFloat("VelocityY", rb2d.velocity.y);

        // Jump
        if (Input.GetKeyDown(KeyCode.Space))
        {
            animator.SetTrigger("Jump");
            isJumping = true;
        }

        // Reset jumping flag when landing (detected by negative velocity)
        if (rb2d.velocity.y < -0.1f && isJumping)
        {
            animator.SetBool("IsJumping", true);
        }
        else if (rb2d.velocity.y > -0.1f && isJumping)
        {
            animator.SetBool("IsJumping", false);
            isJumping = false;
        }
    }

    void FixedUpdate()
    {
        // Apply movement (physics)
        rb2d.velocity = new Vector2(horizontalInput * 5f, rb2d.velocity.y);
    }
}

// Animation State Machine managed by Animator controller
// Parameters:
//   IsRunning (bool)
//   IsJumping (bool)
//   Jump (trigger)
//   VelocityY (float)
//
// States & Transitions:
//   Idle → Run (IsRunning = true)
//   Run → Idle (IsRunning = false)
//   Idle/Run → Jump (Jump trigger)
//   Jump → Fall (exit time 0.5)
//   Fall → Idle (VelocityY > -1)
```

---

### Day 24: Prefabs & Complete Systems

#### Key Concepts
- **Prefab:** A template GameObject that can be instantiated multiple times
- **Prefab Asset:** The template file in the Project folder
- **Prefab Instance:** A copy of the prefab in the scene
- **Overrides:** Changes to a prefab instance that differ from the template
- **Instantiate():** Creates a copy of a prefab at runtime
- **Destroy():** Removes a GameObject from the scene
- **Object Pooling:** Reusing objects instead of creating/destroying (optimization)

#### Content
Prefabs are essential for game development. Instead of recreating the same GameObject repeatedly, create it once as a prefab, then instantiate copies.

**Creating Prefabs:**
1. Build a complete GameObject (with all components, scripts, etc.)
2. Drag it from the Hierarchy into the Project folder
3. A blue prefab icon appears in the Project
4. Delete the instance from the Hierarchy
5. Drag the prefab back to instantiate copies

**Using Prefabs in Code:**
```csharp
public GameObject enemyPrefab;
Instantiate(enemyPrefab, spawnPosition, Quaternion.identity);
```

**Benefits:**
- Consistency: All enemies behave identically
- Efficiency: Change the prefab once, all copies update
- Performance: Efficient memory management

#### Annotated Code Example

```csharp
using UnityEngine;

public class EnemySpawner : MonoBehaviour
{
    public GameObject enemyPrefab;
    public Transform[] spawnPoints;
    public int enemyCount = 5;

    void Start()
    {
        SpawnEnemies();
    }

    void SpawnEnemies()
    {
        for (int i = 0; i < enemyCount; i++)
        {
            // Pick a random spawn point
            Transform spawnPoint = spawnPoints[Random.Range(0, spawnPoints.Length)];

            // Instantiate a copy of the enemy prefab
            GameObject newEnemy = Instantiate(
                enemyPrefab,
                spawnPoint.position,
                Quaternion.identity
            );

            // Optional: name the instance
            newEnemy.name = "Enemy_" + i;

            // Optional: set as child of spawner
            newEnemy.transform.parent = transform;
        }
    }
}

public class Enemy : MonoBehaviour
{
    public float speed = 2f;
    public int health = 10;
    public GameObject deathEffectPrefab;

    void Update()
    {
        // Simple patrolling
        transform.Translate(speed * Time.deltaTime, 0, 0);
    }

    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        // Instantiate death effect
        if (deathEffectPrefab != null)
        {
            Instantiate(deathEffectPrefab, transform.position, Quaternion.identity);
        }

        // Remove this enemy
        Destroy(gameObject);
    }
}

// Object Pooling example (optimization for frequent instantiation)
public class BulletPool : MonoBehaviour
{
    public GameObject bulletPrefab;
    private Queue<GameObject> bulletPool = new Queue<GameObject>();

    void Start()
    {
        // Pre-create bullets
        for (int i = 0; i < 20; i++)
        {
            GameObject bullet = Instantiate(bulletPrefab);
            bullet.SetActive(false);
            bulletPool.Enqueue(bullet);
        }
    }

    public GameObject GetBullet(Vector3 position)
    {
        GameObject bullet;

        if (bulletPool.Count > 0)
        {
            // Reuse pooled bullet
            bullet = bulletPool.Dequeue();
            bullet.SetActive(true);
            bullet.transform.position = position;
        }
        else
        {
            // Create new if pool is empty
            bullet = Instantiate(bulletPrefab, position, Quaternion.identity);
        }

        return bullet;
    }

    public void ReturnBullet(GameObject bullet)
    {
        bullet.SetActive(false);
        bulletPool.Enqueue(bullet);
    }
}
```

---

## Practice Problems

### Beginner Tier

**Problem 1:** Import a sprite image and display it using Sprite Renderer. Change its sorting order and color.

<details>
<summary>Hint</summary>
Import PNG, set Texture Type to "Sprite". Drag onto GameObject. Access SpriteRenderer in Inspector or script.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class SpriteDisplay : MonoBehaviour
{
    void Start()
    {
        SpriteRenderer sr = GetComponent<SpriteRenderer>();
        sr.sortingOrder = 5;
        sr.color = new Color(1, 0.5f, 0);  // Orange
    }
}
```
</details>

---

**Problem 2:** Create a simple 2D platformer level using Tilemaps. Include platforms and a player spawning area.

<details>
<summary>Hint</summary>
Create a Tilemap. Create a Tile Palette. Paint tiles on the grid. Position a player GameObject on the platform.
</details>

<details>
<summary>Answer</summary>
This is a visual design task. Create a Tilemap, paint platforms, add ground, add platforms at varying heights.
</details>

---

**Problem 3:** Implement 2D movement with jump using Rigidbody2D and velocity.

<details>
<summary>Hint</summary>
Use rb2d.velocity to control movement. Add upward impulse for jumping. Check grounding with raycast.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 22 (Player2D class).
</details>

---

### Intermediate Tier

**Problem 4:** Create a 2D sprite animation with multiple frames. Set up the Animator to play idle and run animations based on input.

<details>
<summary>Hint</summary>
Create animation clips from sprite sheets. Add states to the Animator. Use SetBool() to control transitions.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 23 (PlayerAnimator class).
</details>

---

**Problem 5:** Create an enemy prefab that spawns multiple instances at different positions.

<details>
<summary>Hint</summary>
Build a complete enemy GameObject. Drag it to Project to create a prefab. Use Instantiate() to spawn copies.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 24 (EnemySpawner class).
</details>

---

**Problem 6:** Create a complete 2D game with player movement, enemies, collectibles, and score system.

<details>
<summary>Hint</summary>
Combine: 2D movement, sprite animation, prefabs for enemies/coins, collision detection, score UI.
</details>

<details>
<summary>Answer</summary>
Combine code from Days 22, 23, and 24. Add collision detection for coin collection.
</details>

---

### Challenge Tier

**Problem 7:** Design a complete 2D mini-game with multiple levels, difficulty progression, and persistent high score.

<details>
<summary>Hint</summary>
Create multiple levels with increasing enemy count/speed. Save high score with PlayerPrefs. Implement level transitions.
</details>

<details>
<summary>Answer</summary>
Combine Units 5 and 6. Create multiple scenes, use Tilemaps for level design, implement progression.
</details>

---

**Problem 8:** Implement an object pooling system for bullets or enemies to optimize performance.

<details>
<summary>Hint</summary>
Pre-create objects and disable them. Reuse disabled objects instead of instantiating new ones.
</details>

<details>
<summary>Answer</summary>
See annotated code example in Day 24 (BulletPool class).
</details>

---

## Practice Bank (15 Problems)

1. **Sprite Sheet Management:** Import a sprite sheet and configure slice settings to separate individual sprites.

2. **Sorting Order Layers:** Create a scene with 5 sprites at different sorting orders. Verify layering is correct.

3. **Tilemap Painting:** Create a Tilemap level with 3+ different tile types. Paint a diverse landscape.

4. **2D Rigidbody Configuration:** Set up a 2D Rigidbody with appropriate mass, gravity, and drag for a platformer character.

5. **Grounding Detection:** Implement raycast-based grounding detection and verify it correctly detects when player is on platforms.

6. **Sprite Flipping:** Create movement that automatically flips the sprite based on direction (left/right).

7. **Animation Transitions:** Create a 4-state animation system (Idle, Run, Jump, Fall) with smooth transitions.

8. **Animator Parameters:** Use multiple parameter types (bool, float, trigger) to control complex animation states.

9. **Prefab Variants:** Create a prefab and then create variants with different colors/sizes.

10. **Instantiation Practice:** Spawn prefabs at runtime using random positions. Destroy them on collision.

11. **Sprite Animation:** Manually animate a sprite by changing the sprite frame each update.

12. **2D Collider Shapes:** Use different 2D collider types (Box, Circle, Polygon) for different objects.

13. **Collision Detection 2D:** Use OnCollisionEnter2D() and OnTriggerEnter2D() to handle 2D interactions.

14. **Physics2D Raycast:** Use Physics2D.Raycast() to detect walls, slopes, and platforms.

15. **Complete Mini-Game:** Build a playable 2D game from scratch including player, enemies, collectibles, scoring, and a game over state.

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Sprite doesn't appear | Texture Type not set to "Sprite" | Always set Texture Type to "Sprite (2D and UI)" in import settings |
| Rigidbody2D falls off screen | No collider on ground or gravity too high | Add colliders to all collidable objects; adjust gravity scale |
| 2D movement feels stiff | Using transform.position instead of velocity | Always modify velocity for smooth physics-based movement |
| Animation doesn't play | Animator Controller not assigned or no states | Assign Animator Controller; create states and transitions |
| Prefab changes don't affect instances | Instance has overrides that override prefab | Select the instance and "Revert" overrides to match prefab |
| Sprites overlap incorrectly | Sorting order not configured properly | Set consistent sorting order: background (0), player (5), UI (10) |
| Instantiate() creates wrong object | Wrong prefab assigned in Inspector | Double-check the public field references the correct prefab |
| Animation loops incorrectly | Loop setting wrong or animation too long | Adjust animation duration; check "Loop" checkbox for looping animations |
| Grounding detection always false | Raycast distance too small or colliders missing | Increase raycast distance; ensure platform has collider |
| Performance issues with many objects | Creating/destroying too frequently | Use object pooling to reuse instances |

---

## Assessment Prep: 10 Q&As

**Q1: What is a Sprite Renderer and what does it do?**
A: A Sprite Renderer displays a 2D sprite on a GameObject. It controls which sprite is displayed, color, sorting order, and flip state.

**Q2: Explain the difference between Tilemap and individual sprites for level design.**
A: Tilemaps use a grid of repeated tiles for efficient level building. Individual sprites are placed manually. Tilemaps are better for large levels; individual sprites for unique objects.

**Q3: How do you implement grounded detection in 2D?**
A: Use Physics2D.Raycast() downward from the player. If it hits a collider, the player is grounded.

**Q4: What is the difference between animation clips and the Animator component?**
A: Animation clips are sequences of frames. The Animator plays clips and manages transitions between them based on parameters and conditions.

**Q5: How do you create a prefab and why is it useful?**
A: Build a GameObject, drag it to the Project folder. Prefabs are useful because you can spawn multiple copies and changes to the prefab affect all instances.

**Q6: Explain what a Sprite Sheet is and how to use it in Unity.**
A: A Sprite Sheet is an image with multiple sprites in a grid. Set Texture Type to "Sprite (2D and UI)", adjust slice settings, and separate individual sprites.

**Q7: How do you control which animation plays using the Animator?**
A: Set animator parameters (bool, float, trigger) that trigger transitions: `animator.SetBool("IsRunning", true);`

**Q8: What is object pooling and when should you use it?**
A: Pre-creating and reusing objects instead of instantiating/destroying. Use it when spawning many objects frequently (bullets, enemies, particles).

**Q9: How do you flip a 2D sprite based on movement direction?**
A: `spriteRenderer.flipX = (moveDirection.x < 0);`

**Q10: Describe the components needed for a complete 2D platformer character.**
A: Sprite Renderer (visual), Rigidbody2D (physics), Collider2D (collision), Animator (animation), and a script controlling input/movement.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **Sprite** | A 2D image used in 2D games |
| **Sprite Renderer** | Component that displays a sprite |
| **Sorting Order** | Z-layer determining draw order (higher = in front) |
| **Tilemap** | A grid of tiles for efficient level building |
| **Tile Palette** | A set of available tiles for painting |
| **Rigidbody2D** | 2D physics component |
| **Collider2D** | 2D collision shape |
| **Velocity** | 2D speed and direction (x, y) |
| **Animation Clip** | Sequence of sprites or keyframes |
| **Animator** | Component playing animations and managing states |
| **Prefab** | Template GameObject for spawning copies |
| **Instantiate()** | Creates a copy of a GameObject at runtime |
| **isGrounded** | Boolean indicating if touching ground |

### 2D Components Quick Reference

```csharp
// Sprite Renderer
SpriteRenderer sr = GetComponent<SpriteRenderer>();
sr.sprite = mySprite;
sr.color = Color.red;
sr.sortingOrder = 5;
sr.flipX = true;  // Flip horizontally

// Rigidbody2D
Rigidbody2D rb2d = GetComponent<Rigidbody2D>();
rb2d.velocity = new Vector2(5, 0);
rb2d.AddForce(Vector2.up * 5, ForceMode2D.Impulse);
rb2d.gravityScale = 1f;

// Collider2D types
BoxCollider2D box = GetComponent<BoxCollider2D>();
CircleCollider2D circle = GetComponent<CircleCollider2D>();
PolygonCollider2D poly = GetComponent<PolygonCollider2D>();

// 2D Collision/Trigger
void OnCollisionEnter2D(Collision2D collision) { }
void OnTriggerEnter2D(Collider2D collision) { }

// Physics2D Raycast
RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.1f);
bool isGrounded = hit.collider != null;
```

### Animation Quick Reference

```csharp
// Animator parameter control
Animator animator = GetComponent<Animator>();
animator.SetBool("IsRunning", true);
animator.SetFloat("Speed", moveSpeed);
animator.SetTrigger("Jump");
animator.SetInteger("Direction", 1);

// Common animation states
// Idle, Run, Jump, Fall, Attack, Die, etc.

// Animator Controller structure (set up in editor):
// Parameters: IsRunning (bool), IsJumping (bool), etc.
// States: Idle, Run, Jump, Fall, etc.
// Transitions with conditions between states
```

### Prefab Quick Reference

```csharp
// Instantiate a prefab
public GameObject prefab;
GameObject instance = Instantiate(prefab, position, rotation);
GameObject instance = Instantiate(prefab);  // Uses prefab's position/rotation

// Instantiate with parent
Instantiate(prefab, position, rotation, parentTransform);

// Destroy instance
Destroy(instance);
Destroy(gameObject);  // Destroy self
```

---

## Additional Resources

- **2D Sprite Documentation:** https://docs.unity3d.com/Manual/2DSpriteProperties.html
- **Tilemap Tutorial:** https://docs.unity3d.com/Manual/Tilemap.html
- **Animator Documentation:** https://docs.unity3d.com/Manual/AnimatorConcepts.html
- **Prefab Best Practices:** https://docs.unity3d.com/Manual/Prefabs.html

