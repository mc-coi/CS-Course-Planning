# Unit 4 Answer Key: Player Controls & Input

Comprehensive answer key for all 15 practice problems covering input detection, movement, animation, and advanced control mechanics.

---

## Problem 1: Basic Input Detection

### Solution

```csharp
using UnityEngine;

public class InputDetection : MonoBehaviour
{
    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
            Debug.Log("Jump!");

        if (Input.GetKey(KeyCode.Space))
            Debug.Log("Holding jump...");

        if (Input.GetKeyUp(KeyCode.Space))
            Debug.Log("Released!");
    }
}
```

### What Success Looks Like
- "Jump!" prints once per press
- "Holding jump..." prints every frame while held
- "Released!" prints once on release

### Common Mistakes
- Confusing GetKey (hold) with GetKeyDown (press)
- Using GetKeyDown for continuous actions (only fires once)

---

## Problem 2: Directional Movement

### Solution

```csharp
using UnityEngine;

public class DirectionalMovement : MonoBehaviour
{
    public float moveSpeed = 5f;

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");
        Vector3 newPos = transform.position + Vector3.right * input * moveSpeed * Time.deltaTime;
        newPos.x = Mathf.Clamp(newPos.x, -10f, 10f);
        transform.position = newPos;

        Debug.Log($"Position: {transform.position.x:F2}");
    }
}
```

### What Success Looks Like
- Object moves left/right with arrow keys
- Movement constrained between -10 and 10 on X axis
- Smooth, frame-rate independent motion

### Common Mistakes
- Forgetting Time.deltaTime (jerky motion dependent on frame rate)
- Wrong axis name (use "Horizontal" not "Horizontal Axis")
- Not clamping position (object escapes bounds)

---

## Problem 3: Simple Jump

### Solution

```csharp
using UnityEngine;

public class SimpleJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;
    public LayerMask groundLayer;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && IsGrounded())
        {
            rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        }
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

### What Success Looks Like
- Player jumps on Space press
- Only works when grounded (raycasted)
- Jump has consistent force

### Common Mistakes
- Not resetting Y velocity before jump (height inconsistent)
- Not checking IsGrounded (infinite jumping)
- Using AddForce with Force mode (jumping inconsistent with gravity)

---

## Problem 4: Mouse Position to World Space

### Solution

```csharp
using UnityEngine;

public class MouseToWorld : MonoBehaviour
{
    private void Update()
    {
        Vector3 mouseScreenPos = Input.mousePosition;
        mouseScreenPos.z = 10f;
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);

        Debug.DrawLine(Camera.main.transform.position, mouseWorldPos, Color.blue);
        Debug.Log($"Mouse world position: {mouseWorldPos}");
    }
}
```

### What Success Looks Like
- World position updates as mouse moves
- Line drawn from camera to mouse position
- Console shows coordinates continuously

### Common Mistakes
- Forgetting to set Z distance (returns camera position)
- Not normalizing screen position (coordinates off)
- Using Screen.width/height instead of mousePosition

---

## Problem 5: Animator Parameter Control

### Solution

```csharp
using UnityEngine;

public class AnimatorControl : MonoBehaviour
{
    private Animator animator;
    private float jumpTimer = 0f;

    private void Start()
    {
        animator = GetComponent<Animator>();
    }

    private void Update()
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        animator.SetFloat("Speed", Mathf.Abs(horizontalInput));

        if (Input.GetKeyDown(KeyCode.Space))
        {
            animator.SetBool("IsJumping", true);
            jumpTimer = 0.5f;
        }

        jumpTimer -= Time.deltaTime;
        if (jumpTimer <= 0)
        {
            animator.SetBool("IsJumping", false);
        }
    }
}
```

### What Success Looks Like
- Speed parameter follows movement input
- IsJumping flag triggers on Space
- Jump animation state transitions properly

### Common Mistakes
- Using SetInteger instead of SetFloat for Speed (integer animation won't blend)
- Not resetting IsJumping (animation gets stuck)
- Case-sensitive parameter names must match Animator

---

## Problem 6: Sprite Flipping

### Solution

```csharp
using UnityEngine;

