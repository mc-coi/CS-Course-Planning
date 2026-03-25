# Day 8: Transform Manipulation with Vectors & Time.deltaTime

**Learning Target:** I can use Vector3 to represent position and direction, and create smooth, frame-rate-independent movement.

## Key Concepts

- **Vector3:** A structure representing 3D position or direction (x, y, z)
- **Position:** Where something is in 3D space
- **Direction:** Which way something is facing (normalized vectors have length 1)
- **transform.Translate():** Moves an object relative to its orientation
- **transform.position:** The absolute position of an object
- **transform.Rotate():** Rotates an object
- **Time.deltaTime:** Time elapsed since the last frame (essential for frame-rate-independent movement)
- **Magnitude:** The length of a vector; useful for distance calculations

Vector3 is fundamental to game development. It represents a point in 3D space or a direction.

**Creating Vectors:**
```csharp
Vector3 position = new Vector3(5, 0, 10);  // Position: x=5, y=0, z=10
Vector3 forward = new Vector3(0, 0, 1);   // Direction: pointing forward
Vector3 zero = Vector3.zero;                // Shorthand for (0, 0, 0)
Vector3 up = Vector3.up;                    // Shorthand for (0, 1, 0)
Vector3 right = Vector3.right;              // Shorthand for (1, 0, 0)
```

**Frame-Rate Independence:** Time.deltaTime is essential. Computers run at different frame rates (30 fps, 60 fps, 120 fps). Without deltaTime, faster computers would move faster.

```csharp
// WRONG: Frame-rate dependent (varies by fps)
transform.position += new Vector3(5, 0, 0);

// RIGHT: Frame-rate independent (always 5 units per second)
transform.position += new Vector3(5 * Time.deltaTime, 0, 0);
```

## Code Examples

```csharp
using UnityEngine;

public class SmoothMovement : MonoBehaviour
{
    public float moveSpeed = 5f;           // Units per second
    public float rotationSpeed = 100f;     // Degrees per second
    private Vector3 currentDirection = Vector3.zero;

    void Update()
    {
        // Store the horizontal input
        float horizontalInput = 0f;
        if (Input.GetKey(KeyCode.D))
            horizontalInput += 1f;
        if (Input.GetKey(KeyCode.A))
            horizontalInput -= 1f;

        // Calculate movement direction
        Vector3 moveDirection = new Vector3(horizontalInput, 0, 0);

        // Move the GameObject smoothly using Time.deltaTime
        transform.Translate(moveDirection * moveSpeed * Time.deltaTime);

        // Rotate toward the direction of movement (if moving)
        if (moveDirection.magnitude > 0)
        {
            // Rotate to face movement direction
            float angle = Mathf.Atan2(moveDirection.x, moveDirection.z) * Mathf.Rad2Deg;
            transform.rotation = Quaternion.Euler(0, angle, 0);
        }
    }

    // Calculate distance to another object
    public float DistanceTo(GameObject target)
    {
        Vector3 directionToTarget = target.transform.position - transform.position;
        return directionToTarget.magnitude;
    }

    // Get the direction to another object (normalized)
    public Vector3 DirectionTo(GameObject target)
    {
        Vector3 directionToTarget = target.transform.position - transform.position;
        return directionToTarget.normalized;  // Length = 1
    }
}
```

## Guided Practice

1. Create a script called "VectorPractice"
2. Declare a Vector3 position variable
3. Create a method that calculates the distance between this object and another object
4. Create a method that calculates the direction to another object
5. Print both to the Console and attach the script to a GameObject

## Practice Problems

**Problem 1 — Beginner:** Write a script that calculates the distance between the player and an enemy. The distance should update every frame and print to the Console.

**Problem 2 — Intermediate:** Write a script that rotates a GameObject when you press the Right arrow key, and rotates the opposite direction when you press the Left arrow key.

**Problem 3 — Challenge:** Write a script that calculates velocity as (distance / time). Assume distance and time are known values.

<details>
<summary>Hints</summary>

**Problem 1:** Use Vector3 subtraction to find the direction, then use .magnitude to get the distance.

**Problem 2:** Use Input.GetKey() and transform.Rotate(). Remember to use Time.deltaTime for smooth rotation.

**Problem 3:** Velocity = change in position / time. Use Vector3 operations to calculate the change in position.
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
using UnityEngine;

public class DistanceTracker : MonoBehaviour
{
    public GameObject enemy;

    void Update()
    {
        if (enemy != null)
        {
            Vector3 direction = enemy.transform.position - transform.position;
            float distance = direction.magnitude;
            Debug.Log("Distance to enemy: " + distance);
        }
    }
}
```

**Problem 2:**
```csharp
using UnityEngine;

public class ArrowRotator : MonoBehaviour
{
    public float rotationSpeed = 100f;

    void Update()
    {
        if (Input.GetKey(KeyCode.RightArrow))
        {
            transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
        }

        if (Input.GetKey(KeyCode.LeftArrow))
        {
            transform.Rotate(0, -rotationSpeed * Time.deltaTime, 0);
        }
    }
}
```

**Problem 3:**
```csharp
public class VelocityCalculator : MonoBehaviour
{
    public GameObject startPoint;
    public GameObject endPoint;
    public float timeElapsed = 2f;

    void Start()
    {
        Vector3 displacement = endPoint.transform.position - startPoint.transform.position;
        float distance = displacement.magnitude;
        float velocity = distance / timeElapsed;
        Debug.Log("Velocity: " + velocity + " units per second");
    }
}
```
</details>
