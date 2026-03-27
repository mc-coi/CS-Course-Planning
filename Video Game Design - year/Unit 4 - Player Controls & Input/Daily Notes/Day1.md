# Day 1: Input.GetAxis & Smooth Keyboard Movement

**Learning Target:** I can use Input.GetAxis to read keyboard input and create smooth directional movement.

---

## Key Concepts

**Input.GetAxis("Horizontal")** and **Input.GetAxis("Vertical")** — These Unity methods return a float between **–1 and 1**, smoothly ramping up and down. Unlike GetKeyDown (which fires once), GetAxis is perfect for **continuous movement** because it applies acceleration and deceleration.

**Why smooth input?** Games like *Super Mario Bros* (Nintendo) and *Celeste* feel responsive because movement ramps smoothly rather than snapping on/off. A float value lets you move diagonally and blend animation speeds.

**Keyboard Mapping (Default)**
- WASD or arrow keys → Horizontal (–1 left, +1 right) and Vertical (–1 down, +1 up)
- You can configure this in Edit > Project Settings > Input Manager

---

## Code Example

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // Read smooth input (–1 to 1 range)
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        // Create movement direction
        Vector3 moveDirection = new Vector3(horizontal, 0, vertical).normalized;

        // Apply velocity (Rigidbody physics-based)
        Vector3 newVelocity = moveDirection * moveSpeed;
        rb.velocity = new Vector3(newVelocity.x, rb.velocity.y, newVelocity.z);

        Debug.Log($"Input: H={horizontal}, V={vertical}");
    }
}
```

---

## Unity Setup Steps

1. **Create Player GameObject**
   - Hierarchy: Right-click → 3D Object → Cube
   - Name: "Player"
   - Scale to `(1, 1, 1)` and position at `(0, 0.5, 0)`

2. **Add Physics Components**
   - Inspector: Add Component → Rigidbody
   - Set **Freeze Rotation** (X, Y, Z) to prevent tipping
   - **Mass**: 1

3. **Add PlayerController Script**
   - Assets: Right-click → Create → C# Script → "PlayerController"
   - Drag script onto Player GameObject

4. **Test**
   - Press Play
   - Use **WASD or arrow keys** to move
   - Watch the Debug Log output

---

## Guided Practice

1. **Read Input & Log It** (5 min)
   - Open your PlayerController script
   - Add `Debug.Log()` to print H and V values every frame
   - Press Play, hold W, watch the console ramp from 0 → 1 smoothly

2. **Move the Player** (10 min)
   - Set `rb.velocity` using the horizontal/vertical input
   - Move the Player around the scene
   - Try pressing W+D simultaneously → diagonal movement

3. **Adjust Speed & Feel** (5 min)
   - Change `moveSpeed` from 5 to 10 in the Inspector
   - Notice how the game feels faster/snappier
   - Find a speed that *feels* responsive (this is playtesting!)

---

## Practice Problems

**Beginner:** Create a simple 2D platformer player (use a Quad instead of Cube). Move left/right with WASD. Print the current direction to the console.

**Intermediate:** Add a debug visualizer: draw a `Debug.DrawRay(transform.position, moveDirection * 2, Color.green)` to see the movement vector in the Scene view.

**Challenge:** Implement **input buffering**: store the last input direction for 0.1 seconds, so rapid direction changes feel snappy rather than sluggish. (Hint: Use a float timer that counts down, only overwrite buffer if timer ≤ 0.)

<details><summary>💡 Hints</summary>
- `Vector3.normalized` removes the magnitude so diagonal movement isn't faster than cardinal movement.
- If movement feels too fast, reduce `moveSpeed`. If it feels sluggish, increase it.
- The Input Manager applies acceleration automatically; you don't need to manually lerp the axis value.
</details>

<details><summary>✅ Sample Answers</summary>

**Beginner Solution:**
```csharp
public class SimplePlayer : MonoBehaviour
{
    public float moveSpeed = 5f;
    private Rigidbody rb;

    void Start() => rb = GetComponent<Rigidbody>();

    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        Vector3 move = new Vector3(h, 0, v).normalized * moveSpeed;
        rb.velocity = new Vector3(move.x, rb.velocity.y, move.z);
        Debug.Log($"Direction: {move.normalized}");
    }
}
```

**Challenge Solution (Input Buffer):**
```csharp
private Vector3 bufferedDirection;
private float bufferTimer = 0f;
private const float BUFFER_DURATION = 0.1f;

void Update()
{
    float h = Input.GetAxis("Horizontal");
    float v = Input.GetAxis("Vertical");

    if (bufferTimer <= 0 && (h != 0 || v != 0))
    {
        bufferedDirection = new Vector3(h, 0, v).normalized;
        bufferTimer = BUFFER_DURATION;
    }

    bufferTimer -= Time.deltaTime;
    rb.velocity = new Vector3(bufferedDirection.x * moveSpeed, rb.velocity.y, bufferedDirection.z * moveSpeed);
}
```

</details>
