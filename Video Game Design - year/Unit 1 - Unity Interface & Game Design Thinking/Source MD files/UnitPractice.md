# Unit 1 Practice Problems

Complete these 15 problems to reinforce Unit 1 concepts. Solutions included.

---

## Problem 1: MDA Analysis (Game Design)

**Analyze a game you know well using the MDA framework.**

- Name the game
- List 3 core Mechanics
- Describe what Dynamics emerge from those mechanics
- Explain what Aesthetics (emotional response) the game creates
- Propose one mechanic change and predict its effect on dynamics/aesthetics

### Solution Example (Minecraft)

**Game:** Minecraft

**Mechanics:**
1. Place and destroy blocks
2. Crafting system (recipe-based creation)
3. Survival mode: health, hunger, darkness

**Dynamics:**
- Exploration encourages curiosity (discovery)
- Resource scarcity creates planning necessity
- Night cycles force shelter-seeking behavior
- Crafting gates progression (early-game bottleneck)

**Aesthetics:**
- Empowering (players create freely)
- Explorative (world is yours to discover)
- Survival-driven (in hard mode especially)
- Relaxing (in creative/peaceful modes)

**Proposed Change:** If crafting was instant (no crafting table needed), mechanics would shift. Dynamic: instead of "plan expeditions to gather resources," it becomes "constant upgrading." Aesthetic: from exploratory to achievement-focused/goal-driven. Trade-off: less "downtime" for planning, more constant progression.

---

## Problem 2: Editor Navigation

**Task:** Without using shortcuts, describe the path to accomplish each:

1. Add a Box Collider to a cube GameObject
2. Create a new material and apply it to the cube
3. Hide an entire layer in the scene
4. Access the Console window
5. Save the scene

### Solution

1. **Add Box Collider:**
   - Select the cube in Hierarchy
   - In Inspector, click "Add Component"
   - Type "Box Collider"
   - Click the result

2. **Create and apply material:**
   - Right-click in Project window → Material
   - Name it (e.g., "RedMaterial")
   - In Inspector, click the white Albedo color square
   - Set to red
   - Drag the material onto the cube or into the Mesh Renderer's Material slot

3. **Hide a layer:**
   - Select an object assigned to that layer
   - Look at Inspector → Layer dropdown (shows current layer)
   - In Hierarchy, find the eye icon next to layer names
   - Click to toggle visibility

4. **Open Console:**
   - Menu → Window → General → Console
   - Or: Cmd/Ctrl+Shift+C

5. **Save scene:**
   - File → Save
   - Or: Cmd/Ctrl+S

---

## Problem 3: Transform Manipulation

**Create a scene with these specifications:**

1. A ground plane (cube scaled 10,1,10 at position 0,0,0)
2. Three towers: Each is a column of 3 stacked cubes. Towers at positions (−3, 0, 0), (0, 0, 0), (3, 0, 0)
3. A bridge connecting towers: A flat elongated cube from X=−3 to X=3 at Y=3

**Describe the transforms (position, rotation, scale) for each object.**

### Solution

**Ground:**
- Position: (0, 0, 0)
- Rotation: (0, 0, 0)
- Scale: (10, 1, 10)

**Tower 1 (leftmost):**
- Base cube: Pos (−3, 0.5, 0), Scale (1, 1, 1)
- Middle cube: Pos (−3, 1.5, 0), Scale (1, 1, 1)
- Top cube: Pos (−3, 2.5, 0), Scale (1, 1, 1)

**Tower 2 (center):**
- Base: Pos (0, 0.5, 0)
- Middle: Pos (0, 1.5, 0)
- Top: Pos (0, 2.5, 0)

**Tower 3 (right):**
- Base: Pos (3, 0.5, 0)
- Middle: Pos (3, 1.5, 0)
- Top: Pos (3, 2.5, 0)

**Bridge:**
- Position: (0, 3, 0)
- Scale: (6, 0.5, 1)

*Note: Individual cubes are 1×1×1. Stacking them requires offsetting Y by 1 each.*

