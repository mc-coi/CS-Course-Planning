# Day 13: Player State Machine – Fundamentals

**Learning Target:** I can implement a state machine to manage player states (Idle, Walking, Jumping, Attacking).

---

## Key Concepts

**State Machine** — A system that manages discrete states and transitions between them. Games use state machines to organize behavior:
- **Idle:** Standing still
- **Walking:** Moving
- **Jumping:** Airborne
- **Attacking:** Playing attack animation

**Enum Pattern:**
```csharp
enum PlayerState { Idle, Walking, Jumping, Attacking }
```

**Switch Statement:** Handle different behavior based on current state:
```csharp
switch (currentState)
{
    case PlayerState.Idle: HandleIdleInput(); break;
    case PlayerState.Walking: HandleWalking(); break;
    case PlayerState.Jumping: HandleJumping(); break;
}
```

**Why State Machines?** Prevents messy `if (isJumping && isAttacking && isMoving)` logic. Each state handles its own behavior cleanly.

---

## Code Example

```csharp
using UnityEngine;

public class PlayerStateMachine : MonoBehaviour
{
    enum PlayerState { Idle, Walking, Jumping, Attacking }
    private PlayerState currentState = PlayerState.Idle;

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
        HandleInput();
        UpdateState();
        ApplyGravity();
    }

    private void HandleInput()
    {
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
            currentState = PlayerState.Jumping;
        
        if (Input.GetMouseButtonDown(0))
            currentState = PlayerState.Attacking;
    }

    private void UpdateState()
    {
        switch (currentState)
        {
            case PlayerState.Idle:
                UpdateIdle();
                break;
            case PlayerState.Walking:
                UpdateWalking();
                break;
            case PlayerState.Jumping:
                UpdateJumping();
                break;
            case PlayerState.Attacking:
                UpdateAttacking();
                break;
        }
    }

    private void UpdateIdle()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        if (h != 0 || v != 0)
            currentState = PlayerState.Walking;
    }

    private void UpdateWalking()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        if (h == 0 && v == 0)
            currentState = PlayerState.Idle;

        Vector3 moveDir = new Vector3(h, 0, v).normalized;
        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void UpdateJumping()
    {
        velocity.y = jumpForce;
        
        Vector3 motion = Vector3.zero;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);

        if (controller.isGrounded && velocity.y < 0)
            currentState = PlayerState.Idle;
    }

    private void UpdateAttacking()
    {
        Debug.Log("Attacking!");
        currentState = PlayerState.Idle; // Simplistic: attack lasts one frame
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

1. **Create Player**
   - Capsule with CharacterController

2. **Attach PlayerStateMachine Script**
   - Create C# script → "PlayerStateMachine"
   - Attach to Player

3. **Test State Transitions**
   - Press Play
   - Stand still → Idle
   - Move → Walking
   - Press Space → Jumping
   - Click → Attacking

4. **Add Debug Output**
   - In UpdateState(), add `Debug.Log(currentState)`
   - Watch console to verify state changes

---

## Guided Practice

1. **Create State Enum** (5 min)
   - Define enum with Idle, Walking, Jumping, Attacking
   - Create currentState variable

2. **Implement State Transitions** (10 min)
   - In HandleInput(), change state based on input
   - In UpdateState(), call appropriate handler for each state

3. **Test Transitions** (5 min)
   - Verify state changes work
   - Debug.Log each state change
   - Watch the console

---

## Practice Problems

**Beginner:** Create a state machine with Idle and Walking states. Transition based on input.

**Intermediate:** Add a **Dashing state**: press E to dash, move fast for 0.3 seconds, then return to Idle/Walking. Cannot dash while jumping.

**Challenge:** Implement **state stacking**: allow Jumping while Walking (you move horizontally while airborne). Implement proper transitions: Walking+Jump = Jumping+momentum.

<details><summary>💡 Hints</summary>
- Enums make state names readable and prevent typos.
- Each state should only handle its own logic.
- Transitions happen in HandleInput() or UpdateState().
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Dashing):**
```csharp
enum PlayerState { Idle, Walking, Jumping, Dashing, Attacking }
private float dashTimer = 0f;
private const float DASH_DURATION = 0.3f;

void HandleInput()
{
    if (Input.GetKeyDown(KeyCode.E) && (currentState == PlayerState.Idle || currentState == PlayerState.Walking))
    {
        currentState = PlayerState.Dashing;
        dashTimer = DASH_DURATION;
    }
}

void UpdateDashing()
{
    dashTimer -= Time.deltaTime;
    
    // Move fast forward
    Vector3 motion = transform.forward * moveSpeed * 2f;
    motion.y = velocity.y;
    controller.Move(motion * Time.deltaTime);
    
    if (dashTimer <= 0)
        currentState = PlayerState.Idle;
}
```

</details>
