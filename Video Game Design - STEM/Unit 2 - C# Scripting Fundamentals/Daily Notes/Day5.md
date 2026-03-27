# Day 5: Variables & Data Types

**Learning Target:** I can declare variables using common data types and understand the difference between public and private variables.

## Key Concepts

- **Variable:** A named container that stores a value
- **Data Type:** The kind of value a variable holds (int, float, string, bool, Vector3)
- **int:** Integer (whole number) e.g., 5, -10, 0
- **float:** Floating-point number (decimal) e.g., 3.5f, -2.1f, 0.0f
- **string:** Text data e.g., "Hello", "Player Name"
- **bool:** Boolean (true or false)
- **Vector3:** A 3D position or direction (x, y, z)
- **Public vs. Private:** Public variables are visible in the Inspector; private are hidden
- **Serialization:** Unity saves public variables so they persist between play sessions

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
- **Vector3:** A structure with x, y, z components

The Inspector is where you interact with public variables. You can change values in the Inspector and see them reflected in the game. This is powerful for tuning game feel without recompiling code.

## Code Examples

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

## Guided Practice

1. Create a new C# script called "PlayerStats"
2. Declare 5 public variables of different types (int, float, string, bool, Vector3)
3. Declare 3 private variables
4. In Start(), initialize the private variables
5. Attach the script to a GameObject and play the scene
6. In the Inspector, change the public variable values and watch them update

## Practice Problems

**Problem 1 — Beginner:** Declare five variables in a script: an int, a float, a string, a bool, and a Vector3. Assign each one a value. Print them all to the Console.

**Problem 2 — Intermediate:** Create a script with 10 public variables of different types. In the Inspector, change their values and print them to the Console.

**Problem 3 — Challenge:** Design a character data structure using variables. Include stats like health, mana, experience, level, and name. Print all stats to the Console.

<details>
<summary>Hints</summary>

**Problem 1:** Use the syntax: `[type] [name] = [value];` Then use Debug.Log() to print each one.

**Problem 2:** Create the variables with public access modifier. Attach the script to a GameObject and modify the values in the Inspector while the game is running to see real-time updates.

**Problem 3:** Think about what data a character needs to track. Consider which should be public (tunable in Inspector) and which should be private (internal only).
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
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

**Problem 2:** Create multiple public variables like `public int score = 0;`, `public float damage = 15.5f;`, `public string gameName = "MyGame";`, etc. Then in Start(), print them all using Debug.Log().

**Problem 3:**
```csharp
using UnityEngine;

public class Character : MonoBehaviour
{
    public string characterName = "Hero";
    public int level = 1;
    public int maxHealth = 100;
    public int currentHealth = 100;
    public int mana = 50;
    public float experience = 0f;
    public int strength = 10;
    public int defense = 5;

    void Start()
    {
        Debug.Log("Character: " + characterName);
        Debug.Log("Level: " + level);
        Debug.Log("Health: " + currentHealth + "/" + maxHealth);
        Debug.Log("Mana: " + mana);
        Debug.Log("Experience: " + experience);
    }
}
```
</details>
