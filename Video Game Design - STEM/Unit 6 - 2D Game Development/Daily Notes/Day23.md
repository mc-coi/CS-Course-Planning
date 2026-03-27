# Day 23: Animation & Animator

**Learning Target:** Create and control 2D sprite animations using the Animator component with state-based transitions.

### Key Concepts

- **Animation Clip:** A sequence of sprites or keyframes
- **Animator:** Component that plays animations and manages states
- **Animation State:** A named animation (Idle, Run, Jump)
- **Transition:** Change from one animation to another
- **Condition:** Requirement for a transition to happen
- **Parameter:** Variables controlling animation (bool, int, float, trigger)
- **Blend Tree:** Smooth transitions between similar animations

### Content

Animation brings 2D sprites to life. The Animator plays animation clips based on state.

**Creating Animations:**
1. Create folder for animation clips
2. Select multiple sprite frames
3. Drag them into the scene (Animator auto-creates)
4. Name the animation (e.g., "Idle", "Run", "Jump")
5. Adjust animation speed and loop settings

**Setting Up the Animator:**
1. Create an Animator Controller asset
2. Assign it to the Animator component
3. Create animation states by dragging in animation clips
4. Add transitions between states with conditions

**Animation Parameters:**
Use parameters to control which animation plays:
```csharp
animator.SetBool("IsRunning", true);        // Boolean parameter
animator.SetFloat("Speed", moveSpeed);      // Float parameter
animator.SetTrigger("Jump");                // Trigger (one-time)
animator.SetInteger("Direction", 1);       // Integer parameter
```

**Common Setup:**
```
Parameters: IsRunning (bool), IsJumping (bool)
States: Idle, Run, Jump, Fall
Transitions:
  Idle → Run (IsRunning = true)
  Run → Idle (IsRunning = false)
  Idle/Run → Jump (IsJumping = true)
  Jump → Fall (on animation complete)
  Fall → Idle (IsJumping = false)
```

### Code Examples

```csharp
using UnityEngine;

public class PlayerAnimator : MonoBehaviour
{
    private Animator animator;
    private Rigidbody2D rb2d;
    private float horizontalInput = 0f;
    private bool isJumping = false;

    void Start()
    {
        animator = GetComponent<Animator>();
        rb2d = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Get input
        horizontalInput = Input.GetAxis("Horizontal");

        // Determine if running
        bool isRunning = Mathf.Abs(horizontalInput) > 0.1f;

        // Update animator parameters
        animator.SetBool("IsRunning", isRunning);
        animator.SetFloat("VelocityY", rb2d.velocity.y);

        // Jump
        if (Input.GetKeyDown(KeyCode.Space))
        {
            animator.SetTrigger("Jump");
            isJumping = true;
        }

        // Reset jumping flag when landing (detected by negative velocity)
        if (rb2d.velocity.y < -0.1f && isJumping)
        {
            animator.SetBool("IsJumping", true);
        }
        else if (rb2d.velocity.y > -0.1f && isJumping)
        {
            animator.SetBool("IsJumping", false);
            isJumping = false;
        }
    }

    void FixedUpdate()
    {
        // Apply movement (physics)
        rb2d.velocity = new Vector2(horizontalInput * 5f, rb2d.velocity.y);
    }
}

// Animation State Machine managed by Animator controller
// Parameters:
//   IsRunning (bool)
//   IsJumping (bool)
//   Jump (trigger)
//   VelocityY (float)
//
// States & Transitions:
//   Idle → Run (IsRunning = true)
//   Run → Idle (IsRunning = false)
//   Idle/Run → Jump (Jump trigger)
//   Jump → Fall (exit time 0.5)
//   Fall → Idle (VelocityY > -1)
```

### Guided Practice

**Activity:** Create a 3-state animation system

1. Create or prepare 3 sets of sprite frames (Idle, Run, Jump)
2. Create animation clips from each set
3. Create an Animator Controller
4. Add 3 states: Idle, Run, Jump
5. Create transitions with conditions:
   - Idle ↔ Run (based on IsRunning bool)
   - Any state → Jump (Jump trigger)
6. Attach PlayerAnimator script and test

### Practice Problems

**Problem 1 — Beginner:** Create a 2D sprite animation with multiple frames. Set up the Animator to play idle and run animations based on input.

**Problem 2 — Intermediate:** Create a 4-state animation system (Idle, Run, Jump, Fall) with smooth transitions based on movement direction and velocity.

**Problem 3 — Challenge:** Implement complex animation logic with blend trees, directional movement (8-way), and smooth transitions between states.

<details>
<summary>Hints</summary>

**Problem 1:** Create animation clips from sprite sheets. Add states to the Animator. Use SetBool() to control transitions.

**Problem 2:** Add a VelocityY float parameter. Use it to transition between Jump and Fall states. Create a Jump state and a Fall state.

**Problem 3:** Use Blend Trees to smoothly blend between walk and run based on speed. Handle 8 directions with directional input.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
See PlayerAnimator code example above.

**Problem 2:**
Expand PlayerAnimator with:
```csharp
// Add these parameters to Animator Controller:
// - IsRunning (bool)
// - IsFalling (bool)
// - VelocityY (float)

// Create states: Idle, Run, Jump, Fall
// Transitions:
// - Idle/Run → Jump (Jump trigger)
// - Jump → Fall (when VelocityY < 0)
// - Fall → Idle (when grounded)
```

**Problem 3:**
Create Blend Tree for movement:
- Parameter: "Speed" (float 0-1)
- Blend between Walk (0.5) and Run (1.0) animations

</details>
