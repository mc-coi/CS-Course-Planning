# Day 2: Transform Component & Manipulation Tools

**Learning Target:** I can use Transform properties to position, rotate, and scale GameObjects using manipulation tools and code.

## Key Concepts

- **Transform Component:** Stores position (x, y, z), rotation (x, y, z), and scale (x, y, z)
- **Position:** Where the GameObject is in 3D space, relative to its parent
- **Rotation:** The angle of the GameObject in three axes (degrees)
- **Scale:** The size multiplier (1.0 = normal size, 2.0 = twice as large)
- **Parent/Child Relationship:** GameObjects can be nested (child inherits parent's transform)
- **Gizmos:** Visual handles in the Scene view for moving, rotating, scaling
- **Local vs. World Space:** Local is relative to parent; world is absolute position in scene

The **Move Tool** (W key), **Rotate Tool** (E key), and **Scale Tool** (R key) are the primary manipulation tools. When you select a GameObject:
- Press W to activate the Move gizmo (three colored arrows for X, Y, Z axes)
- Press E to activate the Rotate gizmo (three colored circles)
- Press R to activate the Scale gizmo (three colored handles)

The Hierarchy panel shows the scene structure. When one GameObject is a child of another, the child's position is relative to the parent. This is useful for organizing complex objects (e.g., a weapon might be a child of a player's hand).

## Code Examples

```csharp
using UnityEngine;

public class Rotator : MonoBehaviour
{
    // Speed of rotation in degrees per second
    public float rotationSpeed = 50f;

    void Update()
    {
        // Rotate the GameObject around the Y axis (vertical)
        // Multiply by Time.deltaTime for frame-rate-independent movement
        transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
    }
}
```

```csharp
using UnityEngine;

public class Mover : MonoBehaviour
{
    // The speed at which the GameObject moves
    public float speed = 5f;

    void Update()
    {
        // Move the GameObject forward along its Z axis
        // Time.deltaTime ensures smooth movement regardless of frame rate
        transform.Translate(0, 0, speed * Time.deltaTime);
    }
}
```

## Guided Practice

1. Create a new scene with a Cube and Plane
2. Use the Move tool (W) to position the Cube above the Plane
3. Use the Rotate tool (E) to tilt the Cube
4. Use the Scale tool (R) to make the Cube larger
5. Create a child GameObject under the Cube and move the parent to see the child move with it

## Practice Problems

**Problem 1 — Beginner:** What are the Transform coordinates of a Cube positioned 3 units right, 2 units up, and 1 unit forward from the origin?

**Problem 2 — Intermediate:** Create a GameObject with a child GameObject nested under it. Move the parent and describe what happens to the child.

**Problem 3 — Challenge:** Write a script that rotates a GameObject 360 degrees over 10 seconds smoothly using transform.Rotate() and Time.deltaTime.

<details>
<summary>Hints</summary>

**Problem 1:** Position uses (X, Y, Z) coordinates. Right is positive X, up is positive Y, forward is positive Z.

**Problem 2:** Drag a GameObject onto another in the Hierarchy to make it a child. Then use the Move tool to move the parent.

**Problem 3:** Calculate rotationSpeed = 360 / 10 = 36 degrees per second. Use Time.deltaTime to make it frame-rate independent.
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:** Position: (3, 2, 1). X = 3 (right), Y = 2 (up), Z = 1 (forward).

**Problem 2:** When you move the parent GameObject, the child moves with it while maintaining its relative position. The child's local position stays the same, but its world position changes because it's attached to the parent.

**Problem 3:**
```csharp
using UnityEngine;

public class FullRotation : MonoBehaviour
{
    void Update()
    {
        // 36 degrees per second = 360 degrees in 10 seconds
        transform.Rotate(0, 36 * Time.deltaTime, 0);
    }
}
```
</details>
