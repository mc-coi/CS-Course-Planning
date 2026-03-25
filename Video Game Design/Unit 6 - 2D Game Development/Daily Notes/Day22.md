# Day 22: 2D Movement with Rigidbody2D

**Learning Target:** Implement smooth 2D movement and jumping using physics-based velocity control and grounded detection.

### Key Concepts

- **Rigidbody2D:** Physics component for 2D games
- **Velocity:** Speed and direction in 2D (x, y)
- **Gravity Scale:** How much gravity affects the object
- **Constraints:** Lock position or rotation axes
- **isGrounded Check:** Detecting if on the ground using raycasts or collisions
- **Collider2D:** 2D collision shape (BoxCollider2D, CircleCollider2D, etc.)
- **Direction Flipping:** Flipping sprite to face movement direction

### Content

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

### Code Examples

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

### Guided Practice

**Activity:** Implement a simple 2D platformer controller

1. Create a player GameObject with Sprite Renderer and BoxCollider2D
2. Add a Rigidbody2D component
3. Attach the Player2D script from above
4. Create some platform objects with BoxCollider2D (no Rigidbody2D)
5. Test movement and jumping on the platforms

Adjust moveSpeed and jumpForce to feel good.

### Practice Problems

**Problem 1 — Beginner:** Implement 2D movement with jump using Rigidbody2D and velocity.

**Problem 2 — Intermediate:** Create a grounded detection system that correctly identifies when the player is on platforms vs. in the air.

**Problem 3 — Challenge:** Create advanced movement with double jump, variable jump height (hold button longer for higher jump), and wall sliding.

<details>
<summary>Hints</summary>

**Problem 1:** Use rb2d.velocity to control movement. Add upward impulse for jumping. Check grounding with raycast.

**Problem 2:** Use Physics2D.Raycast() downward from the player. Adjust raycast distance to match your collider size.

**Problem 3:** For double jump: track if you've jumped in air; reset on ground. For variable jump: use Input.GetKey() while jumping. For wall slide: raycast to the side; reduce fall speed on walls.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
See the Player2D class code example above.

**Problem 2:**
```csharp
RaycastHit2D hit = Physics2D.Raycast(
    transform.position,
    Vector2.down,
    0.1f,  // Raycast distance - adjust based on collider size
    LayerMask.GetMask("Ground")  // Only check Ground layer
);
isGrounded = hit.collider != null;
```

**Problem 3:**
Add to Player2D:
```csharp
private bool hasAirJump = true;

if (Input.GetKeyDown(KeyCode.Space))
{
    if (isGrounded)
    {
        Jump();
        hasAirJump = true;
    }
    else if (hasAirJump)
    {
        Jump();
        hasAirJump = false;
    }
}
```

</details>
