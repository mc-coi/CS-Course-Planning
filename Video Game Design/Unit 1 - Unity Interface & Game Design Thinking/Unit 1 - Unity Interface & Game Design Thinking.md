# Unit 1: Unity Interface & Game Design Thinking

## Unit Overview

**Duration:** Days 1-4 (4 days)
**Key Concepts:** Game design terminology, Unity editor layout, GameObjects, Transform component, scene hierarchy, basic scripting
**Big Idea:** Game design is both art and science. Unity is a tool that manages GameObjects in scenes using the engine's core building blocks: Transform, Renderer, and Script components.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Define key game design terms (mechanics, dynamics, aesthetics; MDA framework)
- [ ] Navigate the Unity editor panels (Scene, Game, Inspector, Hierarchy, Project)
- [ ] Create and manipulate GameObjects using the Transform component
- [ ] Understand the relationship between GameObjects, components, and scenes
- [ ] Write a basic C# MonoBehaviour script with Start() and Update() methods
- [ ] Use Debug.Log() to print messages to the Console for debugging
- [ ] Distinguish between the Scene view and Game view in the editor
- [ ] Build simple static scenes with multiple GameObjects and materials

---

## Day-by-Day Content

### Day 1: Game Design Vocabulary & Unity Panels

#### Key Concepts
- **Game Design:** The art and science of defining game rules, systems, and player experiences
- **MDA Framework:** Mechanics (rules) → Dynamics (behavior) → Aesthetics (player feeling)
- **Mechanics:** The rules and systems that govern gameplay (jumping, collecting coins, health)
- **Dynamics:** How mechanics interact during play (collecting coins gets faster, enemies adapt)
- **Aesthetics:** The emotional response players have (fun, tension, satisfaction)
- **Unity Editor:** A visual development environment for creating games
- **Scene:** A container for GameObjects and their relationships

#### Content
The Unity editor is divided into five main panels:

1. **Scene View** – A 3D viewport where you arrange and edit GameObjects
2. **Game View** – Shows what the camera sees (player perspective)
3. **Hierarchy Panel** – Displays all GameObjects in the current scene as a tree
4. **Inspector Panel** – Shows properties/components of the selected GameObject
5. **Project Panel** – File browser for all project assets (scripts, prefabs, sprites)

GameObjects are the fundamental building blocks in Unity. Each scene contains GameObjects, and each GameObject has components attached to it. The **Transform** component is the most essential—it stores position, rotation, and scale.

#### Example Workflow
1. Open Unity and create a new 3D scene
2. Right-click in the Hierarchy and create a new GameObject
3. In the Inspector, observe the Transform component showing x, y, z position
4. Drag the GameObject in the Scene view to move it
5. Open the Game view tab to see what the camera sees

#### Annotated Code Example

```csharp
using UnityEngine;

// MonoBehaviour is the base class for all scripts attached to GameObjects
public class GameManager : MonoBehaviour
{
    // This method runs once when the scene starts
    void Start()
    {
        // Print a debug message to the Console window
        Debug.Log("Game started!");
    }

    // This method runs once per frame
    void Update()
    {
        // We'll add gameplay logic here later
    }
}
```

---

### Day 2: Transform Component & Manipulation Tools

#### Key Concepts
- **Transform Component:** Stores position (x, y, z), rotation (x, y, z), and scale (x, y, z)
- **Position:** Where the GameObject is in 3D space, relative to its parent
- **Rotation:** The angle of the GameObject in three axes (degrees)
- **Scale:** The size multiplier (1.0 = normal size, 2.0 = twice as large)
- **Parent/Child Relationship:** GameObjects can be nested (child inherits parent's transform)
- **Gizmos:** Visual handles in the Scene view for moving, rotating, scaling
- **Local vs. World Space:** Local is relative to parent; world is absolute position in scene

#### Content
The **Move Tool** (W key), **Rotate Tool** (E key), and **Scale Tool** (R key) are the primary manipulation tools. When you select a GameObject:
- Press W to activate the Move gizmo (three colored arrows for X, Y, Z axes)
- Press E to activate the Rotate gizmo (three colored circles)
- Press R to activate the Scale gizmo (three colored handles)

The Hierarchy panel shows the scene structure. When one GameObject is a child of another, the child's position is relative to the parent. This is useful for organizing complex objects (e.g., a weapon might be a child of a player's hand).

