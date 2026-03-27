# Day 2: Input.GetKeyDown & Discrete Input Actions

**Learning Target:** I can use Input.GetKeyDown to detect discrete button presses and trigger one-time actions.

---

## Key Concepts

**Input.GetKeyDown(KeyCode)** — Fires **only once** when a key is first pressed, unlike GetAxis which is continuous. This is perfect for **discrete actions**: jumping, attacking, reloading, dashing.

**Difference from GetAxis:**
- `Input.GetAxis("Horizontal")` → Continuous, smoothly ramps 0 → 1
- `Input.GetKeyDown(KeyCode.Space)` → Fires once per press

**Why this matters:** In *Hollow Knight*, pressing Space once triggers a jump—not holding it down. GetKeyDown ensures the action fires exactly once per press.

**Common Keys:** `Space`, `Return`, `E`, `Q`, `LeftShift`, `Escape`, `Mouse0` (left-click), `Mouse1` (right-click)

---

## Code Example

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    private Rigidbody rb;
    private bool isGrounded = true;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        HandleMovement();
        HandleJump();
    }

    private void HandleMovement()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        Vector3 moveDirection = new Vector3(horizontal, 0, vertical).normalized;
        Vector3 newVelocity = moveDirection * moveSpeed;
        rb.velocity = new Vector3(newVelocity.x, rb.velocity.y, newVelocity.z);
    }

    private void HandleJump()
    {
        // Jump only fires once per Space press
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.velocity = new Vector3(rb.velocity.x, jumpForce, rb.velocity.z);
            isGrounded = false;
            Debug.Log("Jumped!");
        }
    }

    // Call this from OnCollisionStay or raycasts
    public void SetGrounded(bool grounded) => isGrounded = grounded;
}
```

---

## Unity Setup Steps

1. **Use Player from Day 1** (or create new Cube-based player)

2. **Set Up Ground Detection**
   - Create a Plane under the Player: Hierarchy → 3D Object → Plane
   - Scale Plane to `(10, 1, 10)` and position at `(0, –1, 0)`
   - Add a Collider to the Plane (it should already have one)

3. **Add Ground Check Script**
   - Add a simple raycast or collision check (we'll do this fully on Day 5)
   - For now, manually set `isGrounded` to true in Start, or use collision events

4. **Test**
   - Press Play
   - Hold WASD to move
   - Press Space to jump

---

## Guided Practice

1. **Add Jump Action** (10 min)
   - Modify your PlayerController to handle `Input.GetKeyDown(KeyCode.Space)`
   - Apply a `jumpForce` upward velocity
   - Print to console when jump triggers

2. **Test One-Time Fire** (5 min)
   - Press Space and hold it down
   - Verify the player jumps **only once**, not continuously

3. **Add Custom Key (Dash)** (5 min)
   - Add a **dash** action triggered by **E key**
   - Apply a quick horizontal velocity boost
   - Reset isGrounded when landing

---

## Practice Problems

**Beginner:** Create a script that logs "Jump Pressed" to the console each time Space is pressed. Use GetKeyDown, not GetKey.

**Intermediate:** Implement a **double-tap dash**: press E twice within 0.3 seconds to dash in the current movement direction. (Hint: Track the time since last E press.)

**Challenge:** Implement **action priority queuing**: if the player presses Jump and Dash at the same time, Jump takes priority. Log which action was executed.

<details><summary>💡 Hints</summary>
- GetKeyDown fires only in the frame the key goes down. GetKey fires every frame the key is held.
- For ground detection now, just set `isGrounded = true` in Start. We'll add proper raycasts later.
- A "double-tap" requires tracking `Time.time` and comparing the interval between presses.
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
        Debug.Log("Jump Pressed");
}
```

**Intermediate Solution (Double-Tap Dash):**
```csharp
private float lastEPressTime = 0f;
private const float DOUBLE_TAP_WINDOW = 0.3f;

void Update()
{
    if (Input.GetKeyDown(KeyCode.E))
    {
        if (Time.time - lastEPressTime < DOUBLE_TAP_WINDOW)
        {
            Debug.Log("Double-tap dash!");
            // Apply dash force
        }
        lastEPressTime = Time.time;
    }
}
```

</details>
