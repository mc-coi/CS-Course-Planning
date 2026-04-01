# Unit 4 Assessment: Player Controls & Input

**Total Points: 70** | **Passing: 49+** | **Time: 90 minutes**

---

## Multiple Choice Section (10 questions, 2 points each)

**1.** Which method is called every frame and should handle input detection?
A) FixedUpdate
B) LateUpdate
C) Update ✓
D) OnCollisionEnter

**2.** What does the Input class method GetKeyDown() do?
A) Returns true every frame the key is held
B) Returns true only on the frame the key is first pressed ✓
C) Returns true when the key is released
D) Detects gamepad input only

**3.** How should you apply movement forces to a player Rigidbody?
A) In Update() with AddForce
B) In FixedUpdate() with velocity or AddForce ✓
C) In LateUpdate() with position manipulation
D) In OnGUI() for immediate response

**4.** What is "coyote time" in platformer design?
A) A time delay before jumping is allowed
B) A short window after leaving ground where jumping is still possible ✓
C) The time between two jumps
D) Air acceleration modifier

**5.** Which Animator parameter type is best for storing a speed value?
A) Bool
B) Trigger
C) Float ✓
D) Integer

**6.** How do you flip a 2D sprite to face the opposite direction?
A) Rotate the GameObject 180 degrees
B) Negate the scale.x value
C) Use SetBool("FacingRight", false)
D) Both B and C ✓

**7.** What does Camera.main.ScreenToWorldPoint do?
A) Converts screen pixel position to world position ✓
B) Moves the camera to a world position
C) Calculates aiming direction
D) Detects ray-screen intersections

**8.** Which method should be used to detect if the player is touching ground?
A) OnCollisionEnter only
B) Physics.Raycast or Physics.OverlapCircle ✓
C) Just check rb.velocity.y < 0
D) A timer that counts down from jump

**9.** What is object pooling used for?
A) Storing completed objects for deletion
B) Reusing bullet/projectile instances instead of Instantiate/Destroy ✓
C) Managing player inventory
D) Tracking all active GameObjects

**10.** How do you prevent jump spam in a controller?
A) Check if input was received last frame
B) Use a jump cooldown timer or check grounded state ✓
C) Freeze the Rigidbody rotation
D) Disable input during jump animation

**Answer Key:** 1-C, 2-B, 3-B, 4-B, 5-C, 6-D, 7-A, 8-B, 9-B, 10-B

---

## Short Answer Section (5 questions, 4 points each)

**1.** Explain how you would implement acceleration-based movement (gradual speed increase) instead of instant-speed movement. Why is this better for game feel?

**Scoring Rubric (4 points):**
- Code explanation or pseudocode (2 pts)
- Game feel benefit explanation (2 pts)

**Model Answer:**
- Increase currentSpeed gradually each frame: `currentSpeed += input * acceleration * Time.deltaTime`
- Clamp to maxSpeed: `currentSpeed = Mathf.Clamp(currentSpeed, -maxSpeed, maxSpeed)`
- Apply to velocity: `rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0)`
- Better feel: Players expect gradual acceleration, not instant. Feels more responsive and weighty. More natural movement.

---

**2.** What is a jump buffer, and how would you implement it in code? Why is it important for player experience?

**Scoring Rubric (4 points):**
- Definition of jump buffer (1 pt)
- Implementation description or pseudocode (2 pts)
- Importance explanation (1 pt)

**Model Answer:**
- **Jump Buffer:** Stores jump input for a brief window (~0.05-0.1s) so player can jump slightly before landing.
- **Implementation:** Create a timer that counts down. When Space pressed, set `jumpBuffer = jumpBufferTime`. Decrement each frame. If buffer > 0 AND grounded, execute jump.
- **Importance:** Improves responsiveness. Players feel heard even if they tap jump slightly early. Reduces frustration with mistimed inputs.

---

**3.** Describe the difference between using `rb.velocity` directly and using `AddForce()` for player movement. When would you use each?

**Scoring Rubric (4 points):**
- Velocity description and use case (2 pts)
- AddForce description and use case (2 pts)

**Model Answer:**
- **rb.velocity:** Direct position change. Instant, immediate response. Good for platformers, player-controlled movement, precise feel. Doesn't respect physics mass.
- **AddForce:** Physics-based, respects mass (F = ma). More realistic. Slower, momentum-based. Good for objects pushed by environment, projectiles, physics-heavy games.
- **Use velocity for:** Player movement (platformers, responsive controls)
- **Use AddForce for:** Physics objects, knockback, explosions, environment interactions

---

**4.** How would you create a mechanic where the player can aim a gun with the mouse and fire a bullet prefab? Include ground check to prevent mid-air shooting.

