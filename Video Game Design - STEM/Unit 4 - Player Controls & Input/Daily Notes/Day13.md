# Day 13: Input.GetAxis() & Smooth Input

**Learning Target:** Implement smooth, analog input using GetAxis() for responsive player movement.

### Key Concepts

- **Input.GetAxis():** Returns a float from -1 to 1 (smooth analog input)
- **Input.GetAxisRaw():** Returns -1, 0, or 1 (discrete digital input)
- **Input Manager:** Configuration panel for defining axes (horizontal, vertical, etc.)
- **Acceleration:** Axis builds up smoothly from 0 (good for movement)
- **Dead Zone:** Small threshold before input is registered (prevents controller drift)
- **Sensitivity:** Speed at which axis reaches maximum value

### Content

GetAxis() is superior to GetKey() for continuous movement. Instead of instant on/off, it provides smooth ramping from 0 to 1. This feels much better for player movement.

**GetAxis vs GetKey:**
```
GetKey(KeyCode.D)          // Returns true or false (instant)
GetAxis("Horizontal")      // Returns -1, -0.5, 0, 0.5, 1 (smooth)
```

**Input Manager Setup:**
1. Edit > Project Settings > Input Manager
2. View the predefined axes: "Horizontal", "Vertical"
3. Horizontal is mapped to: A/D keys and Left Stick (controller)
4. Vertical is mapped to: W/S keys and Left Stick (controller)

GetAxis() automatically returns smooth values for both keyboard and controller, making your game feel responsive and natural.

### Code Examples

```csharp
using UnityEngine;

public class SmoothMovementController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float acceleration = 1f;
    public float deceleration = 2f;

    private Rigidbody rb;
    private Vector3 currentVelocity = Vector3.zero;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Get smooth input from -1 to 1
        float horizontal = Input.GetAxis("Horizontal");  // A/D or Left Stick
        float vertical = Input.GetAxis("Vertical");      // W/S or Left Stick

        // Build desired velocity
        Vector3 desiredVelocity = new Vector3(horizontal, 0, vertical).normalized * moveSpeed;

        // Smoothly interpolate toward desired velocity
        currentVelocity = Vector3.Lerp(currentVelocity, desiredVelocity, Time.deltaTime * acceleration);

        Debug.Log("Input: (" + horizontal + ", " + vertical + ")");
    }

    void FixedUpdate()
    {
        // Apply the smoothed velocity
        rb.velocity = new Vector3(currentVelocity.x, rb.velocity.y, currentVelocity.z);
    }

    // Method to create custom axes in Input Manager
    // This is usually done in Edit > Project Settings > Input Manager
}
```

### Guided Practice

1. Create a Capsule (player character) with a Rigidbody
2. Create a Plane as the ground
3. Create a script that uses Input.GetAxis("Horizontal") and Input.GetAxis("Vertical")
4. Implement smooth movement by setting rb.velocity based on input
5. Press Play and test movement with A/D/W/S keys
6. Compare the feel to using GetKey() directly
7. Adjust moveSpeed and acceleration values to find a good feel

### Practice Problems

**Problem 1 — Beginner:** Set up smooth movement using Input.GetAxis("Horizontal") and Input.GetAxis("Vertical").

**Problem 2 — Intermediate:** Implement acceleration and deceleration so the character doesn't instantly reach max speed.

**Problem 3 — Challenge:** Create a custom axis in the Input Manager and use it to control something (like camera zoom).

<details>
<summary>Hints</summary>

**Hint 1:** Use GetAxis() instead of GetKey(). GetAxis() returns smooth values from -1 to 1.

**Hint 2:** Normalize the input vector to prevent faster diagonal movement: `new Vector3(h, 0, v).normalized`

**Hint 3:** Apply input in Update() but set velocity in FixedUpdate() for consistent physics.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void Update()
{
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");

    Vector3 moveDirection = new Vector3(horizontal, 0, vertical);
    rb.velocity = new Vector3(moveDirection.x * moveSpeed, rb.velocity.y, moveDirection.z * moveSpeed);
}
```

**Answer 2:**
```csharp
float horizontal = Input.GetAxis("Horizontal");
Vector3 desiredVelocity = new Vector3(horizontal, 0, 0) * moveSpeed;
currentVelocity = Vector3.Lerp(currentVelocity, desiredVelocity, Time.deltaTime * acceleration);
rb.velocity = new Vector3(currentVelocity.x, rb.velocity.y, currentVelocity.z);
```

**Answer 3:** Go to Edit > Project Settings > Input Manager and add a new axis with custom key bindings.

</details>
