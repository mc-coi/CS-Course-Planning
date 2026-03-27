# Day 4: Conditionals (if, else if, else)

**Learning Target:** I can write conditional statements to make decisions based on values and comparisons.

---

## Key Concepts

**Conditional** — A statement that executes code only if a condition is true.

**Comparison Operators** — `==` (equal), `!=` (not equal), `<`, `>`, `<=`, `>=`.

**if/else if/else** — Structure for multiple decision branches.

**Logical Operators** — `&&` (AND), `||` (OR), `!` (NOT).

---

## Conditional Examples

```csharp
using UnityEngine;

public class HealthSystem : MonoBehaviour
{
    public int health = 100;
    public int maxHealth = 100;
    
    void Update()
    {
        // Simple if
        if(health <= 0)
        {
            Debug.Log("Game Over!");
        }
        
        // if/else
        if(health > 50)
        {
            Debug.Log("Healthy");
        }
        else
        {
            Debug.Log("Weak");
        }
        
        // if/else if/else
        if(health >= 80)
        {
            Debug.Log("Excellent health");
        }
        else if(health >= 50)
        {
            Debug.Log("Good health");
        }
        else if(health >= 20)
        {
            Debug.Log("Low health");
        }
        else
        {
            Debug.Log("Critical!");
        }
        
        // Logical operators
        if(health > 0 && health < 30)
        {
            Debug.Log("Critical and alive");
        }
        
        if(health <= 0 || health >= maxHealth)
        {
            Debug.Log("Extreme state");
        }
    }
}
```

---

## Comparison Operators Reference

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | true |
| `!=` | Not equal | `5 != 3` | true |
| `<` | Less than | `3 < 5` | true |
| `>` | Greater than | `5 > 3` | true |
| `<=` | Less than or equal | `5 <= 5` | true |
| `>=` | Greater than or equal | `5 >= 3` | true |

---

## Logical Operators

```csharp
// AND: Both must be true
if(health > 0 && isAlive)
{
    Debug.Log("Player is alive");
}

// OR: At least one must be true
if(canJump || hasDoubleJump)
{
    Debug.Log("Player can jump");
}

// NOT: Inverts the condition
if(!isDead)
{
    Debug.Log("Player is not dead");
}
```

---

## Unity Setup Steps

1. **Create a script: "EnemyAI"**
2. **Add variables:**
   ```csharp
   public int health = 50;
   public float distance = 10f;
   ```
3. **In Update(), add conditions:**
   ```csharp
   if(distance < 5f)
       Debug.Log("Player is close!");
   if(health <= 0)
       Debug.Log("Enemy defeated");
   ```
4. **Attach to a cube and test**

---

## Guided Practice

1. **Create a character level-up system** — if XP >= levelThreshold, level up
2. **Create a damage calculation** — if enemy defense is high, reduce damage to minimum 1
3. **Create an inventory check** — if item count > 0, can use item

---

## Practice Problems

**Beginner:** Write a script that checks if a number is positive, negative, or zero. Log each case.

**Intermediate:** Create a health system where damage is applied differently based on armor value. If armor >= 80, reduce all damage to 1.

**Challenge:** Write a script that determines which "zone" a player is in based on distance from origin. Zones: <5 (close), <15 (medium), <30 (far), >=30 (very far). Log the zone.

<details>
<summary>💡 Hints</summary>
- Use `==` for equality, `=` for assignment
- `else if` allows multiple branches
- Always use `&&` (AND) for multiple true conditions
- Use `||` (OR) when one of many conditions works
- Avoid nested if statements when possible (use else if instead)
</details>

<details>
<summary>✅ Sample: Zone System</summary>

```csharp
using UnityEngine;

public class ZoneDetector : MonoBehaviour
{
    void Update()
    {
        float distance = Vector3.Distance(transform.position, Vector3.zero);
        
        if(distance < 5f)
        {
            Debug.Log("Zone: Close");
        }
        else if(distance < 15f)
        {
            Debug.Log("Zone: Medium");
        }
        else if(distance < 30f)
        {
            Debug.Log("Zone: Far");
        }
        else
        {
            Debug.Log("Zone: Very Far");
        }
    }
}
```

</details>
