# Unit 1 Answer Key: Unity Interface & Game Design Thinking

Comprehensive answer key with solutions for all 15 practice problems.

---

## Problem 1: MDA Analysis (Game Design)

### Solution

**Example Game: Minecraft**

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

### What Success Looks Like
Student provides a clear MDA breakdown for any game they know well, with specific mechanics, emergent dynamics, and emotional responses properly identified. The proposed mechanic change shows understanding of how mechanics drive player experience.

### Common Mistakes
- Confusing mechanics with dynamics (dynamics emerge from mechanics, not stated directly)
- Vague aesthetic descriptions ("fun" without specifics)

---

## Problem 2: Editor Navigation

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
   - In Hierarchy, find the eye icon next to layer names
   - Click to toggle visibility

4. **Open Console:**
   - Menu → Window → General → Console
   - Or: Cmd/Ctrl+Shift+C

5. **Save scene:**
   - File → Save
   - Or: Cmd/Ctrl+S

### What Success Looks Like
Student navigates the Unity interface fluently without tooltips or searching for buttons. All five tasks completed within 5 minutes without getting lost. Console opens immediately showing previous frames' logs.

### Common Mistakes
- Looking for buttons in wrong panels (e.g., looking for material creation in the Hierarchy)
- Forgetting to set the layer before trying to toggle its visibility

---

## Problem 3: Transform Manipulation

### Solution

**Ground:**
- Position: (0, 0, 0)
- Rotation: (0, 0, 0)
- Scale: (10, 1, 10)

**Tower 1 (left):**
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
- Rotation: (0, 0, 0)

### What Success Looks Like
Scene displays a clearly visible ground plane with three tall towers and a bridge connecting them. All objects properly positioned using transforms. Scene is symmetrical and organized.

### Common Mistakes
- Forgetting Y offset when stacking cubes (they overlap if all positioned at 0,0,0)
- Bridge scale is only 6 wide, not 7 (exact distance between towers at ±3)

---

## Problem 4: Parenting Hierarchy

### Solution

**Hierarchy Structure:**
```
Robot_Parent (world pos 0,0,0)
  ├─ Body (local pos 0,0,0, scale 1,2,0.5)
  ├─ Head (local pos 0,1.5,0, scale 0.8,0.8,0.8)
  ├─ Arm_Left (local pos -1,0.5,0, scale 0.3,1,0.3)
  ├─ Arm_Right (local pos 1,0.5,0, scale 0.3,1,0.3)
  ├─ Leg_Left (local pos -0.3,-1,0, scale 0.4,1,0.4)
  └─ Leg_Right (local pos 0.3,-1,0, scale 0.4,1,0.4)
```

**Head Example:**
- **Local Position:** (0, 1.5, 0) — relative to robot center
- **World Position:** (0, 1.5, 0) — if parent is at origin
- If parent moves to (5, 0, 0), Head's world position becomes (5, 1.5, 0)

### What Success Looks Like
Scene shows a recognizable robot figure with all parts properly positioned relative to a parent. Moving the parent moves the entire robot. Child positions make sense relative to parent.

### Common Mistakes
- Forgetting the difference between local and world position
- Body scale being 1,1,1 when it should be 1,2,0.5 for a proportionate torso

---

## Problem 5: Materials & Colors

### Solution

**1. Rough Stone:**
- Albedo: RGB(128, 128, 128) or #808080 (gray)
- Metallic: 0
- Smoothness: 0.15

**2. Shiny Gold:**
- Albedo: RGB(255, 215, 0) or #FFD700
- Metallic: 1
- Smoothness: 0.9

**3. Dull Wood:**
- Albedo: RGB(139, 90, 43) or #8B5A2B (brown)
- Metallic: 0
- Smoothness: 0.35

**4. Plastic (Bright Blue):**
- Albedo: RGB(0, 100, 200) or #0064C8
- Metallic: 0
- Smoothness: 0.6

**5. Rust:**
- Albedo: RGB(184, 92, 51) or #B85C33
- Metallic: 0.2
- Smoothness: 0.1

