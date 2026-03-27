# Day 4: Hands-on Editor Workflow & Scene Building

**Learning Target:** I can efficiently build a 3D scene using the Scene View, manipulate objects with Gizmos, and save scenes properly.

---

## Key Concepts

**Gizmo** — Colored arrows/handles in the Scene View that let you move, rotate, and scale objects visually. **Red = X, Green = Y, Blue = Z**.

**Local vs World Space** — **Local space** moves relative to the object's own axes; **World space** moves relative to the global XYZ grid. Switch in the Scene View toolbar.

**Snapping** — Grid alignment. Useful for tile-based or structured designs. **Shortcut:** Hold `Cmd/Ctrl` while dragging to snap to grid.

**Parenting** — Making one GameObject a child of another in the Hierarchy. Children move/rotate with parents. **How:** Drag in Hierarchy or use Inspector's "Transform" panel.

**Prefab** — A reusable template of a GameObject (you'll explore deeply on Days 13-14). For now: think of it as a "saved blueprint."

---

## Gizmo Tools

| Tool | Shortcut | Use |
|------|----------|-----|
| Move (Position) | `W` | Drag red/green/blue arrows to move |
| Rotate | `E` | Drag colored circles to rotate |
| Scale | `R` | Drag handles to resize |
| Rect (2D) | `T` | For UI only |

---

## Unity Setup Steps

1. **Open the TestScene from yesterday** (File → Open Scene → TestScene)
2. **Switch to Move tool:** Press `W` or click the Move icon in the toolbar
3. **Create a new GameObject:** Right-click Hierarchy → 3D Object → Cube
4. **Switch to Rotate tool:** Press `E`. Notice the colored circles appear
5. **Switch to Local space:** In the Scene View toolbar (top-right), click the position button and select "Local"
6. **Create a parent object:** Right-click Hierarchy → Create Empty. Name it "SceneRoot"
7. **Drag other cubes under SceneRoot** in the Hierarchy to parent them

---

## Guided Practice

1. **Create a grid of 9 cubes** (3x3 arrangement). Use snapping (hold Cmd/Ctrl) for alignment
2. **Create a "Pillar" parent object** and assign 3 cubes as children
3. **Move the Pillar:** Watch how child cubes follow (because they're parented)
4. **Rotate the entire scene 45 degrees:** Create a SceneRoot, parent everything under it, rotate SceneRoot
5. **Name every object meaningfully:** "Ground_Center", "Pillar_A", "Light_Key", etc.

---

## Practice Problems

**Beginner:** Build a 3x3 grid of cubes. All cubes should touch (no gaps). Save the scene as "Grid_Practice".

**Intermediate:** Create a structure with parent-child relationships: a "Building" parent with "Wall_North", "Wall_South", "Roof" children. Rotate the entire Building and verify all parts move together.

**Challenge:** Design a small 3D environment (playground, garden, shrine, etc.) using 20+ objects. Use at least 3 parent-child relationships. Save as "Environment_Design".

<details>
<summary>💡 Hints</summary>
- Hold Cmd/Ctrl while moving to snap to a 1-unit grid
- Middle mouse drag rotates the Scene View; scroll wheel zooms
- Press `F` to frame any selected GameObject
- Parents inherit children's transformations; rotating a parent rotates all children in world space
- Saving early and often prevents heartbreak!
</details>

<details>
<summary>✅ Sample: Simple Structure</summary>

Hierarchy:
- SceneRoot (empty)
  - Building (cube, scaled 5, 5, 5)
    - Wall_North (cube, positioned at Z+2.5)
    - Wall_South (cube, positioned at Z-2.5)
    - Roof (cube, positioned at Y+3, scaled to flat plane)

All children are positioned *relative to parent*, making the whole structure easy to move or rotate.

</details>
