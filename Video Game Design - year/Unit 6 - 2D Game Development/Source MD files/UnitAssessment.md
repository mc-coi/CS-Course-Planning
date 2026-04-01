# Unit 6 Assessment: 2D Game Development

**Total Points: 40**

---

## Part A: Multiple Choice (1 point each)

1. What does Orthographic camera do?
   - A) Shows 3D perspective B) Shows flat 2D view C) Increases FOV D) Enables physics

2. Pixels Per Unit controls:
   - A) Sprite quality B) Sprite size in world C) Animation speed D) Render order

3. What's the correct order for multiple tilemap layers?
   - A) All same layer B) Increasing sorting order C) Random order D) Doesn't matter

4. Jump mechanic requires checking:
   - A) Only vertical velocity B) Ground contact C) Player height D) Animation state

5. Which component enables smooth camera following?
   - A) Rigidbody B) Collider C) Cinemachine D) Animator

6. Parallax factor 0.5 means:
   - A) Double speed B) Half speed C) Normal speed D) Opposite direction

7. SortingOrder property controls:
   - A) Animation playback B) Physics collision C) Render depth D) Movement speed

8. EdgeCollider2D is best for:
   - A) Round objects B) Slopes C) Rectangles D) Physics bodies

9. Sprite animation FPS of 10 means:
   - A) 10 pixels B) 10 frames per second C) 10 size D) 10 rotation

10. Cinemachine Confiner restricts:
    - A) Animation B) Camera bounds C) Sprite movement D) Physics

---

## Part B: Short Answer (2 points each)

1. Explain why you'd use multiple sorting layers instead of relying on Z-position.

2. Describe how coyote time improves jump feel in a platformer.

3. Why would you use PolygonCollider2D instead of BoxCollider2D? Give an example.

4. How does parallax scrolling create a sense of depth?

5. What's the relationship between sprite Pixels Per Unit and camera Orthographic Size?

---

## Part C: Coding Challenges (≈7 points each)

**Challenge 1: Jump Mechanic**
Write a script that implements jumping with ground detection. Include coyote time (0.1 second grace period after leaving platform).

```csharp
// Your solution
```

**Challenge 2: Camera Follow**
Write a camera script that smoothly follows the player with damping, but stops at map boundaries (±10 X, ±5 Y).

```csharp
// Your solution
```

**Challenge 3: Animated Sprite**
Create a script that plays different animations based on player movement direction and speed (Idle, Walk Left, Walk Right, Jump).

```csharp
// Your solution
```

---

## Answer Key

### Part A
1. B | 2. B | 3. B | 4. B | 5. C | 6. B | 7. C | 8. B | 9. B | 10. B

### Part B

**1. Multiple Sorting Layers:**
Z-position only allows limited depth. Sorting layers group related sprites together and improve performance. Multiple layers (Background, Terrain, Player, UI) organize complexity.

**2. Coyote Time:**
Allows jump slightly after leaving platform. Feels more forgiving and fun. Without it, players must jump while platform is under them—feels restrictive.

**3. PolygonCollider2D Example:**
Use for complex shapes like terrain, enemies, obstacles. BoxCollider2D only fits rectangles. Example: An L-shaped platform needs PolygonCollider2D.

**4. Parallax Depth:**
Background moves slower than foreground. Faster movement = closer. Creates illusion of 3D depth on 2D plane.

**5. PPU & Camera Size:**
If sprite is 100 PPU and camera is size 5, you see roughly 10x10 units of world space. Match them: increase PPU = sprite bigger.

### Part C

**Challenge 1:**
```csharp
private Rigidbody2D rb;
private bool isGrounded = false;
private float coyoteCounter = 0;
private const float COYOTE_TIME = 0.1f;

void Update()
{
    CheckGround();
    coyoteCounter -= Time.deltaTime;
    
    if (Input.GetKeyDown(KeyCode.Space) && coyoteCounter > 0)
    {
        rb.velocity = new Vector2(rb.velocity.x, 5f);
        coyoteCounter = 0;
    }
}

void CheckGround()
{
    Collider2D[] cols = Physics2D.OverlapCircleAll((Vector2)transform.position + Vector2.down * 0.5f, 0.2f);
    isGrounded = cols.Length > 1;
    if (isGrounded) coyoteCounter = COYOTE_TIME;
}
```

**Challenge 2:**
```csharp
public Transform player;
public float smoothSpeed = 5f;
public float minX = -10, maxX = 10, minY = -5, maxY = 5;

void LateUpdate()
{
    Vector3 targetPos = new Vector3(player.position.x, player.position.y, -10);
    targetPos.x = Mathf.Clamp(targetPos.x, minX, maxX);
    targetPos.y = Mathf.Clamp(targetPos.y, minY, maxY);
    
    transform.position = Vector3.Lerp(transform.position, targetPos, smoothSpeed * Time.deltaTime);
}
```

**Challenge 3:**
```csharp
private Animator anim;
private float moveInput;
private bool isGrounded;

void Update()
{
    moveInput = Input.GetAxis("Horizontal");
    
    anim.SetFloat("speed", Mathf.Abs(moveInput));
    anim.SetInteger("direction", moveInput > 0 ? 1 : moveInput < 0 ? -1 : 0);
    anim.SetBool("isGrounded", isGrounded);
}
```
