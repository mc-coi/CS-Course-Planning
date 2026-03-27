# Day 16: Animation Integration & State-Driven Movement

**Learning Target:** I can sync animations with player movement and create polished state transitions.

---

## Key Concepts

**Animation-Driven Movement** — Instead of input driving movement, animations drive it. Useful for:
- Heavily animated games (*Dark Souls, Elden Ring*)
- Cinematics
- Stylized games where movement feels more important than speed

**Root Motion** — Let the animation move the character instead of code. The animator "roots" movement to the animation.

**Animation Events** — Trigger code at specific animation frames (e.g., footstep sounds, attack hitbox activation).

**Synchronization** — Keep animations and movement in sync: if animation plays slow, movement speed matches.

---

## Code Example

```csharp
using UnityEngine;

public class AnimationDrivenController : MonoBehaviour
{
    private Animator animator;
    private CharacterController controller;
    private Vector3 animationVelocity = Vector3.zero;

    private void Start()
    {
        animator = GetComponent<Animator>();
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        ReadInput();
    }

    private void ReadInput()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        // Pass input to animator
        animator.SetFloat("InputX", h);
        animator.SetFloat("InputY", v);

        // Jump
        if (Input.GetKeyDown(KeyCode.Space) && animator.GetBool("IsGrounded"))
        {
            animator.SetTrigger("Jump");
        }
    }

    // This is called by an Animation Event at the jump frame
    public void ApplyJumpVelocity()
    {
        animationVelocity.y = 5f;
    }

    // Called by animation event DURING jump animation
    public void ApplyAnimationMovement(float speed)
    {
        Vector3 moveDir = new Vector3(
            animator.GetFloat("InputX"), 
            0, 
            animator.GetFloat("InputY")
        ).normalized;

        animationVelocity.x = moveDir.x * speed;
        animationVelocity.z = moveDir.z * speed;
    }

    private void LateUpdate()
    {
        // Apply gravity
        if (controller.isGrounded && animationVelocity.y < 0)
            animationVelocity.y = -2f;
        else
            animationVelocity.y -= 9.81f * Time.deltaTime;

        // Move
        controller.Move(animationVelocity * Time.deltaTime);

        // Update grounded state
        animator.SetBool("IsGrounded", controller.isGrounded);
    }

    // Public method called by animation event
    public void PlayFootstepSFX()
    {
        Debug.Log("Footstep!");
        // GetComponent<AudioSource>().PlayOneShot(footstepClip);
    }
}
```

---

## Unity Setup Steps

1. **Create Animator with Multiple States**
   - Idle, Walk, Run, Jump animations

2. **Set Up Blend Tree for Movement**
   - 1D Blend Tree blending idle → walk → run based on Speed parameter
   - Or 2D Blend Tree for directional movement

3. **Add Animation Events**
   - In Animation window, click animation timeline
   - Right-click → Add Event
   - Select function to call (e.g., PlayFootstepSFX)

4. **Configure Root Motion** (Optional)
   - In Animator Controller, enable "Root Motion"
   - In Avatar settings, check "Root Motion"
   - Animation drives movement, not code

5. **Attach Script & Test**
   - Drag AnimationDrivenController onto Player
   - Press Play
   - Move around and watch animations play with sounds

---

## Guided Practice

1. **Set Up Blend Tree** (15 min)
   - Create a 1D blend tree with Idle (0) → Walk (0.5) → Run (1.0)
   - Control it with Speed parameter
   - Test smooth blending

2. **Add Animation Events** (10 min)
   - Add footstep sound event to walk animation
   - Call PlayFootstepSFX() when feet hit ground
   - Test footstep sounds play

3. **Integrate with Movement** (5 min)
   - Pass input values to animator
   - Let animator control speed/movement
   - Verify smooth synced movement

---

## Practice Problems

**Beginner:** Create a blend tree that blends Idle → Walk → Run based on a Speed parameter. Control it with WASD input.

**Intermediate:** Implement **directional animation blending**: use a 2D blend tree to blend between idle, walk forward, walk backward, strafe left, strafe right based on movement input.

**Challenge:** Create **animation-only jumping**: don't apply force in code; instead, at the jump animation's peak frame, add upward velocity via animation event. Ensure landing plays impact animation.

<details><summary>💡 Hints</summary>
- Blend trees automatically interpolate between animations based on parameters.
- Animation events fire at specific frames; place them carefully (footsteps when foot lands, not mid-air).
- Root Motion is powerful but requires careful setup; start without it if unsure.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (2D Blend Tree):**
```csharp
void Update()
{
    float h = Input.GetAxis("Horizontal");
    float v = Input.GetAxis("Vertical");

    animator.SetFloat("InputX", h);
    animator.SetFloat("InputY", v);
    
    // 2D blend tree uses both axes
    animator.SetFloat("Speed", new Vector2(h, v).magnitude);
}

// In Animator: Create 2D Blend Tree (Freeform Cartesian)
// Idle at (0, 0)
// Walk Forward at (0, 1)
// Walk Backward at (0, -1)
// Strafe Left at (-1, 0)
// Strafe Right at (1, 0)
```

</details>
