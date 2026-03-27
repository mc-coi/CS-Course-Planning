# Day 14: State Machine – Advanced Patterns

**Learning Target:** I can build scalable state machines using scriptable objects and base classes.

---

## Key Concepts

**Base State Class Pattern** — Instead of one massive switch statement, create a base class for states. Each state inherits and overrides methods:
- `OnEnter()` — Called when entering state (setup)
- `Update()` — Called every frame while in state
- `OnExit()` — Called when leaving state (cleanup)

**Advantages:**
- Each state is its own file (clean)
- Easy to add new states
- Reusable across projects
- Extensible behavior

**Manager Pattern** — A StateMachine script holds references to all states and handles transitions. Cleaner than inline enums.

---

## Code Example

```csharp
using UnityEngine;

// Base class for all states
public abstract class PlayerState : MonoBehaviour
{
    protected PlayerStateMachine stateMachine;
    protected CharacterController controller;

    public virtual void Initialize(PlayerStateMachine sm, CharacterController cc)
    {
        stateMachine = sm;
        controller = cc;
    }

    public virtual void OnEnter() { }
    public virtual void Update() { }
    public virtual void OnExit() { }
}

// Example: Idle State
public class IdleState : PlayerState
{
    public float idleTimeout = 3f;
    private float idleTimer = 0f;

    public override void OnEnter()
    {
        Debug.Log("Entering Idle");
        idleTimer = 0f;
    }

    public override void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        if (h != 0 || v != 0)
            stateMachine.ChangeState(stateMachine.walkingState);

        if (Input.GetKeyDown(KeyCode.Space))
            stateMachine.ChangeState(stateMachine.jumpingState);
    }

    public override void OnExit()
    {
        Debug.Log("Exiting Idle");
    }
}

// Example: Walking State
public class WalkingState : PlayerState
{
    public float moveSpeed = 5f;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;

    public override void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        if (h == 0 && v == 0)
            stateMachine.ChangeState(stateMachine.idleState);

        Vector3 moveDir = new Vector3(h, 0, v).normalized;
        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }
}

// Manager
public class PlayerStateMachine : MonoBehaviour
{
    public IdleState idleState;
    public WalkingState walkingState;
    public JumpingState jumpingState;
    
    private PlayerState currentState;
    private CharacterController controller;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        
        // Initialize all states
        idleState.Initialize(this, controller);
        walkingState.Initialize(this, controller);
        jumpingState.Initialize(this, controller);
        
        ChangeState(idleState);
    }

    private void Update()
    {
        currentState.Update();
    }

    public void ChangeState(PlayerState newState)
    {
        currentState.OnExit();
        currentState = newState;
        currentState.OnEnter();
        Debug.Log($"State changed to {currentState.GetType().Name}");
    }
}
```

---

## Unity Setup Steps

1. **Create Player with CharacterController**

2. **Create State Scripts**
   - C# Script → "PlayerState.cs" (base class)
   - C# Script → "IdleState.cs"
   - C# Script → "WalkingState.cs"
   - C# Script → "JumpingState.cs"

3. **Create StateMachine Script**
   - C# Script → "PlayerStateMachine.cs"
   - Attach to Player

4. **Wire Up in Inspector**
   - In PlayerStateMachine, drag IdleState, WalkingState, JumpingState objects
   - (Or instantiate them in code)

5. **Test**
   - Press Play
   - Watch state transitions in console

---

## Guided Practice

1. **Create Base State Class** (10 min)
   - Define abstract methods: OnEnter, Update, OnExit
   - Create virtual Initialize method

2. **Create Concrete States** (10 min)
   - Inherit from PlayerState
   - Implement Update() for each state
   - Add state-specific logic

3. **Create StateMachine Manager** (5 min)
   - Hold references to all states
   - Implement ChangeState() method
   - Call state methods in Update loop

---

## Practice Problems

**Beginner:** Create Idle and Walking states with proper transitions. Extend the base PlayerState class.

**Intermediate:** Add a **Dodging state**: press Shift to dodge roll in the current direction. Lock input during dodge (0.5s), then return to previous state.

**Challenge:** Implement **state history**: remember the previous state so Jumping can return to either Idle or Walking after landing.

<details><summary>💡 Hints</summary>
- Use abstract methods in base class to enforce implementation in derived classes.
- OnEnter/OnExit are perfect for setup/cleanup (animations, timers, etc.).
- StateMachine.ChangeState() calls OnExit on old state and OnEnter on new state.
</details>

<details><summary>✅ Sample Answers</summary>

**Challenge Solution (State History):**
```csharp
public class PlayerStateMachine : MonoBehaviour
{
    private PlayerState currentState;
    private PlayerState previousState;

    public void ChangeState(PlayerState newState)
    {
        previousState = currentState;
        currentState.OnExit();
        currentState = newState;
        currentState.OnEnter();
    }

    public void ReturnToPreviousState()
    {
        ChangeState(previousState);
    }
}

// In JumpingState:
public override void Update()
{
    // ... jumping logic
    
    if (controller.isGrounded && velocity.y < 0)
        stateMachine.ReturnToPreviousState();
}
```

</details>
