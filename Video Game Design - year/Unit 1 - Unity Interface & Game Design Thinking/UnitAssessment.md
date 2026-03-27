# Unit 1 Assessment

**Name:** ________________  
**Date:** ________________  
**Total Points:** 50

---

## Part A: Multiple Choice (10 questions, 1 point each)

**1.** Which panel displays all GameObjects in a scene in a tree structure?
- A) Inspector
- B) Project Window
- C) Hierarchy
- D) Scene View

**2.** What does the Transform component control?
- A) Lighting and shadows
- B) Physics simulation
- C) Position, Rotation, and Scale
- D) Material appearance

**3.** Which keyboard shortcut activates the Move Gizmo?
- A) `E`
- B) `W`
- C) `R`
- D) `F`

**4.** A Material in Unity primarily defines:
- A) The 3D geometry (shape) of an object
- B) How a surface appears (color, reflectivity, texture)
- C) Physics behavior and collisions
- D) Script behavior

**5.** What is a Prefab?
- A) A unique GameObject in a scene
- B) A reusable template or blueprint for GameObjects
- C) A type of shader
- D) A lighting configuration

**6.** Which C# method is called once when a scene first loads?
- A) Update()
- B) Start()
- C) LateUpdate()
- D) OnEnable()

**7.** What does `Debug.Log()` do?
- A) Saves changes to the scene
- B) Prints a message to the Console window
- C) Deletes a GameObject
- D) Compiles the project

**8.** In Play Mode, changes you make (moving objects, modifying values):
- A) Save automatically to the scene
- B) Persist permanently
- C) Are reverted when you press Stop
- D) Create new prefabs

**9.** A Component is best described as:
- A) A type of GameObject
- B) A module that adds functionality to a GameObject (e.g., Collider, Renderer, Script)
- C) A scene file
- D) A material property

**10.** Which of the following is NOT a built-in light type in Unity?
- A) Directional Light
- B) Point Light
- C) Spotlight
- D) Laser Light

---

## Part B: Short Answer (5 questions, 3 points each)

**11.** Explain the difference between **Local Space** and **World Space** in the Transform component. How does this relate to parenting?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**12.** Describe what happens when you:
1. Create a cube in a scene
2. Drag it from the Hierarchy into the Project folder (creating a prefab)
3. Delete the cube from the scene
4. Drag the prefab back into the scene multiple times
5. Modify the prefab's material color

What happens to the instances in the scene? Why?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**13.** You write a script that moves an object forward using `transform.position += Vector3.forward * speed * Time.deltaTime`. Why is `Time.deltaTime` important here? What would happen if you didn't use it?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**14.** Explain the MDA framework (Mechanics, Dynamics, Aesthetics) in 2-3 sentences. Give an example from a game you know.

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**15.** What is the purpose of layers in the Unity editor? Give two specific use cases.

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

---

## Part C: Coding Challenges (3 questions, 7 points each)

**16. Transform Script (7 points)**

Write a C# script that rotates an object around the Y-axis. The script should:
- Have a public variable for rotation speed (degrees per second)
- Use `transform.Rotate()` to apply the rotation
- Be correct syntax and logic

```csharp
using UnityEngine;

public class YAxisRotator : MonoBehaviour
{
    // Your code here
    
    void Update()
    {
        // Your code here
    }
}
```

**17. Instantiation Script (7 points)**

Write a C# script that:
- Takes a prefab as a public variable
- In Start(), creates 8 instances of that prefab
- Positions them in a circle (radius 3 units) around the origin
- Names each instance "Prefab_0", "Prefab_1", etc.

Hint: Use `Mathf.Cos()` and `Mathf.Sin()` with angles around a circle.

```csharp
using UnityEngine;

public class CircleSpawner : MonoBehaviour
{
    public GameObject prefabToSpawn;
    
    void Start()
    {
        // Your code here
    }
}
```

**18. Multi-Component Scene (7 points)**

Describe the steps to create this scene:
- A parent GameObject named "Environment"
- Three child GameObjects: "Ground", "Wall", "Decoration"
- Each child should have a unique material (colors)
- The entire scene should be lit by a Directional Light

Write the step-by-step workflow (not code, just describe actions in the editor).

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

---

## Answer Key

### Part A: Multiple Choice (1 point each)

| Q | Answer | Q | Answer |
|---|--------|---|--------|
| 1 | C | 6 | B |
| 2 | C | 7 | B |
| 3 | B | 8 | C |
| 4 | B | 9 | B |
| 5 | B | 10 | D |

---

### Part B: Short Answer (3 points each)

**11.** **Local Space** is relative to an object's own axes and position; it moves/rotates with the object. **World Space** is relative to the global origin (0,0,0) and never changes. When a GameObject is a child, its local position is an offset from its parent's position. Moving the parent automatically moves the child because the parent's world position affects the child's world position. (1 point: understanding of local vs world; 1 point: relationship to parenting; 1 point: clear explanation)

