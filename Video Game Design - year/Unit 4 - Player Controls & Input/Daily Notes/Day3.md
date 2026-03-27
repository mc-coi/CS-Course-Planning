# Day 3: CharacterController.Move() & Built-In Movement

**Learning Target:** I can use Unity's CharacterController component to create responsive movement without Rigidbody jitter.

---

## Key Concepts

**CharacterController** — A capsule-shaped collider that moves via code (not physics). It handles collision detection without the complexity of Rigidbody physics, making it ideal for **player-controlled characters**.

**CharacterController vs. Rigidbody:**
- **Rigidbody**: Affected by gravity, other forces; slower setup but "realistic"
- **CharacterController**: Kinematic movement; you control everything; perfect for games like *Half-Life 2*, *Halo*, and *Minecraft*

**Key Method:** `controller.Move(Vector3 motion)` — Moves the controller by the given vector and handles collision detection.

**Advantages:**
- No jitter from physics calculations
- More direct control over movement
- Better for precise platformers and FPS games

---

## Code Example

```csharp
using UnityEngine;

public class CharacterMovement : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float gravity = 9.81f;
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleMovement();
        ApplyGravity();
    }

    private void HandleMovement()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        // Calculate movement direction relative to camera forward (3D)
        Vector3 moveDirection = transform.TransformDirection(
            new Vector3(horizontal, 0, vertical)
        ).normalized;

        // Apply moveSpeed to horizontal movement
        Vector3 motion = moveDirection * moveSpeed;

        // Add vertical velocity (gravity and jumps)
        motion.y = velocity.y;

        // Move the controller
        controller.Move(motion * Time.deltaTime);
    }

    private void ApplyGravity()
    {
        // Always apply downward gravity if not on ground
        if (controller.isGrounded)
        {
            velocity.y = 0f;
        }
        else
        {
            velocity.y -= gravity * Time.deltaTime;
        }
    }
}
```

---

## Unity Setup Steps

1. **Create Player with CharacterController**
   - Hierarchy: 3D Object → Capsule (name: "Player")
   - Position at `(0, 1, 0)`

2. **Add CharacterController Component**
   - Inspector: Add Component → Character Controller
   - Height: `2` (matches capsule height)
   - Radius: `0.5`
   - Center: `(0, 1, 0)` (middle of capsule)

3. **Add CharacterMovement Script**
   - Create C# script → "CharacterMovement"
   - Attach to Player
   - Set moveSpeed to `5` in Inspector

4. **Create Ground**
   - 3D Object → Plane
   - Scale to `(20, 1, 20)`, position at `(0, 0, 0)`
   - Add a Collider (should have one by default)

5. **Test**
   - Press Play
   - Move with WASD
   - Watch the character slide smoothly without Rigidbody physics

---

## Guided Practice

1. **Set Up CharacterController** (10 min)
   - Create a capsule-based player
   - Add the CharacterController component
   - Verify the capsule height and radius match

2. **Implement Basic Movement** (10 min)
   - Write HandleMovement() to read input
   - Use `controller.Move()` to apply motion
   - Test movement in 4 directions

3. **Add Gravity** (5 min)
   - Implement ApplyGravity() to apply downward velocity
   - Watch the player fall to the ground and stop

---

## Practice Problems

**Beginner:** Create a simple scene with a CharacterController player and a ground plane. Move the player left/right (ignore vertical input for now).

**Intermediate:** Make the player face the direction it's moving. Rotate the player toward the input direction smoothly using `Vector3.Slerp()` or `transform.rotation`.

**Challenge:** Implement **frame-rate independent movement** by ensuring the velocity application doesn't cause physics inconsistencies on different frame rates. (Hint: Use `Time.deltaTime` correctly.)

<details><summary>💡 Hints</summary>
- CharacterController.isGrounded tells you if the controller is touching the ground.
- Always multiply motion by `Time.deltaTime` before calling Move().
- Use `transform.TransformDirection()` to rotate movement relative to the player's facing direction.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Face Movement Direction):**
```csharp
private void HandleMovement()
{
    float h = Input.GetAxis("Horizontal");
    float v = Input.GetAxis("Vertical");
    Vector3 moveDir = new Vector3(h, 0, v).normalized;

    if (moveDir.magnitude > 0.1f)
    {
        // Face the movement direction
        Quaternion targetRot = Quaternion.LookRotation(moveDir);
        transform.rotation = Quaternion.Slerp(
            transform.rotation, 
            targetRot, 
            Time.deltaTime * 5f
        );
    }

    Vector3 motion = moveDir * moveSpeed;
    motion.y = velocity.y;
    controller.Move(motion * Time.deltaTime);
}
```

</details>
