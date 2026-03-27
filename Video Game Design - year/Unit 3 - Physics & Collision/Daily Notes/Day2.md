# Day 2: Rigidbody Velocity & AddForce

**Learning Target:** I can manipulate a Rigidbody's velocity and apply forces to create realistic movement.

---

## Key Concepts

**velocity** — A Vector3 property representing current movement speed (units per second). You can read or write this directly.

**AddForce()** — Method to apply a force to a Rigidbody. Takes a Vector3 direction/magnitude and a ForceMode.

**ForceMode.Force** — Applies force continuously. Affected by mass.

**ForceMode.Impulse** — Applies force as a single instant burst. Affected by mass. Good for jumps and explosions.

**Rigidbody.velocity** — Can be set directly to override movement. Useful for clamping speed or instant direction changes.

**Real-world examples:**
- **Mario:** Jump uses AddForce(Impulse). Running uses AddForce(Force) or velocity damping.
- **Flappy Bird:** Each tap applies upward impulse. No gravity adjustment needed.
- **Bowling:** Strike force varies by player swipe length.

---

## Code Example

```csharp
using UnityEngine;

public class VelocityAndForce : MonoBehaviour
{
    private Rigidbody rb;
    public float moveSpeed = 10f;
    public float jumpForce = 5f;
    public float maxSpeed = 15f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // Handle input in Update
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");

        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }

        // Move by modifying velocity directly
        Vector3 movement = new Vector3(horizontalInput, 0, verticalInput) * moveSpeed;
        rb.velocity = new Vector3(movement.x, rb.velocity.y, movement.z);
    }

    private void Jump()
    {
        // Reset Y velocity before jumping to ensure consistent jump height
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }

    private void LimitSpeed()
    {
        // Clamp horizontal speed
        if (rb.velocity.magnitude > maxSpeed)
        {
            rb.velocity = rb.velocity.normalized * maxSpeed;
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a Player cube** with a Rigidbody component
2. **Freeze Rotation** in Rigidbody inspector (X, Y, Z all checked) so it doesn't tip over
3. **Create a ground plane:** 3D Object → Plane, scale to 10, 1, 10
4. **Add Rigidbody to plane:** Set Body Type to Static (won't move)
5. **Attach the VelocityAndForce script to the Player cube**
6. **Press Play and test:** WASD to move, Space to jump
7. **Tune moveSpeed** in the Inspector to find comfortable movement

---

## Guided Practice

1. Create a sphere with a Rigidbody and attach a script
2. In FixedUpdate, apply a horizontal force when W is pressed: `rb.AddForce(Vector3.forward * 10f)`
3. Test: Does the sphere accelerate continuously? (Yes—Force adds each frame)
4. Switch to ForceMode.Impulse and press W multiple times. What's the difference?
5. Add drag to the Rigidbody (set to 1). How does movement feel now?

---

## Practice Problems

**Beginner:** Write a script that moves an object in the direction of the mouse cursor using velocity.

**Intermediate:** Create a "knock-back" system where pressing X applies a random force to the object. Make sure the force is powerful enough to move even heavy objects.

**Challenge:** Build a simple "dash" ability. When player presses E, set velocity directly to a high speed in the forward direction for exactly 0.5 seconds, then return to normal movement.

<details><summary>💡 Hints</summary>
- Use `Time.deltaTime` to make force-based movement frame-rate independent
- `Input.GetAxis("Horizontal")` returns values between -1 and 1
- `Vector3.Normalize()` returns a unit direction without magnitude
- Test your forces by printing `rb.velocity.magnitude` each frame
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Dash ability
public class DashAbility : MonoBehaviour
{
    private Rigidbody rb;
    public float dashSpeed = 20f;
    public float dashDuration = 0.5f;

    private float dashTimer = 0f;
    private bool isDashing = false;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.E) && !isDashing)
        {
            StartDash();
        }

        if (isDashing)
        {
            dashTimer -= Time.deltaTime;
            if (dashTimer <= 0)
            {
                isDashing = false;
                rb.velocity = Vector3.zero;
            }
        }
    }

    private void StartDash()
    {
        isDashing = true;
        dashTimer = dashDuration;
        rb.velocity = transform.forward * dashSpeed;
    }
}
```

</details>
