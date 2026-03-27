# Day 9: Rigidbody & Gravity

**Learning Target:** Understand how Rigidbody components simulate physics and how to apply forces to objects in Unity.

### Key Concepts

- **Rigidbody:** A component that simulates physics (gravity, forces, collisions)
- **Mass:** How heavy an object is; affects acceleration from forces
- **Gravity:** Constant downward acceleration (default: -9.81 m/s²)
- **Drag:** Air resistance; opposes movement
- **Angular Drag:** Air resistance for rotation
- **AddForce():** Applies a force to the Rigidbody
- **Velocity:** The current speed and direction of movement
- **FixedUpdate():** Called at a fixed time step for physics calculations (default: 50 times per second)
- **Physics Timestep:** The rate at which Unity calculates physics (independent of frame rate)

### Content

The Rigidbody component is essential for physics-based games. Without a Rigidbody, an object doesn't fall or respond to forces. With a Rigidbody, gravity and forces work automatically.

**Adding a Rigidbody:**
1. Select a GameObject
2. In the Inspector, click "Add Component"
3. Search for "Rigidbody" and add it
4. Properties appear: Mass, Drag, Angular Drag, gravity enabled, etc.

**Key Properties:**
- **Mass:** Higher mass = harder to push around (default: 1)
- **Drag:** Friction from air (0 = no drag, higher = more resistance to movement)
- **Gravity Scale:** Multiplier for gravity (1 = normal, 2 = twice as strong)
- **Constraints:** Lock axes to prevent unwanted movement/rotation

**FixedUpdate vs Update:**
- **Update():** Called once per frame (variable frame rate)
- **FixedUpdate():** Called at fixed physics timestep (50 times/sec by default)

Physics code should go in FixedUpdate(). If you use Update() for forces, the frame rate will affect physics. FixedUpdate() ensures consistent physics regardless of frame rate.

### Code Examples

```csharp
using UnityEngine;

public class PhysicsBasics : MonoBehaviour
{
    public float jumpForce = 5f;
    public float moveForce = 10f;
    private Rigidbody rb;

    void Start()
    {
        // Cache the Rigidbody component for efficiency
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Jump input detection (use Update for input)
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }
    }

    void FixedUpdate()
    {
        // Apply forces in FixedUpdate for consistent physics
        if (Input.GetKey(KeyCode.D))
        {
            // Add force in the right direction
            rb.AddForce(moveForce, 0, 0, ForceMode.Force);
        }

        if (Input.GetKey(KeyCode.A))
        {
            rb.AddForce(-moveForce, 0, 0, ForceMode.Force);
        }
    }

    void Jump()
    {
        // Apply upward force
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z); // Reset Y velocity
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
        Debug.Log("Jumped!");
    }
}
```

### Guided Practice

1. Create a new Cube in your scene
2. Add a Rigidbody component to the Cube
3. Create a Plane below the Cube as ground
4. Add a BoxCollider to the Plane
5. Press Play and watch the Cube fall due to gravity
6. Experiment with changing the Mass and Drag values
7. Try adding force with the script above and test movement with A/D keys

### Practice Problems

**Problem 1 — Beginner:** Create a Cube, add a Rigidbody to it, and let gravity pull it down. What happens when you run the scene?

**Problem 2 — Intermediate:** Create a script that applies horizontal force with A/D keys and makes the object accelerate smoothly. Adjust the moveForce value to find a good feel.

**Problem 3 — Challenge:** Create a jumping mechanic where pressing Space makes the object jump, but only if it's touching the ground. Use a raycast (you'll learn this soon!) or a simple collision check.

<details>
<summary>Hints</summary>

**Hint 1:** Make sure "Use Gravity" is checked on the Rigidbody. If the Cube doesn't fall, that's likely the issue.

**Hint 2:** For the force script, use FixedUpdate() for all physics operations, not Update().

**Hint 3:** To prevent infinite jumping, you need to track when the object is grounded. A simple approach is to check if the object has been falling for a few frames.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:** The Cube falls down due to gravity. The Rigidbody component simulates gravity by default. If there's a Plane below, the Cube collides with it and stops.

**Answer 2:**
```csharp
void FixedUpdate()
{
    if (Input.GetKey(KeyCode.D))
        rb.AddForce(moveForce, 0, 0);
    if (Input.GetKey(KeyCode.A))
        rb.AddForce(-moveForce, 0, 0);
}
```

**Answer 3:** You need to detect when the object is grounded. This is covered in Day 12, but for now, you can use a simple counter or raycast.

</details>
