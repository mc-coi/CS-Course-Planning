# Day 3: Unity Editor Layout & Navigation

**Learning Target:** I can navigate the Unity editor, identify the major panels, and use keyboard shortcuts efficiently.

---

## Key Concepts

**Scene View** — 3D editor where you design and place GameObjects. **Where:** Top-left by default. **Shortcut:** Press `2` or `Cmd/Ctrl + 1`.

**Game View** — The camera's perspective; what players see when playing. **Where:** Overlaps Scene View; press Play to see it. **Shortcut:** Press `1` or click the Play button.

**Inspector** — Properties panel for the selected GameObject. Change position, rotation, scale, add/remove components. **Where:** Right side. **Keyboard:** Click any GameObject, then look right.

**Hierarchy** — Outline of all GameObjects in the scene, shown as a tree (parent-child relationships). **Where:** Left side. **Shortcut:** Cmd/Ctrl + Shift + H.

**Project Window** — File browser for assets (scripts, images, prefabs, scenes). **Where:** Bottom-left. **Shortcut:** Cmd/Ctrl + Tab.

**Console** — Debug messages and errors. **Where:** Bottom. **Shortcut:** Cmd/Ctrl + Shift + C.

---

## Editor Shortcuts (Mac/Windows)

| Action | Mac | Windows |
|--------|-----|---------|
| Frame selection | `F` | `F` |
| Maximize/minimize panel | `Cmd+M` | `Ctrl+Shift+M` |
| Duplicate GameObject | `Cmd+D` | `Ctrl+D` |
| Delete | `Cmd+Backspace` | `Delete` |
| Copy/Paste | `Cmd+C/V` | `Ctrl+C/V` |
| Undo/Redo | `Cmd+Z / Cmd+Shift+Z` | `Ctrl+Z / Ctrl+Y` |
| Find | `Cmd+F` | `Ctrl+F` |

---

## Unity Setup Steps

1. **Create a new 3D Scene:** File → New Scene → 3D (Built-in Render Pipeline)
2. **Name and save it:** File → Save As → type "TestScene" → Save
3. **Explore the default scene:** You should see a Camera and a Light already placed
4. **Right-click in the Hierarchy:** Select "3D Object → Cube"
5. **Look at the Inspector:** Select the Cube. You'll see Transform properties (Position, Rotation, Scale)
6. **Move the cube in the Scene View:** Click the cube, then drag the red/green/blue arrows (Gizmos) to move it
7. **Check the Console:** Window → General → Console. You should see no errors (yet)

---

## Guided Practice

1. **Create 5 cubes** in the Scene View, each with different positions (spread them out)
2. **In the Inspector, manually change positions:** Select one cube, type new X/Y/Z values in the Transform panel
3. **Duplicate a cube:** Select it, press Cmd/Ctrl+D, notice it appears with an offset
4. **Rename GameObjects:** Double-click names in Hierarchy (e.g., "Cube_Red", "Cube_Blue")
5. **Frame on selection:** Select a GameObject and press `F` — the Scene View zooms to it

---

## Practice Problems

**Beginner:** Create 3 cubes and position them in a line using the Inspector position values. Rotate one 45 degrees on the Y axis.

**Intermediate:** Create 5 cubes, name them "Tower_1" through "Tower_5", scale them progressively larger, and arrange them in a pyramid.

**Challenge:** Create a 3D scene with 10+ objects (mix cubes, spheres, capsules) that form a recognizable shape (castle, bridge, tower, etc.). Use the Scene View Gizmos, not just Inspector values.

<details>
<summary>💡 Hints</summary>
- Hold Shift while moving the Gizmo for slower, more precise movement
- Middle mouse button (or two-finger trackpad) rotates the Scene View
- Right-click in Hierarchy → 3D Object to see all primitive shapes
- Double-click an object's name in Hierarchy to rename it instantly
</details>

<details>
<summary>✅ Sample: Simple Pyramid</summary>

Create 5 cubes:
- Cube 1: Scale (1, 1, 1), Position (0, 0, 0) — base
- Cube 2: Scale (0.8, 0.8, 0.8), Position (0, 1, 0)
- Cube 3: Scale (0.6, 0.6, 0.6), Position (0, 2, 0)
- Cube 4: Scale (0.4, 0.4, 0.4), Position (0, 3, 0)
- Cube 5: Scale (0.2, 0.2, 0.2), Position (0, 4, 0) — tip

</details>
