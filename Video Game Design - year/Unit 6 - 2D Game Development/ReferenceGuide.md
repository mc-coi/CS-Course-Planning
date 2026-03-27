# Unit 6 Reference Guide: 2D Game Development

## Project Setup

### Camera Configuration
- **Projection**: Orthographic (not Perspective)
- **Size**: 5-10 (controls zoom; higher = more area visible)
- **Clipping Planes**: Near 0.1, Far 1000
- **Viewport**: Full screen

### Physics2D Settings
- **Gravity**: (0, -9.81) — negative Y = downward
- **Time Scale**: Default 1.0
- **Default Material**: Friction/Bounce defaults

---

## Sprites & SpriteRenderer

### Import Settings
| Setting | Value | Purpose |
|---------|-------|---------|
| Texture Type | Sprite (2D and UI) | Optimized for UI/2D |
| Sprite Mode | Single or Multiple | Single = one sprite, Multiple = sprite sheet |
| Pixels Per Unit | 100 | Controls size in world (higher = smaller) |
| Filter Mode | Point (Pixel Perfect) or Bilinear | Crisp vs smooth |
| Compression | None (quality) | Trade off size vs. quality |

### SpriteRenderer Component
```csharp
SpriteRenderer sr = GetComponent<SpriteRenderer>();

sr.sprite = mySprite;          // Change sprite
sr.color = Color.red;          // Tint color
sr.sortingOrder = 5;           // Render order (higher = front)
sr.sortingLayerName = "Player"; // Use sorting layer
```

### Sorting Layers
1. Create layers: Window → 2D → Sorting Layers
2. Order matters: Layer 0 = back, Layer 10 = front
3. Within layer: sortingOrder property determines depth
4. Common setup:
   - Background (0)
   - Terrain (1)
   - Props (2)
   - Enemies (3)
   - Player (4)
   - UI (5)

---

## Sprite Animation Basics

### Animation Clip Workflow
1. Select sprite sequence in Project
2. Window → Animation → Animator
3. Create new AnimationClip
4. Drag sprites in order into timeline
5. Set samples (FPS): 10-20 is typical

### Animator Component
- **Controller**: AnimatorController asset
- **Avatar**: Humanoid/Generic (usually Generic for 2D)
- **Update Mode**: Normal (affected by timeScale), Unscaled (not affected)

### Animation Parameters
```csharp
Animator anim = GetComponent<Animator>();

// Set parameters
anim.SetFloat("speed", 1f);
anim.SetBool("isJumping", true);
anim.SetTrigger("attack");
anim.SetInteger("direction", 1); // 0=left, 1=right
```

### State Machine Transitions
- **Conditions**: Parameter value changes
- **Exit Time**: Allow clip to finish before transitioning
- **Duration**: Blend time (0 = instant)

---

## Tilemaps

### Tilemap Setup
1. Window → 2D → Tile Palette
2. Create Tile Palette (new folder, name it)
3. Drag sprites into Palette
4. Create Tilemap in Hierarchy: Right-click Canvas → 2D → Tilemap
5. Attach GridLayout and Tilemap components

### Tilemap Colliders
```csharp
// On Tilemap GameObject:
// Add TilemapCollider2D component
// This creates box colliders for each tile automatically
```

### Tilemap Grid Settings
- **Grid Type**: Rectangular (most common)
- **Cell Size**: Match your tile size (e.g., 1x1)
- **Z Position**: 0 for first layer, -1 for layer behind, +1 for layer in front

### Multiple Tilemaps
- Create separate Tilemaps for each layer
- Set Sorting Order different for each
- Example:
  - Background Tilemap: Sorting Order -1
  - Ground Tilemap: Sorting Order 0
  - Props Tilemap: Sorting Order 1

---

## 2D Physics Components

### Rigidbody2D
| Property | Use Case |
|----------|----------|
| Body Type: Dynamic | Physics-controlled (falls, collides) |
| Body Type: Kinematic | Script-controlled, collides with others |
| Body Type: Static | Immovable (walls, platforms) |
| Gravity Scale | How much gravity affects this object |
| Constraints | Freeze rotation, position, etc. |

