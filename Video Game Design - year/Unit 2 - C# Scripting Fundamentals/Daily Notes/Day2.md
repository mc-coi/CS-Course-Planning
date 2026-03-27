# Day 2: Variables (continued) & Variable Inspector Serialization

**Learning Target:** I can understand serialization, array types, and how variables interact with the Inspector.

---

## Key Concepts

**Serialization** — Unity saves public variables to the scene file so they persist between Play sessions.

**Editor Integration** — Public variables appear in Inspector for tweaking. Useful for designers who don't code.

**Array** — A collection of values of the same type. Declared with `[]`.

**null** — "No value"; an empty reference. Useful for checking if something exists.

---

## Variable Serialization

```csharp
using UnityEngine;

public class GameSettings : MonoBehaviour
{
    // Public: Serialized to scene, visible in Inspector
    public int targetFPS = 60;
    public string gameName = "My Game";
    
    // Private: NOT serialized, hidden from Inspector
    private int currentScore = 0;
    
    // Arrays: Collections of the same type
    public int[] enemyHealthValues = { 10, 20, 30, 40 };
    public string[] weaponNames = { "Sword", "Bow", "Staff" };
}
```

---

## Common Variable Patterns

| Pattern | Use |
|---------|-----|
| `public float speed = 5f;` | Tweakable movement speed |
| `private int health = 100;` | Internal health tracking |
| `public bool debugMode = false;` | Toggle debug logs |
| `public string[] items = { };` | Empty array (fill in Inspector) |
| `public Vector3 targetPosition = Vector3.zero;` | Set position in code/Inspector |

---

## Unity Setup Steps

1. **Create a script: "GameConfig"**
2. **Add these public variables:**
   ```csharp
   public int maxLevel = 10;
   public string[] levelNames = { "Forest", "Mountain", "Cave" };
   public float difficultyMultiplier = 1.5f;
   ```
3. **Attach to a GameObject**
4. **In Inspector:** You see these fields; modify them
5. **Arrays show up as lists:** You can expand and edit individual elements

---

## Guided Practice

1. **Create a script with 3 different arrays** (enemies, items, levels)
2. **In the Inspector, expand each array** and set values
3. **In Start(), log one element from each:** `Debug.Log(enemies[0])`
4. **Press Play and verify output**

---

## Practice Problems

**Beginner:** Create a script with one public int array. In Inspector, set it to {10, 20, 30}. In Start(), print the first and last elements.

**Intermediate:** Create a script with parallel arrays: `enemyNames` (string) and `enemyHealth` (int). Both should have 3 elements. Print pairs: "Spider (10 HP)", "Goblin (15 HP)", etc.

**Challenge:** Understand serialization. Modify a public variable during Play Mode, press Stop, then check the Inspector. Is the variable back to its original value? Why? Document your findings.

<details>
<summary>💡 Hints</summary>
- Array indices start at 0: `array[0]` is the first element
- Array length: `array.Length` (capital L)
- Empty array: `new int[5]` creates 5 slots, all set to 0
- Serialization means public variables are saved to the scene file
- Play Mode changes revert; serialization doesn't make them permanent (you still need Edit Mode to save)
</details>

<details>
<summary>✅ Sample: Parallel Arrays</summary>

```csharp
using UnityEngine;

public class EnemyData : MonoBehaviour
{
    public string[] enemyNames = { "Goblin", "Orc", "Troll" };
    public int[] enemyHealth = { 10, 25, 50 };
    
    void Start()
    {
        for(int i = 0; i < enemyNames.Length; i++)
        {
            Debug.Log(enemyNames[i] + ": " + enemyHealth[i] + " HP");
        }
    }
}
```

Output in Console:
```
Goblin: 10 HP
Orc: 25 HP
Troll: 50 HP
```

</details>
