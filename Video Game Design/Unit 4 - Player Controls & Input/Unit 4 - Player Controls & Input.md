# Unit 4: Player Controls & Input

## Unit Overview

**Duration:** Days 13-16 (4 days)
**Key Concepts:** Advanced input handling, smooth camera follow, game feel and juice, state machines, code organization
**Big Idea:** Great games feel responsive and satisfying. Smooth input, responsive feedback, and polished game feel come from careful control design, camera work, particle effects, and audio.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Use Input.GetAxis() for smooth, analog input
- [ ] Understand the Input Manager and configure axes
- [ ] Implement smooth camera following using Vector3.Lerp()
- [ ] Use LateUpdate() to position the camera after character movement
- [ ] Implement look-at functionality with transform.LookAt()
- [ ] Add particle effects for visual feedback
- [ ] Implement screen shake for impact feedback
- [ ] Add audio feedback with AudioSource
- [ ] Design a basic state machine for character states
- [ ] Organize code into modular, reusable components

---

## Day-by-Day Content

### Day 13: Input.GetAxis() & Smooth Input

#### Key Concepts
- **Input.GetAxis():** Returns a float from -1 to 1 (smooth analog input)
- **Input.GetAxisRaw():** Returns -1, 0, or 1 (discrete digital input)
- **Input Manager:** Configuration panel for defining axes (horizontal, vertical, etc.)
- **Acceleration:** Axis builds up smoothly from 0 (good for movement)
- **Dead Zone:** Small threshold before input is registered (prevents controller drift)
- **Sensitivity:** Speed at which axis reaches maximum value

#### Content
GetAxis() is superior to GetKey() for continuous movement. Instead of instant on/off, it provides smooth ramping from 0 to 1. This feels much better for player movement.

**GetAxis vs GetKey:**
```
GetKey(KeyCode.D)          // Returns true or false (instant)
GetAxis("Horizontal")      // Returns -1, -0.5, 0, 0.5, 1 (smooth)
```

**Input Manager Setup:**
1. Edit > Project Settings > Input Manager
2. View the predefined axes: "Horizontal", "Vertical"
3. Horizontal is mapped to: A/D keys and Left Stick (controller)
4. Vertical is mapped to: W/S keys and Left Stick (controller)

GetAxis() automatically returns smooth values for both keyboard and controller, making your game feel responsive and natural.

#### Annotated Code Example

```csharp
using UnityEngine;

public class SmoothMovementController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float acceleration = 1f;
    public float deceleration = 2f;

    private Rigidbody rb;
    private Vector3 currentVelocity = Vector3.zero;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Get smooth input from -1 to 1
        float horizontal = Input.GetAxis("Horizontal");  // A/D or Left Stick
        float vertical = Input.GetAxis("Vertical");      // W/S or Left Stick

        // Build desired velocity
        Vector3 desiredVelocity = new Vector3(horizontal, 0, vertical).normalized * moveSpeed;

        // Smoothly interpolate toward desired velocity
        currentVelocity = Vector3.Lerp(currentVelocity, desiredVelocity, Time.deltaTime * acceleration);

        Debug.Log("Input: (" + horizontal + ", " + vertical + ")");
    }

    void FixedUpdate()
    {
        // Apply the smoothed velocity
        rb.velocity = new Vector3(currentVelocity.x, rb.velocity.y, currentVelocity.z);
    }

    // Method to create custom axes in Input Manager
    // This is usually done in Edit > Project Settings > Input Manager
}
```

---

### Day 14: Camera Follow & LateUpdate()

#### Key Concepts
- **LateUpdate():** Called after all Update() methods; perfect for camera logic
- **Vector3.Lerp():** Linear interpolation between two vectors (smooth transitions)
- **transform.LookAt():** Rotates an object to face another object
- **Offset:** Distance between camera and target (usually behind and above)
- **Damping:** Smoothness factor for camera following (0-1; higher = smoother)
- **Clipping Planes:** Near and Far planes determining what the camera renders

#### Content
Cameras should update AFTER the player moves. LateUpdate() is called after all Update() methods, making it perfect for camera logic.

