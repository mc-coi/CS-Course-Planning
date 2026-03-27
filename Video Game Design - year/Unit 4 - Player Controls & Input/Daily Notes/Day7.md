# Day 7: Smooth Camera Follow with Lerp

**Learning Target:** I can implement a smooth camera follow system that trails behind the player without jitter.

---

## Key Concepts

**Camera Follow** — The camera should follow the player smoothly, not snap to their position every frame. This creates a cinematic, polished feel.

**Lerp (Linear Interpolation)** — `Vector3.Lerp(a, b, t)` smoothly interpolates from `a` to `b`. Where `t` is a value 0–1:
- `t = 0` → Position is at `a`
- `t = 0.5` → Position is halfway between `a` and `b`
- `t = 1` → Position is at `b`

**Why Lerp for cameras?** Instead of snapping the camera to the player, Lerp it smoothly so it "chases" the player. This feels cinematic and is used in *Zelda*, *Fortnite*, and *Halo*.

**Frame-Rate Independence:** Use `Time.deltaTime` with a speed multiplier to ensure smooth follow on any frame rate.

---

## Code Example

```csharp
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform target; // The player
    public float followDistance = 10f; // Distance behind player
    public float followHeight = 3f; // Height above player
    public float smoothSpeed = 5f; // Higher = snappier follow
    public Vector3 offset = Vector3.zero; // Manual offset

    private void LateUpdate()
    {
        if (target == null) return;

        // Calculate desired position
        Vector3 desiredPosition = target.position 
            + target.right * offset.x 
            + Vector3.up * followHeight 
            + -target.forward * followDistance;

        // Smoothly move camera toward desired position
        transform.position = Vector3.Lerp(
            transform.position,
            desiredPosition,
            smoothSpeed * Time.deltaTime
        );

        // Look at the player
        transform.LookAt(target.position + Vector3.up * followHeight);
    }
}
```

---

## Unity Setup Steps

1. **Set Up Camera**
   - In Hierarchy, select "Main Camera"
   - Remove default Camera script if present
   - Position at `(0, 5, -10)` looking at the player

2. **Attach CameraFollow Script**
   - Create C# script → "CameraFollow"
   - Attach to Main Camera
   - In Inspector, drag Player into "Target" field
   - Set followDistance to `10`
   - Set followHeight to `3`
   - Set smoothSpeed to `5`

3. **Test**
   - Press Play and move the player around
   - Camera should smoothly follow behind

4. **Tune**
   - Increase smoothSpeed (5 → 8) for snappier follow
   - Adjust followDistance and followHeight to find good angles

---

## Guided Practice

1. **Understand Lerp** (5 min)
   - In a separate test script, lerp a cube's position between two points
   - Print the progress (0 → 1) to see interpolation

2. **Implement Basic Follow** (10 min)
   - Calculate a `desiredPosition` based on player position + offset
   - Use `Vector3.Lerp()` to smoothly move toward that position
   - Test following the player

3. **Make Camera Look at Player** (5 min)
   - Add `transform.LookAt()` to have the camera always face the player
   - Adjust the look-at point to be slightly above the player's center

---

## Practice Problems

**Beginner:** Create a camera that smoothly follows the player at a fixed distance and height. Use Lerp to smooth the movement.

**Intermediate:** Implement a **lead-ahead camera**: predict where the player will be based on their velocity and aim the camera slightly ahead. (Hint: Use `rb.velocity * lookAheadTime`.)

**Challenge:** Implement **dynamic distance**: if the player is moving fast, move the camera further back. If stationary, move closer. Use Lerp to smoothly adjust the distance.

<details><summary>💡 Hints</summary>
- Use `LateUpdate()` instead of `Update()` to ensure camera moves after player movement is finalized.
- `Vector3.Lerp(a, b, Time.deltaTime * speed)` is frame-rate independent.
- `transform.LookAt()` makes the transform face a given position.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Lead-Ahead):**
```csharp
private Rigidbody targetRb;
public float lookAheadTime = 0.5f;

void LateUpdate()
{
    Vector3 predictedPos = target.position + targetRb.velocity * lookAheadTime;
    Vector3 desiredPosition = predictedPos 
        + -target.forward * followDistance 
        + Vector3.up * followHeight;

    transform.position = Vector3.Lerp(
        transform.position,
        desiredPosition,
        smoothSpeed * Time.deltaTime
    );

    transform.LookAt(predictedPos + Vector3.up * followHeight);
}
```

**Challenge Solution (Dynamic Distance):**
```csharp
void LateUpdate()
{
    float speed = targetRb.velocity.magnitude;
    float dynamicDistance = Mathf.Lerp(5f, 15f, Mathf.Clamp01(speed / 10f));
    
    Vector3 desiredPosition = target.position 
        + -target.forward * dynamicDistance 
        + Vector3.up * followHeight;

    transform.position = Vector3.Lerp(
        transform.position,
        desiredPosition,
        smoothSpeed * Time.deltaTime
    );
}
```

</details>
