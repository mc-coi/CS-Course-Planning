# Day 18: Unit 1 Assessment

**Learning Target:** Demonstrate mastery of Unity interface, GameObjects, components, materials, lighting, and basic scene design.

---

## Multiple Choice (10 questions, 1 point each)

**1.** Which panel in Unity shows all GameObjects in a scene hierarchically?
- A) Inspector
- B) Hierarchy
- C) Project Window
- D) Scene View

**2.** What does the Transform component store?
- A) Lighting information
- B) Physics properties
- C) Position, Rotation, and Scale
- D) Material colors

**3.** Which shortcut key toggles the Move Gizmo?
- A) `E`
- B) `R`
- C) `W`
- D) `F`

**4.** In Unity, a **Material** primarily defines:
- A) The shape of an object
- B) How a surface looks (color, shininess, reflectivity)
- C) Physics behavior
- D) Script behavior

**5.** What is a **Prefab**?
- A) A temporary GameObject
- B) A template/blueprint that can be reused multiple times
- C) A shader for rendering
- D) A lighting configuration

**6.** Which C# method runs once when a scene starts?
- A) Update()
- B) LateUpdate()
- C) Start()
- D) Awake()

**7.** What does `Debug.Log()` do?
- A) Saves your game
- B) Prints a message to the Console window
- C) Deletes an object
- D) Compiles the scene

**8.** Changes made during **Play Mode** (when testing):
- A) Save to the scene automatically
- B) Are permanent
- C) Are reverted when you press Stop
- D) Create prefabs

**9.** A **Component** is:
- A) A feature of a GameObject (e.g., Transform, Renderer, Collider)
- B) A scene
- C) A type of material
- D) A light type

**10.** To organize GameObjects visually in the scene, you can use:
- A) Layers (for grouping by function/visibility)
- B) Parenting (making one a child of another)
- C) Both A and B
- D) Neither; organization isn't important

---

## Short Answer (5 questions, 2 points each)

**11.** Explain the difference between **Local** and **World** space in the Transform component.

**12.** If you have a cube as a parent and another cube as a child, and you rotate the parent, what happens to the child cube? Why?

**13.** You want to display an error message in red text on the screen during gameplay. Which shader or component setup would be appropriate (not just the "Standard" shader)? Why?

**14.** Describe the workflow for creating and reusing a prefab (name the steps).

**15.** In Play Mode, you modify a public variable of a script attached to a cube. When you press Stop, the variable reverts to its original value. Explain why this happens and why it's intentional design.

---

## Coding Challenges (3 questions, 5 points each)

**16.** Write a C# script that:
   - Moves a GameObject up by 1 unit per second
   - Uses `transform.position` and `Time.deltaTime`
   - Logs the current Y position to the Console every frame

```csharp
// Your script here
```

**17.** Write a script that:
   - Rotates a GameObject 30 degrees per second around the Y axis
   - Uses `transform.Rotate()`
   - Includes a public variable to control the rotation speed

```csharp
// Your script here
```

**18.** Write a script that:
   - Takes a prefab as a public variable
   - Instantiates 5 copies of that prefab in a horizontal line (X positions: 0, 2, 4, 6, 8)
   - All at Y=1, Z=0
   - Names each instance "Clone_0", "Clone_1", etc.

```csharp
// Your script here
```

---

## Answer Key

### Multiple Choice
1. B | 2. C | 3. C | 4. B | 5. B | 6. C | 7. B | 8. C | 9. A | 10. C

### Short Answer

**11.** Local space = relative to the object's own axes and position (moves with the object). World space = relative to the global XYZ grid (fixed in the world). In local space, a child's position is relative to its parent. In world space, everything is relative to the origin (0,0,0).

**12.** The child rotates along with the parent. This is because the parent-child relationship is hierarchical; the child's local axes rotate when the parent rotates. The child maintains its local position relative to the parent, but its world position changes.

**13.** Use a material with an **Unlit Shader** (instead of Standard) so text is visible regardless of lighting. Standard Shaders react to lights; Unlit Shaders ignore lighting and render at full brightness.

**14.** 
   1. Design/customize a GameObject (position, scale, materials, components)
   2. Drag it from the Hierarchy into the Project folder
   3. A Prefab file is created
   4. Delete the original from the scene (or keep it)
   5. Drag the Prefab back into scenes to instantiate copies
   6. Modify the Prefab in the Project and all instances update

**15.** Play Mode is sandboxed. All changes during Play (variables, positions, instantiated objects) exist only in the live simulation. When you press Stop, Unity reverts the scene to its last saved Edit Mode state. This is intentional because it prevents accidental saves of test data; developers must explicitly change values in Edit Mode for them to persist.

### Coding Challenges

**16.**
```csharp
using UnityEngine;

public class MoveUp : MonoBehaviour
{
    public float speed = 1.0f;
    
    void Update()
    {
        transform.position = transform.position + Vector3.up * speed * Time.deltaTime;
        Debug.Log("Current Y position: " + transform.position.y);
    }
}
```

**17.**
```csharp
using UnityEngine;

public class Rotator : MonoBehaviour
{
    public float rotationSpeed = 30.0f;
    
    void Update()
    {
        transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
    }
}
```

**18.**
```csharp
using UnityEngine;

public class Spawner : MonoBehaviour
{
    public GameObject prefab;
    
    void Start()
    {
        for(int i = 0; i < 5; i++)
        {
            Vector3 position = new Vector3(i * 2, 1, 0);
            GameObject clone = Instantiate(prefab, position, Quaternion.identity);
            clone.name = "Clone_" + i;
        }
    }
}
```

---

## Grading

- Multiple Choice: 10 points
- Short Answer: 10 points
- Coding Challenges: 15 points
- **Total: 35 points**

**Passing threshold:** 70% (24.5 points)