**Camera Following Pattern:**
```csharp
void LateUpdate()
{
    // Player has moved in Update()
    // Now move the camera to follow the player
    Vector3 targetPosition = player.position + offset;
    transform.position = Vector3.Lerp(transform.position, targetPosition, dampingSpeed);
}
```

**Vector3.Lerp():**
Lerp stands for "linear interpolation." It smoothly transitions from one vector to another.
```
Vector3.Lerp(a, b, t)
```
- t = 0: returns a
- t = 0.5: returns midpoint
- t = 1: returns b
- t > 1: overshoots beyond b

For camera damping, use a small value like 0.1f or 0.2f to create smooth, non-jarring camera movement.

#### Annotated Code Example

```csharp
using UnityEngine;

public class SmoothCameraFollow : MonoBehaviour
{
    public Transform target;  // The player to follow
    public Vector3 offset = new Vector3(0, 2, -5);  // Camera distance from player
    public float dampingSpeed = 0.1f;  // Lower = smoother but laggier
    public bool lookAtPlayer = true;

    void LateUpdate()
    {
        if (target == null)
        {
            Debug.LogError("Camera target is not assigned!");
            return;
        }

        // Calculate the desired camera position
        Vector3 desiredPosition = target.position + offset;

        // Smoothly move the camera toward the desired position
        transform.position = Vector3.Lerp(transform.position, desiredPosition, dampingSpeed);

        // Optional: Make the camera look at the player
        if (lookAtPlayer)
        {
            transform.LookAt(target);
        }
    }
}
```

```csharp
using UnityEngine;

public class FirstPersonCamera : MonoBehaviour
{
    public Transform player;
    public float mouseSensitivity = 100f;
    public float verticalRotationSpeed = 2f;

    private float xRotation = 0f;

    void LateUpdate()
    {
        // Get mouse input
        float mouseX = Input.GetAxis("Mouse X") * mouseSensitivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensitivity * Time.deltaTime;

        // Rotate player left/right (horizontal)
        player.Rotate(Vector3.up * mouseX);

        // Rotate camera up/down (vertical, clamped)
        xRotation -= mouseY;
        xRotation = Mathf.Clamp(xRotation, -90f, 90f);
        transform.localRotation = Quaternion.Euler(xRotation, 0f, 0f);

        // Position camera at player's head
        transform.position = player.position + Vector3.up * 0.6f;
    }
}
```

---

### Day 15: Game Feel, Juice & Feedback

#### Key Concepts
- **Game Feel:** The responsiveness and satisfaction players feel when interacting with the game
- **Juice:** Visual and audio feedback that makes gameplay more satisfying
- **Particle Effects:** Visual particles for impact, explosions, or effects
- **Screen Shake:** Camera movement that creates impact feedback
- **Audio Feedback:** Sounds for actions (jump, land, collect, impact)
- **Screenshake Strength:** How intense and how long the shake lasts
- **Feedback Loop:** The relationship between player input and game response

#### Content
Game feel is the difference between a game that feels satisfying and one that feels dead. It comes from multiple sources:

1. **Visual Feedback:** Particle effects, animations, color changes
2. **Audio Feedback:** Sound effects, music, volume changes
3. **Physical Feedback:** Screen shake, controller rumble
4. **Responsive Controls:** No input lag, immediate response

"Juice" refers to extra polish that makes games feel alive. A jump with a particle effect, sound, and screen shake feels much better than a silent jump.

#### Annotated Code Example

