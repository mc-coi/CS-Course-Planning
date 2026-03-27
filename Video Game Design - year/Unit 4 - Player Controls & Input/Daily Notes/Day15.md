# Day 15: Animator Component & Parameter Control

**Learning Target:** I can use Unity's Animator component to trigger animations from code.

---

## Key Concepts

**Animator Component** — Plays animations based on parameters you set from code. Controls animation blending, transitions, and playback.

**Animator Parameters:**
- **Bool:** True/False (e.g., isWalking)
- **Float:** Numbers (e.g., speed for blending)
- **Int:** Integer values
- **Trigger:** One-shot events (e.g., Jump, Attack)

**Common Methods:**
- `animator.SetBool("isWalking", true)` — Set bool parameter
- `animator.SetFloat("speed", 1.5f)` — Set float for blending
- `animator.SetTrigger("Jump")` — Trigger animation once

**Animation Blending** — Use floats to smoothly blend between animations. E.g., set speed to 0–1 to fade between idle and walk animations.

---

## Code Example

```csharp
using UnityEngine;

public class AnimatedPlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float gravity = 9.81f;

    private Animator animator;
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;

    private void Start()
    {
        animator = GetComponent<Animator>();
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleMovement();
        HandleJump();
        ApplyGravity();
        UpdateAnimator();
    }

    private void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        Vector3 moveDir = new Vector3(h, 0, v).normalized;

        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;
        controller.Move(motion * Time.deltaTime);
    }

    private void HandleJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && controller.isGrounded)
        {
            velocity.y = jumpForce;
            animator.SetTrigger("Jump");
        }
    }

    private void UpdateAnimator()
    {
        // Calculate current speed for blending
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        float speed = new Vector3(h, 0, v).magnitude;

        // Set animator parameters
        animator.SetFloat("Speed", speed);
        animator.SetBool("IsGrounded", controller.isGrounded);
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

1. **Create Animated Player Model**
   - Import a humanoid character model (or use a simple capsule)
   - Or create in Blender and import FBX

2. **Add Animator Component**
   - Select Player
   - Add Component → Animator
   - Assign an Animator Controller (create one: Assets → Create → Animator Controller)

3. **Create Animation States**
   - Open Animator window (Window → Animation → Animator)
   - Create "Idle" state (animation clip)
   - Create "Walk" state
   - Create "Jump" state

4. **Set Up Parameters**
   - In Animator, create parameters:
     - Bool: "IsGrounded"
     - Float: "Speed"
     - Trigger: "Jump"

5. **Create Transitions**
   - Idle → Walk: when Speed > 0.1
   - Walk → Idle: when Speed < 0.1
   - Any State → Jump: when Jump trigger fires

6. **Attach AnimatedPlayerController Script**
   - Drag script onto Player

7. **Test**
   - Press Play
   - Move and watch animations play
   - Jump and see jump animation trigger

---

## Guided Practice

1. **Set Up Animator** (15 min)
   - Create Animator Controller
   - Add animation states (Idle, Walk, Jump)
   - Create transitions between states

2. **Control Animator from Code** (10 min)
   - Use SetFloat("Speed", speed) to control walk speed
   - Use SetTrigger("Jump") when jumping
   - Watch animations play

3. **Test Animation Blending** (5 min)
   - Walk at different speeds
   - Watch animation blend smoothly (with blend trees)

---

## Practice Problems

**Beginner:** Create Idle and Walk animations. Blend between them using a Speed parameter.

**Intermediate:** Add **attack animation**: press Left Mouse to play attack animation. Cannot move while attacking. Animation lasts 0.6 seconds.

**Challenge:** Implement **locomotion blend tree**: create a 2D blend tree with horizontal/vertical movement to blend between idle, walk forward, walk backward, strafe left, strafe right.

<details><summary>💡 Hints</summary>
- SetTrigger automatically resets after one use (good for one-shot animations).
- SetBool and SetFloat persist until you change them.
- Use speed parameter (0–1) to blend walk animations smoothly.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Attack):**
```csharp
private bool isAttacking = false;
private float attackTimer = 0f;
private const float ATTACK_DURATION = 0.6f;

void Update()
{
    if (Input.GetMouseButtonDown(0) && !isAttacking && controller.isGrounded)
    {
        isAttacking = true;
        attackTimer = ATTACK_DURATION;
        animator.SetTrigger("Attack");
    }

    if (isAttacking)
    {
        attackTimer -= Time.deltaTime;
        if (attackTimer <= 0)
            isAttacking = false;
    }
}
```

</details>
