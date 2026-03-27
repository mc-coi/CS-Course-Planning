# Day 4: MeshCollider & Collider Optimization

**Learning Target:** I can use MeshCollider for complex shapes and optimize collider performance.

---

## Key Concepts

**MeshCollider** — Uses your 3D model's exact mesh as the collision shape. Precise but expensive computationally. Found in Inspector → Add Component → Physics → Mesh Collider.

**Convex checkbox** — In MeshCollider, when checked, the shape is simplified to convex (no indentations). Faster but less precise. Required if the MeshCollider's Rigidbody is not static.

**Is Kinematic** — A Rigidbody property. When true, physics doesn't control the object, but it can still collide. Use for moving platforms, doors, or animated objects.

**Collider optimization tips:**
1. Use simple colliders (Box, Sphere, Capsule) when possible
2. Combine multiple simple colliders instead of one MeshCollider
3. Static colliders (ground, walls) can use MeshCollider
4. Dynamic (moving) colliders should be simple shapes or convex

**Real-world examples:**
- **Complex level geometry:** Ground uses MeshCollider (static)
- **Moving platforms:** Use BoxCollider with isKinematic = true
- **Detailed enemies:** Multiple simple colliders (not one MeshCollider)

---

## Code Example

```csharp
using UnityEngine;

public class MeshColliderSetup : MonoBehaviour
{
    private MeshCollider meshCol;
    private Rigidbody rb;

    private void Start()
    {
        meshCol = GetComponent<MeshCollider>();
        rb = GetComponent<Rigidbody>();

        // For a static ground, MeshCollider with Convex OFF is fine
        if (meshCol != null)
        {
            meshCol.convex = false; // Only works with static Rigidbody
        }

        // If this object moves, enable Convex
        if (rb != null && !rb.isKinematic)
        {
            meshCol.convex = true;
        }
    }

    // After modifying the mesh at runtime, refresh the collider
    public void RefreshCollider()
    {
        if (meshCol != null)
        {
            meshCol.convex = true;
            // Remove and re-add to force refresh
            Destroy(meshCol);
            gameObject.AddComponent<MeshCollider>();
        }
    }
}
```

---

## Unity Setup Steps

1. **Import a complex 3D model** (or use the provided character model)
2. **Select the model in Hierarchy**
3. **Add MeshCollider:** Inspector → Add Component → Physics → Mesh Collider
4. **Set Body Type to Static** in Rigidbody (if not already present, add one)
5. **Uncheck Convex** (it will error if your mesh is concave, but static is OK)
6. **Click Play and test:** Objects should collide with your complex shape
7. **For moving objects:** Add a Rigidbody, check Convex, set isKinematic = true

---

## Guided Practice

1. Import an ornate chair or complex model
2. Add default BoxCollider — see how poorly it fits
3. Add MeshCollider instead — much better fit!
4. Notice the performance impact in Stats (bottom-right of Game view)
5. Replace with three simple BoxColliders positioned around the model
6. Compare performance and collision accuracy

---

## Practice Problems

**Beginner:** Create a static stone wall using a 3D model. Add MeshCollider and test collisions.

**Intermediate:** Create a moving platform (use Rigidbody with isKinematic = true and Convex MeshCollider). Make it move back and forth using transform.position changes.

**Challenge:** Build a complex dungeon room with walls, pillars, and doorways. Use MeshCollider for the room geometry and simple colliders for interactive objects. Optimize so the player can walk through without lag.

<details><summary>💡 Hints</summary>
- Static colliders (Rigidbody with Body Type = Static or no Rigidbody) can use non-convex MeshCollider
- Moving colliders must use Convex MeshCollider (less accurate but required for dynamic physics)
- Compound colliders (multiple simple shapes) are faster than one MeshCollider
- Use `Physics.BakeMesh()` if you need to update a MeshCollider at runtime
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Intermediate: Moving platform
public class MovingPlatform : MonoBehaviour
{
    private Vector3 startPos;
    private Vector3 endPos;
    public float speed = 2f;
    private float t = 0f;

    private void Start()
    {
        startPos = transform.position;
        endPos = startPos + Vector3.forward * 5f;
    }

    private void FixedUpdate()
    {
        t += Time.deltaTime * speed;
        if (t > 1f) t = 0f;
        
        transform.position = Vector3.Lerp(startPos, endPos, t);
    }
}
```

</details>
