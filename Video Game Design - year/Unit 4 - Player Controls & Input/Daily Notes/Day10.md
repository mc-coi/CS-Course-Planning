# Day 10: Screen-to-World Conversion & Raycasting

**Learning Target:** I can convert screen clicks to world positions and use raycasts to detect what the player clicked.

---

## Key Concepts

**Screen-to-World Conversion:**
1. Get mouse position in screen space: `Input.mousePosition`
2. Convert to world ray: `Camera.main.ScreenPointToRay(mousePos)`
3. Raycast into world: `Physics.Raycast(ray, out hit)`
4. Get hit position: `hit.point`

**Raycasting** — Casting an invisible ray through the world and checking what it hits. Perfect for:
- Click-to-move games (*Diablo, StarCraft*)
- Weapon aiming
- UI raycasting

**Optimization:** Raycasts are fast but can be slow if done every frame on large scenes. Use layer masks to limit what can be hit.

---

## Code Example

```csharp
using UnityEngine;

public class ClickToMove : MonoBehaviour
{
    public float moveSpeed = 5f;
    public LayerMask groundLayer;
    private Vector3 targetPosition;
    private bool hasTarget = false;
    private CharacterController controller;
    private Vector3 velocity = Vector3.zero;
    private float gravity = 9.81f;

    private void Start()
    {
        controller = GetComponent<CharacterController>();
        targetPosition = transform.position;
    }

    private void Update()
    {
        HandleClick();
        MoveToTarget();
        ApplyGravity();
    }

    private void HandleClick()
    {
        if (Input.GetMouseButtonDown(0)) // Left-click
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            
            if (Physics.Raycast(ray, out RaycastHit hit, 1000f, groundLayer))
            {
                targetPosition = hit.point;
                hasTarget = true;
                Debug.Log($"Target set to {targetPosition}");
            }
        }
    }

    private void MoveToTarget()
    {
        if (!hasTarget) return;

        Vector3 directionToTarget = (targetPosition - transform.position).normalized;
        float distanceToTarget = Vector3.Distance(transform.position, targetPosition);

        if (distanceToTarget < 0.5f)
        {
            hasTarget = false;
            return;
        }

        Vector3 motion = directionToTarget * moveSpeed;
        motion.y = velocity.y;
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

1. **Create Player & Ground**
   - Capsule (Player) at `(0, 1, 0)`
   - Plane (Ground) at `(0, 0, 0)`, scaled to `(20, 1, 20)`

2. **Set Up Layers**
   - Ground: Inspector → Layer → Add "Ground"
   - Assign Ground plane to "Ground" layer

3. **Add ClickToMove Script**
   - Create C# script → "ClickToMove"
   - Attach to Player
   - In Inspector, set groundLayer to "Ground"

4. **Test**
   - Press Play
   - Click on the ground
   - Player should move to click point

---

## Guided Practice

1. **Raycast from Mouse** (10 min)
   - On left-click, cast a ray from the camera through the mouse position
   - If it hits the ground, log the hit position
   - Draw the raycast in the Scene view

2. **Set Movement Target** (10 min)
   - Store the hit point as a target
   - Move the player toward that target each frame
   - Stop when distance is small enough

3. **Add Visual Feedback** (5 min)
   - Instantiate a marker (sphere) at the click point
   - Destroy it when the player reaches it
   - Gives visual feedback to the player

---

## Practice Problems

**Beginner:** On left-click, raycast and log the hit object name and position. Only raycast to objects on the "Ground" layer.

**Intermediate:** Create a **targeting system**: right-click on an enemy to select it, then left-click on the ground to move while facing the selected enemy.

**Challenge:** Implement **pathfinding waypoints**: left-click multiple times to queue up movement points. The player visits each point in order. (Hint: Use a Queue<Vector3> to store waypoints.)

<details><summary>💡 Hints</summary>
- Use `Physics.Raycast()` with a LayerMask to limit what can be hit.
- Layer masks are created in Edit → Project Settings → Tags and Layers.
- `Vector3.Distance()` is useful for checking if you've reached a target.
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
void Update()
{
    if (Input.GetMouseButtonDown(0))
    {
        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
        if (Physics.Raycast(ray, out RaycastHit hit, 1000f, LayerMask.GetMask("Ground")))
        {
            Debug.Log($"Hit {hit.collider.name} at {hit.point}");
        }
    }
}
```

**Challenge Solution (Waypoint Queue):**
```csharp
private Queue<Vector3> waypoints = new Queue<Vector3>();

void HandleClick()
{
    if (Input.GetMouseButtonDown(0))
    {
        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
        if (Physics.Raycast(ray, out RaycastHit hit))
            waypoints.Enqueue(hit.point);
    }
}

void MoveToTarget()
{
    if (waypoints.Count == 0) return;

    Vector3 currentTarget = waypoints.Peek();
    float dist = Vector3.Distance(transform.position, currentTarget);

    if (dist < 0.5f)
        waypoints.Dequeue();
    else
        // Move toward current target
}
```

</details>
