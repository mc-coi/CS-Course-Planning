# Day 1: Rigidbody Basics & Mass

**Learning Target:** I can add a Rigidbody component to a GameObject and understand how mass and gravity affect object behavior.

---

## Key Concepts

**Rigidbody** is the component that makes a GameObject subject to physics simulation. You'll find it in the **Inspector** by clicking **Add Component > Physics > Rigidbody** (or **Rigidbody 3D** in newer Unity versions).

**Mass** — How heavy the object is. Higher mass = more force needed to move it. Default is 1 kg.

**Gravity Scale** — How much the global gravity affects this object. Set to 1 for normal falling, 0 to ignore gravity (floating), 2 to fall twice as fast.

**Drag** — Air resistance. Higher values slow the object down over time. Default 0 = no drag.

**Angular Drag** — Rotational resistance. Controls how quickly spinning slows down.

**isKinematic** — When checked, the object won't be affected by physics forces, but you can move it manually with scripts. Useful for moving platforms.

**Real-world examples:**
- **Super Mario:** Mario has a Rigidbody that falls due to gravity and responds to jump forces.
- **Angry Birds:** Blocks have Rigidbodies with varying masses — wood is lighter than stone.
- **Portal:** The Weighted Storage Cube has a Rigidbody that can be picked up by portals.

---

## Code Example

```csharp
using UnityEngine;

public class RigidbodyBasics : MonoBehaviour
{
    private Rigidbody rb;

    private void Start()
    {
        // Get the Rigidbody component attached to this GameObject
        rb = GetComponent<Rigidbody>();

        // Print mass to console
        Debug.Log("Object mass: " + rb.mass + " kg");
    }

    private void FixedUpdate()
    {
        // Always use FixedUpdate for physics-related code
        // This runs at fixed time intervals (50 times per second by default)

        // Apply a downward force (additional to gravity)
        rb.AddForce(Vector3.down * 5f, ForceMode.Force);
    }

    // Method to jump
    public void Jump(float jumpForce)
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }
}
```

---

## Unity Setup Steps

1. **Create a cube:** Right-click in Hierarchy → 3D Object → Cube
2. **Add Rigidbody:** Select the cube → Inspector → Add Component → Physics → Rigidbody
3. **Observe default values:** Mass = 1, Drag = 0, Angular Drag = 0.05
4. **Press Play:** Watch the cube fall (gravity is enabled by default)
5. **Pause and inspect:** Notice velocity increased in Rigidbody component as it fell
6. **Increase Mass to 5:** Press Play again and compare fall speed (mass doesn't affect fall speed in uniform gravity, but it affects force response)
7. **Set Gravity Scale to 0:** Press Play and the cube floats

---

## Guided Practice

1. Create three cubes with masses 0.5, 1, and 3 kg
2. Attach a script to each that applies the same upward force (AddForce)
3. Observe which cube accelerates fastest (the lightest one!)
4. Modify the script to print velocity each frame: `Debug.Log(rb.velocity.magnitude)`
5. Change Drag to 2 on one cube — notice it slows down faster

---

## Practice Problems

**Beginner:** Create a script that makes a sphere fall twice as fast as normal. (Hint: Use gravity scale or AddForce in FixedUpdate.)

**Intermediate:** Create a "feather" (low mass, high drag) and a "bowling ball" (high mass, low drag). Add the same upward force to both. Which reaches higher? Explain why in a comment.

**Challenge:** Build a simple "jump" system. In Update, detect when the player presses Space. In a Jump() method, reset vertical velocity to 0, then AddForce upward. Print "Jump!" to the console.

<details><summary>💡 Hints</summary>
- Use `rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z)` to zero out only vertical velocity
- ForceMode.Impulse applies force as a single instant push
- ForceMode.Force applies force over time (default physics tick)
- FixedUpdate is called before physics calculations, so it's the right place for physics code
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Beginner: Faster falling
public class FastFall : MonoBehaviour
{
    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        rb.gravityScale = 2f; // Fall twice as fast
    }
}

// Challenge: Simple jump system
public class SimpleJump : MonoBehaviour
{
    private Rigidbody rb;
    public float jumpForce = 5f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }
    }

    private void Jump()
    {
        // Zero out only the Y velocity so we jump from the ground
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        Debug.Log("Jump!");
    }
}
```

</details>
