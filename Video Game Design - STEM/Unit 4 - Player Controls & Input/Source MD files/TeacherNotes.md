# Unit 4 - Player Controls & Input: Teacher Misconception & Callout Guide

## Overview

This unit teaches students to build a responsive player controller—the foundation of all gameplay. The challenge is that "feel" is subjective and hard to debug: students write technically correct code that feels sluggish or unresponsive. In a STEM semester course, you can't afford weeks of iteration to develop intuition. The biggest pitfalls are skipping Time.deltaTime (causing frame-rate-dependent movement), confusing GetKey with GetAxis (misses smoothing), and building fragile ground detection. Unlike the year-long course, provide a working controller template and teach students to customize it—don't have them build from scratch. Use 🚨 flags to know when to pause everything.

---

## Misconceptions by Topic

### Movement & Time.deltaTime (Days 1–3)

**⚠️ Misconception:** "My player moves, but it's faster or slower depending on the computer. The game must have a bug."

**What it looks like:** A student moves the player without Time.deltaTime. On a slow machine, the player crawls; on a fast machine, the player flies.

**Why students think this:** They think of movement as "move X units" not "move X units per second."

**How to address it:** Make it time-based. "Without Time.deltaTime, your player moves X units per frame—and frames per second vary by machine. With Time.deltaTime, your player moves X units per second, regardless of frame rate. Always multiply movement by Time.deltaTime: `transform.position += direction * speed * Time.deltaTime;`. Think of it as: 'speed is miles per HOUR, not miles per FRAME.'"

🚨 **STEM Priority — STOP THE CLASS:** If any students are building movement without Time.deltaTime, stop immediately. Every project will break on a different machine.

```csharp
// WRONG — frame-rate dependent
transform.position += Vector3.right * speed;

// RIGHT — time-based, consistent across machines
transform.position += Vector3.right * speed * Time.deltaTime;
```

---

**⚠️ Misconception:** "I'm using Input.GetKey() for movement and it works, but the movement feels jerky and digital—there's no acceleration."

**What it looks like:** A student uses `if (Input.GetKey(KeyCode.D)) rb.velocity = new Vector3(speed, rb.velocity.y, 0);`. Movement snaps on/off with no ramp-up.

**Why students think this:** GetKey() is the intuitive "is this key held" check. They don't know GetAxis exists.

**How to address it:** Use GetAxis for smooth movement. "`Input.GetAxis('Horizontal')` returns a float from -1 to 1 and smoothly ramps up/down when the key is held or released. `Input.GetAxisRaw('Horizontal')` returns exactly -1, 0, or 1 (no ramping—good for tight platformers). GetKey() is best for one-time events like jumping; GetAxis/GetAxisRaw are better for continuous movement."

```csharp
// Smooth movement with acceleration
float moveInput = Input.GetAxis("Horizontal");         // -1 to 1, with smoothing
float moveInput = Input.GetAxisRaw("Horizontal");      // -1, 0, or 1, no smoothing (tighter)

rb.velocity = new Vector3(moveInput * speed, rb.velocity.y, 0);
```

---

**⚠️ Misconception:** "My player accelerates but never reaches maximum speed. Or it reaches max speed instantly with no feel."

**What it looks like:** A student wants acceleration but either can't cap the velocity or the acceleration is so fast it might as well not exist.

**Why students think this:** They don't know how to interpolate toward a target velocity.

**How to address it:** Use Lerp or a manual clamp. "To add acceleration and a top speed: use `Mathf.Lerp()` to gradually approach the target velocity. Or add force in FixedUpdate() and cap: `if (rb.velocity.magnitude > maxSpeed) rb.velocity = rb.velocity.normalized * maxSpeed;`. Lerp gives smooth 'feel'; force+cap gives more physical behavior."

```csharp
// Smooth acceleration with Lerp
float targetSpeed = moveInput * maxSpeed;
float currentSpeed = Mathf.Lerp(rb.velocity.x, targetSpeed, acceleration * Time.fixedDeltaTime);
rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
```

---

### Jump Mechanics (Days 3–5)

**⚠️ Misconception:** "My jump works, but you can jump infinitely. I need to add a jump counter."

**What it looks like:** A student adds a jump counter (maxJumps = 2) but the real problem is their ground detection is broken.

**Why students think this:** They see the symptom (infinite jump) but not the cause (broken ground detection).

**How to address it:** Fix ground detection first. "Before adding jump counters, make sure isGrounded is actually working. Test: add `Debug.Log(isGrounded);` and watch the Console while jumping. If isGrounded never goes false, the detection is broken. Use a downward raycast to detect ground reliably. Once ground detection is solid, add a jump counter if you want double-jump."

