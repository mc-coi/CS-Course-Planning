# Day 16: State Machines & Code Organization

**Learning Target:** Organize complex behavior using state machines and modular code design.

### Key Concepts

- **State Machine:** A system that manages different states and transitions
- **Enum:** An enumeration type listing possible states (Idle, Running, Jumping, Falling)
- **State Transitions:** Rules defining when to switch from one state to another
- **Modular Code:** Breaking code into smaller, reusable components
- **Separation of Concerns:** Each script handles one thing (Input, Movement, Camera, etc.)
- **GetComponent Caching:** Storing references to components for efficiency

### Content

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

### Code Examples

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

### Guided Practice

1. Create a player character with a Rigidbody
2. Create the PlayerController script with the state machine
3. Implement all five states (Idle, Running, Jumping, Falling, Dead)
4. Test state transitions by moving, jumping, and checking the Console for state changes
5. Add a camera follow that works with the state machine
6. Add particle effects that trigger on state changes (landing, jumping)
7. Create a separate script for camera control to demonstrate modular design

### Practice Problems

**Problem 1 — Beginner:** Implement a state machine with at least three states (Idle, Running, Jumping).

**Problem 2 — Intermediate:** Create a complete player controller with state machine, smooth movement, camera follow, and multiple states.

**Problem 3 — Challenge:** Design and implement a game feel enhancement system with visual, audio, and physical feedback tied to state transitions.

<details>
<summary>Hints</summary>

**Hint 1:** Use an enum for states. In Update(), use a switch statement to handle each state's logic.

**Hint 2:** Store references to components in Start() (caching). This is faster than GetComponent() every frame.

**Hint 3:** Keep state transitions simple and clear. Each state should only transition based on specific conditions.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
public enum State { Idle, Running, Jumping }

void Update()
{
    float input = Input.GetAxis("Horizontal");

    switch (currentState)
    {
        case State.Idle:
            if (input != 0) currentState = State.Running;
            break;
        case State.Running:
            if (input == 0) currentState = State.Idle;
            break;
    }
}
```

**Answer 2:** See the annotated code example above (PlayerController.cs).

**Answer 3:** Add particle effects and sounds to state transition methods. Trigger them when entering/exiting states.

</details>
