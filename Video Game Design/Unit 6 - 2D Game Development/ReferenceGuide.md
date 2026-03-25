# Vocabulary & Quick Reference

## Key Terms

| Term | Definition |
|------|-----------|
| **Sprite** | A 2D image used in 2D games |
| **Sprite Renderer** | Component that displays a sprite |
| **Sorting Order** | Z-layer determining draw order (higher = in front) |
| **Tilemap** | A grid of tiles for efficient level building |
| **Tile Palette** | A set of available tiles for painting |
| **Rigidbody2D** | 2D physics component |
| **Collider2D** | 2D collision shape |
| **Velocity** | 2D speed and direction (x, y) |
| **Animation Clip** | Sequence of sprites or keyframes |
| **Animator** | Component playing animations and managing states |
| **Prefab** | Template GameObject for spawning copies |
| **Instantiate()** | Creates a copy of a GameObject at runtime |
| **isGrounded** | Boolean indicating if touching ground |

## Key Syntax

### 2D Components Quick Reference

```csharp
// Sprite Renderer
SpriteRenderer sr = GetComponent<SpriteRenderer>();
sr.sprite = mySprite;
sr.color = Color.red;
sr.sortingOrder = 5;
sr.flipX = true;  // Flip horizontally

// Rigidbody2D
Rigidbody2D rb2d = GetComponent<Rigidbody2D>();
rb2d.velocity = new Vector2(5, 0);
rb2d.AddForce(Vector2.up * 5, ForceMode2D.Impulse);
rb2d.gravityScale = 1f;

// Collider2D types
BoxCollider2D box = GetComponent<BoxCollider2D>();
CircleCollider2D circle = GetComponent<CircleCollider2D>();
PolygonCollider2D poly = GetComponent<PolygonCollider2D>();

// 2D Collision/Trigger
void OnCollisionEnter2D(Collision2D collision) { }
void OnTriggerEnter2D(Collider2D collision) { }

// Physics2D Raycast
RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.1f);
bool isGrounded = hit.collider != null;
```

### Animation Quick Reference

```csharp
// Animator parameter control
Animator animator = GetComponent<Animator>();
animator.SetBool("IsRunning", true);
animator.SetFloat("Speed", moveSpeed);
animator.SetTrigger("Jump");
animator.SetInteger("Direction", 1);

// Common animation states
// Idle, Run, Jump, Fall, Attack, Die, etc.

// Animator Controller structure (set up in editor):
// Parameters: IsRunning (bool), IsJumping (bool), etc.
// States: Idle, Run, Jump, Fall, etc.
// Transitions with conditions between states
```

### Prefab Quick Reference

```csharp
// Instantiate a prefab
public GameObject prefab;
GameObject instance = Instantiate(prefab, position, rotation);
GameObject instance = Instantiate(prefab);  // Uses prefab's position/rotation

// Instantiate with parent
Instantiate(prefab, position, rotation, parentTransform);

// Destroy instance
Destroy(instance);
Destroy(gameObject);  // Destroy self
```

---

## Common Mistakes & How to Fix Them

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Sprite doesn't appear | Texture Type not set to "Sprite" | Always set Texture Type to "Sprite (2D and UI)" in import settings |
| Rigidbody2D falls off screen | No collider on ground or gravity too high | Add colliders to all collidable objects; adjust gravity scale |
| 2D movement feels stiff | Using transform.position instead of velocity | Always modify velocity for smooth physics-based movement |
| Animation doesn't play | Animator Controller not assigned or no states | Assign Animator Controller; create states and transitions |
| Prefab changes don't affect instances | Instance has overrides that override prefab | Select the instance and "Revert" overrides to match prefab |
| Sprites overlap incorrectly | Sorting order not configured properly | Set consistent sorting order: background (0), player (5), UI (10) |
| Instantiate() creates wrong object | Wrong prefab assigned in Inspector | Double-check the public field references the correct prefab |
| Animation loops incorrectly | Loop setting wrong or animation too long | Adjust animation duration; check "Loop" checkbox for looping animations |
| Grounding detection always false | Raycast distance too small or colliders missing | Increase raycast distance; ensure platform has collider |
| Performance issues with many objects | Creating/destroying too frequently | Use object pooling to reuse instances |