**Scoring Rubric (4 points):**
- Mouse to world conversion (1 pt)
- Direction calculation (1 pt)
- Ground detection check (1 pt)
- Bullet instantiation with velocity (1 pt)

**Model Answer:**
- Convert mouse screen position to world: `Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(Input.mousePosition)`
- Calculate direction: `Vector3 shootDir = (mouseWorldPos - shootPoint.position).normalized`
- Check ground: `Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, ...)`
- Instantiate bullet: `GameObject bullet = Instantiate(bulletPrefab, shootPoint.position, ...)`
- Set velocity: `bullet.GetComponent<Rigidbody>().velocity = shootDir * bulletSpeed`

---

**5.** What is a state machine for a player controller, and what are at least 3 states you might include?

**Scoring Rubric (4 points):**
- Definition of state machine (1 pt)
- 3+ valid states with descriptions (3 pts, ~1 pt each)

**Model Answer:**
- **State Machine:** System that tracks which "state" (mode) the player is in. Only one state active at a time. Transitions between states based on conditions. Each state has different behavior (animations, speeds, abilities).
- **Example States:**
  - **Idle:** Not moving, standing still
  - **Running:** Moving horizontally
  - **Jumping:** In air after jump
  - **Falling:** In air, descending
  - **Dashing:** Special ability active
  - **Attacking:** Melee or ranged action

---

## Coding Challenge Section (3 challenges, 10 points each)

### Challenge 1: Polished Horizontal Movement (Beginner)

Write a script that implements smooth acceleration-based movement:
- Input responds immediately (snappy feel)
- Acceleration gradually increases speed
- Deceleration when input stops
- Maximum speed clamping
- Print current speed to console each frame

```csharp
using UnityEngine;

public class PolishedMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float maxSpeed = 10f;
    public float acceleration = 5f;
    public float deceleration = 8f;

    private float currentSpeed = 0f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // YOUR CODE HERE
    }
}
```

**Scoring Rubric (10 points):**
- GetComponent Rigidbody: 1 pt
- Input.GetAxis detection: 1 pt
- Acceleration calculation with Time.deltaTime: 2 pts
- Deceleration logic: 2 pts
- Speed clamping: 1 pt
- Velocity application: 1 pt
- Debug output: 1 pt
- Code clarity: 1 pt

**Model Answer:**
```csharp
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

    Debug.Log($"Speed: {currentSpeed:F2}");
}
```

---

### Challenge 2: Coyote Time Ground Detection (Intermediate)

Implement ground detection with coyote time:
- Use Physics.OverlapCircle to detect ground
- Allow jumping for 0.2 seconds after leaving ground (coyote time)
- Only allow one jump while airborne
- Use Debug.DrawRay to visualize ground detection
- Print "Can Jump: true/false" each frame

```csharp
using UnityEngine;

public class CoyoteTimeController : MonoBehaviour
{
    private Rigidbody rb;
    public float groundCheckRadius = 0.3f;
    public LayerMask groundLayer;
    public float jumpForce = 5f;
    public float coyoteTime = 0.2f;

    private float coyoteCounter = 0f;

    // YOUR CODE HERE
}
```

**Scoring Rubric (10 points):**
- Physics.OverlapCircle usage: 2 pts
- Coyote timer countdown logic: 2 pts
- Reset coyote on ground touch: 1 pt
- Jump execution with coyote check: 2 pts
- Debug.DrawRay visualization: 1 pt
- Debug.Log output: 1 pt
- Code clarity: 1 pt

**Model Answer:**
```csharp
private void Update()
{
    // Update coyote time
    if (IsGrounded())
    {
        coyoteCounter = coyoteTime;
    }
    else
    {
        coyoteCounter -= Time.deltaTime;
    }

    // Jump if coyote active
    if (Input.GetKeyDown(KeyCode.Space) && coyoteCounter > 0)
    {
        Jump();
    }

    Debug.Log("Can Jump: " + (coyoteCounter > 0));
}

private void Jump()
{
    rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
    rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    coyoteCounter = 0;
}

private bool IsGrounded()
{
    Vector3 checkPos = transform.position + Vector3.down * 0.5f;
    Collider[] hits = Physics.OverlapSphere(checkPos, groundCheckRadius, groundLayer);

    Debug.DrawWireSphere(checkPos, groundCheckRadius, hits.Length > 0 ? Color.green : Color.red);

    return hits.Length > 0;
}
```

---

### Challenge 3: Aim and Shoot System (Advanced)

Create a complete shooting system:
- Detect mouse position with Camera.main.ScreenToWorldPoint
- Calculate direction from player to mouse
- Only allow shooting when grounded (use raycasting)
- Instantiate bullet prefab with correct velocity
- Implement 0.3-second cooldown between shots
- Update sprite rotation to face aim direction
- Visualize aim direction with Debug.DrawRay

