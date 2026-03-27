# Day 6: Double-Jump & Coyote Time

**Learning Target:** I can implement advanced jump mechanics like double-jump and coyote time to make controls feel forgiving.

---

## Key Concepts

**Double-Jump** — Allow the player to jump once while airborne. Used in *Super Smash Bros*, *Celeste*, and many platformers to add mobility and fun.

**Coyote Time** — A forgiving mechanic from *Celeste*: the player can jump for a brief moment (0.15s) after leaving the ground, making platformers feel less frustrating.

**Implementation Strategy:**
- Track `jumpCount` (0 = grounded, 1 = first jump, 2 = second jump)
- Reset jumpCount when grounded
- Allow jump if jumpCount < maxJumps
- Use a timer for coyote time

---

## Code Example

```csharp
using UnityEngine;

public class AdvancedJumpController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float gravity = 9.81f;
    public int maxJumps = 2; // Double-jump
    public float coyoteTime = 0.15f;

    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private int jumpCount = 0;
    private float timeSinceGrounded = 0f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleMovement();
        UpdateCoyoteTime();
        HandleJump();
        ApplyGravity();

        Debug.Log($"Jumps: {jumpCount}/{maxJumps}, Coyote: {timeSinceGrounded:F2}");
    }

    private void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        Vector3 moveDir = new Vector3(h, 0, v).normalized;
        
        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void UpdateCoyoteTime()
    {
        if (controller.isGrounded)
        {
            timeSinceGrounded = 0f;
            jumpCount = 0;
        }
        else
        {
            timeSinceGrounded += Time.deltaTime;
        }
    }

    private void HandleJump()
    {
        bool canJump = jumpCount < maxJumps && timeSinceGrounded < coyoteTime;

        if (Input.GetKeyDown(KeyCode.Space) && canJump)
        {
            velocity.y = jumpForce;
            jumpCount++;
            Debug.Log($"Jump {jumpCount}!");
        }
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0f)
            velocity.y = -2f;
        else
            velocity.y -= gravity * Time.deltaTime;
    }
}
```

---

## Unity Setup Steps

1. **Use JumpController from Day 5** and modify it

2. **Add AdvancedJumpController Script**
   - Create C# script → "AdvancedJumpController"
   - Attach to Player
   - Set maxJumps to `2` in Inspector
   - Set coyoteTime to `0.15` in Inspector

3. **Test Double-Jump**
   - Press Play
   - Jump once (Space)
   - While airborne, press Space again to double-jump
   - Should jump twice total

4. **Test Coyote Time**
   - Jump and walk off a platform
   - You have 0.15 seconds to press Space and still jump
   - Makes platforming feel forgiving

---

## Guided Practice

1. **Track Jump Count** (10 min)
   - Add a `jumpCount` variable
   - Reset it to 0 when grounded
   - Increment it when jumping
   - Print the current jump count

2. **Allow Second Jump** (10 min)
   - Check if `jumpCount < maxJumps` before allowing jump
   - Test that you can jump twice while airborne

3. **Implement Coyote Time** (5 min)
   - Add `timeSinceGrounded` timer
   - Only allow jump if `timeSinceGrounded < coyoteTime`
   - Test walking off a platform and jumping within the window

---

## Practice Problems

**Beginner:** Implement double-jump. Allow jumping twice total (once grounded, once airborne). Log which jump number it is.

**Intermediate:** Add **fall acceleration**: if the player falls longer than 0.5 seconds, increase gravity multiplier to make long falls feel scary.

**Challenge:** Implement **variable jump height with coyote time**: longer Space hold = higher jump, but only if jump is within coyote window. Otherwise, jump is at full force.

<details><summary>💡 Hints</summary>
- Reset `jumpCount` when `controller.isGrounded` becomes true.
- Use a timer (`timeSinceGrounded`) that resets when grounded and increases every frame.
- Coyote time makes platformers forgiving—test different values (0.1 to 0.2) to see what feels best.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Fall Acceleration):**
```csharp
private float fallTime = 0f;

void ApplyGravity()
{
    if (controller.isGrounded)
    {
        velocity.y = -2f;
        fallTime = 0f;
    }
    else
    {
        fallTime += Time.deltaTime;
        float gravityMultiplier = fallTime > 0.5f ? 1.5f : 1f;
        velocity.y -= gravity * gravityMultiplier * Time.deltaTime;
    }
}
```

</details>
