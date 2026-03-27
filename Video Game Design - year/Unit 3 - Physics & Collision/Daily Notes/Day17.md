# Day 17: 2D Physics — Rigidbody2D & Collider2D

**Learning Target:** I can set up physics for 2D games using Rigidbody2D, Collider2D, and Physics2D methods.

---

## Key Concepts

**Rigidbody2D** — 2D version of Rigidbody. Controls gravity, velocity, forces in 2D space. Add with Add Component → Physics 2D → Rigidbody 2D.

**Collider2D types:**
- **BoxCollider2D** — Rectangular collision shape
- **CircleCollider2D** — Circular/round shapes
- **PolygonCollider2D** — Custom convex shapes
- **EdgeCollider2D** — One-way platforms, slopes
- **CapsuleCollider2D** — Character colliders

**Physics2D** — 2D physics system. Physics2D.Raycast, Physics2D.OverlapCircle, etc.

**Gravity Scale** — How much 2D gravity affects object. 0 = no gravity, 1 = normal, 2 = double gravity.

**Constraints** — Freeze X/Y position or Z rotation to prevent unwanted movement.

**Real-world examples:**
- **Flappy Bird:** Uses simple Rigidbody2D with gravity and jump impulses
- **Stardew Valley:** Walking uses Rigidbody2D constraints
- **Hollow Knight:** Wall sliding uses edge colliders
- **2D platformers:** All physics handled by Rigidbody2D + Collider2D

---

## Code Example

```csharp
using UnityEngine;

public class Player2DController : MonoBehaviour
{
    private Rigidbody2D rb2d;
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    
    private bool isGrounded = false;
    public float groundDrag = 0.1f;
    public float airDrag = 0.05f;

    private void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        // Horizontal movement
        float moveInput = Input.GetAxis("Horizontal");
        rb2d.velocity = new Vector2(moveInput * moveSpeed, rb2d.velocity.y);

        // Jump
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }

        // Check ground (raycast down)
        CheckGrounded();
    }

    private void Jump()
    {
        rb2d.velocity = new Vector2(rb2d.velocity.x, 0);
        rb2d.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        Debug.Log("Jumped!");
    }

    private void CheckGrounded()
    {
        RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.5f);
        isGrounded = hit.collider != null;

        Debug.DrawRay(transform.position, Vector2.down * 0.5f, isGrounded ? Color.green : Color.red);
    }
}

public class FlappyBirdStyle : MonoBehaviour
{
    private Rigidbody2D rb2d;
    public float flapForce = 5f;
    public float maxFallSpeed = -10f;

    private void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        // Flap on space
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb2d.velocity = new Vector2(rb2d.velocity.x, 0);
            rb2d.AddForce(Vector2.up * flapForce, ForceMode2D.Impulse);
        }

        // Limit fall speed
        if (rb2d.velocity.y < maxFallSpeed)
        {
            rb2d.velocity = new Vector2(rb2d.velocity.x, maxFallSpeed);
        }
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("Hit: " + collision.gameObject.name);
        // Game over logic
    }
}

public class Physics2DOverlapExample : MonoBehaviour
{
    public float detectionRadius = 2f;
    public LayerMask enemyLayer;

    private void Update()
    {
        // Check for enemies in radius
        Collider2D[] enemies = Physics2D.OverlapCircleAll(transform.position, detectionRadius, enemyLayer);
        
        if (enemies.Length > 0)
        {
            Debug.Log("Found " + enemies.Length + " enemies!");
        }
    }

    private void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position, detectionRadius);
    }
}
```

---

## Unity Setup Steps

1. **Switch to 2D view:** Top-right corner of Scene view → 2D
2. **Create Player (sprite)** with Rigidbody2D and BoxCollider2D
3. **Configure Rigidbody2D:**
   - Body Type: Dynamic
   - Gravity Scale: 1
   - Collision Detection: Continuous
   - Constraints: Freeze Rotation Z
4. **Create ground (sprite)** with Rigidbody2D and BoxCollider2D
   - Body Type: Static
5. **Attach Player2DController script**
6. **Press Play:** Walk and jump

---

## Guided Practice

1. Create a simple 2D platformer
2. Add player with Rigidbody2D and jump logic
3. Add ground platforms
4. Test movement and jumping
5. Adjust moveSpeed and jumpForce until gameplay feels good

---

## Practice Problems

**Beginner:** Create a Flappy Bird-style game. Player taps to flap, avoids obstacles.

**Intermediate:** Build a 2D platformer level with moving platforms, spikes, and coins.

**Challenge:** Create a grappling hook mechanic. Raycast in 2D to detect walls, then pull player toward them.

<details><summary>💡 Hints</summary>
- Use Physics2D for all 2D physics queries (Raycast, OverlapCircle, etc)
- Freeze rotation to prevent objects spinning unexpectedly
- Raycast2D returns RaycastHit2D (different from 3D version)
- EdgeCollider2D is great for one-way platforms
- 2D physics is faster than 3D, good for mobile
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: 2D grappling hook
public class GrappleHook2D : MonoBehaviour
{
    private Rigidbody2D rb2d;
    private LineRenderer rope;
    private Vector2 grapplePoint;
    private bool isGrappling = false;
    public float grappleSpeed = 10f;
    public float maxGrappleDistance = 15f;

    private void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
        rope = GetComponent<LineRenderer>();
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            TryGrapple();
        }

        if (isGrappling)
        {
            MoveTowardGrapplePoint();
            DrawRope();
        }
    }

    private void TryGrapple()
    {
        Vector2 mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
        RaycastHit2D hit = Physics2D.Raycast(transform.position, (mousePos - rb2d.position).normalized, maxGrappleDistance);

        if (hit.collider != null)
        {
            grapplePoint = hit.point;
            isGrappling = true;
        }
    }

    private void MoveTowardGrapplePoint()
    {
        Vector2 direction = (grapplePoint - rb2d.position).normalized;
        rb2d.velocity = direction * grappleSpeed;
    }

    private void DrawRope()
    {
        rope.SetPosition(0, transform.position);
        rope.SetPosition(1, grapplePoint);
    }
}
```

</details>