public class SpriteFlipping : MonoBehaviour
{
    private SpriteRenderer spriteRenderer;
    private float facingDirection = 1f;

    private void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
    }

    private void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");

        if (moveInput != 0)
        {
            facingDirection = Mathf.Sign(moveInput);
            spriteRenderer.flipX = facingDirection < 0;
        }
    }
}
```

### What Success Looks Like
- Sprite faces direction of movement
- Flips only when moving (no flicker)
- Smooth facing transitions

### Common Mistakes
- Flipping every frame (flickering)
- Not using Mathf.Sign (direction calculation wrong)
- flipX logic inverted (flips wrong way)

---

## Problem 7: Velocity-Based Movement with Clamping

### Solution

```csharp
using UnityEngine;

public class VelocityMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float maxSpeed = 10f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");
        float newVelX = input * maxSpeed;
        rb.velocity = new Vector3(newVelX, rb.velocity.y, 0);
    }
}
```

### What Success Looks Like
- Object moves horizontally at maxSpeed
- Vertical velocity preserved (gravity works)
- Movement is instant and responsive

### Common Mistakes
- Using += on velocity (causes acceleration issues)
- Clamping after setting (overridden by input)
- Not preserving Y velocity (player falls instantly)

---

## Problem 8: Acceleration-Based Movement

### Solution

```csharp
using UnityEngine;

public class AccelerationMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float maxSpeed = 10f;
    public float acceleration = 8f;
    public float deceleration = 6f;

    private float currentSpeed = 0f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");

        if (input != 0)
        {
            currentSpeed += input * acceleration * Time.deltaTime;
        }
        else
        {
            float decelDir = Mathf.Sign(currentSpeed);
            currentSpeed -= decelDir * deceleration * Time.deltaTime;
            if (Mathf.Abs(currentSpeed) < 0.1f)
                currentSpeed = 0;
        }

        currentSpeed = Mathf.Clamp(currentSpeed, -maxSpeed, maxSpeed);
        rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
    }
}
```

### What Success Looks Like
- Smooth acceleration to maxSpeed
- Deceleration when input stops
- No instant velocity changes

### Common Mistakes
- Not clamping speed (can exceed maxSpeed)
- Deceleration with wrong direction (moves wrong way)
- Not stopping at near-zero speed (drifts slowly)

---

## Problem 9: Coyote Time (Forgiving Jump)

### Solution

```csharp
using UnityEngine;

public class CoyoteTime : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;
    public float coyoteTime = 0.2f;
    public LayerMask groundLayer;

    private float coyoteCounter = 0f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (IsGrounded())
        {
            coyoteCounter = coyoteTime;
        }
        else
        {
            coyoteCounter -= Time.deltaTime;
        }

        if (Input.GetKeyDown(KeyCode.Space) && coyoteCounter > 0)
        {
            rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            coyoteCounter = 0;
        }
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

### What Success Looks Like
- Can jump for 0.2 seconds after leaving ground
- Grace period feels forgiving but fair
- Jump consumed after use

### Common Mistakes
- Not decrementing coyoteCounter (never expires)
- Resetting counter on every ground check (always available)
- Not clearing counter after jump (double jumping)

---

## Problem 10: Ground Detection with OverlapCircle

### Solution

```csharp
using UnityEngine;

public class OverlapGroundDetection : MonoBehaviour
{
    public float detectionRadius = 0.3f;
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        Vector3 checkPos = transform.position + Vector3.down * 0.5f;
        Collider[] hits = Physics.OverlapSphere(checkPos, detectionRadius, groundLayer);

        Debug.DrawWireSphere(checkPos, detectionRadius, hits.Length > 0 ? Color.green : Color.red);

        return hits.Length > 0;
    }

    private void Update()
    {
        Debug.Log("Grounded: " + IsGrounded());
    }
}
```

### What Success Looks Like
- IsGrounded() returns true when on ground
- Green sphere when grounded, red when airborne
- More reliable than raycasting for curved surfaces

### Common Mistakes
- Sphere radius too small (misses nearby ground)
- Not checking layer mask (detects everything)
- Visualizing wrong position (debug sphere off-screen)

---

## Problem 11: Top-Down 8-Directional Movement

### Solution