#### Annotated Code Example

```csharp
using UnityEngine;

public class Rotator : MonoBehaviour
{
    // Speed of rotation in degrees per second
    public float rotationSpeed = 50f;

    void Update()
    {
        // Rotate the GameObject around the Y axis (vertical)
        // Multiply by Time.deltaTime for frame-rate-independent movement
        transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
    }
}
```

```csharp
using UnityEngine;

public class Mover : MonoBehaviour
{
    // The speed at which the GameObject moves
    public float speed = 5f;

    void Update()
    {
        // Move the GameObject forward along its Z axis
        // Time.deltaTime ensures smooth movement regardless of frame rate
        transform.Translate(0, 0, speed * Time.deltaTime);
    }
}
```

---

### Day 3: Materials, Lighting & Scene Building

#### Key Concepts
- **Material:** Defines how a surface looks (color, texture, shininess)
- **Shader:** A program that tells the GPU how to render a material
- **Light:** An object that illuminates the scene
- **Standard Material:** Unity's default physically-based material
- **Albedo:** The base color of a material
- **Metallic & Smoothness:** Properties that control reflections and specularity
- **Ambient Light:** Overall light in the scene from all directions

#### Content
Every mesh needs a material to be visible. Materials are created in the Project panel and assigned to Renderer components on GameObjects. The **Standard Material** shader is the default and supports:
- **Albedo:** The main color texture or color
- **Metallic:** How metal-like the surface is (0 = non-metal, 1 = pure metal)
- **Smoothness:** How shiny the surface is (0 = rough, 1 = mirror-like)

Lights are essential for visibility. Common light types:
- **Directional Light:** Simulates sunlight; illuminates everything equally
- **Point Light:** Emits light from a position in all directions
- **Spot Light:** A cone of light from a position, like a flashlight

To build a simple scene:
1. Create a Plane (GameObject > 3D Object > Plane) for the ground
2. Create a Cube and move it above the plane
3. Adjust the scale and position of objects
4. Create a Directional Light or use the default one
5. Assign different materials to objects to see how they look

#### Annotated Code Example

```csharp
using UnityEngine;

public class SceneBuilder : MonoBehaviour
{
    // Reference to the material to change color
    private Renderer meshRenderer;

    void Start()
    {
        // Get the Renderer component attached to this GameObject
        meshRenderer = GetComponent<Renderer>();

        // Change the albedo (base color) of the material
        // Note: Create a new material instance so we don't modify the original
        meshRenderer.material.color = new Color(1f, 0.5f, 0f); // Orange
    }

    void Update()
    {
        // Optional: Animate the color over time
        float hue = Time.time % 1f; // Cycles from 0 to 1
        meshRenderer.material.color = Color.HSVToRGB(hue, 1f, 1f);
    }
}
```

---

### Day 4: Creating Scripts & MonoBehaviour Basics

#### Key Concepts
- **C# Script:** A file containing code that defines behavior for a GameObject
- **MonoBehaviour:** The base class that allows scripts to be attached to GameObjects
- **Start() Method:** Called once at the beginning of the scene
- **Update() Method:** Called once per frame (typically 60 frames per second)
- **Debug.Log():** Prints messages to the Console for debugging
- **GetComponent():** Accesses other components attached to the same GameObject

#### Content
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

#### Annotated Code Example

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

---

## Practice Problems

### Beginner Tier

**Problem 1:** Create a new scene with a Cube and a Plane. Move the Cube above the Plane using the Move tool (W key). What are the Transform coordinates of the Cube?

<details>
<summary>Hint</summary>
Use the Scene view to visually position the Cube. Look at the Transform component in the Inspector to see the X, Y, Z values. The Y value should be greater than 0 to be above the Plane.
</details>

<details>
<summary>Answer</summary>
Answers will vary, but an example would be:
- Plane position: (0, 0, 0)
- Cube position: (0, 2, 0) or similar

The Y coordinate must be higher than the Plane's Y coordinate to be visually above it.
</details>

---

**Problem 2:** Explain the difference between Start() and Update() methods in a MonoBehaviour script.

