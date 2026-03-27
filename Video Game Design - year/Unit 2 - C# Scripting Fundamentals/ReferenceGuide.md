# Unit 2 Reference Guide

---

## C# Data Types Cheat Sheet

### Primitive Types

| Type | Range | Use | Example |
|------|-------|-----|---------|
| **int** | -2.1B to 2.1B | Whole numbers | `42`, `-5`, `0` |
| **float** | ±1.5×10⁻⁴⁵ to ±3.4×10³⁸ | Decimals (use `f` suffix) | `3.14f`, `0.5f` |
| **bool** | true / false | Flags and conditions | `true`, `false` |
| **string** | Any text | Names, messages | `"Hello"`, `"Item_1"` |
| **Vector2** | X, Y floats | 2D position/direction | `new Vector2(1, 0)` |
| **Vector3** | X, Y, Z floats | 3D position/direction | `new Vector3(1, 2, 3)` |
| **Quaternion** | Rotation | Rotations in 3D | `Quaternion.Euler(0, 45, 0)` |

### Declaration Patterns

```csharp
// Basic declaration
int myInt = 42;
float myFloat = 3.14f;
string myString = "Hello";
bool myBool = true;

// Without initialization
int uninitialized; // Default: 0
float f; // Default: 0f
string s; // Default: null
bool b; // Default: false

// Arrays
int[] numbers = { 1, 2, 3 };
string[] names = { "Alice", "Bob" };

// Lists (need: using System.Collections.Generic;)
List<int> scores = new List<int>();
List<string> inventory = new List<string>();
```

---

## Operators Reference

### Arithmetic

```csharp
int a = 10, b = 3;
int sum = a + b;          // 13
int diff = a - b;         // 7
int product = a * b;      // 30
int quotient = a / b;     // 3 (integer)
int remainder = a % b;    // 1
float div = a / (float)b; // 3.33 (type cast)
```

### Comparison

```csharp
int x = 5;
bool eq = (x == 5);    // true
bool ne = (x != 5);    // false
bool lt = (x < 10);    // true
bool gt = (x > 3);     // true
bool le = (x <= 5);    // true
bool ge = (x >= 5);    // true
```

### Logical

```csharp
if(health > 0 && isAlive)     // AND: both must be true
if(hasKey || hasLockpick)     // OR: at least one true
if(!isDead)                   // NOT: inverse
```

### Assignment Shortcuts

```csharp
int x = 10;
x += 5;    // x = x + 5 → x = 15
x -= 3;    // x = x - 3 → x = 12
x *= 2;    // x = x * 2 → x = 24
x /= 4;    // x = x / 4 → x = 6
x++;       // x = x + 1 → x = 7
x--;       // x = x - 1 → x = 6
```

---

## Control Flow

### if/else if/else

```csharp
if(condition1)
{
    // Code if condition1 is true
}
else if(condition2)
{
    // Code if condition2 is true (and condition1 was false)
}
else
{
    // Code if both are false
}
```

### for Loop

```csharp
// Basic for loop
for(int i = 0; i < 10; i++)
{
    Debug.Log(i); // 0 to 9
}

// Loop with step
for(int i = 0; i < 10; i += 2)
{
    Debug.Log(i); // 0, 2, 4, 6, 8
}

// Count down
for(int i = 10; i > 0; i--)
{
    Debug.Log(i); // 10 to 1
}
```

### foreach Loop

```csharp
string[] fruits = { "Apple", "Banana", "Cherry" };
foreach(string fruit in fruits)
{
    Debug.Log(fruit);
}

List<int> numbers = new List<int> { 1, 2, 3 };
foreach(int num in numbers)
{
    Debug.Log(num);
}
```

### while Loop

```csharp
int count = 0;
while(count < 5)
{
    Debug.Log(count);
    count++;
}

// break: exit loop
// continue: skip to next iteration
```

---

## Unity MonoBehaviour Methods

### Lifecycle Methods

