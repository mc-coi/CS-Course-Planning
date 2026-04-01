# Unit 4 Reference Guide: Player Controls & Input

A quick-reference for input handling, movement patterns, animation control, and shooting mechanics.

---

## Table of Contents

1. [Input Detection](#input-detection)
2. [Movement Patterns](#movement-patterns)
3. [Ground Detection](#ground-detection)
4. [Jumping Mechanics](#jumping-mechanics)
5. [Animator Integration](#animator-integration)
6. [Sprite Flipping & Direction](#sprite-flipping--direction)
7. [Mouse Input & Aiming](#mouse-input--aiming)
8. [Projectile & Shooting](#projectile--shooting)
9. [Cooldown Systems](#cooldown-systems)
10. [Dash & Special Abilities](#dash--special-abilities)
11. [Feel Improvements](#feel-improvements)
12. [Common Patterns](#common-patterns)

---

## Input Detection

### Input Class Methods

```csharp
using UnityEngine;

// Key Input
Input.GetKey(KeyCode.Space);        // True while held
Input.GetKeyDown(KeyCode.Space);    // True on first frame pressed
Input.GetKeyUp(KeyCode.Space);      // True on first frame released

// Axis Input (smooth, includes gamepad)
float horizontal = Input.GetAxis("Horizontal");     // -1 to 1, smooth
float vertical = Input.GetAxis("Vertical");         // -1 to 1, smooth
float horizontal = Input.GetAxisRaw("Horizontal");  // -1, 0, or 1 (discrete)

// Mouse Input
Vector3 mousePos = Input.mousePosition;             // Screen pixel position
bool mouseClick = Input.GetMouseButton(0);          // Left click
bool mouseDown = Input.GetMouseButtonDown(0);       // Left click first frame
bool mouseUp = Input.GetMouseButtonUp(0);           // Left click release

// Gamepad (via axes)
float trigger = Input.GetAxis("Triggers");
bool jumpButton = Input.GetButtonDown("Jump");
```

### Common Input Patterns

**Movement Input:**
```csharp
private void Update()
{
    float moveInput = Input.GetAxis("Horizontal");  // WASD, D-Pad, or Analog Stick
    // Use moveInput for movement
}
```

**Jump Input (Check in Update, Apply in FixedUpdate):**
```csharp
private bool wantToJump = false;

private void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        wantToJump = true;
    }
}

private void FixedUpdate()
{
    if (wantToJump && IsGrounded())
    {
        Jump();
        wantToJump = false;
    }
}
```

**Ability with Cooldown:**
```csharp
private float dashCooldown = 0f;

private void Update()
{
    dashCooldown -= Time.deltaTime;

    if (Input.GetKeyDown(KeyCode.E) && dashCooldown <= 0)
    {
        Dash();
        dashCooldown = 0.5f; // 0.5 second cooldown
    }
}
```

---

## Movement Patterns

### Pattern 1: Direct Velocity Control (Snappy, Responsive)

**Best for:** Platformers, immediate feel, pixel-perfect controls

```csharp
public class DirectMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float moveSpeed = 5f;

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");
        float newVelX = input * moveSpeed;
        rb.velocity = new Vector3(newVelX, rb.velocity.y, 0);
    }
}
```

### Pattern 2: Acceleration-Based Movement (Polished)

**Best for:** Smooth feel, realistic momentum, modern games

```csharp
public class AccelerationMovement : MonoBehaviour
{
    private Rigidbody rb;
    private float currentSpeed = 0f;
    public float maxSpeed = 10f;
    public float acceleration = 5f;
    public float deceleration = 8f;

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");

        // Accelerate or decelerate
        if (input != 0)
        {
            currentSpeed += input * acceleration * Time.deltaTime;
        }
        else
        {
            // Decelerate towards zero
            float decelDir = Mathf.Sign(currentSpeed);
            currentSpeed -= decelDir * deceleration * Time.deltaTime;
            if (Mathf.Abs(currentSpeed) < 0.1f)
                currentSpeed = 0;
        }

        // Clamp to max speed
        currentSpeed = Mathf.Clamp(currentSpeed, -maxSpeed, maxSpeed);

        // Apply movement
        rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
    }
}
```

### Pattern 3: Physics-Based Movement (Realistic)

**Best for:** Realistic objects, multiplayer, dynamic interactions

```csharp
public class PhysicsMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float moveForce = 10f;
    public float maxSpeed = 10f;

    private void FixedUpdate()
    {
        float input = Input.GetAxis("Horizontal");

        if (Mathf.Abs(rb.velocity.x) < maxSpeed)
        {
            rb.AddForce(Vector3.right * input * moveForce, ForceMode.Force);
        }
    }
}
```

### Pattern 4: Normalized Movement (For Multiplayer)

**Best for:** Consistent movement regardless of frame rate

```csharp
public class NormalizedMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float moveDistance = 0.1f; // Distance per frame-independent step

    private void Update()
    {
        float input = Input.GetAxis("Horizontal");
        Vector3 move = Vector3.right * input * moveDistance;
        rb.MovePosition(rb.position + move);
    }
}
```

### 8-Directional Movement (Top-Down)

```csharp
public class TopDownMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float moveSpeed = 5f;

    private void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        Vector3 direction = new Vector3(horizontal, 0, vertical);

        // Normalize diagonal movement (prevents moving faster diagonally)
        direction = direction.normalized;

        rb.velocity = direction * moveSpeed + Vector3.up * rb.velocity.y;
    }
}
```

---

## Ground Detection

### Method 1: Raycasting (Most Common)

```csharp
public class RaycastGroundDetection : MonoBehaviour
{
    private Rigidbody rb;
    public float groundCheckDistance = 0.1f;
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        Vector3 rayOrigin = transform.position + Vector3.down * 0.5f;

        bool grounded = Physics.Raycast(
            rayOrigin,
            Vector3.down,
            groundCheckDistance,
            groundLayer
        );

        // Debug visualization
        Debug.DrawRay(rayOrigin, Vector3.down * groundCheckDistance,
            grounded ? Color.green : Color.red);

        return grounded;
    }
}
```

### Method 2: OverlapCircle (Detection Area)

```csharp
public class OverlapGroundDetection : MonoBehaviour
{
    public float groundCheckRadius = 0.3f;
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        Vector3 checkPos = transform.position + Vector3.down * 0.5f;

        Collider[] hits = Physics.OverlapSphere(
            checkPos,
            groundCheckRadius,
            groundLayer
        );

        // Debug visualization
        Debug.DrawWireSphere(checkPos, groundCheckRadius,
            hits.Length > 0 ? Color.green : Color.red);

        return hits.Length > 0;
    }
}
```

### Method 3: Multiple Raycasts (More Reliable)

```csharp
public class MultiRayGroundDetection : MonoBehaviour
{
    public float groundCheckDistance = 0.1f;
    public LayerMask groundLayer;
    private float checkWidth = 0.3f;

    public bool IsGrounded()
    {
        // Check center, left, right
        Vector3[] checkPoints = new[]
        {
            transform.position + Vector3.down * 0.5f,
            transform.position + Vector3.down * 0.5f + Vector3.left * checkWidth,
            transform.position + Vector3.down * 0.5f + Vector3.right * checkWidth
        };

        foreach (var point in checkPoints)
        {
            if (Physics.Raycast(point, Vector3.down, groundCheckDistance, groundLayer))
                return true;
        }

        return false;
    }
}
```

---

## Jumping Mechanics

### Basic Jump

```csharp
public class BasicJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && IsGrounded())
        {
            Jump();
        }
    }

    private void Jump()
    {
        // Reset vertical velocity to ensure consistent jump
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f);
    }
}
```

### Variable Jump Height

```csharp
public class VariableJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 10f;
    public float jumpGravityScale = 2f; // Increased gravity while falling

    private bool isJumping = false;

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && IsGrounded())
        {
            Jump();
        }

        // Release space = fall faster (shorter jump)
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
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f);
    }
}
```

### Coyote Time (Forgiving Jump)

```csharp
public class CoyoteTimeJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;
    public float coyoteTime = 0.2f; // 0.2 seconds to jump after leaving ground

    private float coyoteCounter = 0f;

    private void Update()
    {
        // Count down coyote time
        if (IsGrounded())
        {
            coyoteCounter = coyoteTime;
        }
        else
        {
            coyoteCounter -= Time.deltaTime;
        }

        // Jump if coyote time active
        if (Input.GetKeyDown(KeyCode.Space) && coyoteCounter > 0)
        {
            Jump();
            coyoteCounter = 0; // Use up coyote time
        }
    }

    private void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f);
    }
}
```

### Jump Buffer (Input Anticipation)

```csharp
public class JumpBuffer : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;
    public float jumpBufferTime = 0.1f; // Store input for 0.1 seconds

    private float jumpBuffer = 0f;

    private void Update()
    {
        // Detect jump input and store it
        if (Input.GetKeyDown(KeyCode.Space))
        {
            jumpBuffer = jumpBufferTime;
        }
        else
        {
            jumpBuffer -= Time.deltaTime;
        }

        // Jump if buffer has input and we're grounded
        if (jumpBuffer > 0 && IsGrounded())
        {
            Jump();
            jumpBuffer = 0; // Consume the input
        }
    }

    private void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f);
    }
}
```

---

## Animator Integration

### Setting Up Animator

1. Create Animator Controller (right-click → Create → Animator Controller)
2. Assign to Animator component on character
3. Add parameters in Animator window
4. Create states and transitions in state machine

### Parameter Types

| Type | Use Case | SetMethod | GetMethod |
|------|----------|-----------|-----------|
| **Bool** | On/off states | SetBool("name", bool) | GetBool("name") |
| **Float** | Continuous values | SetFloat("name", float) | GetFloat("name") |
| **Integer** | Discrete values | SetInteger("name", int) | GetInteger("name") |
| **Trigger** | One-time events | SetTrigger("name") | ResetTrigger("name") |

### Common Setup

```csharp
public class AnimationController : MonoBehaviour
{
    private Animator animator;
    private Rigidbody rb;

    private void Start()
    {
        animator = GetComponent<Animator>();
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float horizontalSpeed = Mathf.Abs(rb.velocity.x);
        animator.SetFloat("Speed", horizontalSpeed);
        animator.SetBool("IsGrounded", IsGrounded());

        if (Input.GetKeyDown(KeyCode.Space))
        {
            animator.SetTrigger("Jump");
        }
    }

    private bool IsGrounded()
    {
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f);
    }
}
```

### Transition Conditions

- **Bool:** Toggle on/off based on script boolean
- **Float:** Compare speed, distance, or value
- **Integer:** State machine with discrete states
- **Trigger:** One-time events (jump, attack)

**In Animator:**
- From "Idle" → "Run" on condition `Speed > 0.1`
- From "Run" → "Idle" on condition `Speed < 0.1`
- From "Ground" → "Jump" on trigger `Jump`

---

## Sprite Flipping & Direction

### Method 1: Flip X Property

```csharp
public class SpriteFlip : MonoBehaviour
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

### Method 2: Scale Negation

```csharp
public class ScaleFlip : MonoBehaviour
{
    private float facingDirection = 1f;

    private void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");

        if (moveInput != 0)
        {
            facingDirection = Mathf.Sign(moveInput);
        }

        // Flip by negating scale
        transform.localScale = new Vector3(facingDirection, 1, 1);
    }
}
```

### Method 3: Rotation

```csharp
public class RotationFlip : MonoBehaviour
{
    private float facingDirection = 1f;

    private void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");

        if (moveInput != 0)
        {
            facingDirection = Mathf.Sign(moveInput);
        }

        // Rotate 180 degrees for opposite direction
        transform.rotation = facingDirection < 0 ?
            Quaternion.Euler(0, 180, 0) :
            Quaternion.identity;
    }
}
```

### Directional Animation

```csharp
public class DirectionalAnimation : MonoBehaviour
{
    private Animator animator;
    private SpriteRenderer spriteRenderer;
    private float facingDirection = 1f;

    private void Update()
    {
        float horizontalInput = Input.GetAxis("Horizontal");

        // Update facing direction
        if (horizontalInput != 0)
        {
            facingDirection = Mathf.Sign(horizontalInput);
            spriteRenderer.flipX = facingDirection < 0;
        }

        // Update animator
        animator.SetFloat("Speed", Mathf.Abs(horizontalInput));
    }
}
```

---

## Mouse Input & Aiming

### Basic Mouse Position

```csharp
public class MouseAim : MonoBehaviour
{
    private void Update()
    {
        // Get mouse position in screen space
        Vector3 mouseScreenPos = Input.mousePosition;

        // Convert to world space
        mouseScreenPos.z = 10f; // Distance from camera
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);

        // Calculate direction from player to mouse
        Vector3 directionToMouse = (mouseWorldPos - transform.position).normalized;

        Debug.Log("Mouse world position: " + mouseWorldPos);
        Debug.Log("Direction: " + directionToMouse);
    }
}
```

### Aiming with Visual Feedback

```csharp
public class AimSystem : MonoBehaviour
{
    private LineRenderer aimLine;
    public float aimDistance = 10f;

    private void Start()
    {
        aimLine = GetComponent<LineRenderer>();
    }

    private void Update()
    {
        Vector3 mouseScreenPos = Input.mousePosition;
        mouseScreenPos.z = 10f;
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);

        Vector3 aimDirection = (mouseWorldPos - transform.position).normalized;

        // Draw aim line
        aimLine.SetPosition(0, transform.position);
        aimLine.SetPosition(1, transform.position + aimDirection * aimDistance);
    }
}
```

### Aiming & Rotation

```csharp
public class AimRotation : MonoBehaviour
{
    private void Update()
    {
        Vector3 mouseScreenPos = Input.mousePosition;
        mouseScreenPos.z = 10f;
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);

        Vector3 direction = (mouseWorldPos - transform.position).normalized;

        // Rotate to face mouse
        float angle = Mathf.Atan2(direction.y, direction.x) * Mathf.Rad2Deg;
        transform.rotation = Quaternion.AngleAxis(angle, Vector3.forward);
    }
}
```

---

## Projectile & Shooting

### Basic Shooting

```csharp
public class BasicShooter : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform shootPoint;
    public float bulletSpeed = 10f;

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Shoot();
        }
    }

    private void Shoot()
    {
        // Get aim direction
        Vector3 mouseScreenPos = Input.mousePosition;
        mouseScreenPos.z = 10f;
        Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);
        Vector3 shootDirection = (mouseWorldPos - shootPoint.position).normalized;

        // Instantiate bullet
        GameObject bullet = Instantiate(bulletPrefab, shootPoint.position, Quaternion.identity);
        Rigidbody bulletRb = bullet.GetComponent<Rigidbody>();
        bulletRb.velocity = shootDirection * bulletSpeed;

        // Optional: Destroy after time
        Destroy(bullet, 5f);
    }
}
```

### Shooting with Cooldown

```csharp
public class CooldownShooter : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform shootPoint;
    public float bulletSpeed = 10f;
    public float shootCooldown = 0.5f;

    private float shootTimer = 0f;

    private void Update()
    {
        shootTimer -= Time.deltaTime;

        if (Input.GetMouseButtonDown(0) && shootTimer <= 0)
        {
            Shoot();
            shootTimer = shootCooldown;
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
}
```

### Ground Check Before Shooting

```csharp
public class GroundedShooter : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform shootPoint;
    public float bulletSpeed = 10f;
    public LayerMask groundLayer;

    private void Update()
    {
        if (Input.GetMouseButtonDown(0) && CanShoot())
        {
            Shoot();
        }
    }

    private bool CanShoot()
    {
        // Only shoot when grounded
        return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
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
}
```

### Object Pooling (Reuse Bullets)

```csharp
public class BulletPool : MonoBehaviour
{
    public static BulletPool instance;
    private List<GameObject> bulletPool = new List<GameObject>();
    public GameObject bulletPrefab;
    public int poolSize = 20;

    private void Awake()
    {
        instance = this;
        InitializePool();
    }

    private void InitializePool()
    {
        for (int i = 0; i < poolSize; i++)
        {
            GameObject bullet = Instantiate(bulletPrefab);
            bullet.SetActive(false);
            bulletPool.Add(bullet);
        }
    }

    public GameObject GetBullet(Vector3 position, Vector3 velocity)
    {
        foreach (GameObject bullet in bulletPool)
        {
            if (!bullet.activeInHierarchy)
            {
                bullet.SetActive(true);
                bullet.transform.position = position;
                bullet.GetComponent<Rigidbody>().velocity = velocity;
                return bullet;
            }
        }

        // If no pooled bullet, create new
        GameObject newBullet = Instantiate(bulletPrefab, position, Quaternion.identity);
        newBullet.GetComponent<Rigidbody>().velocity = velocity;
        bulletPool.Add(newBullet);
        return newBullet;
    }

    public void ReturnBullet(GameObject bullet)
    {
        bullet.SetActive(false);
    }
}

// Usage in shooter
BulletPool.instance.GetBullet(shootPoint.position, shootDirection * bulletSpeed);
```

---

## Cooldown Systems

### Simple Timer

```csharp
private float cooldownTimer = 0f;
public float cooldownDuration = 0.5f;

private void Update()
{
    cooldownTimer -= Time.deltaTime;

    if (Input.GetKeyDown(KeyCode.E) && cooldownTimer <= 0)
    {
        DoAbility();
        cooldownTimer = cooldownDuration;
    }
}
```

### Cooldown with UI Display

```csharp
public Image cooldownImage;

private void Update()
{
    cooldownTimer -= Time.deltaTime;

    if (Input.GetKeyDown(KeyCode.E) && cooldownTimer <= 0)
    {
        cooldownTimer = cooldownDuration;
    }

    // Update UI
    float cooldownPercent = cooldownTimer / cooldownDuration;
    cooldownImage.fillAmount = cooldownPercent;
}
```

---

## Dash & Special Abilities

### Simple Dash with Timer

```csharp
public class SimpleDash : MonoBehaviour
{
    private Rigidbody rb;
    public float dashSpeed = 20f;
    public float dashDuration = 0.3f;
    public float dashCooldown = 1f;

    private float dashTimer = 0f;
    private float cooldownTimer = 0f;
    private bool isDashing = false;

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
        rb.velocity = Vector3.zero;
    }
}
```

### Dash with Coroutine

```csharp
public class CoroutineDash : MonoBehaviour
{
    private Rigidbody rb;
    public float dashSpeed = 20f;
    public float dashDuration = 0.3f;
    public float dashCooldown = 1f;

    private float cooldownTimer = 0f;

    private void Update()
    {
        cooldownTimer -= Time.deltaTime;

        if (Input.GetKeyDown(KeyCode.E) && cooldownTimer <= 0)
        {
            StartCoroutine(DashCoroutine());
            cooldownTimer = dashCooldown;
        }
    }

    private IEnumerator DashCoroutine()
    {
        float elapsed = 0f;
        Vector3 dashDirection = transform.forward;

        while (elapsed < dashDuration)
        {
            rb.velocity = dashDirection * dashSpeed;
            elapsed += Time.deltaTime;
            yield return null;
        }

        // Optional: Fade out or transition
        rb.velocity = new Vector3(rb.velocity.x * 0.5f, rb.velocity.y, rb.velocity.z * 0.5f);
    }
}
```

---

## Feel Improvements

### Speed Ramp (Acceleration Curve)

```csharp
private float currentSpeed = 0f;

private void Update()
{
    float targetSpeed = Input.GetAxis("Horizontal") * maxSpeed;

    // Smoothly accelerate/decelerate
    currentSpeed = Mathf.Lerp(currentSpeed, targetSpeed, accelerationRate * Time.deltaTime);

    rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
}
```

### Jump Squash

```csharp
private void Jump()
{
    rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    StartCoroutine(JumpSquashCoroutine());
}

private IEnumerator JumpSquashCoroutine()
{
    Vector3 originalScale = transform.localScale;

    // Squash down
    transform.localScale = new Vector3(1.2f, 0.8f, 1f);
    yield return new WaitForSeconds(0.1f);

    // Return to normal
    transform.localScale = originalScale;
}
```

### Landing Impact

```csharp
private bool wasAirborne = false;

private void Update()
{
    bool isGrounded = IsGrounded();

    if (!wasAirborne && isGrounded)
    {
        // Just landed
        OnLanding();
    }

    wasAirborne = !isGrounded;
}

private void OnLanding()
{
    // Play landing animation
    animator.SetTrigger("Land");

    // Optional: Screen shake, impact VFX
    StartCoroutine(CameraShake(0.1f, 0.05f));
}

private IEnumerator CameraShake(float duration, float magnitude)
{
    Vector3 originalPos = Camera.main.transform.position;
    float elapsed = 0f;

    while (elapsed < duration)
    {
        float x = Random.Range(-1f, 1f) * magnitude;
        float y = Random.Range(-1f, 1f) * magnitude;
        Camera.main.transform.position = originalPos + new Vector3(x, y, 0);

        elapsed += Time.deltaTime;
        yield return null;
    }

    Camera.main.transform.position = originalPos;
}
```

---

## Common Patterns

### Complete Player Controller (Simple 2D Platformer)

```csharp
using UnityEngine;

public class SimplePlayerController : MonoBehaviour
{
    private Rigidbody rb;
    private Animator animator;
    private SpriteRenderer spriteRenderer;

    [Header("Movement")]
    public float moveSpeed = 5f;
    public float acceleration = 10f;
    public float groundDrag = 5f;

    [Header("Jumping")]
    public float jumpForce = 5f;
    public float coyoteTime = 0.2f;
    public float jumpBuffer = 0.1f;

    [Header("Ground Detection")]
    public LayerMask groundLayer;
    public float groundCheckDistance = 0.1f;

    private float currentSpeed = 0f;
    private float coyoteCounter = 0f;
    private float jumpBufferCounter = 0f;
    private bool isAirborne = false;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        animator = GetComponent<Animator>();
        spriteRenderer = GetComponent<SpriteRenderer>();
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

        // Acceleration
        if (moveInput != 0)
        {
            currentSpeed = Mathf.Lerp(currentSpeed, moveInput * moveSpeed, acceleration * Time.deltaTime);
            spriteRenderer.flipX = moveInput < 0;
        }
        else
        {
            currentSpeed = Mathf.Lerp(currentSpeed, 0, groundDrag * Time.deltaTime);
        }

        // Jump buffer
        if (Input.GetKeyDown(KeyCode.Space))
        {
            jumpBufferCounter = jumpBuffer;
        }
        else
        {
            jumpBufferCounter -= Time.deltaTime;
        }

        // Jump
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
        Vector3 rayOrigin = transform.position + Vector3.down * 0.5f;
        return Physics.Raycast(rayOrigin, Vector3.down, groundCheckDistance, groundLayer);
    }
}
```

