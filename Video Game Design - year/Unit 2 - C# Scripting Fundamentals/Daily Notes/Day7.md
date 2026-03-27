# Day 7: foreach Loops and Collections

**Learning Target:** I can use foreach loops and work with Lists for dynamic collections.

---

## Key Concepts

**foreach** — Loop that iterates over each element without needing an index.

**List<T>** — A dynamic array that grows/shrinks at runtime.

**Add/Remove** — Modify lists during gameplay.

---

## foreach vs for

```csharp
using UnityEngine;
using System.Collections.Generic;

public class CollectionExample : MonoBehaviour
{
    void Start()
    {
        // Array: fixed size
        string[] items = { "Sword", "Shield", "Potion" };
        
        // foreach over array
        foreach(string item in items)
        {
            Debug.Log("Item: " + item);
        }
        
        // List: dynamic size
        List<string> inventory = new List<string>();
        inventory.Add("Sword");
        inventory.Add("Shield");
        inventory.Add("Potion");
        
        // foreach over list
        foreach(string item in inventory)
        {
            Debug.Log("Inventory: " + item);
        }
        
        // Remove from list
        inventory.Remove("Potion");
        
        // Access by index (like array)
        Debug.Log("First item: " + inventory[0]);
    }
}
```

---

## List Methods

| Method | Use |
|--------|-----|
| `Add(item)` | Add to end |
| `Remove(item)` | Remove by value |
| `RemoveAt(index)` | Remove by position |
| `Count` | How many items |
| `[index]` | Access by position |
| `Clear()` | Remove all |

---

## Practice Problems

**Beginner:** Create a List of 5 numbers, add 2 more, then foreach-loop to print them all.

**Intermediate:** Create an enemy list, add 3 enemies, remove the second one, print what remains.

**Challenge:** Create a game system where enemies spawn dynamically. Add to list when spawned, remove when defeated. Use foreach to damage all enemies.

<details>
<summary>✅ Sample: Dynamic Enemy List</summary>

```csharp
using System.Collections.Generic;
using UnityEngine;

public class EnemyManager : MonoBehaviour
{
    List<string> enemies = new List<string>();
    
    void Start()
    {
        enemies.Add("Goblin");
        enemies.Add("Orc");
        enemies.Add("Troll");
    }
    
    void Update()
    {
        foreach(string enemy in enemies)
        {
            Debug.Log("Enemy: " + enemy);
        }
    }
}
```

</details>
