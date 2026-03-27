# Day 14: Camera Follow & LateUpdate()

**Learning Target:** Implement smooth camera following using LateUpdate() and Vector3.Lerp().

### Key Concepts

- **LateUpdate():** Called after all Update() methods; perfect for camera logic
- **Vector3.Lerp():** Linear interpolation between two vectors (smooth transitions)
- **transform.LookAt():** Rotates an object to face another object
- **Offset:** Distance between camera and target (usually behind and above)
- **Damping:** Smoothness factor for camera following (0-1; higher = smoother)
- **Clipping Planes:** Near and Far planes determining what the camera renders

### Content

Cameras should update AFTER the player moves. LateUpdate() is called after all Update() methods, making it perfect for camera logic.

**Camera Following Pattern:**
```csharp
void LateUpdate()
{
    // Player has moved in Update()
    // Now move the camera to follow the player
    Vector3 targetPosition = player.position + offset;
    transform.position = Vector3.Lerp(transform.position, targetPosition, dampingSpeed);
}
```

**Vector3.Lerp():**
Lerp stands for "linear interpolation." It smoothly transitions from one vector to another.
```
Vector3.Lerp(a, b, t)
```
- t = 0: returns a
- t = 0.5: returns midpoint
- t = 1: returns b
- t > 1: overshoots beyond b

For camera damping, use a small value like 0.1f or 0.2f to create smooth, non-jarring camera movement.

### Code Examples

```csharp
using UnityEngine;

public class SmoothCameraFollow : MonoBehaviour
{
    public Transform target;  // The player to follow
    public Vector3 offset = new Vector3(0, 2, -5);  // Camera distance from player
    public float dampingSpeed = 0.1f;  // Lower = smoother but laggier
    public bool lookAtPlayer = true;

    void LateUpdate()
    {
        if (target == null)
        {
            Debug.LogError("Camera target is not assigned!");
            return;
        }

        // Calculate the desired camera position
        Vector3 desiredPosition = target.position + offset;

        // Smoothly move the camera toward the desired position
        transform.position = Vector3.Lerp(transform.position, desiredPosition, dampingSpeed);

        // Optional: Make the camera look at the player
        if (lookAtPlayer)
        {
            transform.LookAt(target);
        }
    }
}
```

```csharp
using UnityEngine;

public class FirstPersonCamera : MonoBehaviour
{
    public Transform player;
    public float mouseSensitivity = 100f;
    public float verticalRotationSpeed = 2f;

    private float xRotation = 0f;

    void LateUpdate()
    {
        // Get mouse input
        float mouseX = Input.GetAxis("Mouse X") * mouseSensitivity * Time.deltaTime;
        float mouseY = Input.GetAxis("Mouse Y") * mouseSensitivity * Time.deltaTime;

        // Rotate player left/right (horizontal)
        player.Rotate(Vector3.up * mouseX);

        // Rotate camera up/down (vertical, clamped)
        xRotation -= mouseY;
        xRotation = Mathf.Clamp(xRotation, -90f, 90f);
        transform.localRotation = Quaternion.Euler(xRotation, 0f, 0f);

        // Position camera at player's head
        transform.position = player.position + Vector3.up * 0.6f;
    }
}
```

### Guided Practice

1. Create a Capsule (player) with a Rigidbody
2. Create a Camera GameObject as a child of the player OR as a separate object
3. Create a script that implements camera follow in LateUpdate()
4. Set the offset to (0, 2, -5) to position the camera behind and above
5. Test different dampingSpeed values (0.05, 0.1, 0.2, 0.5)
6. Move the player and observe how the camera follows
7. Try using transform.LookAt() to make the camera always face the player

### Practice Problems

**Problem 1 — Beginner:** Implement a simple camera follow that updates in LateUpdate().

**Problem 2 — Intermediate:** Create a camera system with adjustable offset and damping. Test with different values.

**Problem 3 — Challenge:** Implement both third-person (follow behind) and first-person (look from player's perspective) camera modes.

<details>
<summary>Hints</summary>

**Hint 1:** Use LateUpdate() so the camera moves after the player. Use Vector3.Lerp() for smooth following.

**Hint 2:** The offset determines camera distance. Try (0, 2, -5) for behind and above, or (3, 2, 0) for side view.

**Hint 3:** Lower damping values (0.05-0.1) feel smoother but lag behind. Higher values (0.3+) feel snappier but more jarring.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void LateUpdate()
{
    Vector3 desiredPos = target.position + offset;
    transform.position = Vector3.Lerp(transform.position, desiredPos, damping);
}
```

**Answer 2:** Add public float dampingSpeed and Vector3 offset. Expose them in the Inspector for testing.

**Answer 3:** Use a bool to switch between first-person and third-person. Change offset and camera positioning based on the mode.

</details>
