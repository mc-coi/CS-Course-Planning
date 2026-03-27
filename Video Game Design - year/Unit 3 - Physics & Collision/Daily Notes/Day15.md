# Day 15: Physics Materials — Friction & Bounciness

**Learning Target:** I can adjust friction and bounciness using PhysicMaterial to create different surface behaviors.

---

## Key Concepts

**PhysicMaterial** — A material asset that defines how objects interact physically (friction, bounce). Created as separate asset file.

**Friction** — How much an object resists sliding. 0 = ice (slippery), 1+ = carpet (sticky). Two frictions are combined: static friction (prevents initial movement) and dynamic friction (sliding resistance).

**Bounciness** — How much energy is retained when bouncing. 0 = no bounce (dead), 1 = perfect bounce, >1 = infinite energy bounce.

**Friction Combine & Bounce Combine** — How to combine two materials' properties when objects collide.

**Real-world examples:**
- **Ice skating:** Very low friction material
- **Billiard balls:** High bounciness, low friction
- **Mud:** High friction, no bounciness
- **Rubber ball:** High bounciness, medium friction

---

## Code Example

```csharp
using UnityEngine;

public class PhysicMaterialManager : MonoBehaviour
{
    // Reference to objects with different materials
    public Collider iceCollider;
    public Collider mudCollider;
    public Collider rubberCollider;

    private PhysicMaterial iceMaterial;
    private PhysicMaterial mudMaterial;
    private PhysicMaterial rubberMaterial;

    private void Start()
    {
        // Create PhysicMaterials
        iceMaterial = new PhysicMaterial("Ice");
        iceMaterial.staticFriction = 0.1f;
        iceMaterial.dynamicFriction = 0.1f;
        iceMaterial.bounciness = 0.2f;

        mudMaterial = new PhysicMaterial("Mud");
        mudMaterial.staticFriction = 1f;
        mudMaterial.dynamicFriction = 1f;
        mudMaterial.bounciness = 0f;

        rubberMaterial = new PhysicMaterial("Rubber");
        rubberMaterial.staticFriction = 0.6f;
        rubberMaterial.dynamicFriction = 0.6f;
        rubberMaterial.bounciness = 0.9f;

        // Assign materials
        iceCollider.material = iceMaterial;
        mudCollider.material = mudMaterial;
        rubberCollider.material = rubberMaterial;
    }
}

public class SlipperyFloorEffect : MonoBehaviour
{
    private Rigidbody rb;
    public float slideMultiplier = 1.5f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        float moveInput = Input.GetAxis("Horizontal");
        Vector3 moveDir = transform.right * moveInput;

        // Apply force
        rb.AddForce(moveDir * 5f);
    }

    private void OnCollisionEnter(Collision collision)
    {
        // Check if we hit ice
        if (collision.gameObject.name.Contains("Ice"))
        {
            rb.velocity *= slideMultiplier;
            Debug.Log("Sliding on ice!");
        }
    }
}
```

---

## Unity Setup Steps

**Create and assign PhysicMaterial through Inspector:**
1. Right-click in Project → Create → Physics Material
2. Select the material → Inspector shows:
   - Static Friction: 0.6 (default)
   - Dynamic Friction: 0.6 (default)
   - Bounciness: 0 (default)
3. Create 3 materials: Ice, Mud, Rubber with different values
4. Create 3 floors (planes): Ice, Mud, Rubber
5. Select each floor's Collider → Drag material into Material field
6. Test by dropping a bouncy ball on each

---

## Guided Practice

1. Create three surfaces with different materials
2. Drop a ball on ice—watch it slide far
3. Drop same ball on mud—watch it stick
4. Drop on rubber—watch it bounce high
5. Modify friction and bounce values and observe changes

---

## Practice Problems

**Beginner:** Create ice floor (low friction) and mud floor (high friction). Move player around both and feel the difference.

**Intermediate:** Create a ball physics puzzle. Different platforms have different friction and bounciness. Ball must reach the goal by using physics properties correctly.

**Challenge:** Build a "surface detector" system. When player walks on different surfaces, apply movement modifiers (slow on mud, fast on ice). Provide visual feedback.

<details><summary>💡 Hints</summary>
- Static friction prevents initial movement
- Dynamic friction applies while sliding
- Set bounciness to 0 for non-bouncy objects
- Friction values 0-1 are typical (can be higher)
- Combine materials carefully—both frictions matter
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Surface detection with feedback
public class SurfaceDetector : MonoBehaviour
{
    private Rigidbody rb;
    private float currentFriction = 1f;
    public Material iceMaterial;
    public Material mudMaterial;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void OnCollisionEnter(Collision collision)
    {
        PhysicMaterial mat = collision.gameObject.GetComponent<Collider>().material;
        
        if (mat != null)
        {
            currentFriction = mat.dynamicFriction;
            
            if (currentFriction < 0.3f)
            {
                GetComponent<Renderer>().material = iceMaterial;
            }
            else if (currentFriction > 0.8f)
            {
                GetComponent<Renderer>().material = mudMaterial;
            }
        }
    }
}
```

</details>
