# Day 17: First-Person Controller – Mouse Look

**Learning Target:** I can implement FPS-style mouse look with vertical clamping and smooth aiming.

---

## Key Concepts

**Mouse Look (FPS-style)**:
- **Horizontal (Yaw):** Mouse X rotates the body left/right
- **Vertical (Pitch):** Mouse Y rotates the head up/down

**Important:** Pitch (up/down) has limits (typically ±90°) to prevent flipping the camera upside-down.

**Implementation:**
- Rotate body with horizontal mouse movement
- Rotate camera with vertical mouse movement
- Clamp vertical rotation between -90° and +90°

**Cursor Lock:** Lock cursor to screen so it doesn't escape during gameplay. Use `Cursor.lockState = CursorLockMode.Locked`.

---

## Code Example

```csharp
using UnityEngine;

public class FPSController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float mouseSensitivity = 100f;
    public float maxPitch = 90f;

    private CharacterController controller;
    private Camera mainCam;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;
    private float yaw = 0f;
    private float pitch = 0f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        mainCam = Camera.main;
        
        // Lock cursor to game window
        Cursor.lockState = CursorLockMode.Locked;
    }

    private void Update()
    {
        HandleMouseLook();
        HandleMovement();
        HandleJump();
        ApplyGravity();
    }

    private void HandleMouseLook()
    {
        // Get mouse movement
        float mouseX = Input.GetAxis("Mouse X") * mouseSensitivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensitivity * Time.deltaTime;

        // Update angles
        yaw += mouseX;
        pitch -= mouseY; // Negative because mouse Y is inverted
        pitch = Mathf.Clamp(pitch, -maxPitch, maxPitch);

        // Apply rotation to body (yaw)
        transform.rotation = Quaternion.Euler(0, yaw, 0);

        // Apply rotation to camera (pitch)
        mainCam.transform.localRotation = Quaternion.Euler(pitch, 0, 0);
    }

    private void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        // Movement relative to camera facing direction
        Vector3 moveDir = transform.right * h + transform.forward * v;
        Vector3 motion = moveDir.normalized * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void HandleJump()
    {
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

1. **Create FPS Player**
   - Capsule (body) with CharacterController
   - Empty child object named "CameraHolder"
   - Main Camera as child of CameraHolder, positioned at head height

2. **Position Camera**
   - CameraHolder at `(0, 0.6, 0)` relative to player
   - Camera at `(0, 0, 0)` relative to CameraHolder
   - Camera rotates with mouse Y

3. **Attach FPSController Script**
   - Create C# script → "FPSController"
   - Attach to Player body
   - In Inspector, drag CameraHolder child into mainCam reference (or use Camera.main)

4. **Test**
   - Press Play
   - Move mouse to look around
   - WASD to move
   - Space to jump
   - Escape to unlock cursor (add code)

---

## Guided Practice

1. **Implement Horizontal Look** (10 min)
   - Read mouse X input
   - Rotate player body (yaw)
   - Test turning left/right

2. **Implement Vertical Look** (10 min)
   - Read mouse Y input
   - Rotate camera (pitch)
   - Clamp pitch to ±90°
   - Test looking up/down

3. **Add Movement Relative to Camera** (5 min)
   - WASD moves forward/backward/left/right relative to camera facing
   - Test strafing while aiming

---

## Practice Problems

**Beginner:** Implement basic mouse look (yaw only). Rotate the player to follow horizontal mouse movement.

**Intermediate:** Add **scope zoom**: press Z to zoom to 2x. When zoomed, reduce mouse sensitivity so aiming is precise. Use Camera.fieldOfView to zoom.

**Challenge:** Implement **head bobbing**: as the player walks, the camera gently bobs up/down and side-to-side. Intensity varies with movement speed. Use Sine waves.

<details><summary>💡 Hints</summary>
- Yaw rotates the player body; pitch rotates only the camera.
- Clamp pitch to prevent looking too far up/down.
- `Cursor.lockState = CursorLockMode.Locked` keeps cursor in window.
- Mouse sensitivity is typically 1–200; higher = snappier.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Scope Zoom):**
```csharp
private bool isScoped = false;
private float normalFOV = 60f;
private float scopedFOV = 20f;

void Update()
{
    if (Input.GetKeyDown(KeyCode.Z))
        isScoped = !isScoped;

    if (isScoped)
    {
        mainCam.fieldOfView = Mathf.Lerp(mainCam.fieldOfView, scopedFOV, Time.deltaTime * 5f);
        mouseSensitivity = 20f; // Reduced sensitivity when zoomed
    }
    else
    {
        mainCam.fieldOfView = Mathf.Lerp(mainCam.fieldOfView, normalFOV, Time.deltaTime * 5f);
        mouseSensitivity = 100f;
    }
}
```

**Challenge Solution (Head Bob):**
```csharp
private float bobSpeed = 5f;
private float bobAmount = 0.05f;

void Update()
{
    float moveSpeed = new Vector3(h, 0, v).magnitude;
    
    if (moveSpeed > 0)
    {
        float bobOffset = Mathf.Sin(Time.time * bobSpeed) * bobAmount;
        mainCam.transform.localPosition = new Vector3(0, 0.6f + bobOffset, 0);
    }
}
```

</details>
