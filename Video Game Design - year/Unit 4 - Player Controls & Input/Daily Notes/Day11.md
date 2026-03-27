# Day 11: Gamepad Input Basics

**Learning Target:** I can read gamepad input and map it to player controls.

---

## Key Concepts

**Gamepad Input** — Unity maps gamepad axes and buttons to the Input Manager, just like keyboard. Works with Xbox, PlayStation, and generic controllers.

**Default Gamepad Mapping:**
- **Left Stick:** Horizontal & Vertical (same as WASD)
- **Right Stick:** Not mapped by default (you set it up)
- **Triggers:** LT/RT map to "Horizontal" (confusing) or you can add custom axes
- **Buttons:** A, B, X, Y, LB, RB

**How It Works:** Gamepad input goes to Input Manager axes. `Input.GetAxis("Horizontal")` works for both keyboard AND gamepad. No special code needed!

**Input Manager:** Edit → Project Settings → Input Manager. Shows all mapped axes and buttons.

---

## Code Example

```csharp
using UnityEngine;

public class GamepadController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleGamepadMovement();
        HandleGamepadJump();
        ApplyGravity();
    }

    private void HandleGamepadMovement()
    {
        // Left stick controls movement (same as keyboard WASD)
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        Vector3 moveDir = new Vector3(horizontal, 0, vertical).normalized;

        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void HandleGamepadJump()
    {
        // A button (bottom button on Xbox controller)
        if (Input.GetButtonDown("Jump") && controller.isGrounded)
        {
            velocity.y = jumpForce;
            Debug.Log("Gamepad Jump!");
        }

        // Space also works (keyboard compatibility)
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        {
            velocity.y = jumpForce;
        }
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0)
            velocity.y = -2f;
        else
            velocity.y -= gravity * Time.deltaTime;
    }
}
```

---

## Unity Setup Steps

1. **Use Player from Previous Days**
   - Capsule with CharacterController

2. **Test Without Gamepad First**
   - Keyboard should still work (WASD + Space)
   - Proves your code is compatible with both input types

3. **Connect Gamepad**
   - Plug in Xbox, PlayStation, or generic controller
   - Windows/Mac auto-detects
   - Press Play and test

4. **Verify Input Manager**
   - Edit → Project Settings → Input Manager
   - Check that "Horizontal" and "Vertical" are mapped
   - "Jump" should be mapped to Space and gamepad button South (A)

---

## Guided Practice

1. **Test Keyboard First** (5 min)
   - Verify WASD and Space work as before
   - Gamepad code doesn't change your keyboard setup

2. **Connect Gamepad & Test** (10 min)
   - Plug in controller
   - Press Play and move left stick
   - Press A button to jump
   - Test that both work

3. **Test Diagonal Movement** (5 min)
   - Move left stick diagonally
   - Verify movement speed is consistent
   - Debug.Log gamepad input values

---

## Practice Problems

**Beginner:** Read gamepad left stick input and move the player. Test with both keyboard and controller.

**Intermediate:** Map **right stick X-axis** to camera rotation. Add a custom input axis in Input Manager called "RightStickHorizontal" mapped to gamepad right stick X. Use it to rotate the camera.

**Challenge:** Implement **controller vibration (haptic feedback)**: when the player lands from a jump, trigger controller rumble using `GamepadInput.SetGamepadVibration()`. (Note: Platform-dependent; mainly Xbox/PS5.)

<details><summary>💡 Hints</summary>
- `Input.GetAxis()` and `Input.GetButton()` work for both keyboard and gamepad automatically.
- The Input Manager is at Edit → Project Settings → Input Manager.
- Different controllers may map differently on different platforms. Test thoroughly!
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Right Stick Camera):**
```csharp
// First, add to Input Manager:
// New Axis: "RightStickX"
// Type: Joystick Axis
// Axis: 4 (Right Stick X)
// Sensitivity: 1

public float cameraRotationSpeed = 2f;

void Update()
{
    float rightStickX = Input.GetAxis("RightStickX");
    
    if (Mathf.Abs(rightStickX) > 0.1f) // Deadzone
    {
        transform.Rotate(Vector3.up, rightStickX * cameraRotationSpeed * Time.deltaTime);
    }
}
```

</details>
