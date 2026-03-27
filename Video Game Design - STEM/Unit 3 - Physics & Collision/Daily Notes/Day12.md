# Day 12: Physics-Based Movement & Ground Detection

**Learning Target:** Implement character jumping and movement using raycasting for ground detection.

### Key Concepts

- **Raycasting:** Casting a line from a point to detect what it hits
- **Physics.Raycast():** Casts a ray and returns true if it hits something
- **Grounded Check:** Detecting if the player is on the ground using raycasts
- **Jump Mechanics:** Preventing jumping while in the air
- **Falling Velocity:** Acceleration due to gravity accumulates over time
- **Slope Detection:** Using raycasts to determine if the ground is flat or angled
- **Character Controller:** Simplified alternative to Rigidbody for character movement

### Content

Ground detection is crucial for platformer games. You need to know if the player is on the ground to allow jumping. Raycasting is the most reliable method.

**Raycast Basics:**
```csharp
RaycastHit hit;
bool didHit = Physics.Raycast(startPosition, direction, out hit, maxDistance);

if (didHit)
{
    Debug.Log("Ray hit: " + hit.collider.gameObject.name);
    Debug.Log("Distance: " + hit.distance);
    Debug.Log("Hit point: " + hit.point);
}
```

**Ground Detection:**
Cast a ray downward from the player. If it hits something, the player is grounded.

```csharp
RaycastHit hit;
float groundDistance = 0.1f;  // Small distance below the player
bool isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);
```

This works by sending a ray from the player's position straight down. If something is within `groundDistance` below, the player is grounded.

### Code Examples

```csharp
using UnityEngine;

public class PhysicsCharacterController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float groundDrag = 5f;
    public float airDrag = 1f;
    public float groundDistance = 0.2f;

    private Rigidbody rb;
    private bool isGrounded = false;
    private float verticalVelocity = 0f;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Check if grounded using raycast
        RaycastHit hit;
        isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

        Debug.Log("Grounded: " + isGrounded);

        // Input for movement
        float horizontalInput = 0f;
        if (Input.GetKey(KeyCode.D))
            horizontalInput += 1f;
        if (Input.GetKey(KeyCode.A))
            horizontalInput -= 1f;

        // Jump input
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }
    }

    void FixedUpdate()
    {
        // Apply movement
        float horizontalInput = 0f;
        if (Input.GetKey(KeyCode.D))
            horizontalInput += 1f;
        if (Input.GetKey(KeyCode.A))
            horizontalInput -= 1f;

        // Apply horizontal movement
        rb.velocity = new Vector3(horizontalInput * moveSpeed, rb.velocity.y, 0);

        // Apply drag
        if (isGrounded)
        {
            rb.drag = groundDrag;
        }
        else
        {
            rb.drag = airDrag;
        }
    }

    void Jump()
    {
        Debug.Log("Jump!");
        // Reset vertical velocity and apply upward impulse
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
    }
}
```

### Guided Practice

1. Create a player Capsule with a Rigidbody
2. Create a ground Plane with a Box Collider
3. Create a script that uses Physics.Raycast() to detect if the player is grounded
4. Implement jumping that only works when grounded
5. Test different groundDistance values to see how they affect detection
6. Press Space to jump and verify it only works on the ground
7. Try jumping while in the air (should not work)

### Practice Problems

**Problem 1 — Beginner:** Create a script that makes a Cube jump when you press Space, but only if it's grounded (use raycast for ground detection).

**Problem 2 — Intermediate:** Create a complete platformer controller: move left/right, jump when grounded, and prevent double-jumping. Use raycasts for ground detection and Rigidbody for physics.

**Problem 3 — Challenge:** Implement a more complex ground detection system that ignores certain layers or tags, allowing special platforms with different jump mechanics.

<details>
<summary>Hints</summary>

**Hint 1:** The raycast direction should point downward (Vector3.down). The distance should be small (0.1 to 0.3 units).

**Hint 2:** Use `Physics.Raycast()` in Update() to check ground state. Store the result in a boolean `isGrounded`.

**Hint 3:** Only allow jumping if `isGrounded` is true. Reset the vertical velocity before applying jump force.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void Update()
{
    RaycastHit hit;
    isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
        Debug.Log("Jumped!");
    }
}
```

**Answer 2:**
```csharp
void Update()
{
    // Check ground
    RaycastHit hit;
    isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

    // Input
    float moveInput = 0f;
    if (Input.GetKey(KeyCode.D)) moveInput += 1f;
    if (Input.GetKey(KeyCode.A)) moveInput -= 1f;

    // Jump only if grounded
    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
    {
        Jump();
    }
}

void FixedUpdate()
{
    rb.velocity = new Vector3(moveInput * moveSpeed, rb.velocity.y, 0);
    rb.drag = isGrounded ? groundDrag : airDrag;
}
```

**Answer 3:** Use Physics.Raycast with layer masks: `Physics.Raycast(pos, dir, out hit, distance, layerMask);`

</details>
