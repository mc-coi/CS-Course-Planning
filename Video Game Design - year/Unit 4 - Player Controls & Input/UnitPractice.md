# Unit 4 Practice Problems: Player Controls & Input

15 problems ranging from beginner to advanced. Solutions provided.

---

## Problem 1: Basic Input Detection

**Difficulty:** Beginner

Create a script that:
1. Detects when Space is pressed (print "Jump!")
2. Detects when Space is held (print "Holding jump...")
3. Detects when Space is released (print "Released!")

```csharp
using UnityEngine;

public class InputDetection : MonoBehaviour
{
    private void Update()
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 2: Directional Movement

**Difficulty:** Beginner

Create a script that:
1. Reads horizontal input (arrow keys or WASD)
2. Moves the GameObject left/right based on input
3. Clamps movement between -10 and 10 on the X axis
4. Prints current position each frame

```csharp
using UnityEngine;

public class DirectionalMovement : MonoBehaviour
{
    public float moveSpeed = 5f;

    private void Update()
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 3: Simple Jump

**Difficulty:** Beginner

Create a jump script that:
1. Detects Space key press
2. Applies upward velocity using a Rigidbody
3. Only allows jumping when grounded (use raycasting)
4. Resets vertical velocity before jumping

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
        // Your code here
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 4: Mouse Position to World Space

**Difficulty:** Beginner

Create a script that:
1. Gets the mouse position in screen space
2. Converts it to world space
3. Draws a line from the camera to that position
4. Prints the world position

```csharp
using UnityEngine;

public class MouseToWorld : MonoBehaviour
{
    private void Update()
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 5: Animator Parameter Control

**Difficulty:** Intermediate

Create a script that:
1. Gets an Animator component
2. Sets a float parameter "Speed" based on horizontal input magnitude
3. Sets a bool parameter "IsJumping" when Space is pressed
4. Resets "IsJumping" after 0.5 seconds

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 6: Sprite Flipping

**Difficulty:** Intermediate

Create a script that:
1. Flips the sprite based on movement direction
2. Uses Input.GetAxis("Horizontal") to determine direction
3. Only flips when actually moving (input != 0)
4. Uses SpriteRenderer.flipX

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 7: Velocity-Based Movement with Clamping

**Difficulty:** Intermediate

Create a script that:
1. Sets Rigidbody velocity directly each frame
2. Uses Input.GetAxis for smooth input
3. Clamps horizontal speed to maxSpeed
4. Preserves vertical velocity (doesn't override Y)

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 8: Acceleration-Based Movement

**Difficulty:** Intermediate

Create a script that:
1. Gradually accelerates to maxSpeed (not instant)
2. Uses Input.GetAxis("Horizontal")
3. Decelerates when input stops
4. Applies movement every frame

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 9: Coyote Time (Forgiving Jump)

**Difficulty:** Intermediate

Implement coyote time:
1. Allow jumping for 0.2 seconds after leaving ground
2. Use raycasting for ground detection
3. Decrement coyote timer each frame
4. Reset timer when touching ground

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
        // Your code here
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 10: Ground Detection with OverlapCircle

**Difficulty:** Intermediate

Create ground detection using OverlapCircle:
1. Use Physics.OverlapCircle in a detection area
2. Return true if any colliders in groundLayer found
3. Visualize with Debug.DrawWireSphere
4. Adjust radius for feel

```csharp
using UnityEngine;

public class OverlapGroundDetection : MonoBehaviour
{
    public float detectionRadius = 0.3f;
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        // Your code here
        return false;
    }

    private void Update()
    {
        Debug.Log("Grounded: " + IsGrounded());
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 11: Top-Down 8-Directional Movement

**Difficulty:** Intermediate

Create top-down movement:
1. Read both horizontal and vertical input
2. Normalize the direction to prevent diagonal speed increase
3. Apply to Rigidbody velocity
4. Keep vertical velocity (Y axis)

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 12: Projectile Shooting with Cooldown

**Difficulty:** Advanced

Create a shooter that:
1. Aims toward mouse position
2. Only shoots when grounded (use raycasting)
3. Instantiates bullet prefab with velocity
4. Implements 0.5-second cooldown between shots

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
        // Your code here
    }

    private bool CanShoot()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 13: Dash Ability with Cooldown

**Difficulty:** Advanced

Implement a dash ability:
1. Press E to dash in forward direction
2. Dash duration: 0.3 seconds
3. Dash cooldown: 1 second
4. Cannot dash while already dashing
5. Lock other input during dash (optional)

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
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 14: Variable Jump Height

**Difficulty:** Advanced

Create variable-height jumping:
1. Player can control jump height by holding Space
2. Longer hold = higher jump
3. Release early = shorter jump
4. Implement by reducing upward velocity on release
5. Only works while airborne

```csharp
using UnityEngine;

public class VariableJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 10f;
    public LayerMask groundLayer;

    private bool isJumping = false;

    private void Update()
    {
        // Your code here
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
    }
}
```

<details><summary>✅ Solution</summary>

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

</details>

---

## Problem 15: Complete 2D Platformer Controller

**Difficulty:** Advanced

Build a complete 2D platformer controller combining:
1. Smooth horizontal acceleration-based movement
2. Jumping with coyote time
3. Ground detection with OverlapCircle
4. Sprite flipping
5. Animator integration with Speed and IsGrounded parameters
6. Optional: Jump buffer, wall sliding, or double jump

This is a culminating challenge. Use previous solutions as reference.

<details><summary>✅ Solution Outline</summary>

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

</details>

---

## Challenge Extension Problems

**Problem A:** Implement jump buffering that stores input for 0.1 seconds.

**Problem B:** Create a double-jump mechanic with visual/audio feedback.

**Problem C:** Build wall-sliding mechanics where players stick to walls while falling.

**Problem D:** Implement a sprint ability that increases speed for limited duration.

**Problem E:** Create a complete top-down RPG controller with 8-directional movement and animation blending.

