# Day 21: Physics Review & Debugging

**Learning Target:** I can debug physics issues and optimize physics systems for performance.

---

## Common Physics Debugging Issues

**Problem: Objects falling through colliders**
- Collision Detection set to Discrete? Change to Continuous
- Rigidbody moving too fast? Reduce step size in Physics settings
- Collider too thin? Increase collider thickness
- Solution: Use Physics.defaultContactOffset or continuous collision

**Problem: Physics feels jittery or unstable**
- Time step wrong? Check Edit → Project Settings → Physics → Fixed Timestep (0.02 = 50fps)
- Too many forces? Reduce force amounts or check multiple AddForce() calls
- Rigidbody too light? Increase mass
- Solution: Increase solver iterations in Physics settings

**Problem: Object spinning uncontrollably**
- Angular drag too low? Increase to 0.05+
- Rotation constraints not frozen? Check Freeze Rotation
- Collision impact too strong? Use Impulse carefully
- Solution: Freeze rotation unless needed, increase angular drag

**Problem: Raycasts not detecting objects**
- Layer mask set correctly? Check LayerMask in script
- Collider is trigger? Triggers still work with raycasts
- Ray direction wrong? Debug.DrawRay to visualize
- Solution: Use gizmos to draw raycasts, verify layer masks

**Problem: Performance lag with many physics objects**
- Too many dynamic Rigidbodies? Use static or kinematic
- Collision complexity? Use simple colliders (Box, Sphere) instead of Mesh
- MeshCollider not convex? Check for complex shapes
- Solution: Optimize with layers, use pooling, reduce precision

---

## Physics Settings Optimization

```csharp
using UnityEngine;

public class PhysicsDebugger : MonoBehaviour
{
    // Debug visualization
    private void OnDrawGizmos()
    {
        // Draw all raycasts
        DrawDebugRaycasts();
        
        // Draw collision bounds
        DrawCollisionBounds();
    }

    private void DrawDebugRaycasts()
    {
        // Visualization helpers for debugging raycasts
        Gizmos.color = Color.red;
        Gizmos.DrawLine(transform.position, transform.position + Vector3.down * 0.5f);
    }

    private void DrawCollisionBounds()
    {
        // Show collider bounds
        Collider col = GetComponent<Collider>();
        if (col != null)
        {
            Gizmos.color = Color.green;
            Gizmos.DrawWireCube(col.bounds.center, col.bounds.size);
        }
    }

    // Performance profiling
    public void ProfilePhysics()
    {
        int rigidbodyCount = FindObjectsOfType<Rigidbody>().Length;
        int colliderCount = FindObjectsOfType<Collider>().Length;
        
        Debug.Log($"Rigidbodies: {rigidbodyCount}");
        Debug.Log($"Colliders: {colliderCount}");
    }
}

public class PhysicsOptimizer : MonoBehaviour
{
    public void OptimizePhysics()
    {
        // Set physics parameters
        Time.fixedDeltaTime = 0.02f; // 50 physics updates per second
        Physics.defaultSolverIterations = 6; // More iterations = more stable
        Physics.defaultSolverVelocityIterations = 1;
        
        // Use spatial hashing for large numbers of objects
        Physics.bounceThreshold = 2f; // Objects hitting slower than this don't bounce
    }

    public void TestCollision(GameObject obj1, GameObject obj2)
    {
        Rigidbody rb1 = obj1.GetComponent<Rigidbody>();
        Rigidbody rb2 = obj2.GetComponent<Rigidbody>();
        Collider col1 = obj1.GetComponent<Collider>();
        Collider col2 = obj2.GetComponent<Collider>();

        if (rb1 && col1 && rb2 && col2)
        {
            Debug.Log($"{obj1.name} colliding with {obj2.name}?");
            
            // Check layer collision matrix
            int layer1 = obj1.layer;
            int layer2 = obj2.layer;
            
            bool canCollide = Physics.GetIgnoreLayerCollision(layer1, layer2) == false;
            Debug.Log($"Layer collision allowed: {canCollide}");
        }
    }
}
```

---

## Debugging Checklist

- [ ] Enable Gizmos in Scene view to see colliders
- [ ] Use Debug.DrawRay() for raycast visualization
- [ ] Print collision information to console
- [ ] Check Physics settings for correct timestep
- [ ] Verify layer collision matrix
- [ ] Monitor FPS in Stats window
- [ ] Test on target platform (mobile may have performance limits)
- [ ] Profile with Profiler window (Window → Analysis → Profiler)

---

## Common Physics Mistakes

| Mistake | Cause | Fix |
|---------|-------|-----|
| Objects phase through walls | Discrete collision detection | Use Continuous |
| Jittery movement | Fixed timestep too small | Increase to 0.02s |
| Won't jump twice | Checking ground wrong | Use raycast properly |
| Knockback doesn't work | AddForce mode wrong | Use ForceMode.Impulse |
| Trigger not detecting | isTrigger not checked | Check isTrigger box |
| Raycast misses | Layer mask wrong | Verify layer settings |
| Physics slow | Too many objects | Reduce dynamic bodies |
| Door spins wildly | Rotation not frozen | Freeze all rotation axes |

---

## Practice Problems

**Beginner:** Debug a simple scene where ball falls through floor. Identify and fix the issue.

**Intermediate:** Optimize a scene with 100 falling cubes. Reduce lag while keeping gameplay.

**Challenge:** Implement a physics profiler that monitors rigidbodies, collisions, and frame rate. Display stats in-game.

<details><summary>💡 Hints</summary>
- Use Physics.IgnoreCollision() to test collisions dynamically
- Profile with Profiler window to find bottlenecks
- Gizmos.DrawWireCube() visualizes collision bounds
- Time.fixedDeltaTime controls physics update rate
- Solver iterations affect stability (higher = slower but more accurate)
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Debug profiler
public class PhysicsProfiler : MonoBehaviour
{
    private void OnGUI()
    {
        int rbCount = FindObjectsOfType<Rigidbody>().Length;
        int colCount = FindObjectsOfType<Collider>().Length;
        float fps = 1f / Time.deltaTime;

        GUI.Label(new Rect(10, 10, 300, 30), $"Rigidbodies: {rbCount}");
        GUI.Label(new Rect(10, 40, 300, 30), $"Colliders: {colCount}");
        GUI.Label(new Rect(10, 70, 300, 30), $"FPS: {fps:F1}");
    }
}
```

</details>
