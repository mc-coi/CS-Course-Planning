# Unit 6 Answer Key: 2D Game Development

Comprehensive answer key for all 15 practice problems covering sprites, animation, tilemaps, physics, and camera systems.

---

## Problem 1: Sprite Import Settings

### Solution

For a 2D platformer character sprite:
- **Texture Type:** Sprite (2D and UI)
- **Sprite Mode:** Single (if one sprite) or Multiple (if sprite sheet)
- **Pixels Per Unit:** 100 (standard; adjust based on art style)
- **Filter Mode:** Point (Pixel Perfect for pixel art)
- **Compression:** None (for quality, or use appropriate quality setting)

### What Success Looks Like
- Sprite appears crisp and pixel-perfect in scene
- No blurring or anti-aliasing artifacts
- Correct scaling relative to world units

### Common Mistakes
- Using Compressed format (blurs pixel art)
- Filter Mode set to Bilinear (makes pixel art fuzzy)
- PPU mismatch (sprite too large or small)

---

## Problem 2: Animator Setup

### Solution

1. Import sprite sequence (4 frames of walk animation)
2. Create AnimationClip with frames dragged into Animator
3. Set samples to 12 FPS for smooth walking
4. Create Animator Controller
5. Add state for "Walk" animation
6. Add transition: Idle → Walk when speed > 0
7. Add transition: Walk → Idle when speed = 0

### What Success Looks Like
- Character smoothly animates between Idle and Walk states
- Speed parameter controls state transitions
- Animation loops seamlessly

### Common Mistakes
- Wrong frame order in animation clip
- Sample rate too high or low (animation speed wrong)
- Missing exit transitions (stuck in Walk state)

---

## Problem 3: Tilemap Creation

### Solution

1. Window → 2D → Tile Palette
2. Create new Palette, drag sprites into it
3. Create Tilemap in scene (right-click Hierarchy → 2D → Tilemap)
4. Paint tiles using Tile Palette brush
5. Add TilemapCollider2D for collisions
6. Create multiple tilemaps for layers (ground, background, foreground)

### What Success Looks Like
- Tilemap paints smoothly and aligns perfectly
- Collisions work on painted tiles
- Multiple tilemaps layer correctly

