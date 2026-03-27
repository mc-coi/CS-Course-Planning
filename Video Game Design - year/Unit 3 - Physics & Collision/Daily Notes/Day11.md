# Day 11: Raycasting Fundamentals

**Learning Target:** I can use Physics.Raycast to detect objects along a line and create ground detection.

---

## Key Concepts

**Raycast** — A line cast from a point in a direction. Returns true if it hits something.

**Physics.Raycast(Vector3 origin, Vector3 direction, out RaycastHit hit, float distance)** — Shoots a ray and returns hit info.

**RaycastHit** — Contains hit information: distance, point, normal, transform, collider, rigidbody.

**Debug.DrawRay()** — Visualizes a ray in the Scene view (red line). Useful for debugging.

**Ground detection** — Essential for platformers. Raycast downward from player to check if grounded.

**Real-world examples:**
- **Platformer:** Check if player is on ground before allowing jump
- **FPS:** Raycast from camera center to detect what player is aiming at
- **Bowling:** Show trajectory line before rolling ball
- **Grappling hook:** Raycast to find attach points

---

## Code Example

```csharp
using UnityEngine;

public class RaycastGroundDetection : MonoBehaviour
{
    private Rigidbody rb;
    private bool isGrounded = false;
    public float rayDistance = 0.5f;
    public float jumpForce = 5f;
    
    // Raycast down from this distance below the object
    public float rayOffset = 0.1f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // Check if grounded
        CheckGrounded();

        // Jump only if grounded
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }
    }

    private void CheckGrounded()
    {
        // Cast a ray downward from player position
        Vector3 rayStart = transform.position + Vector3.down * rayOffset;
        
        RaycastHit hit;
        
        // Did we hit something below us?
        if (Physics.Raycast(rayStart, Vector3.down, out hit, rayDistance))
        {
            isGrounded = true;
            Debug.Log("Grounded! Hit: " + hit.transform.name);
        }
        else
        {
            isGrounded = false;
        }

        // Visualize the ray
        Debug.DrawRay(rayStart, Vector3.down * rayDistance, isGrounded ? Color.green : Color.red);
    }

    private void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }
}
```

---

## Unity Setup Steps

1. **Create Player (Capsule)** with Rigidbody
2. **Create ground platform (Plane)** with BoxCollider, Rigidbody set to Static
3. **Create wall (Cube)** so player can't jump infinitely
4. **Attach RaycastGroundDetection script to Player**
5. **Open Scene view (not Game view)** — you'll see debug rays
6. **Press Play and move around:** Watch green/red ray below player

---

## Guided Practice

1. Add the ground detection script to player
2. Jump while on ground (green ray) — works fine
3. Jump while in air (red ray) — can't jump twice!
4. Adjust rayDistance and rayOffset values in Inspector
5. Make the visualization more visible by changing ray colors

---

## Practice Problems

**Beginner:** Create a raycast that shoots forward from player. Print distance to first object hit.

**Intermediate:** Build a "wall slide" mechanic. When player is near a wall (raycast to side), reduce fall speed.

**Challenge:** Create a sniper scope system. Raycast from camera center. Show distance to target and whether target is aligned.

<details><summary>💡 Hints</summary>
- `Debug.DrawRay()` only shows in Scene view, not Game view
- Always check `if (Physics.Raycast(..., out hit))` before using hit data
- Multiple raycasts from different positions can detect different surfaces
- Layer masks can filter what raycasts detect
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Sniper scope
public class SniperScope : MonoBehaviour
{
    private Camera cam;
    public LayerMask targetLayer;

    private void Start()
    {
        cam = GetComponent<Camera>();
    }

    private void Update()
    {
        RaycastHit hit;
        
        // Raycast from center of screen
        if (Physics.Raycast(cam.transform.position, cam.transform.forward, out hit, 1000f, targetLayer))
        {
            float distance = hit.distance;
            Debug.Log("Target locked! Distance: " + distance);
        }
        else
        {
            Debug.Log("No target");
        }
    }
}
```

</details>