<details>
<summary>Hint</summary>
Think about when each method is called. One runs at the beginning, the other runs repeatedly.
</details>

<details>
<summary>Answer</summary>
- **Start()** is called once, when the scene begins or when the GameObject is first enabled. Use it for initialization.
- **Update()** is called every frame. Use it for continuous logic like checking input, moving objects, or updating timers.
</details>

---

**Problem 3:** Write a simple script that prints "Hello, Game Developer!" to the Console when the scene starts.

<details>
<summary>Hint</summary>
You need a MonoBehaviour class with a Start() method that uses Debug.Log().
</details>

<details>
<summary>Answer</summary>
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
</details>

---

### Intermediate Tier

**Problem 4:** Create a rotating cube that prints its current rotation to the Console every second.

<details>
<summary>Hint</summary>
Use a timer variable in Update() to track elapsed time. Use Time.deltaTime to make it frame-rate independent.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class RotatingCube : MonoBehaviour
{
    private float rotationSpeed = 50f;
    private float timeSinceLastLog = 0f;

    void Update()
    {
        // Rotate the cube
        transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);

        // Track time and log every second
        timeSinceLastLog += Time.deltaTime;
        if (timeSinceLastLog >= 1f)
        {
            Debug.Log("Rotation: " + transform.eulerAngles);
            timeSinceLastLog = 0f;
        }
    }
}
```
</details>

---

**Problem 5:** Describe the MDA framework and give an example from a game you know.

<details>
<summary>Hint</summary>
MDA stands for Mechanics, Dynamics, Aesthetics. Think about how the rules (mechanics) create interactions (dynamics) that make players feel something (aesthetics).
</details>

<details>
<summary>Answer</summary>
**MDA Framework:**
- **Mechanics:** The rules and systems (e.g., in Mario, the ability to jump, collect coins, defeat enemies)
- **Dynamics:** How those mechanics interact during play (e.g., jumping over obstacles and collecting coins creates a challenging rhythm)
- **Aesthetics:** The emotional response (e.g., players feel excited, accomplished, or challenged)

**Example:** In Super Mario Bros, the mechanic of "press jump to jump higher the longer you hold" creates the dynamic of responsive control, giving players the aesthetic of empowerment and satisfaction.
</details>

---

**Problem 6:** Create a material with a custom color (not the default white). Apply it to a Cube. What color did you choose and why?

<details>
<summary>Hint</summary>
In the Project panel, right-click and create a new Material. In the Inspector, change the Albedo color. Then drag the material onto a Cube in the scene.
</details>

<details>
<summary>Answer</summary>
Answers will vary. Example: A bright red material (#FF0000) was chosen because it's eye-catching and could represent an important object like a power-up or hazard in a game. The specific color depends on the student's creative choice.
</details>

---

### Challenge Tier

**Problem 7:** Design a simple game concept (one paragraph) using the MDA framework. Describe the mechanics, dynamics, and aesthetics.

<details>
<summary>Hint</summary>
Start with a core mechanic (e.g., "dodge falling objects"), then describe how that mechanic creates interesting interactions (dynamics), and finally describe the emotional experience (aesthetics).
</details>

<details>
<summary>Answer</summary>
**Example Game: "Dodge Blocks"**

**Mechanics:** The player controls a square that moves left/right on the screen. Blocks fall from the top. When the player's square touches a block, they lose a life. Collecting a gold square adds a life.

**Dynamics:** As the game continues, blocks fall faster, creating increasing pressure. The player must react quickly and anticipate where blocks will land.

**Aesthetics:** Players experience tension and urgency. When they dodge a block, they feel relief. Collecting gold feels rewarding. The overall experience is one of focused, fast-paced challenge.
</details>

---

**Problem 8:** Build a scene with 5 GameObjects in a parent-child hierarchy. Move the parent and observe how the children move with it. Explain your observations.

<details>
<summary>Hint</summary>
Create a parent GameObject, then drag other GameObjects onto it in the Hierarchy to make them children. Move the parent using the Move tool.
</details>

<details>
<summary>Answer</summary>
When you move a parent GameObject, all children move with it while maintaining their relative positions. This is because each child's position is stored in local space relative to the parent.

**Observation:** If a parent is at (0, 0, 0) and a child is at (1, 1, 1) in local space, moving the parent to (5, 5, 5) moves the child to world space (6, 6, 6). The parent-child relationship maintains the spatial hierarchy, which is useful for organizing complex objects like vehicles with wheels or characters with limbs.
</details>

---

## Practice Bank (15 Problems)

1. **Hierarchy Organization:** Create a scene with 10 GameObjects. Organize them into a logical parent-child hierarchy (e.g., a "Player" parent with "Head," "Body," "Legs" children). Screenshot the Hierarchy panel.

2. **Transform Precision:** Use the Inspector to position a Cube at exactly (3.5, 2.0, -1.5). Verify using the Move tool that you can position it to the exact coordinates.

3. **Material Blending:** Create two materials with different colors. Assign one to a Cube and another to a Sphere. Adjust their Smoothness and Metallic values and describe the visual differences.

4. **Lighting Experiment:** Place a Cube in a dark scene (no lights). Add a Point Light near it. Move the light around and observe how the lighting changes. What happens when you increase the light's intensity?

5. **Script Attachment:** Write a script that prints the time elapsed since the scene started. Attach it to a Cube and run the scene. What does the Console show?

6. **Debug Logging:** Write a script that logs the frame count every 10 frames. Attach it to any GameObject and observe the pattern in the Console.

7. **Public vs. Private:** Create a script with both public and private variables. In the Inspector, verify that you can only edit the public ones.

8. **GetComponent:** Write a script that gets the Transform component of another GameObject in the scene (using GetComponent) and logs its position.

9. **Scale Manipulation:** Using the Scale tool (R key), make a Cube 2x larger in the X and Z axes, but 0.5x smaller in the Y axis. What's the resulting shape?

10. **Scene Navigation:** Create a scene with 20 GameObjects. Use the Hierarchy's search function to find a specific GameObject by name.

11. **Viewport Control:** In the Scene view, use middle-mouse drag to pan, scroll wheel to zoom, and right-click drag to rotate. Navigate to view your scene from 5 different angles.

12. **Time Analysis:** Write a script that prints `Time.deltaTime` to the Console every frame. What range of values do you see? Why does this matter?

13. **Color Interpolation:** Write a script that smoothly changes a Cube's color from red to blue over 5 seconds.

14. **Rotation Display:** Write a script that prints the current rotation (in degrees) every second. Rotate the GameObject and see the values change.

15. **Audio Cue:** Design a game event where collecting an object plays a sound and changes the object's color. Write pseudocode (plain English) describing the steps you'd take.

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Script doesn't attach to GameObject | Unity didn't recompile, or script has errors | Check the Console for errors; wait for compilation to finish |
| Changes in code don't appear in game | Not saving the file, or still editing Play mode | Save the file; don't edit while Play mode is active |
| GameObject moves but nothing happens | No camera or no renderer | Add a Camera to the scene; ensure the GameObject has a Renderer or a Mesh |
| Debug.Log doesn't print | Script not attached or not running | Attach script to a GameObject; check that the method is Start() or Update() |
| Parent-child relationships are wrong | Dragged wrong object in Hierarchy | Carefully select the parent first, then drag the child onto it |
| Material doesn't look right | Wrong shader or missing textures | Check the Inspector; use Standard shader for basic visuals |
| Time.deltaTime is 0 | Game is paused or framerate is very high | Time.deltaTime is never 0 in normal gameplay; check if Time.timeScale == 0 |
| Transform values jump around | Local vs. World space confusion | Check the space toggle in the Inspector (next to position values) |

---

## Assessment Prep: 10 Q&As

**Q1: What is the MDA framework?**
A: The MDA framework stands for Mechanics (rules), Dynamics (interactions), and Aesthetics (emotional response). It's a way to understand and design games by separating what players do, how systems interact, and how they feel.

**Q2: Name the five main panels in the Unity editor.**
A: Scene View, Game View, Hierarchy, Inspector, and Project Panel. These panels are essential for navigating, editing, and organizing your game.

**Q3: What is the Transform component?**
A: The Transform component stores a GameObject's position (X, Y, Z), rotation (X, Y, Z), and scale (X, Y, Z). Every GameObject has exactly one Transform component.

**Q4: What's the difference between Start() and Update()?**
A: Start() is called once when the scene begins (initialization). Update() is called every frame (continuous logic). Use Start() for setup; use Update() for gameplay.

**Q5: How do you attach a C# script to a GameObject?**
A: Drag the script file from the Project panel onto the GameObject in the Hierarchy, or select the GameObject and drag the script into the Inspector's Component area.

**Q6: What does Debug.Log() do?**
A: Debug.Log() prints a message to the Console window. It's essential for debugging: print variable values, track code execution, and understand what's happening in your game.

**Q7: Explain parent-child relationships in the Hierarchy.**
A: A child GameObject's position is relative to its parent (local space). When the parent moves, rotates, or scales, all children move with it. This is useful for organizing complex objects.

**Q8: What are the three tools for manipulating GameObjects in the Scene view?**
A: Move tool (W key), Rotate tool (E key), and Scale tool (R key). These tools have visual gizmos (handles) that let you adjust Transform values.

**Q9: What is a Material, and why do GameObjects need them?**
A: A Material defines how a surface looks (color, texture, reflectivity). It's made of a Shader (a program) and textures/properties. GameObjects need materials to be visible and to look the way you want.

**Q10: What is Time.deltaTime, and why is it important?**
A: Time.deltaTime is the time elapsed since the last frame (in seconds). It makes movement and animation frame-rate independent. Without it, faster computers would run games faster.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **GameObject** | The fundamental building block in Unity; a container for components |
| **Component** | A functional piece of a GameObject (Transform, Renderer, Script, Rigidbody) |
| **Prefab** | A saved template of a GameObject that can be instantiated multiple times |
| **Scene** | A container for GameObjects; equivalent to a "level" in a game |
| **Hierarchy** | The tree structure showing parent-child relationships of GameObjects |
| **Inspector** | The panel showing all properties and components of a selected GameObject |
| **Gizmo** | A visual handle in the Scene view for manipulating Transform properties |
| **Script** | A C# file containing code that defines behavior for a GameObject |
| **MonoBehaviour** | The base class for all scripts in Unity; provides Start(), Update(), and other methods |
| **Shader** | A program that tells the GPU how to render a material |
| **Texture** | An image file used to add detail to materials |
| **Light** | An object that illuminates the scene (Directional, Point, Spot) |
| **Camera** | The object that renders what the player sees; essential for the Game view |
| **Canvas** | A container for UI elements like buttons, text, and images (covered in Unit 5) |

### C# Syntax Quick Reference

**Variable Declaration:**
```csharp
public int health = 100;           // Public, editable in Inspector
private float speed = 5.5f;        // Private, hidden in Inspector
float localVar = 10f;              // Local to the method
```

**Method Definition:**
```csharp
void Start() { }                   // No return value, called once
void Update() { }                  // No return value, called every frame
int Add(int a, int b)              // Returns an int value
{
    return a + b;
}
```

**Accessing Components:**
```csharp
Renderer renderer = GetComponent<Renderer>();
Transform tf = GetComponent<Transform>();
// Or directly via the transform property (shorthand)
transform.position = new Vector3(0, 1, 0);
```

**Debug Output:**
```csharp
Debug.Log("Message");              // Normal log
Debug.LogWarning("Warning!");      // Yellow warning
Debug.LogError("Error!");          // Red error
```

**Transform Manipulation:**
```csharp
transform.position = new Vector3(5, 2, 0);  // Set position
transform.Rotate(0, 50, 0);                 // Rotate by degrees
transform.Translate(1, 0, 0);               // Move relative to orientation
transform.localScale = new Vector3(2, 2, 2); // Set scale
```

### Common Shortcuts

| Shortcut | Action |
|----------|--------|
| W | Move tool |
| E | Rotate tool |
| R | Scale tool |
| Q | Hand tool (pan view) |
| Space | Focus on selected object |
| F | Frame selected object in Scene view |
| Ctrl+D | Duplicate selected GameObject |
| Delete | Delete selected GameObject |

---

## Additional Resources

- **Official Unity Documentation:** https://docs.unity.com
- **Unity Learn:** Interactive tutorials and projects
- **Game Design Document Template:** Available in course materials

