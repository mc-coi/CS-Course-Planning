# Day 5: Input Handling (Input.GetKey and Input.GetAxis)

**Learning Target:** I can detect player input and use it to control GameObjects in real time.

---

## Key Concepts

**Input.GetKey()** — Returns true while a key is held down.

**Input.GetKeyDown()** — Returns true only on the frame the key is first pressed.

**Input.GetAxis()** — Returns a smooth value (-1 to 1) for movement axes (WASD, arrows, joystick).

**Input.GetMouseButton()** — Detects mouse clicks.

**Time.deltaTime** — Essential for frame-rate-independent movement.

---

## Input Examples

```csharp
using UnityEngine;

public class PlayerInput : MonoBehaviour
{
    public float moveSpeed = 5f;
    
    void Update()
    {
        // Detect single key press
        if(Input.GetKeyDown(KeyCode.Space))
        {
            Debug.Log("Jump!");
        }
        
        // Detect key held
        if(Input.GetKey(KeyCode.W))
        {
            Debug.Log("Moving forward");
        }
        
        // Use GetAxis for smooth movement (returns -1 to 1)
        float horizontalInput = Input.GetAxis("Horizontal"); // A/D or arrows
        float verticalInput = Input.GetAxis("Vertical");     // W/S or arrows
        
        // Apply movement
        Vector3 move = new Vector3(horizontalInput, 0, verticalInput) * moveSpeed * Time.deltaTime;
        transform.position += move;
        
        // Mouse input
        if(Input.GetMouseButton(0))
        {
            Debug.Log("Left mouse button held");
        }
        
        if(Input.GetMouseButtonDown(1))
        {
            Debug.Log("Right mouse button pressed");
        }
    }
}
```

---

## Input Keys Reference

| Input | Code |
|-------|------|
| **W/A/S/D** | Use `Input.GetAxis("Horizontal"/"Vertical")` |
| **Arrow Keys** | Use `Input.GetAxis()` (same as WASD) |
| **Space** | `KeyCode.Space` |
| **Shift** | `KeyCode.LeftShift` or `KeyCode.RightShift` |
| **Ctrl** | `KeyCode.LeftControl` |
| **Enter/Return** | `KeyCode.Return` |
| **Escape** | `KeyCode.Escape` |
| **Mouse Button 0** | Left click (use `GetMouseButton(0)`) |
| **Mouse Button 1** | Right click (use `GetMouseButton(1)`) |

---

## Unity Setup Steps

1. **Create a script: "PlayerController"**
2. **Add movement code:**
   ```csharp
   public float speed = 5f;
   
   void Update()
   {
       float h = Input.GetAxis("Horizontal");
       float v = Input.GetAxis("Vertical");
       transform.position += new Vector3(h, 0, v) * speed * Time.deltaTime;
   }
   ```
3. **Attach to a cube**
4. **Press Play and test WASD movement**

---

## Guided Practice

1. **Create WASD movement** for a cube
2. **Add Space to jump** (just print "Jump" for now)
3. **Add mouse click detection** that logs "Shot!"
4. **Test all inputs**

---

## Practice Problems

**Beginner:** Write a script that logs "Forward" when W is pressed, "Backward" when S is pressed.

**Intermediate:** Create a cube that moves forward/backward with W/S at variable speed, and rotates left/right with A/D.

**Challenge:** Create a script that simulates a game cursor. Use mouse position (Input.mousePosition) to move a UI element, and detect clicks to "select" objects.

<details>
<summary>💡 Hints</summary>
- `GetAxis("Horizontal")` returns -1 (left), 0 (neutral), or 1 (right)
- Always use `Time.deltaTime` for frame-independent movement
- GetKey() runs every frame while held; GetKeyDown() runs only once
- Mouse position is in screen pixels, not world space
- Test input in Update(), not Start()
</details>

<details>
<summary>✅ Sample: Full Movement Script</summary>

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 90f;
    
    void Update()
    {
        // Movement (W/S forward/backward)
        float verticalInput = Input.GetAxis("Vertical");
        Vector3 moveDirection = transform.forward * verticalInput;
        transform.position += moveDirection * moveSpeed * Time.deltaTime;
        
        // Rotation (A/D left/right)
        float horizontalInput = Input.GetAxis("Horizontal");
        transform.Rotate(0, horizontalInput * rotateSpeed * Time.deltaTime, 0);
        
        // Jump (Space)
        if(Input.GetKeyDown(KeyCode.Space))
        {
            Debug.Log("Jump!");
        }
        
        // Interact (E)
        if(Input.GetKeyDown(KeyCode.E))
        {
            Debug.Log("Interact!");
        }
    }
}
```

</details>