🚨 **STEM Priority — Handle 1-on-1:** This is the most common jump bug. Tackle it before students build double-jump on a broken foundation.

```csharp
// Solid ground detection with raycast
[SerializeField] LayerMask groundLayer;
bool isGrounded;

void Update()
{
    isGrounded = Physics.Raycast(transform.position, Vector3.down, 0.6f, groundLayer);

    if (Input.GetButtonDown("Jump") && isGrounded)
    {
        rb.velocity = new Vector3(rb.velocity.x, jumpForce, 0);
    }
}
```

---

**⚠️ Misconception:** "My jump feels floaty. I want it to feel like Mario—snappy going up, fast coming down."

**What it looks like:** A student's jump uses constant gravity. The character floats at the peak before falling slowly.

**Why students think this:** Default gravity applies uniformly. They don't know you can change gravity mid-jump.

**How to address it:** Implement variable jump gravity. "Professional platformers use different gravity when going up vs. falling. Apply extra gravity when falling: `if (rb.velocity.y < 0) rb.velocity += Vector3.up * Physics.gravity.y * (fallMultiplier - 1) * Time.deltaTime;`. Also apply slightly extra gravity when the jump button is released early (for variable jump height)."

```csharp
// Better jump feel
[SerializeField] float fallMultiplier = 2.5f;
[SerializeField] float lowJumpMultiplier = 2f;

void Update()
{
    if (rb.velocity.y < 0)
    {
        rb.velocity += Vector3.up * Physics.gravity.y * (fallMultiplier - 1) * Time.deltaTime;
    }
    else if (rb.velocity.y > 0 && !Input.GetButton("Jump"))
    {
        rb.velocity += Vector3.up * Physics.gravity.y * (lowJumpMultiplier - 1) * Time.deltaTime;
    }
}
```

---

**⚠️ Misconception:** "I let go of the jump button but the player still jumps to full height. I want shorter jumps when I tap."

**What it looks like:** Jump height is fixed regardless of how long the button is held.

**Why students think this:** They set velocity once on key press. They don't know about variable jump height.

**How to address it:** Cut velocity when button is released. "For variable jump height: when the jump button is released while still moving upward, cut the vertical velocity: `if (Input.GetButtonUp('Jump') && rb.velocity.y > 0) rb.velocity = new Vector3(rb.velocity.x, rb.velocity.y * jumpCutMultiplier, 0);`. Set jumpCutMultiplier to 0.5 (half height on release) to start."

---

### Coyote Time & Input Buffering (Days 5–6)

**⚠️ Misconception:** "My player can't jump right at the edge of a platform. It feels unresponsive."

**What it looks like:** A student's character falls off a ledge and the player presses jump immediately after—but the jump doesn't register because isGrounded went false.

**Why students think this:** Ground detection is binary—either you're grounded or you're not.

**How to address it:** Implement coyote time. "Coyote time gives the player a brief window (~0.1s) to jump after walking off a ledge. Track: `coyoteTimeCounter -= Time.deltaTime;` and reset to `coyoteTime` when grounded. Allow jump if `coyoteTimeCounter > 0`. This makes platformers feel fair without breaking physics."

🚨 **STEM Priority — Monitor:** Add this to the template. Students will notice the missing feel without knowing the name.

```csharp
float coyoteTime = 0.1f;
float coyoteTimeCounter;

void Update()
{
    if (isGrounded)
        coyoteTimeCounter = coyoteTime;
    else
        coyoteTimeCounter -= Time.deltaTime;

    if (Input.GetButtonDown("Jump") && coyoteTimeCounter > 0f)
    {
        rb.velocity = new Vector3(rb.velocity.x, jumpForce, 0);
        coyoteTimeCounter = 0f; // prevent double-use
    }
}
```

---

**⚠️ Misconception:** "Sometimes when I press jump just before landing, nothing happens. The input is eaten."

**What it looks like:** The player presses jump a few frames before landing, but since isGrounded is still false, the jump is ignored.

**Why students think this:** Input is checked only in the same frame it's pressed.

**How to address it:** Add jump buffering. "Jump buffering stores the jump request briefly. When the player presses jump, set `jumpBufferCounter = jumpBufferTime;`. Decrement each frame. On landing, if `jumpBufferCounter > 0`, jump immediately. This makes inputs feel responsive even with slight timing errors."