**12.** All instances in the scene inherit the prefab's properties. When you modify the prefab's material color (in the Project folder), all instances update to reflect the change. This is because instances are linked to the prefab; they "pull" their properties from it. If you modify an individual instance (without modifying the prefab), only that copy changes. (1 point: instances inherit; 1 point: modification propagates; 1 point: explanation of linking)

**13.** `Time.deltaTime` is the time elapsed since the last frame (in seconds). It makes movement **frame-rate independent**. Without it, movement would be frame-dependent: faster machines (higher FPS) would move objects faster, creating inconsistent gameplay. With `Time.deltaTime`, the same physical distance is covered regardless of frame rate. (1 point: definition of deltaTime; 1 point: frame-rate independence; 1 point: consequence without it)

**14.** **Mechanics** are the rules/systems (what players can do). **Dynamics** are what happens when those mechanics interact (how they feel in practice). **Aesthetics** are the emotional response (the mood/experience). *Example:* In Tetris, the mechanic is "rotate falling pieces." The dynamic is "pressure to decide quickly." The aesthetic is "excitement and satisfaction." (1 point: each of M, D, A clearly explained; 1 point: game example; 1 point: connections between them)

**15.** **Purpose:** Organize GameObjects by function/visibility, control rendering, filter physics interactions. **Use cases:** (1) Hide decoration layer while building core level structure; (2) Set camera culling mask to render only UI layer on top of game layer. (1 point: purpose; 1 point: each use case)

---

### Part C: Coding Challenges (7 points each)

**16. YAxisRotator Script**

```csharp
using UnityEngine;

public class YAxisRotator : MonoBehaviour
{
    public float rotationSpeed = 45f; // degrees per second
    
    void Update()
    {
        transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
    }
}
```

**Grading:**
- 2 points: Correct class structure and inheritance
- 2 points: Public variable declared
- 2 points: Correct use of `transform.Rotate()` with Y-axis
- 1 point: Uses `Time.deltaTime`

**17. CircleSpawner Script**

```csharp
using UnityEngine;

public class CircleSpawner : MonoBehaviour
{
    public GameObject prefabToSpawn;
    public float radius = 3f;
    
    void Start()
    {
        for(int i = 0; i < 8; i++)
        {
            float angle = (i / 8f) * 2 * Mathf.PI;
            float x = Mathf.Cos(angle) * radius;
            float z = Mathf.Sin(angle) * radius;
            Vector3 position = new Vector3(x, 0, z);
            
            GameObject instance = Instantiate(prefabToSpawn, position, Quaternion.identity);
            instance.name = "Prefab_" + i;
        }
    }
}
```

**Grading:**
- 1 point: Correct loop structure (8 iterations)
- 2 points: Correct angle calculation for circle
- 2 points: Correct X, Z positions using Cos/Sin
- 1 point: Correct Instantiate syntax
- 1 point: Correct naming

**18. Multi-Component Scene Workflow**

Acceptable answer should include:

1. Right-click Hierarchy → Create Empty → name "Environment"
2. Right-click Environment → Create Empty → name "Ground"
3. Create a Cube, name "Ground_Mesh", parent to Ground
4. Repeat steps 2-3 for "Wall" and "Decoration"
5. Create 3 materials with different colors in Project/Materials folder
6. Apply each material to the corresponding child (Ground_Mesh, Wall_Mesh, Decoration_Mesh)
7. In Hierarchy, right-click → Light → Directional Light
8. Adjust light rotation/intensity for good visibility

**Grading:**
- 1 point: Create parent Environment
- 1 point: Create 3 children (Ground, Wall, Decoration)
- 2 points: Add GameObjects and materials to each
- 2 points: Apply unique materials to each
- 1 point: Add Directional Light and adjust

---

## Scoring Rubric

| Section | Points | Criteria |
|---------|--------|----------|
| Part A (MC) | 10 | 1 point per correct answer |
| Part B (SA) | 15 | 3 points per question; deduct for incomplete/incorrect explanations |
| Part C (Code) | 21 | 7 points per challenge; see grading details above |
| **Total** | **50** | Passing: 35+ (70%) |

---

## Remediation & Next Steps

**If score < 35 (70%):**
- Review daily notes for weak areas (game design, editor navigation, scripting)
- Redo practice problems in UnitPractice.md
- Meet with instructor for targeted support

**If score 35-42 (70-84%):**
- Strong understanding; minor gaps
- Focus on weakest section (A, B, or C) before Unit 2

**If score > 42 (84%+):**
- Mastery achieved; ready for Unit 2 (C# Scripting Fundamentals)
- Consider challenge problems in Unit 2 for advanced exploration

