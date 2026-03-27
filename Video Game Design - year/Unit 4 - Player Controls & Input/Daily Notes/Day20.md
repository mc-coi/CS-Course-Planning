# Day 20: Perspective-Agnostic Controllers & Camera-Relative Movement

**Learning Target:** I can build movement systems that automatically adjust to any camera angle or perspective.

---

## Key Concepts

**Camera-Relative Movement** — Move relative to camera facing direction, not world axes. Works for any camera angle (FPS, 3rd person, fixed angle).

**Implementation:**
- Read input
- Get camera forward/right vectors
- Apply movement in those directions
- Works for any camera type

**Benefits:**
- Same movement code for multiple camera perspectives
- Players expect movement relative to what they see
- Professional, polished feel

**Input Abstraction** — Decouple input system from movement system, allowing easy controller/UI switching.

---

## Code Example

```csharp
using UnityEngine;

public class CameraRelativeController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float gravity = 9.81f;
    
    private CharacterController controller;
    private Camera mainCam;
    private Vector3 velocity = Vector3.zero;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        mainCam = Camera.main;
    }

    private void Update()
    {
        HandleMovement();
        HandleJump();
        ApplyGravity();
    }

    private void HandleMovement()
    {
        // Read input
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        // Get camera directions
        Vector3 camForward = mainCam.transform.forward;
        Vector3 camRight = mainCam.transform.right;

        // Zero out vertical components (so we move on ground plane)
        camForward.y = 0;
        camRight.y = 0;
        camForward.Normalize();
        camRight.Normalize();

        // Calculate movement relative to camera
        Vector3 moveDir = (camRight * h + camForward * v).normalized;
        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;

        controller.Move(motion * Time.deltaTime);
    }

    private void HandleJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
            velocity.y = jumpForce;
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0)
            velocity.y = -2f;
        else
            velocity.y -= gravity * Time.deltaTime;
    }

    // Optional: Switch camera perspectives at runtime
    public void SwitchToTopDown()
    {
        mainCam.transform.position = transform.position + Vector3.up * 10f;
        mainCam.transform.LookAt(transform.position);
    }

    public void SwitchToThirdPerson()
    {
        mainCam.transform.position = transform.position + Vector3.back * 5f + Vector3.up * 2f;
        mainCam.transform.LookAt(transform.position + Vector3.up);
    }
}
```

---

## Unity Setup Steps

1. **Create Player with CharacterController**

2. **Create Multiple Camera Rigs** (Optional)
   - FPS camera (child of player, at head height)
   - 3rd person camera (separate, looking at player)
   - Top-down camera (above player)

3. **Attach CameraRelativeController Script**
   - Create C# script → "CameraRelativeController"
   - Script automatically uses Camera.main

4. **Test Different Perspectives**
   - Press Play with FPS camera
   - Test movement (should feel relative to camera)
   - Switch cameras and re-test
   - Movement should adapt automatically

5. **Add Perspective Switcher** (Optional)
   - Press 1 for FPS, 2 for 3rd person, 3 for top-down
   - Call SwitchToTopDown(), etc. based on input

---

## Guided Practice

1. **Understand Camera-Relative Movement** (10 min)
   - Get camera forward/right vectors
   - Zero out Y components
   - Apply movement in those directions

2. **Test With Multiple Cameras** (10 min)
   - Create 2–3 different camera positions
   - Switch between them
   - Verify movement feels correct in each perspective

3. **Add Perspective Switching** (5 min)
   - Press 1, 2, 3 to switch cameras
   - Movement automatically adapts
   - No code changes needed!

---

## Practice Problems

**Beginner:** Create camera-relative movement that works with any camera angle. Test with FPS, 3rd person, and top-down cameras.

**Intermediate:** Implement **smooth camera transition**: when switching perspectives, smoothly lerp between old and new camera positions/rotations.

**Challenge:** Create **context-sensitive input**: in tight corridors, rotate movement to push forward along corridor direction. On open ground, use camera-relative movement. (Hint: Use raycasts to detect corridor walls.)

<details><summary>💡 Hints</summary>
- Always normalize camera directions (especially after zeroing Y).
- A well-designed controller works with any camera without code changes.
- Context-sensitive input requires environment awareness (raycasts, colliders).
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Smooth Camera Transition):**
```csharp
private Camera activeCamera;
private Camera targetCamera;
private float cameraTransitionTime = 0.5f;
private float cameraTransitionTimer = 0f;

void Update()
{
    // Camera transition
    if (cameraTransitionTimer < cameraTransitionTime)
    {
        float t = cameraTransitionTimer / cameraTransitionTime;
        
        activeCamera.transform.position = Vector3.Lerp(
            activeCamera.transform.position,
            targetCamera.transform.position,
            t
        );
        activeCamera.transform.rotation = Quaternion.Lerp(
            activeCamera.transform.rotation,
            targetCamera.transform.rotation,
            t
        );
        
        cameraTransitionTimer += Time.deltaTime;
    }
}

public void SwitchCamera(Camera newCam)
{
    targetCamera = newCam;
    cameraTransitionTimer = 0f;
}
```

</details>