```csharp
using UnityEngine;

public class TopDownMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float moveSpeed = 5f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        Vector3 direction = new Vector3(horizontal, 0, vertical).normalized;
        rb.velocity = direction * moveSpeed + Vector3.up * rb.velocity.y;
    }
}
```

### What Success Looks Like
- Movement in 8 directions (diagonal moves same speed as cardinal)
- Normalized direction prevents diagonal speed boost
- Y velocity preserved for jumping/falling

### Common Mistakes
- Not normalizing direction (diagonal moves faster)
- Using transform.position instead of velocity (ignores physics)
- Not clamping Y velocity (breaks physics)

---

## Problem 12: Projectile Shooting with Cooldown

### Solution

```csharp
using UnityEngine;

public class GroundedShooter : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform shootPoint;
    public float bulletSpeed = 10f;
    public float shootCooldown = 0.5f;
    public LayerMask groundLayer;

    private float cooldownTimer = 0f;

    private void Update()
    {
        cooldownTimer -= Time.deltaTime;

        if (Input.GetMouseButtonDown(0) && cooldownTimer <= 0 && CanShoot())
        {
            Shoot();
            cooldownTimer = shootCooldown;
        }
    }

    private void Shoot()
    {
        Vector3 mouseScreenPos = Input.mousePosition;
        mouseScreenPos.z = 10f;
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);
        Vector3 shootDirection = (mouseWorldPos - shootPoint.position).normalized;

        GameObject bullet = Instantiate(bulletPrefab, shootPoint.position, Quaternion.identity);
        Rigidbody bulletRb = bullet.GetComponent<Rigidbody>();
        bulletRb.velocity = shootDirection * bulletSpeed;

        Destroy(bullet, 5f);
    }

    private bool CanShoot()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

### What Success Looks Like
- Click to shoot bullets toward mouse
- Only works when grounded
- 0.5 second cooldown between shots
- Bullets destroyed after 5 seconds

### Common Mistakes
- Not normalizing shoot direction (inconsistent speed)
- Not checking cooldown (rapid fire)
- Not checking CanShoot (shooting while airborne)

---

## Problem 13: Dash Ability with Cooldown

### Solution

```csharp
using UnityEngine;

public class DashAbility : MonoBehaviour
{
    private Rigidbody rb;
    public float dashSpeed = 20f;
    public float dashDuration = 0.3f;
    public float dashCooldown = 1f;

    private float dashTimer = 0f;
    private float cooldownTimer = 0f;
    private bool isDashing = false;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        cooldownTimer -= Time.deltaTime;

        if (Input.GetKeyDown(KeyCode.E) && !isDashing && cooldownTimer <= 0)
        {
            StartDash();
        }

        if (isDashing)
        {
            dashTimer -= Time.deltaTime;
            if (dashTimer <= 0)
            {
                EndDash();
            }
        }
    }

    private void StartDash()
    {
        isDashing = true;
        dashTimer = dashDuration;
        cooldownTimer = dashCooldown;
        rb.velocity = transform.forward * dashSpeed;
    }

    private void EndDash()
    {
        isDashing = false;
        rb.velocity = new Vector3(rb.velocity.x * 0.5f, rb.velocity.y, rb.velocity.z * 0.5f);
    }
}
```

### What Success Looks Like
- E key triggers dash in forward direction
- Dash lasts 0.3 seconds at high speed
- 1 second cooldown before next dash
- Velocity reduced on dash end

### Common Mistakes
- Not preventing multiple dashes (overlap)
- Not tracking cooldown separately from dash timer
- Velocity not reduced properly (maintains boost)

---

## Problem 14: Variable Jump Height

### Solution

```csharp
using UnityEngine;

