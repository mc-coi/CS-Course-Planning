# Day 11: Scene View Workflow & Gizmos Mastery

**Learning Target:** I can navigate the Scene View efficiently, use Gizmos for alignment, and build scenes quickly.

---

## Key Concepts

**Gizmo** — Visual tool for moving, rotating, scaling in the Scene View. **Modes:** Move (W), Rotate (E), Scale (R).

**Pivot vs Center** — **Pivot:** rotation/scale around object's origin. **Center:** around average of all vertices. Toggle in Scene View toolbar.

**Local vs World** — **Local:** axes aligned to object's rotation. **World:** axes aligned to global grid. Toggle in Scene View toolbar.

**Vertex Snapping** — Hold `Cmd/Ctrl+Shift` while dragging to snap vertices to grid intersections (useful for precise alignment).

**Focus shortcut** — Press `F` to frame selection (center camera on selected object).

---

## Scene View Shortcuts

| Action | Shortcut |
|--------|----------|
| Move (toggle to Move Gizmo) | `W` |
| Rotate (toggle to Rotate Gizmo) | `E` |
| Scale (toggle to Scale Gizmo) | `R` |
| Frame selection | `F` |
| Duplicate | `Cmd/Ctrl+D` |
| Increase gizmo size | `.` (period) |
| Decrease gizmo size | `,` (comma) |
| Toggle wireframe | `Z` (some editors) |

---

## Unity Setup Steps

1. **Create a 3x3 grid of cubes** at positions:
   - (0,0,0), (1,0,0), (2,0,0)
   - (0,0,1), (1,0,1), (2,0,1)
   - (0,0,2), (1,0,2), (2,0,2)
2. **Use vertex snapping:** Press `W`, hold `Cmd/Ctrl+Shift`, drag cubes to snap edges together
3. **Toggle Local/World space** (top-right of Scene View) and notice the Gizmo orientation changes
4. **Select the Move Gizmo** (press `W`) and drag a cube only on the X axis (red arrow)

---

## Guided Practice

1. **Build a wall:** 5 cubes in a horizontal line, snapped together (no gaps)
2. **Build a second wall perpendicular** using vertex snapping for perfect corners
3. **Create a roof:** Position and scale a flat cube above both walls
4. **Select all (Cmd/Ctrl+A) and rotate 45 degrees** — use the Rotate Gizmo
5. **Frame on the entire structure** (press `F`)

---

## Practice Problems

**Beginner:** Build a 3x3x3 cube grid with no gaps. All cubes should touch their neighbors.

**Intermediate:** Design a small building: 4 walls (cubes), a floor, and a roof. Use vertex snapping to align everything perfectly.

**Challenge:** Create a complex structure (staircase, bridge, tower) with 20+ precisely aligned objects. All edges should line up (demonstrate alignment with screenshots).

<details>
<summary>💡 Hints</summary>
- Vertex snapping (Cmd/Ctrl+Shift + drag) is your friend for precise grid-based designs
- After snapping, you might see z-fighting (flickering due to overlapping faces); scale slightly to prevent
- Press `F` frequently to reset the camera to your current selection
- Use layers (right-side dropdown) to group objects organizationally
- Color-coding materials helps visually organize complex scenes
</details>

<details>
<summary>✅ Sample: Simple Room</summary>

Hierarchy:
- Wall_North (cube, scale 5,2,0.2, pos 0,1,2)
- Wall_South (cube, scale 5,2,0.2, pos 0,1,-2)
- Wall_East (cube, scale 0.2,2,4.2, pos 2.5,1,0)
- Wall_West (cube, scale 0.2,2,4.2, pos -2.5,1,0)
- Floor (cube, scale 5,0.2,4, pos 0,0,0)
- Roof (cube, scale 5,0.2,4, pos 0,2.2,0)

All walls and floor snap perfectly with no gaps.

</details>
