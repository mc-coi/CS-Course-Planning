# Day 4: CharacterController.SimpleMove() & Simplified Physics

**Learning Target:** I can use SimpleMove() for automatic gravity-based movement with cleaner code.

---

## Key Concepts

**CharacterController.SimpleMove(Vector3 speed)** — Automatically applies gravity and expects a **velocity vector** (not motion over time). This simplifies jump and gravity code.

**Move vs. SimpleMove:**
- `Move(Vector3)` → Direct displacement; you manage gravity manually
- `SimpleMove(Vector3)` → Expects velocity; applies gravity for you

**When to use SimpleMove:** Platformers, top-down games, and FPS games where you want gravity handled automatically without worrying about Time.deltaTime for vertical motion.

---

## Code Example

```csharp
using UnityEngine;

public class SimpleCharacterController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
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
        HandleJump();
    }

    private void HandleMovement()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        Vector3 moveDirection = new Vector3(horizontal, 0, vertical).normalized;

        // SimpleMove automatically applies gravity based on velocity.y
        velocity = moveDirection * moveSpeed;
        controller.SimpleMove(velocity);
    }

    private void HandleJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        {
            velocity.y = jumpForce;
            Debug.Log("Jumped!");
        }
    }
}
```

---

## Unity Setup Steps

1. **Use CharacterController player from Day 3** (or create new one)

2. **Attach SimpleCharacterController Script**
   - Create C# script → "SimpleCharacterController"
   - Drag onto Player
   - Set moveSpeed to `5`, jumpForce to `5`

3. **Test Jump Behavior**
   - Press Play
   - Press Space to jump
   - Watch the player float mid-air and fall

4. **Adjust Jump Feel**
   - Increase jumpForce to `8` for a higher jump
   - Decrease gravity to `6` for floatier feel

---

## Guided Practice

1. **Replace Move() with SimpleMove()** (5 min)
   - Copy the Day 3 code
   - Replace `controller.Move(motion * Time.deltaTime)` with `controller.SimpleMove(velocity)`
   - Notice the code is simpler

2. **Add Jump with SimpleMove** (10 min)
   - In HandleJump(), set `velocity.y = jumpForce` when Space is pressed
   - Test the jump

3. **Tweak Gravity & Jump Feel** (5 min)
   - Increase jumpForce and see how high the jump is
   - Adjust gravity to change how fast the player falls
   - Find values that feel like a game you enjoy

---

## Practice Problems

**Beginner:** Implement a simple jump using SimpleMove. Print "Landing" to the console when the player touches the ground (check `controller.isGrounded`).

**Intermediate:** Add a **fall multiplier**: if the player is falling faster than `–2f`, increase gravity to make falls feel snappier. (Hint: Check if `velocity.y < -2f` and increase gravity accordingly.)

**Challenge:** Implement **variable jump height**: the longer you hold Space, the higher you jump. Release Space to jump at that height. (Hint: Track how long Space has been held in seconds.)

<details><summary>💡 Hints</summary>
- SimpleMove automatically applies gravity, so you don't need the separate ApplyGravity() method.
- velocity.y persists between frames, so setting it to jumpForce once will only affect one frame.
- To make a variable jump, use `gravity` to decrease velocity.y while Space is held.
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
void Update()
{
    HandleMovement();
    HandleJump();

    if (controller.isGrounded && velocity.y < 0)
        Debug.Log("Landing");
}

void HandleJump()
{
    if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        velocity.y = jumpForce;
}
```

**Challenge Solution (Variable Jump):**
```csharp
private float jumpHoldTime = 0f;
private bool isJumping = false;

void HandleJump()
{
    if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
    {
        isJumping = true;
        jumpHoldTime = 0f;
    }

    if (isJumping)
    {
        jumpHoldTime += Time.deltaTime;
        velocity.y = jumpForce + (jumpHoldTime * 2f); // More height per second held
    }

    if (Input.GetKeyUp(KeyCode.Space))
        isJumping = false;

    // Apply gravity while jumping
    if (!controller.isGrounded)
        velocity.y -= gravity * Time.deltaTime;
}
```

</details>
