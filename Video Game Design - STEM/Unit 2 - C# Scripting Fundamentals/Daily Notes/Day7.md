# Day 7: Conditionals & Input Detection

**Learning Target:** I can use if/else statements and detect player input to control program flow.

## Key Concepts

- **if Statement:** Executes code if a condition is true
- **else Statement:** Executes code if the if condition is false
- **else if:** Checks additional conditions
- **Comparison Operators:** == (equals), != (not equals), > (greater), < (less), >= (greater or equal), <= (less or equal)
- **Logical Operators:** && (and), || (or), ! (not)
- **Input.GetKeyDown():** Returns true the frame a key is pressed
- **Input.GetKey():** Returns true while a key is held down
- **KeyCode Enum:** Represents keyboard keys (KeyCode.Space, KeyCode.W, etc.)

Conditionals let you make decisions in code. The basic structure is:

```
if (condition)
{
    // Code runs if condition is true
}
else
{
    // Code runs if condition is false
}
```

You can chain multiple conditions with else if:

```
if (health > 75)
{
    state = "healthy";
}
else if (health > 50)
{
    state = "injured";
}
else if (health > 0)
{
    state = "critical";
}
else
{
    state = "dead";
}
```

**Input Detection:** Use Input.GetKeyDown() to detect key presses and Input.GetKey() to detect key holds.
- **Input.GetKeyDown():** True only on the frame the key is pressed (useful for actions like jumping)
- **Input.GetKey():** True while the key is held down (useful for continuous movement)

## Code Examples

```csharp
using UnityEngine;

public class PlayerInput : MonoBehaviour
{
    public float jumpForce = 5f;
    public float moveSpeed = 3f;
    private bool isGrounded = true;

    void Update()
    {
        // Check if the Space key is pressed
        if (Input.GetKeyDown(KeyCode.Space))
        {
            if (isGrounded)
            {
                Debug.Log("Jump!");
                isGrounded = false;
                // We'll add actual jump physics in Unit 3
            }
            else
            {
                Debug.Log("Can't jump; not grounded.");
            }
        }

        // Check for horizontal movement (A and D keys)
        if (Input.GetKey(KeyCode.D))
        {
            // Move right
            transform.Translate(moveSpeed * Time.deltaTime, 0, 0);
            Debug.Log("Moving right");
        }

        if (Input.GetKey(KeyCode.A))
        {
            // Move left
            transform.Translate(-moveSpeed * Time.deltaTime, 0, 0);
            Debug.Log("Moving left");
        }

        // Check for a dash ability with cooldown
        if (Input.GetKeyDown(KeyCode.LeftShift))
        {
            Dash();
        }
    }

    void Dash()
    {
        Debug.Log("Dashing!");
        // Move forward quickly
        transform.Translate(10 * Time.deltaTime, 0, 0);
    }

    // Called by other scripts to set grounded state
    public void SetGrounded(bool grounded)
    {
        isGrounded = grounded;
    }
}
```

## Guided Practice

1. Create a script called "InputHandler"
2. Write an Update() method that detects WASD key presses
3. For each key, print which direction is being pressed
4. Attach the script to a GameObject and run the scene
5. Press keys and watch the Console output

## Practice Problems

**Problem 1 — Beginner:** Write an if/else statement that checks if a variable `score` is greater than 100. If true, print "High score!"; if false, print "Keep practicing!".

**Problem 2 — Intermediate:** Write a script that moves a GameObject left when you press A and right when you press D. The movement should be smooth and frame-rate independent.

**Problem 3 — Challenge:** Create a multi-key input system where W moves forward, A/D rotate left/right, and Space makes the object jump (just move up; we'll do real physics later). The object should only jump if it's on the ground.

<details>
<summary>Hints</summary>

**Problem 1:** Use the comparison operator > and Debug.Log().

**Problem 2:** Use Input.GetKey() with KeyCode.A and KeyCode.D. Use transform.Translate() with Time.deltaTime.

**Problem 3:** Track a `isGrounded` bool. Use Input.GetKey() for continuous movement and Input.GetKeyDown() for jump. Use transform.Translate() and transform.Rotate().
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
int score = 150;
if (score > 100)
{
    Debug.Log("High score!");
}
else
{
    Debug.Log("Keep practicing!");
}
```

**Problem 2:**
```csharp
using UnityEngine;

public class SimpleMovement : MonoBehaviour
{
    public float moveSpeed = 5f;

    void Update()
    {
        if (Input.GetKey(KeyCode.D))
        {
            transform.Translate(moveSpeed * Time.deltaTime, 0, 0);
        }

        if (Input.GetKey(KeyCode.A))
        {
            transform.Translate(-moveSpeed * Time.deltaTime, 0, 0);
        }
    }
}
```

**Problem 3:**
```csharp
using UnityEngine;

public class ComplexMovement : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotationSpeed = 100f;
    public float jumpHeight = 2f;
    private bool isGrounded = true;
    private float jumpTimer = 0f;

    void Update()
    {
        // Forward movement
        if (Input.GetKey(KeyCode.W))
        {
            transform.Translate(0, 0, moveSpeed * Time.deltaTime);
        }

        // Rotation
        if (Input.GetKey(KeyCode.D))
        {
            transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
        }

        if (Input.GetKey(KeyCode.A))
        {
            transform.Rotate(0, -rotationSpeed * Time.deltaTime, 0);
        }

        // Jump
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            jumpTimer = 0.5f;  // Duration of jump
            isGrounded = false;
        }

        // Jump physics (simple up/down movement)
        if (jumpTimer > 0)
        {
            transform.Translate(0, jumpHeight * Time.deltaTime, 0);
            jumpTimer -= Time.deltaTime;
        }
        else if (!isGrounded)
        {
            isGrounded = true;  // Land after jump
        }
    }
}
```
</details>
