# Day 18: 2D Physics Advanced — Constraints & Raycasting

**Learning Target:** I can use 2D constraints, Physics2D.Raycast, and advanced 2D physics features.

---

## Key Concepts

**Rigidbody2D Constraints:**
- **Freeze Position X/Y** — Lock object to specific axes
- **Freeze Rotation Z** — Prevent spinning

**Physics2D.Raycast** — 2D version of raycasting. Same concept as 3D but for 2D space.

**Gravity Scale** — Control how much gravity affects object independently of global gravity.

**Drag & Angular Drag** — 2D versions slow movement and rotation.

**One-way platforms** — Use EdgeCollider2D and script logic to allow jumping through from below but standing on top.

**Real-world examples:**
- **Celeste:** Precise movement uses constraints and careful force application
- **Hollow Knight:** Wall slides use specialized colliders and movement logic
- **Jump King:** Simple vertical movement with constrained X axis
- **Metroid:** One-way platforms and bouncy jumps

---

## Code Example

```csharp
using UnityEngine;

public class Advanced2DController : MonoBehaviour
{
    private Rigidbody2D rb2d;
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float wallSlideSpeed = 1f;
    public float jumpPower = 10f;

    private bool isGrounded = false;
    private bool isOnWall = false;
    private Vector2 wallNormal;

    private void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        HandleMovement();
        CheckGround();
        CheckWalls();
        HandleJump();
    }

    private void HandleMovement()
    {
        float moveInput = Input.GetAxis("Horizontal");
        rb2d.velocity = new Vector2(moveInput * moveSpeed, rb2d.velocity.y);
    }

    private void CheckGround()
    {
        RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.5f);
        isGrounded = hit.collider != null && !hit.collider.CompareTag("OneWay");
    }

    private void CheckWalls()
    {
        // Check left wall
        RaycastHit2D hitLeft = Physics2D.Raycast(transform.position, Vector2.left, 0.5f);
        
        // Check right wall
        RaycastHit2D hitRight = Physics2D.Raycast(transform.position, Vector2.right, 0.5f);

        if ((hitLeft.collider != null || hitRight.collider != null) && !isGrounded)
        {
            isOnWall = true;
            wallNormal = hitLeft.collider != null ? hitLeft.normal : hitRight.normal;
            
            // Slow fall on wall
            rb2d.velocity = new Vector2(rb2d.velocity.x, Mathf.Max(rb2d.velocity.y, -wallSlideSpeed));
        }
        else
        {
            isOnWall = false;
        }
    }

    private void HandleJump()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            if (isGrounded)
            {
                rb2d.velocity = new Vector2(rb2d.velocity.x, 0);
                rb2d.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
            }
            else if (isOnWall)
            {
                // Wall jump
                Vector2 jumpDirection = new Vector2(wallNormal.x * jumpPower, jumpForce);
                rb2d.velocity = Vector2.zero;
                rb2d.AddForce(jumpDirection, ForceMode2D.Impulse);
            }
        }
    }
}

public class OneWayPlatform : MonoBehaviour
{
    private EdgeCollider2D edgeCol;
    private Collider2D playerCollider;

    private void Start()
    {
        edgeCol = GetComponent<EdgeCollider2D>();
    }

    private void OnTriggerStay2D(Collider2D collision)
    {
        // Allow jumping through platform from below
        if (collision.CompareTag("Player"))
        {
            playerCollider = collision;

            if (collision.transform.position.y < transform.position.y)
            {
                // Player is below platform, disable collision
                Physics2D.IgnoreCollision(playerCollider, edgeCol);
            }
            else
            {
                // Player is above platform, enable collision
                Physics2D.IgnoreCollision(playerCollider, edgeCol, false);
            }
        }
    }
}

public class Physics2DRaycastExample : MonoBehaviour
{
    public float rayDistance = 2f;

    private void Update()
    {
        // Cast ray in direction of movement
        Vector2 moveDir = new Vector2(Input.GetAxis("Horizontal"), 0);
        
        if (moveDir != Vector2.zero)
        {
            RaycastHit2D hit = Physics2D.Raycast(transform.position, moveDir, rayDistance);

            if (hit.collider != null)
            {
                Debug.Log("Can see: " + hit.collider.gameObject.name);
            }

            Debug.DrawRay(transform.position, moveDir * rayDistance, Color.red);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create advanced platformer level**
2. **Set up Player with Rigidbody2D:**
   - Gravity Scale: 1
   - Constraints: Freeze Rotation Z
3. **Create one-way platform:**
   - Use EdgeCollider2D instead of BoxCollider2D
   - Attach OneWayPlatform script
4. **Create walls for wall-slide testing**
5. **Attach Advanced2DController to player**
6. **Press Play:** Test movement, jumping, wall sliding

---

## Guided Practice

1. Build a challenging 2D platformer level
2. Implement wall-sliding mechanics
3. Add one-way platforms that work correctly
4. Test wall jumping to reach high areas
5. Refine movement feel with speed/force adjustments

---

## Practice Problems

**Beginner:** Create a one-way platform. Player can jump through from below, but stands on top when landing from above.

**Intermediate:** Build a wall-slide system. When touching a wall, player slides down slowly and can wall-jump.

**Challenge:** Create a "momentum-based" platformer. Player builds speed by running and can slide under low passages if moving fast enough.

<details><summary>💡 Hints</summary>
- EdgeCollider2D works great for one-way platforms with careful collision handling
- Use Physics2D.IgnoreCollision() to dynamically disable/enable collisions
- Wall-sliding needs normal detection to push player away from wall
- Raycast2D is cheaper than OverlapCircle for single-line checks
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Momentum-based sliding
public class MomentumSlide : MonoBehaviour
{
    private Rigidbody2D rb2d;
    public float minSpeedToSlide = 8f;
    public float slideHeight = 0.5f;
    public BoxCollider2D normalCollider;
    public BoxCollider2D slideCollider;

    private bool isSliding = false;

    private void Start()
    {
        rb2d = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        bool shouldSlide = rb2d.velocity.magnitude > minSpeedToSlide && Input.GetKey(KeyCode.S);

        if (shouldSlide && !isSliding)
        {
            StartSlide();
        }
        else if (!shouldSlide && isSliding)
        {
            EndSlide();
        }
    }

    private void StartSlide()
    {
        isSliding = true;
        normalCollider.enabled = false;
        slideCollider.enabled = true;
    }

    private void EndSlide()
    {
        isSliding = false;
        normalCollider.enabled = true;
        slideCollider.enabled = false;
    }
}
```

</details>
