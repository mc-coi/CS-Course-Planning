# Vocabulary & Quick Reference

## Key Terms

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

## Key Syntax

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

## Common Shortcuts

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

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Script doesn't attach to GameObject | Unity didn't recompile, or script has errors | Check the Console for errors; wait for compilation to finish |
| Changes in code don't appear in game | Not saving the file, or still editing Play mode | Save the file; don't edit while Play mode is active |
| GameObject moves but nothing happens | No camera or no renderer | Add a Camera to the scene; ensure the GameObject has a Renderer or a Mesh |
| Debug.Log doesn't print | Script not attached or not running | Attach script to a GameObject; check that the method is Start() or Update() |
| Parent-child relationships are wrong | Dragged wrong object in Hierarchy | Carefully select the parent first, then drag the child onto it |
| Material doesn't look right | Wrong shader or missing textures | Check the Inspector; use Standard shader for basic visuals |
| Time.deltaTime is 0 | Game is paused or framerate is very high | Time.deltaTime is never 0 in normal gameplay; check if Time.timeScale == 0 |
| Transform values jump around | Local vs. World space confusion | Check the space toggle in the Inspector (next to position values) |