| Method | When Called | Use |
|--------|-------------|-----|
| **Awake()** | Before any Start(), on instantiation | Initialize between scripts |
| **Start()** | First frame, before Update() | Initial setup |
| **Update()** | Every frame | Input, gameplay logic |
| **FixedUpdate()** | Every physics frame (~0.02s) | Physics calculations |
| **LateUpdate()** | After all Updates | Camera following |
| **OnDestroy()** | When GameObject destroyed | Cleanup |

### Method Signatures

```csharp
void Awake()
{
    // Called when script is loaded
}

void Start()
{
    // Called on first frame
}

void Update()
{
    // Called every frame (60+ times/sec)
    // Use for input, movement, game logic
}

void FixedUpdate()
{
    // Called on physics timestep (usually 50/sec)
    // Use for physics-based movement
}

void OnTriggerEnter(Collider other)
{
    // Called when trigger is entered
    Debug.Log("Hit: " + other.gameObject.name);
}
```

---

## Input Reference

### Keyboard Input

```csharp
// Key held down
if(Input.GetKey(KeyCode.W))
{
    Debug.Log("W is held");
}

// Key pressed (once per press)
if(Input.GetKeyDown(KeyCode.Space))
{
    Debug.Log("Space pressed");
}

// Key released
if(Input.GetKeyUp(KeyCode.W))
{
    Debug.Log("W released");
}
```

### Common Key Codes

```csharp
KeyCode.W / KeyCode.A / KeyCode.S / KeyCode.D
KeyCode.Space
KeyCode.Return
KeyCode.Escape
KeyCode.LeftShift
KeyCode.LeftControl
```

### Axis Input (Smooth)

```csharp
float horizontal = Input.GetAxis("Horizontal");  // -1 to 1 (A/D, arrows)
float vertical = Input.GetAxis("Vertical");      // -1 to 1 (W/S, arrows)

// Applied movement
Vector3 move = new Vector3(horizontal, 0, vertical) * speed * Time.deltaTime;
transform.position += move;
```

### Mouse Input

```csharp
if(Input.GetMouseButton(0))  // Left click held
{
    Debug.Log("Shooting");
}

if(Input.GetMouseButtonDown(1))  // Right click pressed
{
    Debug.Log("Aiming");
}

Vector3 mousePos = Input.mousePosition;  // Screen pixels
```

---

## String Operations

### Concatenation

```csharp
string firstName = "John";
string lastName = "Doe";
string fullName = firstName + " " + lastName;  // "John Doe"

// String interpolation (modern, cleaner)
string message = $"{firstName} {lastName}"; // "John Doe"
string formatted = $"Level: {level}, HP: {health}/{maxHealth}";
```

### Common Methods

```csharp
string text = "Hello World";

text.Length             // 11 (character count)
text.ToLower()          // "hello world"
text.ToUpper()          // "HELLO WORLD"
text.Contains("World")  // true
text.Replace("o", "0")  // "Hell0 W0rld"
text.Substring(0, 5)    // "Hello"
text.Split(' ')         // Array: ["Hello", "World"]
```

---

## Transform Reference

### Position

```csharp
// Read position
Vector3 pos = transform.position;
float x = transform.position.x;

// Set position
transform.position = new Vector3(5, 0, 0);
transform.position += Vector3.forward * speed * Time.deltaTime;

// Move towards target
transform.position = Vector3.Lerp(transform.position, target, speed * Time.deltaTime);
```

### Rotation

```csharp
// Euler angles (degrees)
transform.rotation = Quaternion.Euler(0, 45, 0);  // 45° on Y
transform.Rotate(0, 45 * Time.deltaTime, 0);      // Rotate 45°/sec

// Local rotation (relative to parent)
transform.localRotation = Quaternion.Euler(0, 45, 0);
```

### Scale

```csharp
transform.localScale = new Vector3(2, 2, 2);  // 2× size
transform.localScale = new Vector3(1, 0.5f, 1);  // Half-height
```

### Direction