---

## Problem 4: Parenting Hierarchy

**Design a "Robot" GameObject with a hierarchical structure.**

Sketch the Hierarchy tree and describe the world-space position and local-space position of each part.

### Solution

**Hierarchy:**
```
Robot_Parent (world pos 0,0,0)
  ├─ Body (local pos 0,0,0, scale 1,2,0.5)
  ├─ Head (local pos 0,1.5,0, scale 0.8,0.8,0.8)
  ├─ Arm_Left (local pos -1,0.5,0, scale 0.3,1,0.3)
  ├─ Arm_Right (local pos 1,0.5,0, scale 0.3,1,0.3)
  ├─ Leg_Left (local pos -0.3,-1,0, scale 0.4,1,0.4)
  └─ Leg_Right (local pos 0.3,-1,0, scale 0.4,1,0.4)
```

**Example (Head):**
- **Local Position:** (0, 1.5, 0) — relative to robot center
- **World Position:** (0, 1.5, 0) — if parent is at origin
- If parent (Robot_Parent) moves to (5, 0, 0), Head's world position becomes (5, 1.5, 0)

---

## Problem 5: Materials & Colors

**Create 5 materials matching these descriptions:**

1. Rough stone (gray, matte)
2. Shiny gold (yellow, reflective)
3. Dull wood (brown, slightly shiny)
4. Plastic (bright blue, smooth)
5. Rust (orange-brown, very rough)

For each, specify Albedo color (RGB or hex) and Metallic/Smoothness values.

### Solution

**1. Rough Stone:**
- Albedo: RGB(128, 128, 128) or #808080 (gray)
- Metallic: 0
- Smoothness: 0.15

**2. Shiny Gold:**
- Albedo: RGB(255, 215, 0) or #FFD700 (gold)
- Metallic: 1
- Smoothness: 0.9

**3. Dull Wood:**
- Albedo: RGB(139, 90, 43) or #8B5A2B (brown)
- Metallic: 0
- Smoothness: 0.35

**4. Plastic (Bright Blue):**
- Albedo: RGB(0, 100, 200) or #0064C8 (bright blue)
- Metallic: 0
- Smoothness: 0.6

**5. Rust:**
- Albedo: RGB(184, 92, 51) or #B85C33 (orange-brown)
- Metallic: 0.2 (slight metallic for aged effect)
- Smoothness: 0.1

---

## Problem 6: Lighting Setup

**Design a lighting scheme for an indoor room.**

Specify:
- Type of each light (Directional, Point, Spot)
- Position, intensity, color, range
- Overall mood you're creating

### Solution

**Scene: Cozy Living Room**

1. **Directional Light (Sun through window)**
   - Rotation: (45, 30, 0)
   - Intensity: 0.7
   - Color: Warm white (slight yellow tint)
   - Effect: Key light, creates shadows

2. **Point Light (Ceiling lamp)**
   - Position: (0, 3, 0)
   - Intensity: 1.2
   - Range: 20
   - Color: Warm white
   - Effect: Main room lighting

3. **Point Light (Table lamp)**
   - Position: (3, 1, -2)
   - Intensity: 0.8
   - Range: 10
   - Color: Warm white
   - Effect: Accent light, cozy warmth

**Ambient Light:** Slight warm tint (avoid pitch black shadows)

**Mood:** Warm, cozy, welcoming. Multiple warm lights create depth.

---

## Problem 7: Prefab Workflow

**Describe the complete workflow for creating a "Tree" prefab and using it 5 times in a scene.**

Include file paths, steps, and verification.

### Solution

1. **Create a tree GameObject:**
   - Right-click Hierarchy → 3D Object → Cylinder (trunk)
   - Scale to (0.5, 3, 0.5)
   - Create a Sphere (foliage)
   - Parent sphere to cylinder
   - Position sphere at (0, 2.5, 0), scale (2, 2, 2)
   - Apply green material to foliage

