# Unit 2: C# Scripting Fundamentals

## Unit Overview

**Duration:** Days 5-8 (4 days)
**Key Concepts:** Variables, data types, methods, conditionals, input handling, transform manipulation with vectors
**Big Idea:** C# is the programming language that powers game logic. Understanding variables, data types, methods, and control flow lets you build responsive, interactive games.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Declare variables using common data types (int, float, string, bool)
- [ ] Understand the difference between public and private variables
- [ ] Edit public variables in the Inspector and understand serialization
- [ ] Write and call methods with parameters and return types
- [ ] Use if/else conditionals to control program flow
- [ ] Detect player input with Input.GetKeyDown() and Input.GetKey()
- [ ] Use Vector3 to represent position and direction
- [ ] Move and rotate GameObjects smoothly using Time.deltaTime
- [ ] Distinguish between position, velocity, and acceleration in game physics

---

## Day-by-Day Content

### Day 5: Variables & Data Types

#### Key Concepts
- **Variable:** A named container that stores a value
- **Data Type:** The kind of value a variable holds (int, float, string, bool, Vector3)
- **int:** Integer (whole number) e.g., 5, -10, 0
- **float:** Floating-point number (decimal) e.g., 3.5f, -2.1f, 0.0f
- **string:** Text data e.g., "Hello", "Player Name"
- **bool:** Boolean (true or false)
- **Vector3:** A 3D position or direction (x, y, z)
- **Public vs. Private:** Public variables are visible in the Inspector; private are hidden
- **Serialization:** Unity saves public variables so they persist between play sessions

#### Content
Variables are the foundation of all programming. Every variable has a **name**, a **type**, and a **value**.

**Basic Declaration:**
```
[access modifier] [type] [name] = [initial value];
```

**Access Modifiers:**
- **public:** Visible in Inspector; can be accessed from other scripts
- **private:** Hidden in Inspector; only accessible within this script (default if not specified)

**Common Data Types:**
- **int:** -2147483648 to 2147483647
- **float:** Decimals; always use the 'f' suffix (5.5f, not 5.5)
- **string:** Text in double quotes ("Hello World")
- **bool:** true or false
- **Vector3:** A structure with x, y, z components (more on this in Day 8)

The Inspector is where you interact with public variables. You can change values in the Inspector and see them reflected in the game. This is powerful for tuning game feel without recompiling code.

#### Annotated Code Example

```csharp
using UnityEngine;

public class PlayerStats : MonoBehaviour
{
    // Public variables: visible and editable in the Inspector
    public int maxHealth = 100;
    public float movementSpeed = 5.5f;
    public string playerName = "Hero";
    public bool isAlive = true;

    // Private variables: hidden in Inspector, only for internal use
    private int currentHealth;
    private float experience = 0f;
    private bool hasWeapon = false;

    void Start()
    {
        // Initialize currentHealth to maxHealth
        currentHealth = maxHealth;

        // Print all player stats to the Console
        Debug.Log("Player: " + playerName);
        Debug.Log("Health: " + currentHealth + "/" + maxHealth);
        Debug.Log("Speed: " + movementSpeed);
    }

    void Update()
    {
        // We'll add interactive logic here in later units
    }
}
```

---

### Day 6: Methods & Functions

#### Key Concepts
- **Method:** A block of code that performs a specific task
- **Method Signature:** Defines the return type, name, and parameters
- **void:** A method that doesn't return a value
- **Return Type:** The type of value the method returns (int, float, string, bool)
- **Parameter:** A value passed to a method
- **Calling a Method:** Executing the method by writing its name with parentheses
- **Local Variables:** Variables declared inside a method; only exist while the method runs

#### Content
Methods organize code into reusable blocks. Every method has:
1. **Access Modifier:** public, private, etc.
2. **Return Type:** void (no return) or a specific type (int, float, bool, etc.)
3. **Method Name:** Descriptive name using PascalCase (e.g., CalculateDamage)
4. **Parameters:** Optional inputs, enclosed in parentheses
5. **Body:** The code that runs when the method is called

**Example:**
```
public void Jump(float force)
{
    // This method accepts one parameter: force
    // And doesn't return a value (void)
}

public int Add(int a, int b)
{
    // This method accepts two parameters
    // And returns an int (the sum)
    return a + b;
}
```

Methods should have a single responsibility. If a method does too much, break it into smaller methods. This makes code easier to test and reuse.

#### Annotated Code Example