### What Success Looks Like
Five distinct materials in scene, each visually representing their intended surface. Gold is reflective, stone is matte, wood looks woody, plastic is shiny but not metallic, rust looks aged.

### Common Mistakes
- Metallic values too high on non-metallic materials
- Smoothness and roughness inverted (remembering that high smoothness = shiny)

---

## Problem 6: Lighting Setup

### Solution

**Scene: Cozy Living Room**

1. **Directional Light (Sun through window)**
   - Rotation: (45, 30, 0)
   - Intensity: 0.7
   - Color: Warm white (RGB 255, 240, 200)
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

**Ambient Light:** Slight warm tint (RGB 200, 190, 180) to avoid pitch black shadows

**Mood:** Warm, cozy, welcoming. Multiple warm lights create depth without harsh shadows.

### What Success Looks Like
Room is well-lit with distinct light sources visible. Shadows are soft, not too dark. Overall feeling is warm and inviting, not cold or clinical.

### Common Mistakes
- Using cold white color temperature instead of warm
- Ambient light too bright (washes out shadows)
- Only one light source (no depth)

---

## Problem 7: Prefab Workflow

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
   - A "Tree.prefab" file appears in Project

3. **Use in scene:**
   - Delete the original tree from Hierarchy
   - Drag Tree.prefab into scene 5 times
   - Position each at different locations

4. **Verify:**
   - Select the prefab in Project → modify material color
   - All 5 instances in scene change color
   - Confirmation: The prefab system works!

### What Success Looks Like
5 identical tree instances scattered around scene. Modifying the prefab causes all instances to update. Instances can have unique positions while maintaining linked prefab structure.

### Common Mistakes
- Not deleting the original before creating prefab (creating confusion about which is the template)
- Trying to edit instances individually instead of the prefab

---

## Problem 8: Script Attachment & Debug.Log

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

### What Success Looks Like
Console fills with output immediately on Play. First message appears once. Frame numbers increment continuously. Console remains clean and readable.

### Common Mistakes
- Forgetting `using UnityEngine;` directive
- FrameLogger logging every frame causing performance issues (though minor)
- Mistyping Debug.Log as Debug.log (case-sensitive)

---

## Problem 9: Transform from Script

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

### What Success Looks Like
Sphere orbits smoothly in a perfect circle around the origin. One complete orbit takes exactly 10 seconds. Circle has radius of 3 units.

### Common Mistakes
- Using degrees instead of radians (Mathf.PI needed)
- Period calculation wrong (Time.time / period should give normalized 0-1 value)
- Using only x and y instead of x and z (z creates proper 3D orbit)

---

## Problem 10: GetComponent & Rigidbody

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

### What Success Looks Like
Cube moves continuously to the right at 5 units/second. Console shows velocity approximately (5, 0, 0) every second.

### Common Mistakes
- Not checking if rb is null before setting velocity
- Logging every frame instead of every second (performance issue)
- Setting velocity in Update instead of modifying it (better to use Rigidbody.velocity)

---

## Problem 11: Instantiation Loop

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

### What Success Looks Like
25 cubes (5x5 grid) spawn in scene, evenly spaced 5 units apart, centered around origin. Each cube is named "Cube_X_Z" for identification.

### Common Mistakes
- Forgetting to center the grid (subtract gridSize/2 from position)
- Loop indexing off-by-one errors
- Not assigning the cubePrefab in Inspector

---

## Problem 12: Play Mode vs Edit Mode

### Solution

**Result:** Cube returns to (0,0,0)

**Why:** Play Mode is sandboxed. The scene is loaded from disk. Any changes during Play Mode (moving objects, changing values, instantiating) exist only in the live simulation. When you press Stop, Unity reverts to the last saved state (which has the cube at 0,0,0).

**Important:** This is intentional design. It prevents accidental saves of test data. Use Play Mode to test without committing changes to the scene file.

