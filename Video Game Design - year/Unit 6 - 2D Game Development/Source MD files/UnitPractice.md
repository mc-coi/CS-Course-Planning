# Unit 6 Practice Problems

15 problems covering sprites, animation, tilemaps, physics, and camera.

---

## Problem 1: Sprite Import Settings (Beginner)
You're importing a character sprite for a 2D platformer. What settings would you use?

<details><summary>Solution</summary>
- Texture Type: Sprite (2D and UI)
- Sprite Mode: Single
- Pixels Per Unit: 100
- Filter Mode: Point (Pixel Perfect)
- Compression: None (quality)
</details>

---

## Problem 2: Animator Setup (Beginner)
How do you create an animation that plays when the player walks?

<details><summary>Solution</summary>
1. Import sprite sequence (4 frames)
2. Create AnimationClip with frames
3. Set samples to 12 (FPS)
4. Create Animator Controller
5. Add state for "Walk" animation
6. Transition from Idle to Walk when speed > 0
</details>

---

## Problem 3: Tilemap Creation (Intermediate)
Describe steps to create a tilemap-based level.

<details><summary>Solution</summary>
1. Window → 2D → Tile Palette
2. Create new Palette, drag sprites into it
3. Create Tilemap in scene
4. Paint tiles using Tile Palette
5. Add TilemapCollider2D for collisions
6. Create multiple tilemaps for layers
</details>

---

## Problem 4: Sorting Layers (Beginner)
You have background, terrain, player, and UI. In what order should sorting layers be?

<details><summary>Solution</summary>
- Background (0)
- Terrain (1)
- Enemies (2)
- Player (3)
- Effects (4)
- UI (5)
(Higher number = rendered in front)
</details>

---

## Problem 5: Physics2D Jump (Challenge)
Write a jump mechanic with ground detection.

<details><summary>Solution</summary>
```csharp
private Rigidbody2D rb;
private bool isGrounded = false;

void Update()
{
    Collider2D[] groundColliders = Physics2D.OverlapCircleAll(
        (Vector2)transform.position + Vector2.down * 0.5f, 0.2f
    );
    isGrounded = groundColliders.Length > 1;
    
    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        rb.velocity = new Vector2(rb.velocity.x, 5f);
}
```
</details>

---

## Problem 6: Parallax Scrolling (Intermediate)
How would you implement parallax on a background layer?

<details><summary>Solution</summary>
```csharp
public float parallaxFactor = 0.5f;
private Vector3 startPos;

void LateUpdate()
{
    Vector3 newPos = startPos + Camera.main.transform.position * parallaxFactor;
    transform.position = newPos;
}
```
</details>

---

## Problem 7: Sprite Animation Blending (Intermediate)
Create transitions between Idle, Walk, and Jump animations.

<details><summary>Solution</summary>
1. Create three animation clips
2. In Animator: Idle → Walk (speed > 0), Walk → Idle (speed == 0)
3. Any State → Jump (onJump trigger)
4. Jump → Idle (onLand trigger)
5. Set transitions to blend (duration 0.1s)
</details>

---

## Problem 8: Moving Platform (Challenge)
Create a platform that moves up and down, carrying the player.

<details><summary>Solution</summary>
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
</details>

---

## Problem 9: Camera Follow (Beginner)
Write a simple camera follow script for a 2D platformer.

<details><summary>Solution</summary>
```csharp
public Transform player;
public float smoothSpeed = 5f;

void LateUpdate()
{
    Vector3 targetPos = new Vector3(player.position.x, player.position.y, -10);
    transform.position = Vector3.Lerp(transform.position, targetPos, smoothSpeed * Time.deltaTime);
}
```
</details>

---

## Problem 10: One-Way Platform (Challenge)
Create a platform that the player can pass through from below but walk on from above.

<details><summary>Solution</summary>
```csharp
void OnCollisionEnter2D(Collision2D col)
{
    if (col.gameObject.CompareTag("Player"))
    {
        Rigidbody2D rb = col.gameObject.GetComponent<Rigidbody2D>();
        // Only collide if player coming from below
        if (rb.velocity.y < 0)
            Physics2D.IgnoreCollision(GetComponent<Collider2D>(), col.collider, false);
    }
}

void OnCollisionExit2D(Collision2D col)
{
    Physics2D.IgnoreCollision(GetComponent<Collider2D>(), col.collider, true);
}
```
</details>

---

## Problem 11: Animated Tilemap (Intermediate)
How would you create an animated water tile?

<details><summary>Solution</summary>
1. Create sprite sheet with water animation frames
2. Window → 2D → Tile Palette
3. In Tile Palette, right-click tile → Edit
4. Create AnimatedTile component
5. Add animation frames
6. Set frame duration
7. Paint as normal tile
</details>

---

## Problem 12: Pixel Perfect Rendering (Beginner)
Your pixel art sprites look blurry. How do you fix it?

<details><summary>Solution</summary>
1. Sprite import setting: Filter Mode = Point
2. Camera: PPU (Pixels Per Unit) must match sprite import PPU
3. Disable anti-aliasing in Project Settings
4. Position objects on whole pixel coordinates
</details>

---

## Problem 13: Multiple Animation Parameters (Challenge)
Create a player that animates differently based on movement direction and speed.

<details><summary>Solution</summary>
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

// Animator transitions:
// Idle (speed == 0) → Walk (speed > 0)
// Look at direction parameter for flip
```
</details>

---

## Problem 14: Slope Physics (Intermediate)
How would you handle a sloped platform in 2D physics?

<details><summary>Solution</summary>
Use EdgeCollider2D for slopes instead of BoxCollider2D. Shape it to follow the slope geometry. Physics2D will handle sliding naturally.
</details>

---

## Problem 15: Cinemachine Virtual Camera (Challenge)
Set up Cinemachine to follow player with smooth damping and confiner.

<details><summary>Solution</summary>
1. GameObject → Cinemachine → 2D Camera
2. Assign: Follow = Player, Look At = Player
3. Damping: Adjust X/Y damping for smoothness
4. Add Confiner2D component
5. Create bounds polygon/box
6. Camera stays within bounds while following
</details>

---

## Answer Summary

| Problem | Concept |
|---------|---------|
| 1 | Sprite import |
| 2 | Animation clips |
| 3 | Tilemap setup |
| 4 | Sorting layers |
| 5 | Physics + jump |
| 6 | Parallax scrolling |
| 7 | Animation blending |
| 8 | Moving platforms |
| 9 | Camera follow |
| 10 | One-way platform |
| 11 | Animated tilemap |
| 12 | Pixel perfect |
| 13 | Multi-parameter animation |
| 14 | Slope physics |
| 15 | Cinemachine setup |