```csharp
using UnityEngine;

public class AimAndShoot : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform shootPoint;
    public float bulletSpeed = 10f;
    public float shootCooldown = 0.3f;
    public LayerMask groundLayer;

    private float shootTimer = 0f;
    private SpriteRenderer spriteRenderer;

    private void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();
    }

    private void Update()
    {
        // YOUR CODE HERE
    }
}
```

**Scoring Rubric (10 points):**
- ScreenToWorldPoint conversion: 1 pt
- Direction calculation and normalization: 1 pt
- Grounded check with raycasting: 1 pt
- Bullet instantiation: 1 pt
- Velocity assignment: 1 pt
- Cooldown timer logic: 1 pt
- Sprite rotation/flipping: 1 pt
- Debug.DrawRay visualization: 1 pt
- Code organization/clarity: 1 pt

**Model Answer:**
```csharp
private void Update()
{
    shootTimer -= Time.deltaTime;

    // Get aim direction
    Vector3 mouseScreenPos = Input.mousePosition;
    mouseScreenPos.z = 10f;
    Vector3 mouseWorldPos = Camera.main.ScreenToWorldPoint(mouseScreenPos);
    Vector3 aimDir = (mouseWorldPos - shootPoint.position).normalized;

    // Face aim direction
    spriteRenderer.flipX = aimDir.x < 0;

    // Visualize aim
    Debug.DrawRay(shootPoint.position, aimDir * 10f, Color.yellow);

    // Shoot if ready and grounded
    if (Input.GetMouseButtonDown(0) && shootTimer <= 0 && IsGrounded())
    {
        GameObject bullet = Instantiate(bulletPrefab, shootPoint.position, Quaternion.identity);
        bullet.GetComponent<Rigidbody>().velocity = aimDir * bulletSpeed;
        shootTimer = shootCooldown;
        Destroy(bullet, 5f);
    }
}

private bool IsGrounded()
{
    return Physics.Raycast(
        transform.position + Vector3.down * 0.5f,
        Vector3.down,
        0.1f,
        groundLayer
    );
}
```

---

## Study Guide for Review

**Key Topics:**
- Input detection: GetKey, GetKeyDown, GetAxis, GetAxisRaw
- Axis configuration in Input Manager
- Movement patterns: velocity, acceleration, physics-based
- Ground detection: Raycast, OverlapCircle, multiple checks
- Coyote time and jump buffering implementation
- Animator integration and parameter types
- Sprite direction and flipping
- 2D animation state machines
- Mouse input and world space conversion
- Projectile spawning and pooling concepts
- Cooldown and timer-based systems
- Special abilities: dash, sprint, charge attacks
- Game feel: acceleration curves, input feedback, responsiveness

**Practice Focus Areas:**
- Tweak movement values for different feels
- Test keyboard and gamepad input
- Build different controller types
- Debug input responsiveness
- Iterate on feel through playtesting
- Combine multiple mechanics into cohesive controllers

---

## Scoring Rubric Summary

| Section | Points | Passing |
|---------|--------|---------|
| Multiple Choice | 20 | 70% = 14 pts |
| Short Answer | 20 | 70% = 14 pts |
| Coding Challenges | 30 | 70% = 21 pts |
| **TOTAL** | **70** | **49+** |

**Grade Scale:**
- A: 63-70 (90-100%)
- B: 56-62 (80-89%)
- C: 49-55 (70-79%)
- Below C: Needs remediation

---

## Extra Credit (+5 points max)

**Build a complete 2D platformer controller** demonstrating at least 6 concepts from this unit:
- Smooth horizontal movement with acceleration
- Jump with coyote time and jump buffer
- Ground detection visualization (Raycast or OverlapCircle)
- Animation state machine (Idle, Running, Jumping, Falling)
- Sprite direction flipping
- Dash ability with cooldown
- BONUS: Wall sliding, double jump, or air control

**Requirements:**
- Well-commented code with clear variable names
- All movement values tweakable in Inspector
- Debug visualizations (rays, spheres, logs)
- Playable test level with platforms
- Feels polished and responsive

---

## Notes for Remediation

If a student scores below 49 (not passing):
1. Review Unit Overview and Daily Notes for Days 1-22
2. Work through at least 5 practice problems from UnitPractice.md
3. Focus on problem areas from assessment
4. Consider starting with Day 1-6 (movement foundations) and rebuilding skills
5. Schedule a retake (must pass with 70%+ to credit)

---

## Real-World Connection

The skills in this unit are used in:
- AAA games: Polished player controllers are hallmarks of quality
- Indie games: Feel matters more than graphics/budget
- Mobile games: Responsive input is critical for touch controls
- VR games: Comfort and responsiveness prevent motion sickness
- Competitive games: Players demand tight, precise controls

Professional game designers spend weeks tuning movement "feel" because it directly impacts how much players enjoy the game.