```csharp
Vector3 forward = transform.forward;    // (0, 0, 1) rotated by transform
Vector3 right = transform.right;        // (1, 0, 0) rotated by transform
Vector3 up = transform.up;              // (0, 1, 0) rotated by transform
```

---

## GetComponent Patterns

### Basic Usage

```csharp
// Get Rigidbody on this GameObject
Rigidbody rb = GetComponent<Rigidbody>();
if(rb != null)
{
    rb.velocity = new Vector3(10, 0, 0);
}

// Get component with null check
Collider col = GetComponent<Collider>();
if(col != null)
{
    col.enabled = false;
}
```

### Common Components

```csharp
Rigidbody rb = GetComponent<Rigidbody>();
Collider col = GetComponent<Collider>();
Transform tr = GetComponent<Transform>();
SpriteRenderer sr = GetComponent<SpriteRenderer>();
Animator anim = GetComponent<Animator>();
```

### GetComponentInChildren / GetComponentInParent

```csharp
// Search children
Transform child = GetComponentInChildren<Transform>();

// Search parent hierarchy
Rigidbody parentRb = GetComponentInParent<Rigidbody>();
```

---

## Time Reference

### Time Variables

```csharp
float deltaTime = Time.deltaTime;        // Seconds since last frame (~0.016 at 60fps)
float elapsed = Time.time;               // Seconds since game start
int frames = Time.frameCount;            // Total frames since start
float timeScale = Time.timeScale;        // Game speed (1.0 = normal, 0 = paused)
```

### Using deltaTime

```csharp
// Frame-independent movement
void Update()
{
    float distance = speed * Time.deltaTime;
    transform.position += Vector3.forward * distance;
}

// Without deltaTime (frame-dependent; inconsistent)
void Update()
{
    transform.position += Vector3.forward * 5;  // BAD: varies with framerate
}
```

### Timing & Delays

```csharp
// Invoke a method after delay
Invoke("FireWeapon", 2.0f);  // Call FireWeapon() in 2 seconds

// Repeat method
InvokeRepeating("Patrol", 1.0f, 3.0f);  // After 1s, repeat every 3s

// Cancel invoke
CancelInvoke("FireWeapon");
```

---

## Common Methods

### Debug

```csharp
Debug.Log("Message");           // White log
Debug.LogWarning("Warning");    // Yellow
Debug.LogError("Error");        // Red
```

### Math

```csharp
int abs = Mathf.Abs(-5);                    // 5
float min = Mathf.Min(3f, 5f);              // 3f
float max = Mathf.Max(3f, 5f);              // 5f
float clamp = Mathf.Clamp(value, 0, 10);   // Limit 0-10
float lerp = Mathf.Lerp(start, end, t);    // Linear interpolation (t: 0-1)
```

### Vector

```csharp
float dist = Vector3.Distance(a, b);       // Distance between points
Vector3 normalized = direction.normalized; // Unit vector (length 1)
float magnitude = vector.magnitude;        // Length of vector
```

---

## Arrays vs Lists

| Feature | Array | List |
|---------|-------|------|
| **Fixed size?** | Yes | No (dynamic) |
| **Syntax** | `int[]` | `List<int>` |
| **Create** | `new int[5]` | `new List<int>()` |
| **Access** | `array[i]` | `list[i]` |
| **Add** | Can't grow | `list.Add()` |
| **Remove** | Can't shrink | `list.Remove()` |
| **Length** | `array.Length` | `list.Count` |

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| `5.5` instead of `5.5f` | Always use `f` for float literals |
| `GetComponent()` returns null, crashes | Check null: `if(comp != null)` |
| Forgetting `Time.deltaTime` | Movement varies with FPS; always use it |
| `array[array.Length]` out of bounds | Arrays are 0-indexed; max is `Length-1` |
| `==` for string comparison | Use `.Equals()` or interpolate carefully |
| Infinite loop in Update() | Avoid while(true) in Update; use breaks |
| Not importing List namespace | Add: `using System.Collections.Generic;` |

