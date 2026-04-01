# Unit 1 Reference Guide

---

## Editor Keyboard Shortcuts (Mac/Windows)

### Core Tools

| Action | Mac | Windows | Use |
|--------|-----|---------|-----|
| Move Tool (Gizmo) | `W` | `W` | Position objects |
| Rotate Tool (Gizmo) | `E` | `E` | Rotate objects |
| Scale Tool (Gizmo) | `R` | `R` | Resize objects |
| Frame Selection | `F` | `F` | Center camera on selection |
| Duplicate | `Cmd+D` | `Ctrl+D` | Copy selected object |
| Delete | `Cmd+Backspace` | `Delete` | Remove object |

### General Editing

| Action | Mac | Windows | Use |
|--------|-----|---------|-----|
| Undo | `Cmd+Z` | `Ctrl+Z` | Undo last action |
| Redo | `Cmd+Shift+Z` | `Ctrl+Y` | Redo undone action |
| Copy | `Cmd+C` | `Ctrl+C` | Copy component/GameObject |
| Paste | `Cmd+V` | `Ctrl+V` | Paste |
| Select All | `Cmd+A` | `Ctrl+A` | Select all GameObjects |
| Find | `Cmd+F` | `Ctrl+F` | Search Hierarchy/Project |

### View Navigation

| Action | Method | Use |
|--------|--------|-----|
| Rotate Scene View | Middle mouse drag | Spin camera |
| Pan Scene View | Cmd+Middle drag | Move camera |
| Zoom | Scroll wheel | Zoom in/out |
| Focus on Selection | `F` | Center and frame |

### Gizmo Precision

| Action | Key | Use |
|--------|-----|-----|
| Snap to Grid (Move) | Hold `Cmd/Ctrl` while dragging | Align to 1-unit increments |
| Vertex Snap | Hold `Cmd/Ctrl+Shift` while dragging | Snap vertices to grid intersections |
| Increase Gizmo Size | `.` (period) | Larger handles |
| Decrease Gizmo Size | `,` (comma) | Smaller handles |

---

## Transform Component Cheat Sheet

### Position (in meters)

```
X = Left/Right (-left, +right)
Y = Up/Down (-down, +up)
Z = Forward/Back (-back, +forward)
```

### Rotation (in degrees)

```
X = Rotate around X axis (pitch/nod)
Y = Rotate around Y axis (yaw/spin)
Z = Rotate around Z axis (roll/tilt)

Common values:
  90° = 90-degree rotation
  -90° = -90-degree rotation
  0° = no rotation
```

### Scale (multipliers)

```
1.0 = normal size
2.0 = twice as large
0.5 = half size
-1.0 = flipped (avoid; causes rendering issues)
```

---

## Prefab Workflow Quick Reference

### Creating a Prefab

1. **Customize a GameObject** (position, scale, material, components)
2. **Drag from Hierarchy into Project folder**
3. **A new prefab file appears** — you now have a template
4. **Delete the instance from the scene** (optional; the prefab persists)

### Using Prefabs

- **Drag from Project into Scene** — Creates an instance
- **Duplicate (Cmd/Ctrl+D)** — Another instance appears
- **Modify the prefab** (in Project) — All instances update
- **Modify an instance** — Only that copy changes; prefab unchanged
- **Right-click instance → Prefab → Unlink** — Detach from prefab (becomes unique)

### Instantiating from Script

```csharp
public GameObject myPrefab;

void Start()
{
    // Create one instance
    Instantiate(myPrefab, new Vector3(5, 0, 0), Quaternion.identity);
    
    // Create 10 instances in a loop
    for(int i = 0; i < 10; i++)
    {
        Instantiate(myPrefab, new Vector3(i * 2, 0, 0), Quaternion.identity);
    }
}
```

---

## Common Editor Mistakes & Fixes

| Problem | Cause | Fix |
|---------|-------|-----|
| Object is black/invisible | No lighting or no Mesh Renderer | Add a Light or check the Renderer component |
| Objects overlap/flicker | Z-fighting (same position) | Slightly move one object or check Collider bounds |
| Can't select an object | It's behind another or hidden by layer | Use Hierarchy to select, or toggle layer visibility |
| Prefab changes don't affect instances | Instance was unpacked/unlinked | Re-link or recreate the prefab |
| Script doesn't attach | Filename doesn't match class name | Rename file to match (case-sensitive) |
| Scene looks dark | Camera far clipping plane too small | Adjust Camera → Far clip plane |
| Gizmo handles are too small | Zoom too far out | Press `F` to frame, or increase Gizmo size (`.`) |

---

## Quick Reference: Component Types