### Common Mistakes
- TilemapCollider2D missing (no collisions)
- Collider on wrong tilemap (layers don't collide properly)
- Palette not set to Paint mode

---

## Problem 4: Sorting Layers

### Solution

**Layer order (back to front):**
- Background (0)
- Terrain (1)
- Enemies (2)
- Player (3)
- Effects (4)
- UI (5)

(Higher number = rendered in front)

### What Success Looks Like
- Objects appear in correct depth order
- Player visible in front of enemies
- UI appears on top of everything
- No overlapping confusion

### Common Mistakes
- Sorting layers not created (everything on Default)
- Player sorting layer below enemies (can't see player)
- UI not on highest layer (hidden behind game world)

---

## Problem 5: Physics2D Jump

### Solution

```csharp
private Rigidbody2D rb;
private bool isGrounded = false;

void Update()
{
    Collider2D[] groundColliders = Physics2D.OverlapCircleAll(
        (Vector2)transform.position + Vector2.down * 0.5f, 0.2f
    );
    isGrounded = groundColliders.Length > 1;  // More than self

    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        rb.velocity = new Vector2(rb.velocity.x, 5f);
}
```

### What Success Looks Like
- Player jumps on Space press
- Only jumps when grounded
- Jump height consistent
- Falls back down due to gravity

### Common Mistakes
- Using > 0 instead of > 1 (player collider counts as hit)
- Not checking isGrounded (infinite jumping)
- Setting velocity before checking ground (might jump mid-air)

---

## Problem 6: Parallax Scrolling

### Solution

```csharp
public float parallaxFactor = 0.5f;
private Vector3 startPos;

void Start()
{
    startPos = transform.position;
}

void LateUpdate()
{
    Vector3 newPos = startPos + Camera.main.transform.position * parallaxFactor;
    transform.position = newPos;
}
```

### What Success Looks Like
- Background moves slower than camera
- Creates depth illusion
- Factor 0.5 moves at half camera speed
- Smooth continuous parallax

### Common Mistakes
- Using Update instead of LateUpdate (jittery movement)
- Not storing startPos (accumulates offset)
- Factor > 1 (background moves faster than player)

---

## Problem 7: Sprite Animation Blending

### Solution

**Animator Transitions:**
1. Create three animation clips: Idle, Walk, Jump
2. Idle → Walk (speed > 0.1)
3. Walk → Idle (speed < 0.1)
4. Any State → Jump (Jump trigger)
5. Jump → Idle (onLand trigger)
6. Set all transitions to blend (duration 0.1s)

### What Success Looks Like
- Smooth transitions between animation states
- No popping or sudden changes
- Parameters control state flow correctly

### Common Mistakes
- Transitions not set to blend (instant switching)
- Triggers not being reset (stuck in Jump)
- Conditions are too sensitive (flickering between states)

---

## Problem 8: Moving Platform

### Solution

```csharp
public Vector3 startPos, endPos;
public float moveSpeed = 2f;
private bool movingToEnd = true;

void Update()
{
    if (movingToEnd)
        transform.position = Vector3.Lerp(transform.position, endPos, moveSpeed * Time.deltaTime);
    else
        transform.position = Vector3.Lerp(transform.position, startPos, moveSpeed * Time.deltaTime);

    if (Vector3.Distance(transform.position, endPos) < 0.1f)
        movingToEnd = false;
    else if (Vector3.Distance(transform.position, startPos) < 0.1f)
        movingToEnd = true;
}
```

### What Success Looks Like
- Platform smoothly moves between start and end positions
- Player carried with platform
- Motion continuous and loops seamlessly
- Speed adjustable

### Common Mistakes
- Not using Lerp (jittery movement)
- Turning around before reaching destination (doesn't reach waypoint)
- Speed too fast or too slow

---

## Problem 9: Camera Follow

### Solution

```csharp
public Transform player;
public float smoothSpeed = 5f;

void LateUpdate()
{
    Vector3 targetPos = new Vector3(player.position.x, player.position.y, -10);
    transform.position = Vector3.Lerp(transform.position, targetPos, smoothSpeed * Time.deltaTime);
}
```

### What Success Looks Like
- Camera smoothly follows player
- Z position stays at -10 (2D standard)
- Smooth damping effect
- Player stays in view

### Common Mistakes
- Using Update instead of LateUpdate (camera updates before player)
- Smoothness value wrong (too fast is jittery, too slow is laggy)
- Not setting Z position (camera might be in front of scene)

---

## Problem 10: One-Way Platform

### Solution

```csharp
void OnCollisionEnter2D(Collision2D col)
{
    if (col.gameObject.CompareTag("Player"))
    {
        Rigidbody2D rb = col.gameObject.GetComponent<Rigidbody2D>();
        // Only collide if player coming from below
        if (rb.velocity.y < 0)  // Moving downward
            Physics2D.IgnoreCollision(GetComponent<Collider2D>(), col.collider, false);
    }
}

void OnCollisionExit2D(Collision2D col)
{
    Physics2D.IgnoreCollision(GetComponent<Collider2D>(), col.collider, true);
}
```

### What Success Looks Like
- Player passes through from below
- Player stands on platform from above
- Relative velocity determines behavior

### Common Mistakes
- Using > 0 instead of < 0 (inverted direction)
- Not resetting collision on exit (might stick)
- Checking absolute velocity instead of relative

---

## Problem 11: Animated Tilemap

### Solution

1. Create sprite sheet with water animation frames
2. Window → 2D → Tile Palette
3. In Tile Palette, right-click tile → Edit
4. Create AnimatedTile component
5. Add animation frames in order
6. Set frame duration (e.g., 0.1 seconds)
7. Paint as normal tile

### What Success Looks Like
- Tiles animate in tilemap
- Animation loops smoothly
- Different tiles can have different animations
- Synchronization across tiles (all animate together)

### Common Mistakes
- Frames in wrong order (animation jumps)
- Frame duration too short or long
- Animation component not applied to tile

---

## Problem 12: Pixel Perfect Rendering

### Solution

1. **Sprite import:** Filter Mode = Point
2. **Camera:** PPU (Pixels Per Unit) must match sprite import PPU (usually 100)
3. **Project Settings:** Disable anti-aliasing
4. **Positioning:** Place objects on whole pixel coordinates (no 1.5, use integers)

### What Success Looks Like
- Sprites appear crisp and sharp
- No blurring or anti-aliasing artifacts
- Consistent pixel size across screen
- Professional pixel art appearance

### Common Mistakes
- Mismatched PPU (sprite looks wrong size)
- Anti-aliasing enabled (blurs edges)
- Objects positioned at fractional coordinates (subpixel rendering)

---

## Problem 13: Multiple Animation Parameters

### Solution

```csharp
private Animator anim;

void Update()
{
    float speed = Mathf.Abs(Input.GetAxis("Horizontal"));
    anim.SetFloat("speed", speed);

    if (Input.GetAxis("Horizontal") > 0)
        anim.SetInteger("direction", 1);
    else if (Input.GetAxis("Horizontal") < 0)
        anim.SetInteger("direction", -1);
}

// Animator Transitions:
// Idle (speed == 0) → Walk Right (speed > 0 AND direction == 1)
// Idle (speed == 0) → Walk Left (speed > 0 AND direction == -1)
// Walk → Idle (speed == 0)
```

### What Success Looks Like
- Character animates based on both speed and direction
- Facing direction respected in animations
- Smooth transitions between states

### Common Mistakes
- Using single speed parameter (can't differentiate left/right)
- Not resetting direction (stuck facing one way)
- Multiple parameters not synced

---

## Problem 14: Slope Physics

### Solution

Use **EdgeCollider2D** instead of BoxCollider2D for slopes. Shape the edge collider to follow the slope geometry. Physics2D handles the sliding naturally without special code.

### What Success Looks Like
- Player can walk up slopes smoothly
- Slides down when too steep
- Foot contact maintained naturally
- No bouncing or clipping

### Common Mistakes
- Using BoxCollider2D on slopes (feet don't touch ground)
- EdgeCollider2D shape doesn't match visuals
- Gravity or friction settings wrong

---

## Problem 15: Cinemachine Virtual Camera

### Solution

1. GameObject → Cinemachine → 2D Camera
2. Assign: Follow = Player, Look At = Player
3. Damping: Adjust X/Y damping for smoothness (0.5-1.5 typical)
4. Add Confiner2D component
5. Create bounds polygon or box for level
6. Camera stays within bounds while following

### What Success Looks Like
- Camera smoothly follows player with damping
- Stays within level bounds
- No sudden jumps or jitter
- Professional cinematic feel

### Common Mistakes
- No damping (camera tracks instantly, jittery)
- Confiner bounds too small (clips player from view)
- Wrong follow target (follows wrong object)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | Sprite Import | Beginner |
| 2 | Animation Setup | Beginner |
| 3 | Tilemap Creation | Intermediate |
| 4 | Sorting Layers | Beginner |
| 5 | Physics2D Jump | Intermediate |
| 6 | Parallax Scrolling | Intermediate |
| 7 | Animation Blending | Intermediate |
| 8 | Moving Platforms | Intermediate |
| 9 | Camera Follow | Beginner |
| 10 | One-Way Platforms | Advanced |
| 11 | Animated Tiles | Intermediate |
| 12 | Pixel Perfect | Intermediate |
| 13 | Multi-Parameter Animation | Advanced |
| 14 | Slope Physics | Intermediate |
| 15 | Cinemachine Setup | Advanced |
