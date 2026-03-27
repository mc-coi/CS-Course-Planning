# Day 19: Top-Down & Isometric Movement

**Learning Target:** I can implement top-down and isometric camera systems with adjusted movement controls.

---

## Key Concepts

**Top-Down Camera:**
- Camera points straight down at the player
- Player moves in screen space (up-key = move up on screen)
- Used in *The Legend of Zelda*, *Pokeémon*, *Hollow Knight*

**Isometric Projection:**
- Camera at 45° angle, slightly elevated
- Creates pseudo-3D look from 2D controls
- Used in *Diablo*, *Baldur's Gate*, *Hades*

**Movement Adjustment:**
- Top-down: Input maps directly to world (no camera rotation needed)
- Isometric: Rotate input 45° to match camera angle

**Grid Snapping:** Optional—snap movement to grid for pixel-perfect aesthetics (*Legend of Zelda*, *Binding of Isaac*).

---

## Code Example

```csharp
using UnityEngine;

public class TopDownController : MonoBehaviour
{
    enum CameraStyle { TopDown, Isometric }
    private CameraStyle cameraStyle = CameraStyle.TopDown;

    public float moveSpeed = 5f;
    public float gridSize = 1f; // 0 = no grid snapping
    
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
    }

    private void Update()
    {
        HandleMovement();
        ApplyGravity();
    }

    private void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        Vector3 moveDir;

        if (cameraStyle == CameraStyle.TopDown)
        {
            // Top-down: input maps directly to world
            moveDir = new Vector3(h, 0, v).normalized;
        }
        else // Isometric
        {
            // Rotate input 45° to match isometric camera
            // Forward becomes diagonal (1, 1), Right becomes diagonal (1, -1)
            moveDir = new Vector3(h - v, 0, h + v).normalized;
        }

        Vector3 motion = moveDir * moveSpeed;
        motion.y = velocity.y;

        // Grid snapping (optional)
        if (gridSize > 0)
        {
            Vector3 gridPos = transform.position;
            gridPos.x = Mathf.Round(gridPos.x / gridSize) * gridSize;
            gridPos.z = Mathf.Round(gridPos.z / gridSize) * gridSize;
            transform.position = gridPos;
        }

        controller.Move(motion * Time.deltaTime);
    }

    private void ApplyGravity()
    {
        if (controller.isGrounded && velocity.y < 0)
            velocity.y = -2f;
        else
            velocity.y -= gravity * Time.deltaTime;
    }
}
```

---

## Unity Setup Steps

1. **Create Player**
   - Capsule with CharacterController

2. **Position Top-Down Camera**
   - Main Camera at `(0, 10, 0)` looking straight down
   - Or isometric at `(5, 5, 5)` at 45° angle

3. **Attach TopDownController Script**
   - Create C# script → "TopDownController"
   - Set moveSpeed to `5`
   - Set cameraStyle to TopDown or Isometric

4. **Create Grid (Optional)**
   - Set gridSize to `1` for 1x1 grid snapping
   - Set to `0` to disable

5. **Test**
   - Press Play
   - Move with WASD
   - Watch movement match camera perspective

---

## Guided Practice

1. **Implement Top-Down Movement** (10 min)
   - Position camera straight above player
   - Map input directly to movement
   - Test 4-directional movement

2. **Switch to Isometric** (10 min)
   - Reposition camera to 45° angle
   - Rotate input vector by 45°
   - Test diagonal movement feeling correct

3. **Add Grid Snapping** (5 min)
   - Enable grid snapping
   - Move in grid increments
   - Adjust gridSize to fit your game

---

## Practice Problems

**Beginner:** Create a top-down player that moves relative to camera direction. Movement feels correct when viewed from above.

**Intermediate:** Implement **grid-based movement**: player snaps to grid cells. Each input press moves one cell. Cannot move through walls.

**Challenge:** Create **dual-camera system**: press Tab to switch between top-down and isometric views. Movement adjusts automatically based on active camera.

<details><summary>💡 Hints</summary>
- Top-down: Input axes map directly to X and Z.
- Isometric: Rotate input 45° using matrix math or manual formula.
- Grid snapping uses `Mathf.Round()` to snap positions.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Grid-Based):**
```csharp
private Vector3 targetGridPos;
private float gridMoveTime = 0.2f;
private float gridMoveTimer = 0f;

void Update()
{
    if (gridMoveTimer <= 0)
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");

        Vector3 moveDir = new Vector3(h, 0, v).normalized;
        Vector3 nextGrid = transform.position + moveDir * gridSize;

        // Raycast to check for walls
        if (!Physics.Raycast(transform.position, moveDir, gridSize * 0.9f))
        {
            targetGridPos = nextGrid;
            gridMoveTimer = gridMoveTime;
        }
    }

    // Smoothly move toward grid position
    transform.position = Vector3.Lerp(
        transform.position, 
        targetGridPos, 
        Time.deltaTime / gridMoveTime
    );

    gridMoveTimer -= Time.deltaTime;
}
```

**Challenge Solution (Dual Camera):**
```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.Tab))
    {
        cameraStyle = (cameraStyle == CameraStyle.TopDown) 
            ? CameraStyle.Isometric 
            : CameraStyle.TopDown;
        
        AdjustCamera();
    }

    HandleMovement();
}

void AdjustCamera()
{
    if (cameraStyle == CameraStyle.TopDown)
        Camera.main.transform.position = transform.position + Vector3.up * 10f;
    else
        Camera.main.transform.position = transform.position + new Vector3(5, 5, 5);
}
```

</details>