```csharp
using UnityEngine;

public class JuicyGameFeels : MonoBehaviour
{
    public ParticleSystem jumpEffect;
    public AudioSource jumpSound;
    public float screenShakeStrength = 0.1f;
    public float screenShakeDuration = 0.2f;

    private Camera mainCamera;
    private float shakeTimer = 0f;
    private Vector3 originalCameraPosition;

    void Start()
    {
        mainCamera = Camera.main;
        originalCameraPosition = mainCamera.transform.position;
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }

        // Update screen shake
        if (shakeTimer > 0)
        {
            shakeTimer -= Time.deltaTime;
            Vector3 randomShake = Random.insideUnitSphere * screenShakeStrength;
            mainCamera.transform.position = originalCameraPosition + randomShake;
        }
        else
        {
            mainCamera.transform.position = originalCameraPosition;
        }
    }

    void Jump()
    {
        Debug.Log("Jumped with juice!");

        // Play particle effect at jump location
        if (jumpEffect != null)
        {
            Instantiate(jumpEffect, transform.position, Quaternion.identity);
        }

        // Play sound effect
        if (jumpSound != null)
        {
            jumpSound.PlayOneShot(jumpSound.clip);
        }

        // Apply screen shake
        StartScreenShake();

        // Physics
        GetComponent<Rigidbody>().AddForce(Vector3.up * 5f, ForceMode.Impulse);
    }

    void StartScreenShake()
    {
        shakeTimer = screenShakeDuration;
    }
}
```

```csharp
using UnityEngine;

public class CollectionFeedback : MonoBehaviour
{
    public ParticleSystem collectEffect;
    public AudioClip collectSound;
    public float popScale = 1.2f;  // How large the collected item becomes

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Collectible"))
        {
            // Particle effect
            if (collectEffect != null)
            {
                Instantiate(collectEffect, transform.position, Quaternion.identity);
            }

            // Sound effect
            if (collectSound != null)
            {
                AudioSource.PlayClipAtPoint(collectSound, transform.position);
            }

            // Visual pop (scale up briefly)
            StartCoroutine(PopAndDestroy(other.gameObject));
        }
    }

    System.Collections.IEnumerator PopAndDestroy(GameObject obj)
    {
        Vector3 originalScale = obj.transform.localScale;
        obj.transform.localScale = originalScale * popScale;
        yield return new WaitForSeconds(0.1f);
        Destroy(obj);
    }
}
```

---

### Day 16: State Machines & Code Organization

#### Key Concepts
- **State Machine:** A system that manages different states and transitions
- **Enum:** An enumeration type listing possible states (Idle, Running, Jumping, Falling)
- **State Transitions:** Rules defining when to switch from one state to another
- **Modular Code:** Breaking code into smaller, reusable components
- **Separation of Concerns:** Each script handles one thing (Input, Movement, Camera, etc.)
- **GetComponent Caching:** Storing references to components for efficiency

#### Content
As games grow more complex, organizing code becomes critical. A **state machine** is a common pattern:

```csharp
enum PlayerState { Idle, Running, Jumping, Falling }
PlayerState currentState = PlayerState.Idle;

void Update()
{
    switch (currentState)
    {
        case PlayerState.Idle:
            // Handle idle logic
            if (inputMagnitude > 0) currentState = PlayerState.Running;
            break;

        case PlayerState.Running:
            // Handle running logic
            if (inputMagnitude == 0) currentState = PlayerState.Idle;
            if (isJumping) currentState = PlayerState.Jumping;
            break;

        case PlayerState.Jumping:
            // Handle jumping logic
            if (velocity.y < 0) currentState = PlayerState.Falling;
            break;

        case PlayerState.Falling:
            // Handle falling logic
            if (isGrounded) currentState = PlayerState.Idle;
            break;
    }
}
```

**Code Organization:**
Instead of one massive script, create multiple smaller scripts:
- `PlayerInput.cs` – Handles input
- `PlayerMovement.cs` – Handles physics and movement
- `PlayerAnimator.cs` – Handles animations
- `CameraController.cs` – Handles camera
- `GameManager.cs` – Handles game state

Each script does one thing, making code easier to debug and reuse.

#### Annotated Code Example

