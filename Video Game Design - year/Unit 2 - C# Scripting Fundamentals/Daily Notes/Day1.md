# Day 1: Variables and Data Types

**Learning Target:** I can declare variables of different types (int, float, string, bool, Vector3) and understand public vs private visibility.

---

## Key Concepts

**Variable** — A named container that stores a value. Must have a type and a name.

**Data Types** — Different kinds of values:
- **int** — Whole numbers: -5, 0, 42, 1000
- **float** — Decimal numbers: 3.14, -0.5, 2.0 (always suffix with `f`: `5f`)
- **string** — Text: "Hello", "Player_1", "" (empty string)
- **bool** — True or False (lowercase)
- **Vector3** — 3D position/direction: (x, y, z)

**Public vs Private:**
- **public** — Visible in Inspector; can be tweaked without recompiling
- **private** — Hidden from Inspector; internal use only (default if not specified)

**Initialization** — Setting a value when declaring: `int score = 0;`

---

## Common Variables in Games

```csharp
using UnityEngine;

public class PlayerStats : MonoBehaviour
{
    // Visible in Inspector; tweakable during development
    public int maxHealth = 100;
    public float moveSpeed = 5.5f;
    public string playerName = "Hero";
    public bool isAlive = true;
    public Vector3 respawnPoint = new Vector3(0, 1, 0);
    
    // Hidden from Inspector; internal tracking
    private int currentHealth;
    private float timeAlive;
    
    void Start()
    {
        currentHealth = maxHealth;
        Debug.Log(playerName + " spawned at " + respawnPoint);
    }
}
```

---

## Data Type Reference Table

| Type | Example | Use |
|------|---------|-----|
| **int** | `42`, `-5`, `0` | Counters, health, ammo, scores |
| **float** | `3.14f`, `0.5f`, `-1.2f` | Speed, damage, time, rotation angles |
| **string** | `"Hello"`, `"Item_Sword"` | Names, messages, UI text |
| **bool** | `true`, `false` | Flags: is alive? is jumping? has key? |
| **Vector3** | `(1, 2, 3)`, `(0, 1, 0)` | Position, direction, scale |
| **Vector2** | `(1, 0)` | 2D position, UI coordinates |

---

## Unity Setup Steps

1. **Create a script:** "PlayerStats"
2. **Inside, declare these variables:**
   ```csharp
   public int level = 1;
   public float experience = 0f;
   public string characterClass = "Warrior";
   public bool hasKey = false;
   ```
3. **In Start(), log them:**
   ```csharp
   Debug.Log("Level: " + level);
   Debug.Log("Class: " + characterClass);
   ```
4. **Attach to a cube** and select it
5. **In Inspector, you see all public variables** — change them
6. **Press Play** — Console shows your values

---

## Guided Practice

1. **Create a script with 5 variables:** health (int), speed (float), name (string), alive (bool), position (Vector3)
2. **In Start(), print all of them** using Debug.Log
3. **Attach to a GameObject** and run
4. **Change values in Inspector** and run again
5. **Confirm:** Public variables are editable, private are not

---

## Practice Problems

**Beginner:** Declare 3 variables: playerHealth (int, 100), playerSpeed (float, 5.5), playerName (string, "Hero"). Print them to Console.

**Intermediate:** Create a script for an enemy. Declare variables: health, damage, attackRange (float), patrolSpeed (float). Log them in Start().

**Challenge:** Create a script for a game system. Include variables tracking: current level (int), total score (int), elapsed time (float), game state (string: "menu" or "playing"), is paused (bool). Print the game state.

<details>
<summary>💡 Hints</summary>
- Always use `f` suffix for float literals: `5.5f`, not `5.5`
- Strings are in double quotes: `"Hello"`, not 'Hello'
- Vector3 requires `new`: `new Vector3(1, 2, 3)`
- Private variables are the default; use them for internal data you don't want to tweak
- Public variables appear in Inspector in alphabetical order
</details>

<details>
<summary>✅ Sample: Complete PlayerStats</summary>

```csharp
using UnityEngine;

public class PlayerStats : MonoBehaviour
{
    public int health = 100;
    public float speed = 5.5f;
    public string name = "Hero";
    public bool isAlive = true;
    public Vector3 spawnPoint = Vector3.zero; // (0,0,0)
    
    private int damageDealt = 0; // Track internally
    
    void Start()
    {
        Debug.Log("Player: " + name);
        Debug.Log("Health: " + health);
        Debug.Log("Speed: " + speed);
        Debug.Log("Spawn Point: " + spawnPoint);
    }
}
```

</details>
