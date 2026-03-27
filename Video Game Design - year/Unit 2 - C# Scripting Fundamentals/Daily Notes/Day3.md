# Day 3: Arithmetic Operators and String Operations

**Learning Target:** I can perform arithmetic operations and concatenate/manipulate strings in C#.

---

## Key Concepts

**Arithmetic Operators** — `+`, `-`, `*`, `/`, `%` (modulo: remainder after division).

**String Concatenation** — Combining strings with `+`.

**String Interpolation** — Embedding variables in strings with `$"text {variable}"` (modern approach).

**Order of Operations** — Multiplication and division before addition and subtraction (PEMDAS).

---

## Arithmetic Examples

```csharp
using UnityEngine;

public class MathExamples : MonoBehaviour
{
    void Start()
    {
        // Arithmetic
        int a = 10;
        int b = 3;
        
        int sum = a + b;              // 13
        int difference = a - b;        // 7
        int product = a * b;           // 30
        int quotient = a / b;          // 3 (integer division)
        int remainder = a % b;         // 1 (10 divided by 3 leaves remainder 1)
        
        // String concatenation
        string playerName = "Hero";
        int health = 100;
        string message = playerName + " has " + health + " HP";
        // Result: "Hero has 100 HP"
        
        // String interpolation (cleaner)
        string message2 = $"{playerName} has {health} HP";
        
        Debug.Log(message2);
    }
}
```

---

## Operator Reference

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `5 + 3` | 8 |
| `-` | Subtraction | `5 - 3` | 2 |
| `*` | Multiplication | `5 * 3` | 15 |
| `/` | Division | `15 / 3` | 5 |
| `%` | Modulo (remainder) | `10 % 3` | 1 |
| `+` | String concat | `"Hello" + " World"` | "Hello World" |

---

## Unity Setup Steps

1. **Create a script: "Calculator"**
2. **In Start(), declare variables and perform operations:**
   ```csharp
   int damage = 25;
   int defense = 10;
   int trueDamage = damage - defense;
   Debug.Log("True damage: " + trueDamage);
   ```
3. **Test string operations:**
   ```csharp
   string itemName = "Sword";
   int itemPrice = 50;
   Debug.Log($"Item: {itemName}, Price: {itemPrice}g");
   ```
4. **Attach and run**

---

## Guided Practice

1. **Create a score calculation:**
   - Base score = 100
   - Bonus points = 25
   - Multiplier = 2
   - Calculate: (base + bonus) * multiplier
   - Log: "Final score: X"

2. **String formatting:**
   - Use interpolation to create: "Level 5: Defeat 10 enemies"
   - Use concatenation for the same (compare readability)

3. **Modulo practice:**
   - Calculate if a number is even or odd using `%`
   - If `number % 2 == 0`, it's even

---

## Practice Problems

**Beginner:** Write a script that calculates total cost: 3 items at 10 gold each, plus 5 gold tax. Log the result.

**Intermediate:** Create a script that calculates damage after defense. Damage = 50, Defense = 15. Result should account for both. Log in a nicely formatted message.

**Challenge:** Write a script that simulates level progression. Current XP = 1500, XP per level = 1000. Calculate current level (use `/`), remaining XP to next level (use `%`), and log both.

<details>
<summary>💡 Hints</summary>
- Integer division (`/`) truncates decimals: 10 / 3 = 3, not 3.33
- Use float if you need decimals: 10f / 3f = 3.33
- `%` is useful for cycles (checking every Nth frame) or even/odd
- String interpolation with `$"..."` is cleaner than concatenation
- Order of operations matters: `10 + 5 * 2` = 20, not 30
</details>

<details>
<summary>✅ Sample: XP Calculator</summary>

```csharp
using UnityEngine;

public class XPCalculator : MonoBehaviour
{
    void Start()
    {
        int currentXP = 1500;
        int xpPerLevel = 1000;
        
        int currentLevel = currentXP / xpPerLevel;
        int xpInCurrentLevel = currentXP % xpPerLevel;
        int xpNeeded = xpPerLevel - xpInCurrentLevel;
        
        Debug.Log($"Level: {currentLevel}");
        Debug.Log($"Progress: {xpInCurrentLevel}/{xpPerLevel}");
        Debug.Log($"XP needed for next level: {xpNeeded}");
    }
}
```

Output:
```
Level: 1
Progress: 500/1000
XP needed for next level: 500
```

</details>
