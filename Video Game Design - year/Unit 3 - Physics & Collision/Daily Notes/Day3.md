# Day 3: Colliders — Types & Setup

**Learning Target:** I can add and configure different collider types (Box, Sphere, Capsule) to detect collisions.

---

## Key Concepts

**Collider** — A component that defines the physical shape used for collision detection. Every physics object needs at least one.

**BoxCollider** — Rectangular collision shape. Best for cubes, crates, walls, platforms. Found in Inspector → Add Component → Physics → Box Collider.

**SphereCollider** — Spherical collision shape. Best for balls, projectiles, round obstacles.

**CapsuleCollider** — Cylinder with rounded ends. Best for humanoid characters (tall and narrow).

**MeshCollider** — Uses the 3D model's actual mesh shape for precise collision. Slower but accurate for complex shapes. Avoid on moving objects.

**Edit Collider button** — Click to visually resize/adjust collider shape in the Scene view (green wireframe).

**isTrigger checkbox** — When checked, the collider becomes a trigger zone (no physical collision, but OnTriggerEnter fires). Useful for pickups and damage zones.

**Real-world examples:**
- **Super Mario:** Mario is a Capsule, blocks are BoxColliders, coins are SphereColliders set as triggers
- **Sonic:** Ring pickups are SphereColliders with isTrigger = true
- **Dark Souls:** Enemy weapon hitboxes are often trigger zones for damage detection

---

## Code Example

```csharp
using UnityEngine;

public class ColliderSetup : MonoBehaviour
{
    private BoxCollider boxCol;
    private SphereCollider sphereCol;
    private CapsuleCollider capsuleCol;

    private void Start()
    {
        // Get colliders attached to this GameObject
        boxCol = GetComponent<BoxCollider>();
        sphereCol = GetComponent<SphereCollider>();
        capsuleCol = GetComponent<CapsuleCollider>();

        // Disable all except the first one
        if (boxCol != null) boxCol.enabled = true;
        if (sphereCol != null) sphereCol.enabled = false;
        if (capsuleCol != null) capsuleCol.enabled = false;

        // You can resize colliders in code too
        if (boxCol != null)
        {
            boxCol.size = new Vector3(2f, 1f, 1f);
            boxCol.center = new Vector3(0, 0.5f, 0);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create three objects:** Cube, Sphere, Capsule
2. **To Cube, add BoxCollider:** Already has one by default!
3. **To Sphere, add SphereCollider:** It has this by default too
4. **To Capsule, add CapsuleCollider:** Default component
5. **Click Edit Collider button:** You'll see a green wireframe outline. Resize by dragging
6. **Create a ground plane** and add a BoxCollider (disable Rigidbody or set to Static)
7. **Press Play:** Objects should collide and stack realistically
8. **Experiment:** Adjust collider sizes in Inspector while playing to see effect

---

## Guided Practice

1. Create a humanoid character by stacking a Capsule (body), Sphere (head), two Capsules (arms)
2. Each part should have its own collider (some already built-in)
3. Add Rigidbody to the body only, then to the head — what happens?
4. Now disable Rigidbody on the head and make it a child of the body (drag in Hierarchy)
5. Add a child collider to each limb and see them fall together

---

## Practice Problems

**Beginner:** Create three different objects (cube, sphere, cylinder) and add appropriate colliders. Drop them onto a ground plane. Do they collide realistically?

**Intermediate:** Create a "player" using a capsule and a "coin" using a sphere with isTrigger = true. Add a script to the coin that prints "Coin picked up!" when the player touches it.

**Challenge:** Build a bowling alley. Create pins (capsules) and a ball (sphere). Adjust mass and friction so the ball can knock over the pins realistically.

<details><summary>💡 Hints</summary>
- Every 3D object created in Unity already has a default collider (BoxCollider for Cube, SphereCollider for Sphere, etc.)
- Use Edit Collider to visually match the collider to your object's actual shape
- MeshCollider is powerful but slow—only use for static or rarely-moving objects
- For a character, use one tall Capsule instead of stacking shapes
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Intermediate: Coin with trigger
public class CoinTrigger : MonoBehaviour
{
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            Debug.Log("Coin picked up!");
            Destroy(gameObject);
        }
    }
}
```

</details>