```csharp
using UnityEngine;

public enum PlayerState
{
    Idle,
    Running,
    Jumping,
    Falling,
    Dead
}

public class PlayerController : MonoBehaviour
{
    [Header("Movement")]
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float groundDrag = 5f;
    public float airDrag = 1f;
    public float groundDistance = 0.2f;

    [Header("References")]
    private Rigidbody rb;
    private PlayerState currentState = PlayerState.Idle;
    private PlayerAnimator animator;
    private AudioSource audioSource;

    private bool isGrounded = false;
    private Vector3 moveInput = Vector3.zero;

    void Start()
    {
        // Cache all components
        rb = GetComponent<Rigidbody>();
        animator = GetComponent<PlayerAnimator>();
        audioSource = GetComponent<AudioSource>();

        if (rb == null) Debug.LogError("Rigidbody not found!");
    }

    void Update()
    {
        // Check ground state
        UpdateGroundState();

        // Get input
        UpdateInput();

        // State machine
        UpdateState();
    }

    void FixedUpdate()
    {
        // Apply movement based on current state
        if (currentState != PlayerState.Dead)
        {
            ApplyMovement();
            ApplyDrag();
        }
    }

    void UpdateGroundState()
    {
        RaycastHit hit;
        isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);
    }

    void UpdateInput()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        moveInput = new Vector3(horizontal, 0, vertical).normalized;
    }

    void UpdateState()
    {
        switch (currentState)
        {
            case PlayerState.Idle:
                HandleIdleState();
                break;
            case PlayerState.Running:
                HandleRunningState();
                break;
            case PlayerState.Jumping:
                HandleJumpingState();
                break;
            case PlayerState.Falling:
                HandleFallingState();
                break;
            case PlayerState.Dead:
                HandleDeadState();
                break;
        }

        // Update animator with current state
        if (animator != null)
        {
            animator.SetState(currentState);
        }
    }

    void HandleIdleState()
    {
        if (moveInput.magnitude > 0.1f)
        {
            currentState = PlayerState.Running;
        }

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            currentState = PlayerState.Jumping;
        }
    }

    void HandleRunningState()
    {
        if (moveInput.magnitude < 0.1f)
        {
            currentState = PlayerState.Idle;
        }

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            currentState = PlayerState.Jumping;
        }

        if (!isGrounded)
        {
            currentState = PlayerState.Falling;
        }
    }

    void HandleJumpingState()
    {
        if (rb.velocity.y < 0)
        {
            currentState = PlayerState.Falling;
        }
    }

    void HandleFallingState()
    {
        if (isGrounded)
        {
            currentState = PlayerState.Idle;
        }
    }

    void HandleDeadState()
    {
        // Do nothing; character is dead
    }

    void ApplyMovement()
    {
        Vector3 targetVelocity = moveInput * moveSpeed;
        rb.velocity = new Vector3(targetVelocity.x, rb.velocity.y, targetVelocity.z);
    }

    void ApplyDrag()
    {
        rb.drag = isGrounded ? groundDrag : airDrag;
    }

    public void Jump()
    {
        if (isGrounded)
        {
            rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);

            if (audioSource != null)
            {
                audioSource.Play();
            }

            currentState = PlayerState.Jumping;
        }
    }

    public void TakeDamage(int damage)
    {
        currentState = PlayerState.Dead;
        Debug.Log("Player took damage!");
        Destroy(gameObject);
    }
}
```

```csharp
using UnityEngine;

public class PlayerAnimator : MonoBehaviour
{
    private Animator animator;

    void Start()
    {
        animator = GetComponent<Animator>();
    }

    public void SetState(PlayerState state)
    {
        // Convert state to animation parameter
        animator.SetInteger("State", (int)state);
    }
}
```

---

## Practice Problems

### Beginner Tier

**Problem 1:** Set up smooth movement using Input.GetAxis("Horizontal") and Input.GetAxis("Vertical").

<details>
<summary>Hint</summary>
Use GetAxis() instead of GetKey(). GetAxis() returns smooth values from -1 to 1.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class SmoothMovement : MonoBehaviour
{
    public float moveSpeed = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        Vector3 moveDirection = new Vector3(horizontal, 0, vertical);
        rb.velocity = new Vector3(moveDirection.x * moveSpeed, rb.velocity.y, moveDirection.z * moveSpeed);
    }
}
```
</details>

---

**Problem 2:** Implement a simple camera follow that updates in LateUpdate().

<details>
<summary>Hint</summary>
Use LateUpdate() so the camera moves after the player. Use Vector3.Lerp() for smooth following.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform target;
    public Vector3 offset = new Vector3(0, 2, -5);
    public float damping = 0.1f;

    void LateUpdate()
    {
        Vector3 desiredPos = target.position + offset;
        transform.position = Vector3.Lerp(transform.position, desiredPos, damping);
    }
}
```
</details>