2. **Save as prefab:**
   - In Project, create folder "Prefabs" if not existing
   - Drag the tree GameObject from Hierarchy into Prefabs folder
   - A "Tree.prefab" file appears

3. **Use in scene:**
   - Delete the original tree from Hierarchy (it's only a template now)
   - Drag Tree.prefab into scene 5 times
   - Position each at different locations

4. **Verify:**
   - Select the prefab in Project → modify material color
   - All 5 instances in scene change color
   - Confirmation: The prefab system works!

---

## Problem 8: Script Attachment & Debug.Log

**Write and attach a simple script.**

1. Create a script that logs a message in Start()
2. Create a script that logs frame count in Update()
3. Attach both to a cube
4. Press Play and verify Console output

### Solution

**Script 1: Greeter.cs**
```csharp
using UnityEngine;

public class Greeter : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Game started! Cube is ready.");
    }
}
```

**Script 2: FrameLogger.cs**
```csharp
using UnityEngine;

public class FrameLogger : MonoBehaviour
{
    void Update()
    {
        Debug.Log("Frame: " + Time.frameCount);
    }
}
```

**Attachment:**
- Create a cube
- Select it
- In Inspector, Add Component → Greeter
- Add Component → FrameLogger
- Press Play
- Console shows: "Game started! Cube is ready." then many "Frame: #" messages

---

## Problem 9: Transform from Script

**Write a script that moves an object in a circle.**

The circle should have a radius of 3 units and complete one revolution per 10 seconds.

### Solution

```csharp
using UnityEngine;

public class CircularMotion : MonoBehaviour
{
    public float radius = 3f;
    public float period = 10f; // seconds per revolution
    
    void Update()
    {
        // Angle in radians (2π radians = 360°)
        float angle = (Time.time / period) * 2 * Mathf.PI;
        
        // Position on circle
        float x = Mathf.Cos(angle) * radius;
        float z = Mathf.Sin(angle) * radius;
        
        transform.position = new Vector3(x, 0, z);
    }
}
```

**Verification:**
- Attach to a sphere
- Press Play
- Sphere orbits in a circle around origin

---

## Problem 10: GetComponent & Rigidbody

**Write a script that:**
1. Finds the Rigidbody component on the same GameObject
2. Sets its velocity to move right at 5 units/second
3. Logs the velocity every second

### Solution

```csharp
using UnityEngine;

public class RigidbodyMover : MonoBehaviour
{
    private Rigidbody rb;
    private float logTimer = 0f;
    
    void Start()
    {
        rb = GetComponent<Rigidbody>();
        if(rb != null)
        {
            rb.velocity = Vector3.right * 5f;
        }
    }
    
    void Update()
    {
        logTimer += Time.deltaTime;
        if(logTimer >= 1f)
        {
            Debug.Log("Current velocity: " + rb.velocity);
            logTimer = 0f;
        }
    }
}
```

---

## Problem 11: Instantiation Loop

**Write a script that creates a 5×5 grid of cubes.**

Grid should be 5 units apart, centered at origin.

### Solution

```csharp
using UnityEngine;

public class CubeGridSpawner : MonoBehaviour
{
    public GameObject cubePrefab;
    public int gridSize = 5;
    public float spacing = 5f;
    
    void Start()
    {
        for(int x = 0; x < gridSize; x++)
        {
            for(int z = 0; z < gridSize; z++)
            {
                float posX = (x - gridSize / 2) * spacing;
                float posZ = (z - gridSize / 2) * spacing;
                
                Vector3 position = new Vector3(posX, 0, posZ);
                GameObject cube = Instantiate(cubePrefab, position, Quaternion.identity);
                cube.name = "Cube_" + x + "_" + z;
            }
        }
    }
}
```

---

## Problem 12: Play Mode vs Edit Mode

**Demonstrate the difference and explain consequences.**

1. Create a cube with position (0,0,0)
2. Press Play and move it to (5,0,0) using Gizmo
3. Press Stop
4. Where is the cube? Why?

### Solution

**Result:** Cube returns to (0,0,0)

**Why:** Play Mode is sandboxed. The scene is loaded from disk. Any changes during Play Mode (moving objects, changing values, instantiating) exist only in the live simulation. When you press Stop, Unity reverts to the last saved state (which has the cube at 0,0,0).

**Important:** This is intentional design. It prevents accidental saves of test data.

---

## Problem 13: Layer Organization

**Organize a complex scene into logical layers.**

Scene contains:
- 1 ground plane
- 3 buildings
- 10 trees
- 5 benches
- 3 lampposts
- 2 lights (directional + point)

Create appropriate layers and assign all objects.

### Solution

**Layers Created:**
1. Default
2. Environment (ground)
3. Buildings
4. Vegetation (trees)
5. Props (benches, lampposts)
6. Lighting

**Assignment:**
- Ground plane → Environment
- 3 buildings → Buildings
- 10 trees → Vegetation
- 5 benches → Props
- 3 lampposts → Props
- 2 lights → Lighting

**Usage:** Hide/show layers to focus on specific parts (e.g., hide Vegetation to see building layout).

---

## Problem 14: Mini-Scene Design

**Create a small scene (5-10 objects) representing a specific location.**

Examples: café table, bedroom corner, garden corner, office desk

Specify:
- Objects (names, positions, scales)
- Materials used
- Lighting scheme
- Parenting structure

### Solution Example (Café Table)

**Objects:**
- Table (Cube, scale 2,0.2,1, Pos 0,0,0, brown material)
  - Chair_1 (Cube, scale 0.4,1,0.4, Pos 1,0,0.3, brown material)
  - Chair_2 (Cube, scale 0.4,1,0.4, Pos -1,0,0.3, brown material)
  - Plate (Cylinder, scale 0.4,0.1,0.4, Pos 0,0.3,0, white material)
  - Cup (Cylinder, scale 0.2,0.3,0.2, Pos 0.5,0.3,-0.3, ceramic material)

**Materials:**
- Wood (brown, matte)
- Ceramic (off-white, slightly shiny)

**Lighting:**
- Directional Light (warm, simulating afternoon light)
- Point Light above table (warm white, Intensity 1.2)

**Hierarchy:**
```
Café_Table (empty parent)
  ├─ Table_Surface
  ├─ Chair_Left
  ├─ Chair_Right
  ├─ Plate
  └─ Cup
```

---

## Problem 15: Prefab Variants (Challenge)

**Create a base "Box" prefab, then design two variants.**

1. Create "Box.prefab" (cube, blue material)
2. Create "Box_Gold.prefab" (variant: same shape, gold material)
3. Create "Box_Large.prefab" (variant: same shape, 2× scale, red material)
4. Instantiate one of each in a scene
5. Modify the base Box prefab's mesh size slightly
6. Document what changes in each variant

### Solution

**Box.prefab (Base):**
- GameObject: Cube
- Scale: (1, 1, 1)
- Material: Blue Matte
- Rigidbody: enabled

**Box_Gold.prefab (Variant):**
- Inherits from Box.prefab
- Override: Material = Gold Shiny
- Inherits: Scale, Rigidbody, all else

**Box_Large.prefab (Variant):**
- Inherits from Box.prefab
- Override: Scale = (2, 2, 2), Material = Red Matte
- Inherits: Rigidbody, collision behavior

**Scene Verification:**
- Instantiate all three in scene
- Modify base Box.prefab's Rigidbody settings (e.g., increase drag)
- All three variants inherit the change
- Variants' material/scale overrides remain intact

**Why this matters:** Variants allow you to create families of similar objects without duplicating code/components. Changes to the base apply everywhere; overrides remain unique.

---

## How to Use These Solutions

1. **Attempt each problem without looking at solutions first**
2. **Compare your approach to the solution** — Is there a better way?
3. **Implement in Unity** — Actually do it in the editor to feel the concepts
4. **Iterate** — Modify the solution (different values, more objects, etc.)
5. **Ask questions** — If stuck, re-read the corresponding daily note

