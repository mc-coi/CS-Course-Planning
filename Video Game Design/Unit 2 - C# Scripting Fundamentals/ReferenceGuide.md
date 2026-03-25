# Vocabulary & Quick Reference

## Key Terms

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

## C# Data Types Quick Reference

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

## Control Flow Quick Reference

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

## Input & Transform Quick Reference

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

## Method Syntax Quick Reference

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

## Common Mistakes & How to Fix Them

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