---

**Problem 3:** Create a script that plays a sound when the player jumps.

<details>
<summary>Hint</summary>
Get the AudioSource component. Use PlayOneShot() to play a single sound without stopping other audio.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class JumpSound : MonoBehaviour
{
    public AudioClip jumpClip;
    private AudioSource audioSource;

    void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            audioSource.PlayOneShot(jumpClip);
        }
    }
}
```
</details>

---

### Intermediate Tier

**Problem 4:** Implement a state machine with at least three states (Idle, Running, Jumping). Transitions should be smooth and based on input.

<details>
<summary>Hint</summary>
Use an enum for states. In Update(), use a switch statement to handle each state's logic and transitions.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public enum State { Idle, Running, Jumping }

public class StateMachine : MonoBehaviour
{
    private State currentState = State.Idle;
    private Rigidbody rb;
    private bool isGrounded = true;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        float input = Input.GetAxis("Horizontal");
        bool jumping = Input.GetKeyDown(KeyCode.Space);

        switch (currentState)
        {
            case State.Idle:
                if (input != 0)
                    currentState = State.Running;
                if (jumping)
                    currentState = State.Jumping;
                break;

            case State.Running:
                if (input == 0)
                    currentState = State.Idle;
                if (jumping)
                    currentState = State.Jumping;
                break;

            case State.Jumping:
                if (isGrounded)
                    currentState = State.Idle;
                break;
        }

        Debug.Log("State: " + currentState);
    }
}
```
</details>

---

**Problem 5:** Add a screen shake effect that triggers when the player jumps.

