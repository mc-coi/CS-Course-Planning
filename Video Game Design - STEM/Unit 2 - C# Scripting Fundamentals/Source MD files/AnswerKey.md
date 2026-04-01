# Unit 2 Answer Key: C# Scripting Fundamentals

Comprehensive answer key for all 15 practice problems covering variables, operators, control flow, and basic game mechanics.

---

## Problem 1: Variable Declaration and Types

### Solution

```csharp
using UnityEngine;

public class CharacterStats : MonoBehaviour
{
    public string characterName = "Hero";
    public int level = 1;
    public float experience = 0f;
    public int health = 100;
    public bool isAlive = true;
    public Vector3 spawnPoint = new Vector3(0, 1, 0);

    void Start()
    {
        Debug.Log("Character: " + characterName);
        Debug.Log("Level: " + level);
        Debug.Log("Health: " + health);
        Debug.Log("Is Alive: " + isAlive);
        Debug.Log("Spawn Point: " + spawnPoint);
    }
}
```

### What Success Looks Like
Console displays all five values on game start. All data types correctly chosen (string for name, int for discrete values, bool for true/false, Vector3 for position).

### Common Mistakes
- Using wrong type for level (should be int, not float)
- Forgetting initialization values
- Using `Int` instead of `int` (C# is case-sensitive for built-in types)

---

## Problem 2: Arithmetic and XP System

### Solution

```csharp
void Start()
{
    int currentXP = 1500;
    int xpPerLevel = 1000;

    int level = currentXP / xpPerLevel;        // 1500 / 1000 = 1
    int xpInLevel = currentXP % xpPerLevel;    // 1500 % 1000 = 500
    int xpNeeded = xpPerLevel - xpInLevel;     // 1000 - 500 = 500

    Debug.Log("Level " + level + ": " + xpInLevel + "/" + xpPerLevel + " XP");
    Debug.Log("Progress: " + xpNeeded + " XP to next level");
}
```

**Console Output:**
```
Level 1: 500/1000 XP
Progress: 500 XP to next level
```

### What Success Looks Like
Correct calculations using division (/) and modulo (%) operators. Player understands progression system math.

### Common Mistakes
- Using `%` operator incorrectly (gives remainder, not division)
- Order of operations (modulo has same precedence as division)
- Integer division truncates decimals (1500 / 1000 = 1, not 1.5)

---

## Problem 3: Health System with Conditionals

### Solution

```csharp
void Start()
{
    int maxHealth = 100;
    int damage = 35;
    int currentHealth = maxHealth - damage;  // 65

    if(currentHealth > 50)
        Debug.Log("Healthy");
    else if(currentHealth > 20)
        Debug.Log("Hurt");
    else
        Debug.Log("Critical");
}
```

**Console Output:**
```
Hurt
```

### What Success Looks Like
Correctly uses if-else-if chain. Evaluates conditions in order. Output matches expected health state.

### Common Mistakes
- Using `&&` when they mean nested if statements
- Checking conditions in wrong order (would always use first true)
- Using assignment (=) instead of comparison (==)

---

## Problem 4: Inventory with Arrays

### Solution

```csharp
using System.Collections.Generic;
using UnityEngine;

void Start()
{
    string[] inventory = { "Sword", "Shield", "Potion" };

    for(int i = 0; i < inventory.Length; i++)
    {
        Debug.Log("Item " + i + ": " + inventory[i]);
    }

    Debug.Log("Total items: " + inventory.Length);
}
```

**Console Output:**
```
Item 0: Sword
Item 1: Shield
Item 2: Potion
Total items: 3
```

### What Success Looks Like
Array loop works correctly. .Length property used correctly. Items logged with zero-based indexing.

### Common Mistakes
- Starting loop at 1 instead of 0 (off-by-one error)
- Using `inventory.Count` instead of `inventory.Length` (Count is for Lists, Length for arrays)
- Trying to modify array size after creation (arrays have fixed size)

---

## Problem 5: Player Movement with Input

### Solution

```csharp
public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 90f;

    void Update()
    {
        // Movement
        if(Input.GetKey(KeyCode.W))
            transform.position += transform.forward * moveSpeed * Time.deltaTime;
        if(Input.GetKey(KeyCode.S))
            transform.position -= transform.forward * moveSpeed * Time.deltaTime;

        // Rotation
        if(Input.GetKey(KeyCode.A))
            transform.Rotate(0, -rotateSpeed * Time.deltaTime, 0);
        if(Input.GetKey(KeyCode.D))
            transform.Rotate(0, rotateSpeed * Time.deltaTime, 0);

        // Jump
        if(Input.GetKeyDown(KeyCode.Space))
            Debug.Log("Jump!");
    }
}
```

### What Success Looks Like
- W/S moves forward/backward smoothly
- A/D rotates left/right
- Space prints "Jump!" once per press
- Movement uses Time.deltaTime for frame-rate independence

### Common Mistakes
- Using `GetKeyDown` for movement (fires only once per press)
- Forgetting Time.deltaTime (movement depends on frame rate)
- Using `transform.position = ...` instead of `+=` (resets instead of increments)
- Rotation in wrong order (Y axis controls left/right, not X)

---

## Problem 6: Spawn Objects in a Loop

### Solution

```csharp
public GameObject cubePrefab;

void Start()
{
    for(int i = 0; i < 10; i++)
    {
        Vector3 position = new Vector3(i, 0, 0);
        Instantiate(cubePrefab, position, Quaternion.identity);
    }
}
```

### What Success Looks Like
10 cubes appear in a line from (0,0,0) to (9,0,0). Each cube is identical in size and appearance.

### Common Mistakes
- Forgetting to assign cubePrefab in Inspector
- Using i directly without multiplying by spacing (all cubes overlap at origin)
- Loop going from 1 to 10 instead of 0 to 9 (wrong spacing)

---

## Problem 7: Foreach Over List

### Solution

```csharp
using System.Collections.Generic;

void Start()
{
    List<string> enemies = new List<string>();
    enemies.Add("Goblin");
    enemies.Add("Orc");
    enemies.Add("Troll");
    enemies.Add("Skeleton");
    enemies.Add("Zombie");

    foreach(string enemy in enemies)
        Debug.Log("Enemy: " + enemy);
}
```

**Console Output:**
```
Enemy: Goblin
Enemy: Orc
Enemy: Troll
Enemy: Skeleton
Enemy: Zombie
```

### What Success Looks Like
All 5 enemies logged. List grows dynamically. Foreach loop is clean and readable.

### Common Mistakes
- Forgetting `using System.Collections.Generic;`
- Using for loop instead of foreach (less elegant but functional)
- Attempting to remove items while iterating (causes exceptions)

---

## Problem 8: GetComponent and Rigidbody

### Solution

```csharp
private Rigidbody rb;

void Start()
{
    rb = GetComponent<Rigidbody>();
    if(rb != null)
        rb.velocity = transform.forward * 10f;
}

void Update()
{
    if(rb != null)
        Debug.Log("Velocity: " + rb.velocity.magnitude);
}
```

### What Success Looks Like
Object moves forward consistently. Console shows velocity magnitude (approximately 10).

### Common Mistakes
- Not checking if rb is null (null reference exception)
- Using `rb.AddForce` instead of assigning velocity (different behavior)
- Logging every frame causes console spam
- Forgetting to add Rigidbody component to GameObject

---

## Problem 9: Method with Parameters

### Solution

```csharp
private int currentHealth = 100;

void TakeDamage(int damageAmount)
{
    currentHealth -= damageAmount;
    Debug.Log("Health: " + currentHealth + "/100");
}

void Start()
{
    TakeDamage(25);  // Health: 75/100
    TakeDamage(30);  // Health: 45/100
}
```

**Console Output:**
```
Health: 75/100
Health: 45/100
```

### What Success Looks Like
Method correctly reduces health. Multiple calls stack properly. Output shows correct values.

### Common Mistakes
- Forgetting to declare parameter type (just `TakeDamage(damage)` fails)
- Not returning void if method doesn't return anything
- Using global health variable instead of instance variable

---

## Problem 10: Circular Motion

### Solution

```csharp
public float radius = 3f;
public float period = 10f;

void Update()
{
    float angle = (Time.time / period) * 2 * Mathf.PI;
    float x = Mathf.Cos(angle) * radius;
    float z = Mathf.Sin(angle) * radius;
    transform.position = new Vector3(x, 0, z);
}
```

### What Success Looks Like
Object orbits smoothly in a circle. Radius is 3 units. One orbit takes exactly 10 seconds.

### Common Mistakes
- Using degrees instead of radians (forgetting Mathf.PI)
- Using `y` and `z` instead of `x` and `z` (wrong orbit plane)
- Not multiplying by `2 * Mathf.PI` (angle range is 0-360°, not 0-1)

---

## Problem 11: String Interpolation

### Solution

```csharp
void Start()
{
    string name = "Hero";
    int level = 5;
    int health = 80, maxHealth = 100;
    int xp = 1500, maxXp = 2000;

    string profile = $"{name} (Level {level}): {health}/{maxHealth} HP, {xp}/{maxXp} XP";
    Debug.Log(profile);
}
```

**Console Output:**
```
Hero (Level 5): 80/100 HP, 1500/2000 XP
```

### What Success Looks Like
Single line output with proper formatting. String interpolation (`$"..."`) used correctly.

### Common Mistakes
- Using concatenation instead of interpolation (messy: `"" + name + " (Level " + level + ")..."`)
- Forgetting the `$` prefix (string is not interpreted)
- Missing braces around variables (causes syntax error)

---

## Problem 12: Conditions and Damage Calculation

### Solution

```csharp
void CalculateDamage(int baseDamage, int armor)
{
    int finalDamage;

    if(armor >= 80)
        finalDamage = 1;  // Minimum damage
    else
        finalDamage = baseDamage - armor;

    if(finalDamage < 0)
        finalDamage = 0;

    Debug.Log("Damage: " + finalDamage);
}

void Start()
{
    CalculateDamage(50, 30);   // Output: Damage: 20
    CalculateDamage(50, 80);   // Output: Damage: 1
    CalculateDamage(50, 100);  // Output: Damage: 1
}
```

### What Success Looks Like
Correct damage values output. Armor scaling works. Minimum damage enforced.

### Common Mistakes
- Forgetting minimum damage check (negative damage)
- Using `>` instead of `>=` for armor threshold
- Not clamping negative results

---

## Problem 13: Time-Based Countdown

### Solution

```csharp
private float startTime;

void Start()
{
    startTime = Time.time;
}

void Update()
{
    float elapsed = Time.time - startTime;
    int remaining = 10 - (int)elapsed;

    if(remaining >= 0)
        Debug.Log("Time remaining: " + remaining);
    else
        Debug.Log("Done!");
}
```

**Console Output (each frame):**
```
Time remaining: 10
Time remaining: 9
Time remaining: 8
... (continues)
Time remaining: 0
Done!
```

### What Success Looks Like
Countdown progresses from 10 to 0. "Done!" prints when countdown complete.

### Common Mistakes
- Not storing startTime in Start()
- Using Time.deltaTime instead of Time.time (doesn't accumulate correctly)
- Logging every frame causes spam (should add delay)
- Integer casting truncates decimals

---

## Problem 14: FindGameObjectWithTag Search

### Solution

```csharp
void Start()
{
    GameObject player = GameObject.FindGameObjectWithTag("Player");

    if(player != null)
    {
        Rigidbody rb = player.GetComponent<Rigidbody>();

        if(rb != null)
        {
            rb.AddForce(Vector3.up * 10f, ForceMode.Impulse);
            Debug.Log("Force applied to player");
        }
    }
}
```

### What Success Looks Like
Script finds the Player GameObject by tag. If found and has Rigidbody, applies upward force. Console confirms action.

### Common Mistakes
- Not checking if player is null (null reference exception)
- Forgetting to tag the Player GameObject
- Using wrong tag name (case-sensitive)
- Not checking if Rigidbody exists before using it

---

## Problem 15: Inventory Management with Lists

### Solution

```csharp
using System.Collections.Generic;

public List<string> inventory = new List<string>();

void Start()
{
    inventory.Add("Sword");
    inventory.Add("Shield");
    inventory.Add("Potion");

    PrintInventory();

    inventory.Remove("Shield");
    PrintInventory();

    inventory.Add("Scroll");
    PrintInventory();
}

void PrintInventory()
{
    Debug.Log("Inventory (" + inventory.Count + " items):");
    foreach(string item in inventory)
        Debug.Log("  - " + item);
}
```

**Console Output:**
```
Inventory (3 items):
  - Sword
  - Shield
  - Potion
Inventory (2 items):
  - Sword
  - Potion
Inventory (3 items):
  - Sword
  - Potion
  - Scroll
```

### What Success Looks Like
List properly adds and removes items. Count updates correctly. Foreach iteration works.

### Common Mistakes
- Using arrays instead of List (fixed size)
- Not using `Count` property (using `Length`)
- Not checking if item exists before removing
- Not clearing inventory when switching scenes

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | Variable Declaration | Beginner |
| 2 | Arithmetic Operators | Beginner |
| 3 | If/Else Conditionals | Beginner |
| 4 | Arrays | Beginner |
| 5 | Input & Movement | Intermediate |
| 6 | Instantiation & Loops | Beginner |
| 7 | Lists & Foreach | Intermediate |
| 8 | GetComponent | Intermediate |
| 9 | Methods & Parameters | Beginner |
| 10 | Math & Trigonometry | Intermediate |
| 11 | String Interpolation | Beginner |
| 12 | Complex Conditionals | Intermediate |
| 13 | Time Management | Intermediate |
| 14 | GameObject Finding | Intermediate |
| 15 | Inventory Systems | Intermediate |
