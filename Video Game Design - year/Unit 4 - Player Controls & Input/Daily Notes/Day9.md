# Day 9: Mouse Input & Input.mousePosition

**Learning Target:** I can read mouse position and use it to aim weapons or control character direction.

---

## Key Concepts

**Input.mousePosition** — Returns the mouse position in **screen pixels** (0,0 at bottom-left in game world, but confusingly top-left on screen). Returns a Vector3 with depth as 0.

**Screen Space vs. World Space:**
- **Screen Space:** (0, 0) is bottom-left of screen. Used for UI.
- **World Space:** Game world coordinates. Used for game objects.

**Key Methods:**
- `Input.GetMouseButton(0)` → Left-click held down
- `Input.GetMouseButtonDown(0)` → Left-click pressed this frame
- `Camera.main.ScreenToWorldPoint()` → Convert screen pixel to world position

**Common Uses:** Aiming a gun (*FPS games*), pointing at targets (*point-and-click games*), moving a character toward mouse (*strategy games*).

---

## Code Example

```csharp
using UnityEngine;

public class MouseAim : MonoBehaviour
{
    public float rotationSpeed = 10f;
    private Camera mainCam;

    private void Start()
    {
        mainCam = Camera.main;
    }

    private void Update()
    {
        HandleMouseAim();
    }

    private void HandleMouseAim()
    {
        // Get mouse position in screen space
        Vector3 mouseScreenPos = Input.mousePosition;

        // Convert to world position at player height
        Plane playerPlane = new Plane(Vector3.up, transform.position);
        Ray mouseRay = mainCam.ScreenPointToRay(mouseScreenPos);
        
        if (playerPlane.Raycast(mouseRay, out float hitDistance))
        {
            Vector3 targetPoint = mouseRay.origin + mouseRay.direction * hitDistance;

            // Calculate direction to mouse
            Vector3 directionToMouse = (targetPoint - transform.position).normalized;

            // Rotate toward mouse
            Quaternion targetRotation = Quaternion.LookRotation(directionToMouse);
            transform.rotation = Quaternion.Slerp(
                transform.rotation, 
                targetRotation, 
                Time.deltaTime * rotationSpeed
            );

            Debug.DrawRay(transform.position, directionToMouse * 10f, Color.red);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a Player**
   - 3D Object → Capsule (name: "Player")
   - Add a simple movement script

2. **Attach MouseAim Script**
   - Create C# script → "MouseAim"
   - Attach to Player
   - Set rotationSpeed to `10` in Inspector

3. **Create Ground Plane**
   - 3D Object → Plane
   - Scale to `(20, 1, 20)` at `(0, 0, 0)`

4. **Test**
   - Press Play
   - Move the mouse around
   - Player should rotate to face the mouse cursor

---

## Guided Practice

1. **Log Mouse Position** (5 min)
   - Print `Input.mousePosition` every frame
   - Notice it updates as you move the mouse
   - Understand the pixel range

2. **Convert to World Position** (10 min)
   - Use `ScreenPointToRay()` to convert screen coords to a world ray
   - Cast a ray into the world and find where it hits the ground plane
   - Print the world position

3. **Rotate Player Toward Mouse** (5 min)
   - Calculate direction from player to mouse hit point
   - Use `Quaternion.LookRotation()` to face that direction
   - Smooth with `Slerp()` for snappy aiming

---

## Practice Problems

**Beginner:** Log the mouse position in world space (at ground level) every frame. Draw a red line from the player to the mouse point.

**Intermediate:** Create a **targeting reticle**: instantiate a small sphere at the mouse hit point that updates position every frame. Make it transparent so it doesn't block view.

**Challenge:** Implement **mouse look for a third-person camera**: the camera rotates based on mouse X/Y position, always keeping the player in view while allowing free aiming.

<details><summary>💡 Hints</summary>
- `Input.mousePosition.z` is always 0 because it's screen space. Use the camera ray to find world position.
- A Plane raycast is fast and perfect for ground targeting.
- `Quaternion.LookRotation()` faces an object toward a direction vector.
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
void Update()
{
    Vector3 mouseScreenPos = Input.mousePosition;
    Plane groundPlane = new Plane(Vector3.up, 0);
    Ray ray = Camera.main.ScreenPointToRay(mouseScreenPos);
    
    if (groundPlane.Raycast(ray, out float dist))
    {
        Vector3 worldPos = ray.origin + ray.direction * dist;
        Debug.Log($"Mouse at world: {worldPos}");
        Debug.DrawLine(transform.position, worldPos, Color.red);
    }
}
```

</details>