```csharp
using UnityEngine;

public class Combat : MonoBehaviour
{
    public int baseAttackDamage = 10;
    private int currentHealth = 50;

    void Start()
    {
        // Call the TakeDamage method to test it
        TakeDamage(25);
    }

    // A method that takes a parameter and modifies health
    public void TakeDamage(int damageAmount)
    {
        currentHealth -= damageAmount;
        Debug.Log("Took " + damageAmount + " damage. Health: " + currentHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    // A method that calculates and returns a damage value
    public int CalculateDamage(int enemyDefense)
    {
        int damage = baseAttackDamage - enemyDefense;
        // Ensure damage is at least 1
        if (damage < 1)
            damage = 1;
        return damage;
    }

    // A method with no parameters and no return value
    private void Die()
    {
        Debug.Log("Player died!");
        Destroy(gameObject); // Remove this GameObject from the scene
    }

    void Update()
    {
        // Call CalculateDamage with an enemy defense value
        int finalDamage = CalculateDamage(5);
        Debug.Log("Final damage: " + finalDamage);
    }
}
```

---

### Day 7: Conditionals & Input Detection

#### Key Concepts
- **if Statement:** Executes code if a condition is true
- **else Statement:** Executes code if the if condition is false
- **else if:** Checks additional conditions
- **Comparison Operators:** == (equals), != (not equals), > (greater), < (less), >= (greater or equal), <= (less or equal)
- **Logical Operators:** && (and), || (or), ! (not)
- **Input.GetKeyDown():** Returns true the frame a key is pressed
- **Input.GetKey():** Returns true while a key is held down
- **KeyCode Enum:** Represents keyboard keys (KeyCode.Space, KeyCode.W, etc.)

#### Content
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

#### Annotated Code Example

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

---

### Day 8: Transform Manipulation with Vectors & Time.deltaTime

#### Key Concepts
- **Vector3:** A structure representing 3D position or direction (x, y, z)
- **Position:** Where something is in 3D space
- **Direction:** Which way something is facing (normalized vectors have length 1)
- **transform.Translate():** Moves an object relative to its orientation
- **transform.position:** The absolute position of an object
- **transform.Rotate():** Rotates an object
- **Time.deltaTime:** Time elapsed since the last frame (essential for frame-rate-independent movement)
- **Magnitude:** The length of a vector; useful for distance calculations

#### Content
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

#### Annotated Code Example

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

---

## Practice Problems

### Beginner Tier

**Problem 1:** Declare five variables in a script: an int, a float, a string, a bool, and a Vector3. Assign each one a value. Print them all to the Console.

<details>
<summary>Hint</summary>
Use the syntax:
```
[type] [name] = [value];
```
Then use Debug.Log() to print each one.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class VariableDemo : MonoBehaviour
{
    void Start()
    {
        int health = 100;
        float speed = 5.5f;
        string playerName = "Hero";
        bool isAlive = true;
        Vector3 position = new Vector3(0, 1, 5);

        Debug.Log("Health: " + health);
        Debug.Log("Speed: " + speed);
        Debug.Log("Name: " + playerName);
        Debug.Log("Alive: " + isAlive);
        Debug.Log("Position: " + position);
    }
}
```
</details>

---

**Problem 2:** Write a method called AddNumbers that takes two integers as parameters and returns their sum.

<details>
<summary>Hint</summary>
The method signature should be:
```
public int AddNumbers(int a, int b)
```
</details>

<details>
<summary>Answer</summary>
```csharp
public int AddNumbers(int a, int b)
{
    return a + b;
}
```
</details>

---

**Problem 3:** Write an if/else statement that checks if a variable `score` is greater than 100. If true, print "High score!"; if false, print "Keep practicing!".

<details>
<summary>Hint</summary>
Use the comparison operator > and Debug.Log().
</details>

<details>
<summary>Answer</summary>
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
</details>

---

### Intermediate Tier

**Problem 4:** Write a script that moves a GameObject left when you press A and right when you press D. The movement should be smooth and frame-rate independent.

<details>
<summary>Hint</summary>
Use Input.GetKey() with KeyCode.A and KeyCode.D. Use transform.Translate() with Time.deltaTime.
</details>

<details>
<summary>Answer</summary>
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
</details>

---

**Problem 5:** Write a script that calculates the distance between the player and an enemy. The distance should update every frame and print to the Console.

<details>
<summary>Hint</summary>
Use Vector3 subtraction to find the direction, then use .magnitude to get the distance.
</details>

<details>
<summary>Answer</summary>
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
</details>

---

**Problem 6:** Write a script that rotates a GameObject when you press the Right arrow key, and rotates the opposite direction when you press the Left arrow key.

<details>
<summary>Hint</summary>
Use Input.GetKey() and transform.Rotate(). Remember to use Time.deltaTime for smooth rotation.
</details>

<details>
<summary>Answer</summary>
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
</details>

---

### Challenge Tier

**Problem 7:** Write a method called `GetHealthPercentage()` that returns the current health as a percentage of max health. Use it in Update() to print the percentage every second.

<details>
<summary>Hint</summary>
Health percentage = (currentHealth / maxHealth) * 100. Create a timer in Update() to print every second.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class HealthPercentage : MonoBehaviour
{
    public int maxHealth = 100;
    private int currentHealth = 75;
    private float timeSinceLastLog = 0f;

    void Update()
    {
        timeSinceLastLog += Time.deltaTime;
        if (timeSinceLastLog >= 1f)
        {
            float percentage = GetHealthPercentage();
            Debug.Log("Health: " + percentage + "%");
            timeSinceLastLog = 0f;
        }
    }

    public float GetHealthPercentage()
    {
        return (currentHealth / (float)maxHealth) * 100f;
    }
}
```
</details>