public class VariableJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 10f;
    public LayerMask groundLayer;

    private bool isJumping = false;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && IsGrounded())
        {
            Jump();
        }

        if (Input.GetKeyUp(KeyCode.Space) && isJumping && rb.velocity.y > 0)
        {
            rb.velocity = new Vector3(rb.velocity.x, rb.velocity.y * 0.5f, rb.velocity.z);
            isJumping = false;
        }
    }

    private void Jump()
    {
        isJumping = true;
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

### What Success Looks Like
- Tap Space for short jump
- Hold Space for high jump
- Release early to cut height
- Smooth vertical control

### Common Mistakes
- Reducing velocity too much (makes falling weird)
- Not checking if jumping (applies to regular falling)
- Only works while airborne (checks rb.velocity.y > 0)

---

## Problem 15: Complete 2D Platformer Controller

### Solution

```csharp
using UnityEngine;

public class PlatformerController : MonoBehaviour
{
    [Header("Movement")]
    private Rigidbody rb;
    private SpriteRenderer spriteRenderer;
    private Animator animator;

    public float maxSpeed = 8f;
    public float acceleration = 12f;
    public float deceleration = 10f;
    private float currentSpeed = 0f;
    private float facingDirection = 1f;

    [Header("Jumping")]
    public float jumpForce = 8f;
    public float coyoteTime = 0.15f;
    public float jumpBuffer = 0.1f;
    private float coyoteCounter = 0f;
    private float jumpBufferCounter = 0f;
    private bool isAirborne = false;

    [Header("Ground Detection")]
    public float groundCheckRadius = 0.3f;
    public LayerMask groundLayer;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        spriteRenderer = GetComponent<SpriteRenderer>();
        animator = GetComponent<Animator>();
    }

    private void Update()
    {
        HandleInput();
        UpdateAnimation();
    }

    private void FixedUpdate()
    {
        HandleMovement();
        UpdateCoyoteTime();
    }

    private void HandleInput()
    {
        float moveInput = Input.GetAxis("Horizontal");

        if (moveInput != 0)
        {
            currentSpeed = Mathf.Lerp(currentSpeed, moveInput * maxSpeed, acceleration * Time.deltaTime);
            facingDirection = Mathf.Sign(moveInput);
            spriteRenderer.flipX = facingDirection < 0;
        }
        else
        {
            currentSpeed = Mathf.Lerp(currentSpeed, 0, deceleration * Time.deltaTime);
        }

        if (Input.GetKeyDown(KeyCode.Space))
        {
            jumpBufferCounter = jumpBuffer;
        }
        else
        {
            jumpBufferCounter -= Time.deltaTime;
        }

        if (jumpBufferCounter > 0 && coyoteCounter > 0)
        {
            Jump();
            jumpBufferCounter = 0;
        }
    }

    private void HandleMovement()
    {
        rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
    }

    private void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, 0);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        coyoteCounter = 0;
    }

    private void UpdateCoyoteTime()
    {
        isAirborne = !IsGrounded();

        if (!isAirborne)
        {
            coyoteCounter = coyoteTime;
        }
        else
        {
            coyoteCounter -= Time.fixedDeltaTime;
        }
    }

    private void UpdateAnimation()
    {
        animator.SetFloat("Speed", Mathf.Abs(currentSpeed));
        animator.SetBool("IsGrounded", !isAirborne);
    }

    private bool IsGrounded()
    {
        Vector3 checkPos = transform.position + Vector3.down * 0.5f;
        Collider[] hits = Physics.OverlapSphere(checkPos, groundCheckRadius, groundLayer);
        return hits.Length > 0;
    }
}
```

### What Success Looks Like
- Smooth, responsive platformer movement
- All animation states transition properly
- Coyote time makes jumping forgiving
- Jump buffer smooths input timing
- Sprite flips with facing direction

### Common Mistakes
- Not using lerp for acceleration (jerky movement)
- Missing coyote time (frustrating jump timing)
- Animation parameters not updated (character looks frozen)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | Input Detection | Beginner |
| 2 | Directional Movement | Beginner |
| 3 | Jump Mechanics | Beginner |
| 4 | Mouse to World | Intermediate |
| 5 | Animator Control | Intermediate |
| 6 | Sprite Flipping | Beginner |
| 7 | Velocity Movement | Intermediate |
| 8 | Acceleration | Intermediate |
| 9 | Coyote Time | Intermediate |
| 10 | Ground Detection | Intermediate |
| 11 | 8-Dir Movement | Intermediate |
| 12 | Shooting | Advanced |
| 13 | Dash Ability | Advanced |
| 14 | Variable Jump | Advanced |
| 15 | Complete Controller | Advanced |
