# Day 6: Loops (for loops)

**Learning Target:** I can write for loops to repeat code and iterate over collections.

---

## Key Concepts

**Loop** — Code that repeats a block multiple times.

**for loop** — Loop that runs a fixed number of times: `for(int i = 0; i < 10; i++)`

**Loop Variable** — Usually `i`; tracks current iteration (0, 1, 2, ...)

**Increment** — `i++` means add 1 to i each iteration.

---

## for Loop Syntax

```csharp
for(int i = 0; i < 5; i++)
{
    Debug.Log("Iteration: " + i); // Prints 0, 1, 2, 3, 4
}

// Over arrays
int[] scores = { 10, 20, 30 };
for(int i = 0; i < scores.Length; i++)
{
    Debug.Log("Score: " + scores[i]);
}

// Counting down
for(int i = 10; i > 0; i--)
{
    Debug.Log(i); // 10, 9, 8, ..., 1
}

// Stepping by 2
for(int i = 0; i < 10; i += 2)
{
    Debug.Log(i); // 0, 2, 4, 6, 8
}
```

---

## Loop Pattern

```
for(initialization; condition; increment)
{
    // Code runs while condition is true
}
```

- **initialization:** Set starting value (i = 0)
- **condition:** Keep looping while true (i < 10)
- **increment:** Change value each iteration (i++)

---

## Guided Practice

1. **Print 1 to 10**
2. **Sum numbers 1 to 100**
3. **Create 5 cubes in a line** using Instantiate in a loop
4. **Iterate over an array** and print each element

---

## Practice Problems

**Beginner:** Write a loop that prints "Hello" 10 times.

**Intermediate:** Create an array of enemy names. Loop through and log each one.

**Challenge:** Write a script that spawns 10 cubes at positions (0,0,0), (1,0,0), (2,0,0), etc. using a loop.

<details>
<summary>💡 Hints</summary>
- `i++` means i = i + 1
- Array indices: 0 to (length - 1)
- `array.Length` gives the number of elements
- Use `i += 2` to skip every other iteration
- Break out of a loop early with `break`
</details>

<details>
<summary>✅ Sample: Cube Spawner</summary>

```csharp
using UnityEngine;

public class LineSpawner : MonoBehaviour
{
    public GameObject cubePrefab;
    
    void Start()
    {
        for(int i = 0; i < 10; i++)
        {
            Vector3 position = new Vector3(i, 0, 0);
            Instantiate(cubePrefab, position, Quaternion.identity);
        }
    }
}
```

</details>