---

**Problem 8:** Create a multi-key input system where W moves forward, A/D rotate left/right, and Space makes the object jump (just move up; we'll do real physics later). The object should only jump if it's on the ground.

<details>
<summary>Hint</summary>
Track a `isGrounded` bool. Use Input.GetKey() for continuous movement and Input.GetKeyDown() for jump. Use transform.Translate() and transform.Rotate().
</details>

<details>
<summary>Answer</summary>
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

---

## Practice Bank (15 Problems)

1. **Variable Declaration:** Create a script with 10 public variables of different types. In the Inspector, change their values and print them to the Console.

2. **Math Operations:** Write a script that calculates the area and perimeter of a rectangle given width and height values.

3. **Conditionals:** Write a script that assigns a letter grade (A, B, C, D, F) based on a numeric score using if/else if/else.

4. **String Concatenation:** Write a script that takes a first name and last name, combines them, and prints "Hello, [Full Name]!" to the Console.

5. **Boolean Logic:** Write a script that checks if a player has both a weapon AND is at full health. If true, print "Ready for battle!"; otherwise, print "Need preparation."

6. **Method Practice:** Write a method that takes a damage value and an armor value, and returns the final damage (damage minus armor, minimum 1).

7. **Vector Math:** Write a script that calculates the midpoint between two GameObjects.

8. **Input Combination:** Write a script that requires the player to press both A and D simultaneously to trigger an action.

9. **Loop + Conditional:** Write a script that prints numbers 1 to 10, but only prints numbers greater than 5.

10. **Normalize Vectors:** Write a script that finds the direction to a target and normalizes it. Explain why normalization is useful.

11. **Velocity Calculation:** Write a script that calculates velocity as (distance / time). Assume distance and time are known values.

12. **Ternary Operator:** Rewrite an if/else statement using the ternary operator (?:). Example: `string result = (score > 50) ? "Pass" : "Fail";`

13. **GetComponent Practice:** Write a script that gets the Renderer component of the GameObject and changes its color to red.

14. **Method Overloading:** Write two versions of an Add() method—one that adds two ints, and another that adds two floats.

15. **Debug Profiling:** Write a script that prints how much time (in milliseconds) a method takes to execute using `Time.realtimeSinceStartup`.

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Using = instead of == in conditionals | Confusion between assignment and comparison | Remember: = assigns, == compares. Use == in if statements. |
| Forgetting 'f' suffix on floats | C# defaults to double; 5.5 is a double, not a float | Always write 5.5f, not 5.5 |
| Movement is too fast/slow | Not using Time.deltaTime | Always multiply movement by Time.deltaTime for consistency |
| Input doesn't work | Method name is wrong or uppercase mismatch | Use exact names: GetKeyDown, GetKey, GetAxis (case-sensitive) |
| Variables not editable in Inspector | Made them private | Make them public, or use [SerializeField] attribute |
| Method return type is void but trying to return a value | Misunderstanding return types | If returning a value, use a type (int, float, bool), not void |
| Vector3 calculations give wrong results | Forgetting to normalize or convert to float | Be explicit: (float)intValue, .normalized for unit vectors |
| Key press triggers multiple times per frame | Using GetKeyDown in a loop | GetKeyDown only triggers once per press; this is correct behavior |
| Distance calculation is always 0 | Comparing the same object to itself | Make sure you're comparing different GameObjects |

---

## Assessment Prep: 10 Q&As

**Q1: What are the five common data types in C#?**
A: int (whole numbers), float (decimals), string (text), bool (true/false), and Vector3 (3D position/direction).

**Q2: What is the difference between public and private variables?**
A: Public variables are visible and editable in the Inspector. Private variables are hidden and only accessible within the script. Use public for values you want to tune in the editor.

**Q3: Explain the purpose of Time.deltaTime.**
A: Time.deltaTime is the time elapsed since the last frame. It makes movement frame-rate independent: moving at 5 * Time.deltaTime units per frame moves at 5 units per second regardless of frame rate.

**Q4: What is the difference between Input.GetKeyDown() and Input.GetKey()?**
A: GetKeyDown() returns true only the frame a key is pressed (one-time action). GetKey() returns true while the key is held down (continuous action).

**Q5: Write a simple if/else statement that checks if a variable x is positive.**
A:
```csharp
if (x > 0)
    Debug.Log("Positive");
else
    Debug.Log("Not positive");
```

**Q6: What is a method, and why are they useful?**
A: A method is a reusable block of code that performs a specific task. Methods organize code, reduce repetition, and make programs easier to understand and maintain.

**Q7: How do you calculate the distance between two GameObjects?**
A:
```csharp
Vector3 direction = objectB.transform.position - objectA.transform.position;
float distance = direction.magnitude;
```

**Q8: What does Vector3.normalized do?**
A: It returns a unit vector (length = 1) pointing in the same direction. Useful for finding direction without distance: `Vector3 direction = (targetPos - myPos).normalized;`

**Q9: Explain the difference between transform.Translate() and setting transform.position directly.**
A: Translate() moves relative to the object's current orientation. Setting position directly moves to an absolute world position. Translate is more intuitive for "forward" movement.

**Q10: What is the purpose of GetComponent() and when would you use it?**
A: GetComponent() accesses other components on the same GameObject (e.g., GetComponent<Renderer>()). Use it when you need to modify another component from your script.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **Variable** | A named container storing a value |
| **Data Type** | Specifies what kind of value a variable holds |
| **int** | Integer (whole number) e.g., -5, 0, 100 |
| **float** | Floating-point (decimal) e.g., 3.5f, -2.1f |
| **string** | Text data e.g., "Hello" |
| **bool** | Boolean (true or false) |
| **Vector3** | 3D coordinate (x, y, z) or direction |
| **Method** | A reusable block of code |
| **Parameter** | Input to a method |
| **Return Type** | Type of value a method returns |
| **Conditional** | if/else statement controlling flow |
| **Operator** | Symbol performing an operation (=, ==, +, -, &&, \|\|) |
| **GetComponent** | Accesses components on the same GameObject |

### C# Data Types Quick Reference

```csharp
// Integers (whole numbers)
int score = 100;
int negativeNum = -50;

// Floats (decimals - always use 'f' suffix)
float speed = 5.5f;
float height = 1.85f;

// Strings (text)
string name = "Hero";
string message = "Hello, World!";

// Booleans (true or false)
bool isAlive = true;
bool isGrounded = false;

// Vector3 (3D position or direction)
Vector3 position = new Vector3(0, 1, 5);
Vector3 direction = Vector3.forward;  // (0, 0, 1)
Vector3 zero = Vector3.zero;          // (0, 0, 0)
```

### Control Flow Quick Reference

```csharp
// if/else/else if
if (condition)
{
    // runs if condition is true
}
else if (otherCondition)
{
    // runs if otherCondition is true
}
else
{
    // runs if all above are false
}

// Comparison operators
if (a == b)    // equals
if (a != b)    // not equals
if (a > b)     // greater than
if (a < b)     // less than
if (a >= b)    // greater or equal
if (a <= b)    // less or equal

// Logical operators
if (a && b)    // AND (both must be true)
if (a || b)    // OR (at least one must be true)
if (!a)        // NOT (inverts boolean)
```

### Input & Transform Quick Reference

```csharp
// Input detection
if (Input.GetKeyDown(KeyCode.Space))     // Pressed this frame
if (Input.GetKey(KeyCode.Space))         // Held down
if (Input.GetKeyUp(KeyCode.Space))       // Released this frame

// Common KeyCodes
KeyCode.Space, KeyCode.A, KeyCode.D, KeyCode.W, KeyCode.S
KeyCode.LeftArrow, KeyCode.RightArrow, KeyCode.UpArrow, KeyCode.DownArrow
KeyCode.Mouse0 (left click), KeyCode.Mouse1 (right click)

// Transform manipulation (always use Time.deltaTime for smooth movement)
transform.position = new Vector3(5, 2, 0);
transform.Translate(1, 0, 0);                          // Move relative
transform.Rotate(0, 90, 0);                           // Rotate by degrees
transform.localScale = new Vector3(2, 2, 2);         // Set size

// Vector operations
Vector3 direction = targetPos - myPos;
float distance = direction.magnitude;
Vector3 normalizedDirection = direction.normalized;   // Length = 1
```

### Method Syntax Quick Reference

```csharp
// Method with no parameters, no return
void PrintMessage()
{
    Debug.Log("Hello!");
}

// Method with parameters, no return
void SetHealth(int newHealth)
{
    health = newHealth;
}

// Method with parameters, returns a value
public int Add(int a, int b)
{
    return a + b;
}

// Method with default parameters
public void Jump(float force = 10f)
{
    // force defaults to 10f if not provided
}
```

---

## Additional Resources

- **Unity Scripting API:** https://docs.unity3d.com/ScriptReference/
- **C# Documentation:** https://learn.microsoft.com/en-us/dotnet/csharp/
- **Input Manager Settings:** Edit > Project Settings > Input Manager