```csharp
float jumpBufferTime = 0.15f;
float jumpBufferCounter;

void Update()
{
    if (Input.GetButtonDown("Jump"))
        jumpBufferCounter = jumpBufferTime;
    else
        jumpBufferCounter -= Time.deltaTime;

    if (jumpBufferCounter > 0f && coyoteTimeCounter > 0f)
    {
        rb.velocity = new Vector3(rb.velocity.x, jumpForce, 0);
        jumpBufferCounter = 0f;
        coyoteTimeCounter = 0f;
    }
}
```

---

### Projectiles & Shooting (Days 6–7)

**⚠️ Misconception:** "I Instantiate() a bullet every frame while the shoot button is held. My game creates thousands of bullets and freezes."

**What it looks like:** A student uses `if (Input.GetKey(KeyCode.Space)) Instantiate(bullet, ...)` without a cooldown timer.

**Why students think this:** GetKey() fires every frame. They don't think about rate limiting.

**How to address it:** Add a cooldown. "Use a cooldown timer: set a `shootCooldown` float and decrement each frame. Only fire when it reaches 0. Reset to the desired fire rate (e.g., 0.3 seconds) after firing. This controls the fire rate and prevents bullet spam."

```csharp
float shootCooldown = 0f;
[SerializeField] float fireRate = 0.3f;

void Update()
{
    shootCooldown -= Time.deltaTime;

    if (Input.GetKey(KeyCode.Space) && shootCooldown <= 0f)
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
        shootCooldown = fireRate;
    }
}
```

---

**⚠️ Misconception:** "My bullet Prefab moves with AddForce(), but when I Instantiate it, it doesn't move."

**What it looks like:** A student Instantiates a bullet with a Rigidbody and expects AddForce() called inside the Prefab's Start() to fire it. Nothing happens.

**Why students think this:** They think AddForce in Start() is like setting an initial velocity.

**How to address it:** Set velocity directly at spawn. "AddForce() in Start() works, but it's unreliable because it fires one frame after Instantiate(). Instead, get a reference to the spawned object's Rigidbody and set velocity immediately: `GameObject b = Instantiate(bulletPrefab, ...); b.GetComponent<Rigidbody>().velocity = transform.right * bulletSpeed;`. This fires the bullet the frame it's created."

---

## Whole-Class Warning Signs

- **Nobody is multiplying movement by Time.deltaTime.** Stop and address before any movement systems are built. This is non-negotiable.

- **Everyone's jump is broken or allows infinite jumping.** Ground detection is the issue. Do a whole-class raycast demo and provide a working isGrounded template.

- **Players feel floaty with no response feel.** They're using default gravity with no fall multiplier. Show the whole class the fall gravity pattern—it's a standard technique.

- **Bullets are flooding the scene and tanking frame rate.** Cooldown timers need to be part of the shooting template. Show the class the pattern and enforce it.

- **Students can't figure out GetAxis vs GetKey.** Demo both in the Console. `Input.GetAxis("Horizontal")` returns 0.7 when partially pressed; `Input.GetKey(KeyCode.A)` returns true/false. Show the difference in a 5-minute live demo.

---

## Questions That Reveal Understanding

1. **"Why do we multiply movement by Time.deltaTime?"**
   - Good answer: "Without it, movement speed depends on frame rate. With it, movement is measured in units per second—consistent on all machines."
   - Red flag: "I'm not sure" or "It makes it slower." (Fundamental gap—address immediately.)