<details>
<summary>Hint</summary>
Store the original camera position. In a timer, apply random offsets to the camera position, then restore it.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class ScreenShake : MonoBehaviour
{
    private Camera cam;
    private Vector3 originalPos;
    private float shakeTimer = 0f;
    public float shakeStrength = 0.1f;

    void Start()
    {
        cam = Camera.main;
        originalPos = cam.transform.position;
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            shakeTimer = 0.2f;
        }

        if (shakeTimer > 0)
        {
            shakeTimer -= Time.deltaTime;
            Vector3 shake = Random.insideUnitSphere * shakeStrength;
            cam.transform.position = originalPos + shake;
        }
        else
        {
            cam.transform.position = originalPos;
        }
    }
}
```
</details>

---

**Problem 6:** Create a complete player controller with smooth movement, camera follow, and multiple states.

<details>
<summary>Hint</summary>
Combine smooth movement (GetAxis), camera follow (LateUpdate, Lerp), and states. Use FixedUpdate for physics.
</details>

<details>
<summary>Answer</summary>
See the annotated code example in Day 16 (PlayerController.cs).
</details>

---

### Challenge Tier

**Problem 7:** Implement a complete player control system with state machine, camera follow, particle effects on jump, and audio feedback.

<details>
<summary>Hint</summary>
Use the state machine from earlier. Add Instantiate() for particle effects and audioSource.PlayOneShot() for sounds. Use LateUpdate() for camera.
</details>

<details>
<summary>Answer</summary>
Combine the code examples from Days 14, 15, and 16. Add particle and audio references, and trigger them in Jump() and other state changes.
</details>

---

**Problem 8:** Design and implement a game feel enhancement system. Add at least three types of feedback (visual, audio, physical) to different player actions.

<details>
<summary>Hint</summary>
Think about: landing (particles, sound, screen shake), jumping (particles, sound, feedback), collecting items (pop animation, sound), taking damage (red flash, sound, shake).
</details>

<details>
<summary>Answer</summary>
This is an open-ended design task. Create multiple feedback systems and wire them together. Document why each feedback type improves game feel.
</details>

---

## Practice Bank (15 Problems)

1. **Input Axis Exploration:** Open the Input Manager and examine the predefined axes. Create a custom axis and test it.

2. **Lerp Visualization:** Create three GameObjects that move toward a target using Lerp with different damping values. Observe the difference in speed.

3. **Camera Offset Varieties:** Implement camera follow with different offset values (behind, above, to the side) and compare feels.

4. **LookAt Target:** Create a script that makes an object always look at the player using transform.LookAt().

5. **Vector3.Lerp Practice:** Use Lerp to smoothly transition a color from red to blue over 5 seconds.

6. **Audio Volume Control:** Create a script that gradually fades audio in/out using Lerp.

7. **Particle Effect Timing:** Create a particle effect that plays when the player lands, with exact timing.

8. **Controller Support:** Test your input system with a game controller. Does GetAxis work correctly?

9. **Multi-State Transitions:** Design a state machine with 5+ states and clear transition rules.

10. **Code Modularization:** Refactor a large script into multiple smaller, focused scripts.

11. **Enum Practice:** Create an enum for different power-up types and use it to manage pickup behavior.

12. **Switch Statement Optimization:** Rewrite multiple if/else statements using a switch statement for clarity.

13. **GetComponent Caching:** Measure performance difference between caching GetComponent vs. calling it every frame.

14. **Coroutine Timing:** Use coroutines to create delayed feedback (e.g., play sound after 0.5 seconds).

15. **Game Feel Polish:** Take a basic game mechanic and add 5+ game feel enhancements (particles, sounds, screen shake, etc.).

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Camera movement is jerky | Using Update() instead of LateUpdate() | Always update camera in LateUpdate(), after player has moved |
| GetAxis() doesn't work | Wrong axis name (case-sensitive) | Check Input Manager for exact names: "Horizontal", "Vertical" |
| Particle effects don't show | Particle system set to stopped or duration = 0 | Set autoplay = true; duration > 0 |
| Audio doesn't play | AudioSource missing or volume = 0 | Add AudioSource component; check volume slider |
| State machine behavior is erratic | Transitions happen every frame instead of once | Use conditions that persist, or use GetKeyDown() for one-time events |
| Camera clips through objects | Near plane too large or far plane too small | Adjust camera's Near and Far planes in Inspector |
| Smooth movement overshoots | Damping value too high (> 0.3) | Keep Lerp damping between 0.05 and 0.2 for smooth follow |
| Multiple updates to same component | Code spread across multiple scripts fighting each other | Consolidate or use a single source of truth |
| Input not responsive | Reading input in FixedUpdate | Always read input in Update(), then apply in FixedUpdate() |
| Screen shake is continuous | Shake timer doesn't reset properly | Reset timer = 0 after shake ends |

---

## Assessment Prep: 10 Q&As

**Q1: What is the difference between Update() and LateUpdate()?**
A: Update() is called once per frame. LateUpdate() is called after all Update() methods. Use LateUpdate() for camera follow so the player moves first.

**Q2: Explain how Vector3.Lerp() works.**
A: Lerp(a, b, t) smoothly transitions from a to b. t=0 returns a, t=1 returns b, t=0.5 returns halfway point. Useful for smooth movement and damping.

**Q3: What is the difference between GetAxis() and GetKey()?**
A: GetAxis() returns smooth values from -1 to 1 (good for movement). GetKey() returns true/false (good for instant actions like jumping).

**Q4: How do you set up a state machine and why is it useful?**
A: Use an enum for states and a switch statement to handle each state's logic. State machines organize complex behavior and make transitions clear.

**Q5: What is "game feel" and why does it matter?**
A: Game feel is the responsiveness and satisfaction players feel. It comes from smooth controls, visual feedback, audio, and polish. Great game feel makes games feel alive.

**Q6: How do you play a sound effect with an AudioSource?**
A: Use `audioSource.PlayOneShot(audioClip);` to play a one-time sound without interrupting other audio.

**Q7: Explain the purpose of screen shake and how to implement it.**
A: Screen shake adds impact to actions (jumping, explosions, impacts). Apply random offsets to the camera for a short time, then restore it.

**Q8: What is caching a component, and why is it important?**
A: Caching is storing a component reference (e.g., in Start()). It's faster than GetComponent() every frame, improving performance.

**Q9: How do you create a particle effect when the player collects an item?**
A: Use `Instantiate(particleEffect, collectionPoint, Quaternion.identity);` to spawn the effect at the correct position.

**Q10: What is the relationship between game feel and player retention?**
A: Great game feel makes games more satisfying and addictive. Players keep playing when actions feel responsive. Poor game feel drives players away.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **GetAxis()** | Returns smooth float input from -1 to 1 |
| **GetAxisRaw()** | Returns -1, 0, or 1 (no smoothing) |
| **Input Manager** | Configuration panel for input axes |
| **LateUpdate()** | Called after Update(); perfect for camera |
| **Vector3.Lerp()** | Smooth interpolation between two vectors |
| **Damping** | Smoothness factor for following (0-1) |
| **Game Feel** | Responsiveness and satisfaction of interaction |
| **Juice** | Polish and feedback that enhances feel |
| **State Machine** | System for managing and transitioning between states |
| **Enum** | Type listing possible states or values |
| **Modular** | Code organized into focused, reusable components |
| **Particle Effect** | Visual effect made of many small particles |
| **Screen Shake** | Camera movement simulating impact |

### Input Quick Reference

```csharp
// Smooth axis input (0 to 1 range, accelerates)
float horizontal = Input.GetAxis("Horizontal");     // A/D, Left Stick
float vertical = Input.GetAxis("Vertical");         // W/S, Left Stick
float mouseX = Input.GetAxis("Mouse X");            // Mouse X movement
float mouseY = Input.GetAxis("Mouse Y");            // Mouse Y movement