| Component | What It Does | Add Via |
|-----------|--------------|---------|
| **Transform** | Position, Rotation, Scale | Always present (can't remove) |
| **Mesh Filter** | Defines the 3D shape | Primitive (Cube, Sphere, etc.) |
| **Mesh Renderer** | Makes the shape visible | Primitive; needs a Material |
| **Material** | Color, texture, shine | Drag a Material onto renderer or Inspector |
| **Collider** | Physics boundary (Box, Sphere, Capsule, Mesh) | Add Component → search "Collider" |
| **Rigidbody** | Physics simulation (gravity, velocity) | Add Component → Rigidbody |
| **Light** | Illuminates scene (Directional, Point, Spot) | Right-click Hierarchy → Light |
| **Camera** | Player's viewpoint | Usually auto-created in new scenes |
| **Script** | Custom behavior (C# MonoBehaviour) | Create via Create → C# Script, then drag to object |

---

## Layer Organization Best Practices

### Common Layer Setup

```
Default          — Miscellaneous or unorganized objects
Environment      — Ground, walls, terrain
Props            — Decorative objects, furniture
Characters       — Player, NPCs, enemies
Effects          — Particle effects, visual feedback
UI               — UI elements (canvas, buttons, text)
Lights           — All lighting sources
```

### Usage Tips

- **Hide layers temporarily** while building to focus on one section
- **Set Camera culling mask** to render only specific layers
- **Use for physics filtering** (Rigidbody can ignore collisions with certain layers)
- **Organize, not restrict** — Layers don't prevent objects from interacting

---

## Gizmo Guide

### Move Gizmo (Press `W`)

- **Red arrow (X-axis)** — Drag to move left/right
- **Green arrow (Y-axis)** — Drag to move up/down
- **Blue arrow (Z-axis)** — Drag to move forward/backward
- **Center cube** — Drag to move freely in all directions
- **Colored planes** — Drag to move on that plane only

### Rotate Gizmo (Press `E`)

- **Red circle** — Rotate around X axis
- **Green circle** — Rotate around Y axis
- **Blue circle** — Rotate around Z axis
- **White circle** — Free rotation (less precise)

### Scale Gizmo (Press `R`)

- **Red cube on X** — Scale along X only
- **Green cube on Y** — Scale along Y only
- **Blue cube on Z** — Scale along Z only
- **Center cube** — Scale uniformly (all axes)

---

## Material Creation & Common Settings

### Standard Shader Properties

| Property | Min | Max | Common Values | Effect |
|----------|-----|-----|---------------|--------|
| **Albedo (Color)** | Black | White | Any RGB | Base color of surface |
| **Metallic** | 0 | 1 | 0 (matte), 0.5 (partial), 1 (full metal) | How reflective |
| **Smoothness** | 0 | 1 | 0.2 (rough), 0.5 (medium), 0.8 (shiny) | Surface smoothness |

### Quick Material Recipes

**Wood:**
- Albedo: RGB(139, 90, 43) brownish
- Metallic: 0
- Smoothness: 0.3

**Stone:**
- Albedo: RGB(128, 128, 128) gray
- Metallic: 0
- Smoothness: 0.2

**Gold:**
- Albedo: RGB(255, 215, 0) yellow
- Metallic: 1
- Smoothness: 0.8

**Plastic:**
- Albedo: Any color
- Metallic: 0
- Smoothness: 0.5

---

## Lighting Cheat Sheet

### Directional Light (Sun)

- **Purpose:** Overall scene lighting
- **Use:** 1 per scene
- **Key Properties:** Rotation (direction), Intensity, Color
- **Good defaults:** Intensity 1.0, Rotation (45°, 45°, 0°)

### Point Light (Bulb)

- **Purpose:** Local light from a point (lamp, fire, explosion)
- **Use:** Multiple for dynamic lighting
- **Key Properties:** Position, Range, Intensity, Color
- **Good defaults:** Intensity 1.0–1.5, Range 15–20

### Spotlight

- **Purpose:** Directional cone of light
- **Use:** Flashlights, stage lights, focused areas
- **Key Properties:** Position, Rotation, Range, Spot Angle, Intensity
- **Good defaults:** Angle 30–45°, Intensity 1.0

### Ambient Light

- **Purpose:** Fill shadows with flat lighting
- **Where to set:** Window → Rendering → Lighting Settings
- **Effect:** Makes dark areas visible
- **Good practice:** Usually a low-saturation color (gray, slight tint)

---

## Scene Saving & Organization

### File Structure Best Practice

```
Assets/
  ├─ Scenes/
  │   ├─ MainMenu.unity
  │   ├─ Level1.unity
  │   └─ Level2.unity
  ├─ Prefabs/
  │   ├─ Player.prefab
  │   ├─ Enemy.prefab
  │   └─ Collectible.prefab
  ├─ Materials/
  │   ├─ Red_Matte.mat
  │   ├─ Blue_Metallic.mat
  │   └─ Gold_Shiny.mat
  ├─ Scripts/
  │   ├─ PlayerController.cs
  │   └─ EnemyAI.cs
  └─ Models/
      └─ (3D models, if imported)
```

### Saving Scenes

- **First save:** File → Save As → choose location and name
- **Quick save:** Cmd/Ctrl+S (saves to current file)
- **Never save during Play Mode** — Changes will revert anyway; save in Edit Mode

---

## Debugging Tips

### Using the Console

- **Window → General → Console** to open
- **Errors (red):** Script problems (syntax, runtime)
- **Warnings (yellow):** Non-critical issues
- **Logs (white):** Debug.Log() output

### Debug.Log Examples

```csharp
Debug.Log("Simple message");
Debug.Log("Value: " + myVariable);
Debug.LogWarning("Warning message"); // Yellow
Debug.LogError("Error message"); // Red
```

---

## Play Mode Behavior

| Change | Persists? | Reason |
|--------|-----------|--------|
| Move/rotate object (Gizmo) | No | Play mode is sandboxed |
| Change public variable (Inspector) | No | Reverts to saved default |
| Instantiate objects (script) | No | Only live copies exist |
| Modify a Prefab (in Project) | Yes | Prefabs are assets (permanent) |
| Create a new scene | Yes | You explicitly saved it |
| Undo during Play | No | Undo only works in Edit Mode |

---

## Quick Command Reference

| Command | Effect |
|---------|--------|
| Play | Start testing (Alt+P or button) |
| Stop | End testing (Alt+P or button) |
| Pause | Freeze at current frame |
| Step | Advance one frame (while paused) |

