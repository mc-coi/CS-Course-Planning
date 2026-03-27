# Unit 2 Practice Problems

Complete these 15 problems to reinforce Unit 2 concepts. Solutions included.

---

## Problem 1: Variable Declaration and Types

Declare variables for a game character system:
- Name (string)
- Level (int)
- Experience (float)
- Health (int)
- Is Alive (bool)
- Spawn Point (Vector3)

Create a script that logs all values in Start().

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

---

## Problem 2: Arithmetic and XP System

Calculate player progression:
- Current XP: 1500
- XP per level: 1000
- Calculate: current level, remaining XP to next level
- Output: "Level X: XXX/1000 XP"

### Solution

```csharp
void Start()
{
    int currentXP = 1500;
    int xpPerLevel = 1000;
    
    int level = currentXP / xpPerLevel;
    int xpInLevel = currentXP % xpPerLevel;
    int xpNeeded = xpPerLevel - xpInLevel;
    
    Debug.Log("Level " + level + ": " + xpInLevel + "/" + xpPerLevel + " XP");
    Debug.Log("Progress: " + xpNeeded + " XP to next level");
}
```

---

## Problem 3: Health System with Conditionals

Create health damage system:
- Max health: 100
- Take 35 damage
- Log health state: "Healthy" (>50), "Hurt" (>20), "Critical" (<=20)

### Solution

```csharp
void Start()
{
    int maxHealth = 100;
    int damage = 35;
    int currentHealth = maxHealth - damage;
    
    if(currentHealth > 50)
        Debug.Log("Healthy");
    else if(currentHealth > 20)
        Debug.Log("Hurt");
    else
        Debug.Log("Critical");
}
```

---

## Problem 4: Inventory with Arrays

Create an inventory system:
- Array of item names: "Sword", "Shield", "Potion"
- Loop through and log: "Item X: [name]"
- Remove middle item and count remaining

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

---

## Problem 5: Player Movement with Input

Write a script that:
- Moves object forward/backward with W/S at 5 units/sec
- Rotates left/right with A/D at 90°/sec
- Jumps with Space (print "Jump!")

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

---

## Problem 6: Spawn Objects in a Loop

Instantiate 10 cubes at positions (0-9, 0, 0) using a for loop.

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

---

## Problem 7: Foreach Over List

Create a list of enemies, add 5, use foreach to log each.

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

---

## Problem 8: GetComponent and Rigidbody

Write a script that:
- Gets the Rigidbody component
- Sets velocity to 10 units/sec forward
- Logs the velocity each frame

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

---

## Problem 9: Method with Parameters

Write a TakeDamage method that:
- Takes damage (int) as parameter
- Reduces health
- Logs: "Health: XX/100"

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

---

## Problem 10: Circular Motion

Create a script that orbits an object around origin in a circle:
- Radius: 3 units
- Period: 10 seconds (one orbit)

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

---

## Problem 11: String Interpolation

Create a character profile script that logs:
"Hero (Level 5): 80/100 HP, 1500/2000 XP"

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

---

## Problem 12: Conditions and Damage Calculation

Apply damage accounting for armor:
- Damage: 50
- Armor: varies (test: 30, 80, 100)
- If armor >= 80, minimum damage = 1
- Otherwise: damage - armor

### Solution

```csharp
void CalculateDamage(int baseDamage, int armor)
{
    int finalDamage;
    
    if(armor >= 80)
        finalDamage = 1;  // Minimum
    else
        finalDamage = baseDamage - armor;
    
    if(finalDamage < 0)
        finalDamage = 0;
    
    Debug.Log("Damage: " + finalDamage);
}

void Start()
{
    CalculateDamage(50, 30);   // 20
    CalculateDamage(50, 80);   // 1
    CalculateDamage(50, 100);  // 1
}
```

---

## Problem 13: Time-Based Countdown

Write a script that counts down from 10 to 0:
- Use Time.time
- Print when each second passes
- Print "Done!" at 0

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

---

## Problem 14: FindGameObjectWithTag Search

Write a script that:
- Finds a GameObject tagged "Player"
- Gets its Rigidbody
- Applies a force (if exists)

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

---

## Problem 15: Inventory Management with Lists

Create an inventory system that:
- Starts with 3 items
- Can add items
- Can remove items by name
- Logs current inventory

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

