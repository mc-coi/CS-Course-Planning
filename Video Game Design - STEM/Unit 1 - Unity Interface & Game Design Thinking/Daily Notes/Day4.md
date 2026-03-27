# Day 4: Creating Scripts & MonoBehaviour Basics

**Learning Target:** I can write C# scripts and attach them to GameObjects to add behavior.

## Key Concepts

- **C# Script:** A file containing code that defines behavior for a GameObject
- **MonoBehaviour:** The base class that allows scripts to be attached to GameObjects
- **Start() Method:** Called once at the beginning of the scene
- **Update() Method:** Called once per frame (typically 60 frames per second)
- **Debug.Log():** Prints messages to the Console for debugging
- **GetComponent():** Accesses other components attached to the same GameObject

To create a script:
1. Right-click in the Project panel
2. Create > C# Script
3. Name it something descriptive (e.g., PlayerController)
4. Double-click to open in your code editor
5. Write code inside the class
6. Save and return to Unity
7. Drag the script onto a GameObject in the Hierarchy to attach it

The structure of every MonoBehaviour script includes:
```
using UnityEngine;

public class ScriptName : MonoBehaviour
{
    // Member variables (properties of the class)

    void Start() { }       // Initialization
    void Update() { }      // Per-frame logic
}
```

**Start() vs Update():**
- **Start()** runs once when the scene begins (good for initialization)
- **Update()** runs every frame (good for continuous logic like input checking)

**Debug.Log()** is essential for debugging. Print variables to the Console to understand what's happening in your code.

## Code Examples

```csharp
using UnityEngine;

public class SimpleController : MonoBehaviour
{
    // Public variables can be edited in the Inspector
    public float speed = 5f;

    // Private variables are only accessible within this script
    private int score = 0;
    private Renderer meshRenderer;

    // Start() is called before the first frame update
    void Start()
    {
        Debug.Log("Game initialized. Score: " + score);

        // Cache the Renderer component for performance
        meshRenderer = GetComponent<Renderer>();
    }

    // Update() is called once per frame
    void Update()
    {
        // For now, just rotate the GameObject continuously
        transform.Rotate(0, 50 * Time.deltaTime, 0);

        // Print debug info every frame (warning: spam!)
        // Debug.Log("Frame: " + Time.frameCount);
    }

    // A custom method we can call later
    public void AddScore(int points)
    {
        score += points;
        Debug.Log("Score updated to: " + score);
    }
}
```

## Guided Practice

1. Create a new C# script in the Project panel (name it "HelloWorld")
2. Double-click to open it in your code editor
3. Add a Debug.Log() in the Start() method
4. Save the file
5. Drag the script onto a Cube in your scene
6. Press Play and check the Console to see the message
7. Modify the script to add more Debug.Log() messages and test them

## Practice Problems

**Problem 1 — Beginner:** Write a simple script that prints "Hello, Game Developer!" to the Console when the scene starts.

**Problem 2 — Intermediate:** Explain the difference between Start() and Update() methods in a MonoBehaviour script.

**Problem 3 — Challenge:** Write a script that prints the time elapsed since the scene started (using Time.time) to the Console every second.

<details>
<summary>Hints</summary>

**Problem 1:** You need a MonoBehaviour class with a Start() method that uses Debug.Log().

**Problem 2:** Think about when each method is called. One runs at the beginning, the other runs repeatedly.

**Problem 3:** Create a timer variable in Update() to track elapsed time. Use Time.deltaTime to accumulate time, and check if it's greater than 1 second.
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
using UnityEngine;

public class HelloGame : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Hello, Game Developer!");
    }
}
```

**Problem 2:** Start() is called once, when the scene begins or when the GameObject is first enabled. Use it for initialization. Update() is called every frame. Use it for continuous logic like checking input, moving objects, or updating timers.

**Problem 3:**
```csharp
using UnityEngine;

public class ElapsedTimeLogger : MonoBehaviour
{
    private float timeSinceLastLog = 0f;

    void Update()
    {
        timeSinceLastLog += Time.deltaTime;
        if (timeSinceLastLog >= 1f)
        {
            Debug.Log("Time elapsed: " + Time.time);
            timeSinceLastLog = 0f;
        }
    }
}
```
</details>