### What Success Looks Like
Student understands that Play Mode is temporary and non-destructive. They don't expect changes to persist after pressing Stop. They use Play Mode confidently for testing.

### Common Mistakes
- Expecting changes to persist (trying to save Play Mode changes)
- Not realizing this is a feature, not a bug

---

## Problem 13: Layer Organization

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

### What Success Looks Like
Scene organized with objects on appropriate layers. Toggling layer visibility works smoothly. Scene hierarchy is clear and organized by type.

### Common Mistakes
- Creating too many layers (bloats the system)
- Assigning similar objects to different layers inconsistently

---

## Problem 14: Mini-Scene Design

### Solution Example (Café Table)

**Objects:**
- Table (Cube, scale 2,0.2,1, Pos 0,0,0, brown material)
  - Chair_1 (Cube, scale 0.4,1,0.4, Pos 1,0,0.3, brown material)
  - Chair_2 (Cube, scale 0.4,1,0.4, Pos -1,0,0.3, brown material)
  - Plate (Cylinder, scale 0.4,0.1,0.4, Pos 0,0.3,0, white material)
  - Cup (Cylinder, scale 0.2,0.3,0.2, Pos 0.5,0.3,-0.3, ceramic material)

**Materials:**
- Wood (brown #8B5A2B, matte, roughness 0.6)
- Ceramic (off-white #F5F1E8, slightly shiny, smoothness 0.4)

**Lighting:**
- Directional Light (warm, simulating afternoon light, intensity 0.6)
- Point Light above table (warm white, Intensity 1.2, Range 15)

**Hierarchy:**
```
Café_Table (empty parent)
  ├─ Table_Surface
  ├─ Chair_Left
  ├─ Chair_Right
  ├─ Plate
  └─ Cup
```

### What Success Looks Like
Café scene is recognizable with functional table and chairs. Scale and proportions are reasonable. Lighting creates a pleasant atmosphere. Hierarchy is organized logically.

### Common Mistakes
- Objects too small/large to recognize
- No parent organization (flat hierarchy)
- Lighting too harsh or non-existent

---

## Problem 15: Prefab Variants (Challenge)

### Solution

**Box.prefab (Base):**
- GameObject: Cube
- Scale: (1, 1, 1)
- Material: Blue Matte (RGB 0, 0, 255)
- Rigidbody: enabled, mass 1

**Box_Gold.prefab (Variant):**
- Inherits from Box.prefab
- Override: Material = Gold Shiny (RGB 255, 215, 0, metallic 1, smoothness 0.9)
- Inherits: Scale, Rigidbody, all else

**Box_Large.prefab (Variant):**
- Inherits from Box.prefab
- Override: Scale = (2, 2, 2), Material = Red Matte (RGB 255, 0, 0)
- Inherits: Rigidbody, collision behavior

**Scene Verification:**
- Instantiate all three in scene
- Modify base Box.prefab's Rigidbody mass to 2
- All three variants inherit the change
- Variants' material/scale overrides remain intact

### What Success Looks Like
Three variants exist and work independently. Changes to base prefab propagate to all variants. Variant overrides take precedence over base settings. Demonstrates understanding of prefab inheritance.

### Common Mistakes
- Creating copies instead of variants (not linked)
- Not understanding that variants inherit base changes
- Overriding too many properties (defeats purpose of variants)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | MDA Framework | Beginner |
| 2 | Editor Navigation | Beginner |
| 3 | Transform Manipulation | Beginner |
| 4 | Parenting & Hierarchy | Intermediate |
| 5 | Materials & PBR | Intermediate |
| 6 | Lighting Design | Intermediate |
| 7 | Prefab Workflow | Intermediate |
| 8 | Script Basics | Beginner |
| 9 | Math & Transform | Intermediate |
| 10 | GetComponent | Beginner |
| 11 | Loops & Instantiation | Intermediate |
| 12 | Play Mode Concept | Beginner |
| 13 | Layer Organization | Intermediate |
| 14 | Scene Design | Intermediate |
| 15 | Prefab Variants | Advanced |
