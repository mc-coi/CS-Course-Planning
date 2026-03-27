# Day 18: FPS Controller – Advanced Features

**Learning Target:** I can extend FPS controls with sprinting, stamina, and weapon aiming.

---

## Key Concepts

**Sprint Mechanic** — Shift key to run faster, with limited stamina. When stamina depletes, walk speed is forced.

**Stamina System:**
- Sprint reduces stamina per second
- Walking slowly regenerates stamina
- Cannot sprint when stamina = 0

**Weapon Aiming** — Hip-fire vs. ADS (Aim Down Sights). When aiming, camera zooms and movement slows.

**Advanced Feedback:**
- Screen shake on heavy impact (footsteps)
- Crosshair changes on ADS
- Audio cues for stamina depletion

---

## Code Example

```csharp
using UnityEngine;

public class AdvancedFPSController : MonoBehaviour
{
    // Movement
    public float walkSpeed = 5f;
    public float sprintSpeed = 10f;
    public float mouseSensitivity = 100f;
    
    // Stamina
    public float maxStamina = 100f;
    public float staminaDrainPerSecond = 30f;
    public float staminaRegenPerSecond = 15f;
    private float currentStamina;
    
    // Aiming
    public float aimFOV = 30f;
    public float aimSpeed = 0.1f;
    private bool isAiming = false;
    private float normalFOV = 60f;

    private CharacterController controller;
    private Camera mainCam;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;
    private float pitch = 0f;
    private float yaw = 0f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        mainCam = Camera.main;
        currentStamina = maxStamina;
        normalFOV = mainCam.fieldOfView;
        Cursor.lockState = CursorLockMode.Locked;
    }

    private void Update()
    {
        HandleMouseLook();
        HandleMovement();
        HandleAiming();
        HandleJump();
        UpdateStamina();
        ApplyGravity();
    }

    private void HandleMouseLook()
    {
        float mouseX = Input.GetAxis("Mouse X") * mouseSensitivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensitivity * Time.deltaTime;

        yaw += mouseX;
        pitch -= mouseY;
        pitch = Mathf.Clamp(pitch, -90f, 90f);

        transform.rotation = Quaternion.Euler(0, yaw, 0);
        mainCam.transform.localRotation = Quaternion.Euler(pitch, 0, 0);
    }

    private void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        // Check if sprinting
        bool isSprinting = Input.GetKey(KeyCode.LeftShift) && currentStamina > 0;
        float currentSpeed = isSprinting ? sprintSpeed : walkSpeed;

        // Reduce speed while aiming
        if (isAiming)
            currentSpeed *= 0.5f;

        Vector3 moveDir = transform.right * h + transform.forward * v;
        Vector3 motion = moveDir.normalized * currentSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void HandleAiming()
    {
        if (Input.GetMouseButton(1)) // Right-click to aim
            isAiming = true;
        else
            isAiming = false;

        float targetFOV = isAiming ? aimFOV : normalFOV;
        mainCam.fieldOfView = Mathf.Lerp(mainCam.fieldOfView, targetFOV, aimSpeed);
    }

    private void HandleJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        {
            velocity.y = 5f;
        }
    }

    private void UpdateStamina()
    {
        bool isSprinting = Input.GetKey(KeyCode.LeftShift);

        if (isSprinting && currentStamina > 0)
        {
            currentStamina -= staminaDrainPerSecond * Time.deltaTime;
        }
        else
        {
            currentStamina += staminaRegenPerSecond * Time.deltaTime;
        }

        currentStamina = Mathf.Clamp(currentStamina, 0, maxStamina);
        Debug.Log($"Stamina: {currentStamina:F0}/{maxStamina}");
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

1. **Use FPSController from Day 17**

2. **Attach AdvancedFPSController Script**
   - Modify previous script or create new one
   - Set walkSpeed, sprintSpeed, stamina values in Inspector

3. **Create Stamina UI** (Optional)
   - Canvas → Panel (stamina bar)
   - Image component as fill
   - Update fill amount based on stamina percentage

4. **Test**
   - Walk normally
   - Hold Shift to sprint
   - Right-click to aim (zoom in, slow movement)
   - Watch stamina deplete and regenerate

---

## Guided Practice

1. **Implement Sprint** (10 min)
   - Add stamina system
   - Increase speed when Shift held
   - Drain stamina while sprinting
   - Regenerate when not sprinting

2. **Add Aiming** (10 min)
   - Right-click to aim
   - Zoom camera (FOV change)
   - Reduce movement speed while aiming

3. **Create Visual Feedback** (5 min)
   - Add stamina bar UI
   - Change crosshair appearance when aiming
   - Log stamina state

---

## Practice Problems

**Beginner:** Implement sprint with unlimited stamina. Shift = 2x speed.

**Intermediate:** Add **exhaustion state**: when stamina hits 0, movement speed is capped at walk speed for 2 seconds before regenerating.

**Challenge:** Implement **breath mechanics**: stamina depletes 2x faster if jumping while sprinting. Add audio cues when stamina low.

<details><summary>💡 Hints</summary>
- Stamina should regen faster than it drains (so players can recover).
- Sprint speed is typically 1.5–2x walk speed.
- Aiming should feel restrictive but not punishing.
</details>

<details><summary>✅ Sample Answers</summary>

**Challenge Solution (Breath + Audio):**
```csharp
private AudioSource breathingAudio;

void UpdateStamina()
{
    bool isSprinting = Input.GetKey(KeyCode.LeftShift);
    bool isJumping = !controller.isGrounded;
    
    float drainRate = isSprinting ? staminaDrainPerSecond : 0;
    if (isSprinting && isJumping)
        drainRate *= 2f; // Double drain while jump-sprinting
    
    if (isSprinting && currentStamina > 0)
        currentStamina -= drainRate * Time.deltaTime;
    else
        currentStamina += staminaRegenPerSecond * Time.deltaTime;
    
    currentStamina = Mathf.Clamp(currentStamina, 0, maxStamina);
    
    // Play breath sound if stamina low
    if (currentStamina < 20f && !breathingAudio.isPlaying)
        breathingAudio.PlayOneShot(breathingClip);
}
```

</details>
