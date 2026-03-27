# Day 5: Ground Detection & Jumping Mechanics

**Learning Target:** I can detect when the player is grounded and implement reliable jump mechanics.

---

## Key Concepts

**Ground Detection** — Determining if the player is touching the ground is critical for jumping. Methods:
1. **CharacterController.isGrounded** — Built-in flag (easiest)
2. **Raycast** — Shoot a ray downward; if it hits something, you're grounded
3. **Collision events** — OnCollisionEnter/Stay

**isGrounded quirk:** CharacterController.isGrounded only works if SimpleMove/Move is called. It updates *after* the movement call, so check it at the start of the next frame.

**Jump Requirements:**
- Can only jump if grounded
- Apply upward velocity once per button press
- Reset downward velocity to prevent multi-jumps

---

## Code Example

```csharp
using UnityEngine;

public class JumpController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float gravity = 9.81f;
    public float groundDrag = 0.1f;
    
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private bool wasGroundedLastFrame = true;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleMovement();
        HandleJump();
        ApplyGravity();
        
        Debug.Log($"Grounded: {controller.isGrounded}, Velocity.y: {velocity.y:F2}");
        wasGroundedLastFrame = controller.isGrounded;
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

    private void HandleJump()
    {
        // Jump only on the frame the key is pressed AND grounded
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        {
            velocity.y = jumpForce;
            Debug.Log("Jump!");
        }
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0f)
        {
            velocity.y = -2f; // Small downward force to keep grounded
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

1. **Use CharacterController player** (from previous days)

2. **Test Ground Detection**
   - Attach the JumpController script
   - Open the Console (Ctrl+` or Window > General > Console)
   - Press Play and watch the "Grounded" debug output

3. **Add Ground Plane**
   - Create a Plane (3D Object → Plane)
   - Scale it to `(20, 1, 20)` and position at `(0, 0, 0)`
   - Both should have Colliders

4. **Test Jump**
   - Press Play
   - Press Space to jump
   - Verify you can only jump when grounded (not mid-air)

---

## Guided Practice

1. **Debug Ground State** (5 min)
   - Add Debug.Log output showing `controller.isGrounded`
   - Press Play and watch the console
   - Notice it updates after movement is applied

2. **Implement Jump** (10 min)
   - Add Input.GetKeyDown(Space) check
   - Apply `velocity.y = jumpForce` when conditions are met
   - Test jumping

3. **Tweak Feel** (5 min)
   - Adjust jumpForce from 5 to 8
   - Adjust gravity from 9.81 to 15
   - Find settings that feel responsive and game-like

---

## Practice Problems

**Beginner:** Log "Jump Started" when jump begins and "Jump Ended" when landing. Use controller.isGrounded and wasGroundedLastFrame to detect transitions.

**Intermediate:** Add a **land sound effect**: use `GetComponent<AudioSource>().PlayOneShot(landSFX)` when the player lands. (Hint: Create an AudioSource component and assign a sound.)

**Challenge:** Implement a **ground detection raycast** that casts a ray 0.5 units downward from the player's feet. Only allow jumping if the raycast hits something. Use `Physics.Raycast()`.

<details><summary>💡 Hints</summary>
- CharacterController.isGrounded updates after Move/SimpleMove is called, so check it before jumping.
- Keep a small downward velocity (like -2f) when grounded to prevent floating.
- wasGroundedLastFrame helps detect landing (transition from not grounded to grounded).
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
private void Update()
{
    controller.Move(motion * Time.deltaTime);

    if (!wasGroundedLastFrame && controller.isGrounded)
        Debug.Log("Jump Ended / Landing");
    
    if (wasGroundedLastFrame && !controller.isGrounded)
        Debug.Log("Jump Started");

    wasGroundedLastFrame = controller.isGrounded;
}
```

**Challenge Solution (Raycast):**
```csharp
private bool CheckGrounded()
{
    Vector3 rayOrigin = transform.position + Vector3.down * (controller.height / 2);
    return Physics.Raycast(rayOrigin, Vector3.down, 0.5f);
}

private void HandleJump()
{
    if (Input.GetKeyDown(KeyCode.Space) && CheckGrounded())
        velocity.y = jumpForce;
}
```

</details>