// Raw axis (instant -1/0/1)
float hRaw = Input.GetAxisRaw("Horizontal");

// Discrete input
if (Input.GetKeyDown(KeyCode.Space))    // Pressed this frame
if (Input.GetKey(KeyCode.Space))        // Held down
if (Input.GetKeyUp(KeyCode.Space))      // Released this frame

// Mouse
if (Input.GetMouseButtonDown(0))        // Left click
if (Input.GetMouseButton(1))            // Right hold
```

### Camera & Lerp Quick Reference

```csharp
// Smooth camera follow
void LateUpdate()
{
    Vector3 targetPos = player.position + offset;
    transform.position = Vector3.Lerp(transform.position, targetPos, dampingSpeed);
}

// Look at target
transform.LookAt(target);

// Smooth color transition
Color targetColor = Color.blue;
renderer.material.color = Color.Lerp(renderer.material.color, targetColor, Time.deltaTime);

// Smooth value interpolation
currentValue = Mathf.Lerp(currentValue, targetValue, dampingSpeed);
```

### State Machine Quick Reference

```csharp
public enum PlayerState { Idle, Running, Jumping, Falling }
private PlayerState currentState = PlayerState.Idle;

void Update()
{
    switch (currentState)
    {
        case PlayerState.Idle:
            // Idle logic
            if (hasInput) currentState = PlayerState.Running;
            break;

        case PlayerState.Running:
            // Running logic
            if (!hasInput) currentState = PlayerState.Idle;
            break;

        // ... more states
    }
}
```

### Game Feel Quick Reference

```csharp
// Play particle effect
Instantiate(particles, transform.position, Quaternion.identity);

// Play sound
audioSource.PlayOneShot(jumpClip);

// Screen shake
StartCoroutine(ShakeScreen(duration, strength));

// Visual feedback (scaling)
StartCoroutine(PopAnimation(gameObject, targetScale, duration));

// Color feedback
renderer.material.color = Color.red;
Invoke("ResetColor", 0.2f);
```

---

## Additional Resources

- **Input Manager Settings:** Edit > Project Settings > Input Manager
- **Lerp Documentation:** https://docs.unity3d.com/ScriptReference/Vector3.Lerp.html
- **Game Feel Design:** https://www.youtube.com/watch?v=AJR0cqGbR6w (GDC talk on game feel)

