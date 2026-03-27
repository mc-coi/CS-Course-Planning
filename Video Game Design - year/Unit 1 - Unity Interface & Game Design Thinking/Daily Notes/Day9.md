# Day 9: Introduction to C# and MonoBehaviour

**Learning Target:** I can write a simple C# script, attach it to a GameObject, and use Debug.Log to print messages.

---

## Key Concepts

**Script** — A C# file that defines behavior. Attached to a GameObject as a component.

**MonoBehaviour** — The base class all game scripts inherit from. Provides built-in methods like `Start()` and `Update()`.

**Start()** — Method called once when the GameObject first becomes active (before the first Update).

**Update()** — Method called every frame (60+ times per second). Where most gameplay logic happens.

**Debug.Log()** — Prints a message to the Console (debugging tool).

**using UnityEngine;** — Imports the Unity library so you can use GameObjects, transforms, etc.

---

## C# Basics for Games

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    // Variables (declared OUTSIDE methods, at class level)
    public int health = 100;
    private float speed = 5.0f;
    
    // Start is called when the game begins
    void Start()
    {
        Debug.Log("Game started! Player health: " + health);
    }
    
    // Update is called every frame
    void Update()
    {
        Debug.Log("Frame " + Time.frameCount);
    }
}
```

---

## Unity Setup Steps

1. **Create a new C# script:** In Project window, right-click → Create → C# Script → name it "HelloWorld"
2. **Double-click to open it** (in your code editor: VS Code, Visual Studio, or MonoDevelop)
3. **Inside the class, add to Start():**
   ```csharp
   Debug.Log("Hello from Unity!");
   ```
4. **Save the file** (Cmd/Ctrl+S)
5. **Return to Unity** and wait for it to compile (bottom-right corner shows progress)
6. **Create a cube in the scene** and select it
7. **Drag HelloWorld script onto the cube** (or in Inspector: Add Component → search "HelloWorld")
8. **Press Play** and look at the Console (Window → General → Console)
9. **You should see "Hello from Unity!"** printed

---

## Guided Practice

1. **Create a script called "LogNumbers"**
2. **In Start(), print:** "The number 42"
3. **In Update(), print:** "Frame: " + the current frame number
4. **Attach to a cube and press Play**
5. **Open the Console and verify messages appear** (You'll see lots of "Frame" messages!)
6. **Press Stop and look at Console:** Messages are gone (they were live logs)

---

## Practice Problems

**Beginner:** Write a script that prints "Script is working!" in Start(). Attach it to a cube, press Play, and confirm it prints.

**Intermediate:** Create a script that prints the cube's position (transform.position) in Update(). Attach it to a cube, press Play, move the cube in the Scene View, and watch the position update in Console.

**Challenge:** Write a script that tracks elapsed time. In Update(), print the current time (Time.time). What do you notice about the numbers? Why?

<details>
<summary>💡 Hints</summary>
- C# is case-sensitive: `Debug.Log` works, `debug.log` doesn't
- Every script must inherit from MonoBehaviour: `public class MyScript : MonoBehaviour`
- Start() runs once at the beginning; Update() runs every frame
- Time.time = seconds elapsed since Play started
- Time.deltaTime = seconds since last frame (useful for smooth movement)
- Concatenate strings with `+`: "Value: " + 42
</details>

<details>
<summary>✅ Sample: Time Logger</summary>

```csharp
using UnityEngine;

public class TimeLogger : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Game started at Time.time = " + Time.time);
    }
    
    void Update()
    {
        Debug.Log("Current time: " + Time.time + " seconds");
    }
}
```

Note: This will print A LOT of messages because Update runs every frame!

</details>
