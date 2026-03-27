# Day 14: Prefabs (Part 2) & Instantiation

**Learning Target:** I can instantiate prefabs from C# scripts and manage runtime object spawning.

---

## Key Concepts

**Instantiate()** — Creates a copy of a prefab. Can be called anytime, including during gameplay.

**Spawn/Spawning** — Creating objects dynamically at runtime (e.g., bullets, enemies, loot drops).

**Prefab Overrides** — Instance-specific changes that don't affect the prefab or other instances (useful for one-off variations).

**Destroying Objects** — Destroy(gameObject) removes an object from the scene.

---

## Instantiate Syntax

```csharp
// Simplest: Instantiate at origin
Instantiate(prefab);

// With position
Instantiate(prefab, new Vector3(5, 0, 0), Quaternion.identity);

// With position and rotation
Instantiate(prefab, position, Quaternion.Euler(0, 45, 0));

// As child of another transform
Instantiate(prefab, parentTransform);

// Store reference for immediate modification
GameObject newObject = Instantiate(prefab, position, Quaternion.identity);
newObject.name = "Instance_42";
```

---

## Unity Setup Steps

1. **Create a sphere prefab** (blue material, Rigidbody)
2. **Create a script called "Spawner":**
   ```csharp
   using UnityEngine;
   
   public class Spawner : MonoBehaviour
   {
       public GameObject prefabToSpawn;
       
       void Start()
       {
           for(int i = 0; i < 5; i++)
           {
               Instantiate(prefabToSpawn, new Vector3(i * 2, 2, 0), Quaternion.identity);
           }
       }
   }
   ```
3. **Create an empty GameObject** named "Spawner"
4. **Attach the Spawner script** to it
5. **Drag the sphere prefab** into the "Prefab To Spawn" field in Inspector
6. **Press Play:** 5 sphere instances appear and fall (due to gravity)

---

## Guided Practice

1. **Create a prefab with a script** that logs its name when instantiated
2. **Write a spawner script** that instantiates 10 of these prefabs at random positions
3. **Press Play and watch the Console** — you should see 10 log messages
4. **Add random rotations:** Each spawned object rotates differently

---

## Practice Problems

**Beginner:** Write a spawner that creates 10 cube instances in a line (0,0,0 to 9,0,0).

**Intermediate:** Create a spawner that instantiates spheres at random positions within a range (e.g., X: -5 to 5, Y: 0 to 10, Z: -5 to 5).

**Challenge:** Build a "particle effect" spawner: create many small spheres at a single point, each with a random velocity. Use Rigidbody.velocity to make them burst outward.

<details>
<summary>💡 Hints</summary>
- Use Random.Range(min, max) for random values
- Quaternion.identity = no rotation (0, 0, 0 Euler angles)
- You can instantiate prefabs without a parent, making them world-space objects
- Instantiate returns the new object; assign it to a variable to modify it immediately
- Destroy(gameObject) removes objects; useful for cleanup
</details>

<details>
<summary>✅ Sample: Burst Spawner</summary>

```csharp
using UnityEngine;

public class BurstSpawner : MonoBehaviour
{
    public GameObject spherePrefab;
    public int burstCount = 20;
    public float burstSpeed = 10f;
    
    void Start()
    {
        for(int i = 0; i < burstCount; i++)
        {
            // Spawn at this location
            GameObject newSphere = Instantiate(spherePrefab, transform.position, Quaternion.identity);
            
            // Get the Rigidbody and set velocity
            Rigidbody rb = newSphere.GetComponent<Rigidbody>();
            if(rb != null)
            {
                // Random direction
                Vector3 randomDirection = Random.onUnitSphere;
                rb.velocity = randomDirection * burstSpeed;
            }
        }
    }
}
```

Result: 20 spheres burst outward from a central point.

</details>
