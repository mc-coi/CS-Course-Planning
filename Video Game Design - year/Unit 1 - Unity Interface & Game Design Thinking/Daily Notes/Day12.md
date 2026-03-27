# Day 12: Scene View Workflow (Continued)

**Learning Target:** I can organize complex scenes, use layers for visibility control, and debug scene layout problems.

---

## Key Concepts

**Layers** — Groups that control rendering, collisions, and visibility. You can hide entire layers to focus on part of your scene.

**Z-fighting** — Visual glitch when two surfaces overlap (flicker). Caused by vertices at identical positions.

**Culling** — Hiding objects outside the camera view to improve performance. **Occlusion culling:** hide objects behind walls.

**Inspector Lock** — Lock the Inspector to one object while you select others (useful for comparing properties).

---

## Layer System

| Feature | Use |
|---------|-----|
| Create layers | Right-click object → Layer → New Layer |
| Set object layer | Inspector → Layer dropdown |
| Hide/show layer | Eye icon in Hierarchy (select multiple with Cmd/Ctrl) |
| Render specific layers | Camera → Culling Mask |
| Physics layers | Rigidbody → Layer |

---

## Unity Setup Steps

1. **Create 3 new layers:** "Walls", "Props", "Effects"
2. **Create 3 cubes:** Name them Wall1, Prop1, Effect1
3. **Assign Wall1 to "Walls" layer** (Inspector → Layer → Walls)
4. **Assign Prop1 to "Props" layer**
5. **Assign Effect1 to "Effects" layer**
6. **Click the eye icon next to "Effects" layer** — Effect1 disappears
7. **Drag more objects into each layer group** to organize

---

## Guided Practice

1. **Build a scene with 20+ objects**
2. **Organize into layers:** "Environment" (ground, walls), "Decorations" (plants, stones), "Lights" (all Light GameObjects)
3. **Hide the Decorations layer** and verify you can see the core structure
4. **Hide the Lights layer** and see how darkness affects visibility
5. **Show everything again**

---

## Practice Problems

**Beginner:** Create a scene with 10+ objects. Organize them into 3 layers. Show/hide each layer to confirm it works.

**Intermediate:** Design a building interior with multiple rooms. Use layers to hide walls so you can see inside, or hide furniture to see the floor plan.

**Challenge:** Build a complex scene with 30+ objects across 5+ layers. Demonstrate that you can quickly isolate and debug specific parts by toggling layer visibility.

<details>
<summary>💡 Hints</summary>
- Layers are NOT the same as folders in Hierarchy (though you can use empty GameObjects as folder-like containers)
- You can set up the Camera's Culling Mask to render only specific layers (advanced)
- Layer-based hiding is non-destructive: objects are still there, just invisible
- Use layers to organize by function: Walls, Props, UI, Lighting, etc.
- Lock the Inspector (small lock icon top-right) to keep one object's properties visible while selecting others
</details>

<details>
<summary>✅ Sample: Multi-Layer Scene</summary>

Layers created:
- Default (everything starts here)
- Walls
- Decorations
- Effects

Scene structure:
- Ground (Walls layer)
- Wall_North (Walls layer)
- Wall_South (Walls layer)
- Tree (Decorations layer)
- Rock (Decorations layer)
- Light_Main (Effects layer)
- Light_Accent (Effects layer)

Toggling "Decorations" layer hides trees and rocks. Toggling "Effects" dims the scene.

</details>
