# Day 12: Gamepad Input Advanced & Deadzone Handling

**Learning Target:** I can handle gamepad input robustly with deadzones, vibration, and dual input systems.

---

## Key Concepts

**Deadzone** — Gamepad sticks have drift and jitter near center. A deadzone (e.g., 0.1) ignores input below that magnitude to prevent unintended movement.

**Vibration/Haptics** — Controller rumble feedback. Adds impact to jumps, hits, and explosions. Different on Xbox (rumble) vs. PlayStation (haptic feedback).

**Dual Input** — Supporting both keyboard and gamepad seamlessly. Players expect to switch mid-game without restarting.

**Gamepad Stick vs. Trigger:**
- Stick: Analog, two axes (X, Y)
- Trigger: Analog, one axis (0 = released, 1 = fully pressed)

---

## Code Example

```csharp
using UnityEngine;

public class AdvancedGamepadController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float deadzone = 0.1f;
    public float gravity = 9.81f;
    
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private bool wasGroundedLastFrame = true;
    private Gamepad gamepad;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        gamepad = Gamepad.current; // From UnityEngine.InputSystem
    }

    private void Update()
    {
        HandleMovement();
        HandleJump();
        ApplyGravity();
    }

    private void HandleMovement()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        // Apply deadzone
        Vector3 moveDir = new Vector3(horizontal, 0, vertical);
        if (moveDir.magnitude < deadzone)
            moveDir = Vector3.zero;
        else
            moveDir = moveDir.normalized;

        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void HandleJump()
    {
        if (Input.GetButtonDown("Jump") && controller.isGrounded)
        {
            velocity.y = jumpForce;
            
            // Vibrate on jump
            if (gamepad != null)
                gamepad.SetMotorSpeeds(0.5f, 0.5f);
            
            Debug.Log("Jump with rumble!");
        }
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0)
            velocity.y = -2f;
        else
            velocity.y -= gravity * Time.deltaTime;
        
        wasGroundedLastFrame = controller.isGrounded;
    }
}
```

---

## Unity Setup Steps

1. **Enable Input System Package (New)**
   - Package Manager → "Input System"
   - Install if using new Input System
   - Or stick with old Input Manager (legacy)

2. **Attach AdvancedGamepadController**
   - Create C# script → "AdvancedGamepadController"
   - Attach to Player
   - Set deadzone to `0.1` in Inspector

3. **Connect Gamepad & Test**
   - Plug in controller
   - Move left stick near center (within deadzone)
   - Verify no drift
   - Move full range and verify movement

4. **Test Jump Vibration**
   - Press A/Space to jump
   - Feel controller rumble
   - (May not work on all platforms)

---

## Guided Practice

1. **Implement Deadzone** (10 min)
   - Read gamepad stick values
   - If magnitude < 0.1, ignore input
   - Test smooth movement without jitter

2. **Add Vibration on Jump** (10 min)
   - Call `gamepad.SetMotorSpeeds()` when jumping
   - Set left and right motor speeds (0 = off, 1 = full)
   - Feel the feedback

3. **Test Dual Input** (5 min)
   - Switch between keyboard and gamepad mid-game
   - Verify both work seamlessly
   - Verify input switches automatically

---

## Practice Problems

**Beginner:** Implement deadzone handling so gamepad stick drift doesn't cause unintended movement.

**Intermediate:** Create a **trigger-based attack**: pressing RT (right trigger) fully shoots a projectile. Use `Input.GetAxis("RightTrigger")` to detect how far it's pressed.

**Challenge:** Implement **vibration feedback on landing**: when the player lands (transition from airborne to grounded), trigger rumble proportional to fall distance. Longer falls = stronger rumble.

<details><summary>💡 Hints</summary>
- Deadzone is applied by checking `vector.magnitude < threshold` before normalizing.
- SetMotorSpeeds takes left and right motor values (0–1). Different platforms handle it differently.
- You can fade vibration over time by reducing motor speeds gradually.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Trigger-Based Attack):**
```csharp
// In Input Manager, add "RightTrigger" mapped to gamepad right trigger (axis 10)

void Update()
{
    float triggerAmount = Input.GetAxis("RightTrigger");
    
    if (triggerAmount > 0.9f) // Fully pressed
    {
        FireProjectile();
        Debug.Log("Shooting!");
    }
}
```

**Challenge Solution (Landing Rumble):**
```csharp
private float fallStartHeight = 0f;

void HandleJump()
{
    if (Input.GetButtonDown("Jump") && controller.isGrounded)
        fallStartHeight = transform.position.y;
}

void Update()
{
    if (!wasGroundedLastFrame && controller.isGrounded)
    {
        float fallDistance = fallStartHeight - transform.position.y;
        float rumbleStrength = Mathf.Clamp01(fallDistance / 10f);
        
        if (gamepad != null)
            gamepad.SetMotorSpeeds(rumbleStrength, rumbleStrength);
        
        Invoke("StopRumble", 0.2f);
    }
}

void StopRumble() => gamepad?.SetMotorSpeeds(0, 0);
```

</details>