### Collider2D Types
| Type | Use | Shape |
|------|-----|-------|
| BoxCollider2D | Rectangular objects | Rectangle |
| CircleCollider2D | Round objects | Circle |
| PolygonCollider2D | Complex shapes | Custom polygon |
| EdgeCollider2D | Slopes, complex terrain | Line segments |
| TilemapCollider2D | Tilemap tiles | Auto-generated |

### Physics2D Methods
```csharp
Rigidbody2D rb = GetComponent<Rigidbody2D>();

rb.velocity = new Vector2(5f, 0);      // Direct movement
rb.AddForce(Vector2.right * 10f);      // Apply force
rb.AddForce(Vector2.up * 20f, ForceMode2D.Impulse); // One-time force

// Collision detection
void OnCollisionEnter2D(Collision2D col) { }
void OnCollisionStay2D(Collision2D col) { }
void OnCollisionExit2D(Collision2D col) { }

void OnTriggerEnter2D(Collider2D col) { } // If isTrigger = true
```

---

## 2D Camera & Cinemachine

### Basic 2D Camera
```csharp
// Simple follow script
Transform player;
float smoothSpeed = 5f;

void LateUpdate()
{
    Vector3 targetPos = new Vector3(player.position.x, player.position.y, -10);
    transform.position = Vector3.Lerp(transform.position, targetPos, smoothSpeed * Time.deltaTime);
}
```

### Cinemachine Virtual Camera
1. Install: Window → TextMeshPro → Import TMP Essentials (or Package Manager)
2. Create: GameObject → Cinemachine → 2D Camera
3. Assign: Follow = Player, Look At = Player
4. Confiner (optional): Limit camera bounds to level

---

## Parallax Scrolling

### Two-Layer Parallax
```csharp
public class ParallaxBackground : MonoBehaviour
{
    public float parallaxFactor = 0.5f; // 0.5 = moves half as fast
    private Vector3 startPos;
    private Transform cameraTransform;

    void Start()
    {
        startPos = transform.position;
        cameraTransform = Camera.main.transform;
    }

    void LateUpdate()
    {
        Vector3 parallaxPos = new Vector3(
            startPos.x + cameraTransform.position.x * parallaxFactor,
            startPos.y + cameraTransform.position.y * parallaxFactor,
            startPos.z
        );
        transform.position = parallaxPos;
    }
}
```

---

## 2D Lighting

### Light2D Component
- **Light Type**: Point (all directions), Spot (cone), Global (sun)
- **Intensity**: Brightness (0-1 typical)
- **Range**: How far light travels
- **Color**: Light color

### Normal Maps
- Import setting: Texture Type = Normal Map
- Adds depth to 2D sprites with light
- Requires proper lighting setup

### Shadow Casters
- Add ShadowCaster2D to objects that block light
- Requires Global Light2D in scene

---

## Common 2D Code Patterns

### Ground Check (for jumping)
```csharp
private bool isGrounded = false;
private float groundCheckRadius = 0.2f;
private Vector2 groundCheckOffset = Vector2.down * 0.5f;

void Update()
{
    Collider2D[] groundColliders = Physics2D.OverlapCircleAll(
        (Vector2)transform.position + groundCheckOffset,
        groundCheckRadius
    );
    isGrounded = groundColliders.Length > 1; // 1 = self, >1 = ground detected
}
```

### Knockback
```csharp
public void Knockback(Vector2 direction, float force)
{
    rb.velocity = Vector2.zero; // Clear previous velocity
    rb.AddForce(direction.normalized * force, ForceMode2D.Impulse);
}
```

### Clamping Position
```csharp
Vector3 newPos = transform.position;
newPos.x = Mathf.Clamp(newPos.x, -10f, 10f); // Keep within bounds
transform.position = newPos;
```

---

## Performance Tips

1. **Use Object Pooling**: Reuse bullets, enemies instead of Destroy/Instantiate
2. **Optimize Sprites**: Reduce resolution if possible
3. **Limit Colliders**: Use simple shapes over PolygonCollider2D
4. **Batch Draw Calls**: Group similar materials/sorting layers
5. **Use TilemapCollider2D**: Much faster than individual box colliders