2. **"What's the difference between Input.GetKey() and Input.GetAxis()?"**
   - Good answer: "GetKey() returns bool (on/off). GetAxis() returns a float (-1 to 1) with built-in acceleration/deceleration. GetAxisRaw() is like GetKey but returns -1/0/1 without smoothing."
   - Red flag: "They're the same but different names." (They'll use GetKey for everything.)

3. **"Your player can jump infinitely. What's the bug and how do you fix it?"**
   - Good answer: "isGrounded is always true, or never becomes false. Fix: use a downward raycast on a dedicated ground layer instead of OnCollisionEnter."
   - Red flag: "Add a maxJumps counter." (Treating the symptom, not the cause.)

4. **"What is coyote time and why does it matter?"**
   - Good answer: "A short window where you can still jump after walking off a ledge. It makes platformers feel fair—your input isn't punished for a tiny frame gap."
   - Red flag: "I've never heard of it." (Acceptable—explain and show the code. It's not intuitive.)

5. **"You Instantiate a bullet but it doesn't move. What do you check first?"**
   - Good answer: "Check if the Rigidbody velocity is being set. Don't rely on AddForce in Start—get the component reference and set velocity at the spawn site."
   - Red flag: "Check if the Prefab has a Rigidbody" (correct but incomplete—the velocity must be set by the spawner).

---

## Common Student Questions & How to Answer Them

**Q1: "My player slides after I stop pressing keys. How do I make it stop immediately?"**

*A:* "Zero out velocity when there's no input: `if (Mathf.Abs(moveInput) < 0.01f) rb.velocity = new Vector3(0, rb.velocity.y, 0);`. Or use a high drag value on the Rigidbody (Linear Drag = 5–10). Direct velocity zeroing gives tighter control; drag gives a more physical feel."

---

**Q2: "How do I make the player face the direction they're moving?"**

*A:* "Use SpriteRenderer.flipX for 2D: `spriteRenderer.flipX = (rb.velocity.x < 0);`. For 3D, use transform.localScale: `transform.localScale = new Vector3(Mathf.Sign(rb.velocity.x), 1, 1);`. Or use `transform.LookAt()` for 3D characters. For 2D games, flipX is the simplest approach."

---

**Q3: "My player can walk up walls by holding the movement key against them. How do I fix it?"**

*A:* "Zero out horizontal velocity when touching a wall and not on the ground. Or use a Physics Material with zero friction on the player's collider. Or use a layer-based approach: raycasting horizontally to detect walls and blocking movement if a wall is detected. The Physics Material approach is quickest."

---

**Q4: "How do I make the camera follow the player smoothly?"**

*A:* "In a simple script on the Camera: `transform.position = Vector3.Lerp(transform.position, target.position + offset, smoothSpeed * Time.deltaTime);`. The Lerp makes it lag behind the player slightly. Set smoothSpeed to 5–10. For advanced behavior, use Cinemachine (Window → Package Manager → Cinemachine → Virtual Camera)."

---

**Q5: "My player movement works in the Scene view but in the Game view it's mirrored or in the wrong direction. What's wrong?"**

*A:* "Check the player's initial rotation in the Inspector. If it's rotated 180 degrees on Y, forward/backward are flipped. Reset the rotation to (0, 0, 0) and make sure your sprite/mesh is facing the right direction in its default state. Also check that Camera is looking in the right direction (usually -Z for 2D)."

---

## Analogies That Work

1. **"Time.deltaTime is like converting speed units. You wouldn't say 'I drive 60 miles per frame'—you'd say '60 miles per hour.' Time.deltaTime converts your speed from 'per frame' to 'per second.' Same concept, different unit."**
   - Makes Time.deltaTime immediately intuitive.

2. **"Coyote time is named after Wile E. Coyote, who runs off a cliff but doesn't fall until he looks down. In games, the player gets a tiny window to jump after walking off the edge—the 'looking down' moment is when coyote time expires."**
   - Students remember this instantly.

3. **"Jump buffering is like a queue at a checkout. You press the button before you're ready (not grounded), but the cashier (game) remembers your request and serves you as soon as they can (on landing)."**
   - Makes input buffering feel natural.

---

## Unity-Specific Gotchas

- **Input.GetButtonDown() vs Input.GetButton()** — GetButtonDown() fires ONCE on the frame the button is pressed; GetButton() fires every frame it's held. Use GetButtonDown() for jump (one press = one jump) and GetButton() for fire (hold to shoot).

- **GetAxis() has built-in smoothing that can feel wrong for fast games.** Use `Input.GetAxisRaw("Horizontal")` for instant -1/0/1 response with no ramp-up. Year-long students can explore the difference; STEM students should default to GetAxisRaw for platformers.

- **Rigidbody2D.velocity vs Rigidbody.velocity** — if you're in a 2D project, the component is Rigidbody2D and uses Vector2. `rb.velocity = new Vector2(speed, rb.velocity.y);`. The `y` component preserve is the same pattern, just with Vector2.

- **transform.right vs Vector3.right** — `Vector3.right` is always (1, 0, 0) in world space. `transform.right` is the object's local right direction (affected by rotation). For a rotated bullet, use `transform.right` so it fires in the direction the object is facing.

- **Instantiate() returns Object, not the specific type** — cast the result: `GameObject bullet = Instantiate(bulletPrefab, ...) as GameObject;`. Or use the generic version: `Rigidbody rb = Instantiate(bulletPrefab, ...).GetComponent<Rigidbody>();`.

- **Cooldown timers must be decremented in Update(), not FixedUpdate()** — cooldown uses real time (seconds), not physics steps. Always put `cooldown -= Time.deltaTime;` in Update().

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
