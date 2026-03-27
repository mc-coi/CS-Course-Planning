# Day 5: GameObjects and Components (Part 1)

**Learning Target:** I can create GameObjects, understand the component-based architecture, and add/remove components in the Inspector.

---

## Key Concepts

**GameObject** — The fundamental building block of a Unity scene. Everything visible or interactive is a GameObject.

**Component** — A reusable module that adds behavior or properties to a GameObject. **Examples:** Transform (position/rotation/scale), Renderer (makes it visible), Collider (gives it physics), Script (custom behavior).

**Component-Based Architecture** — Instead of deep inheritance, you *compose* objects by adding components. A "player" isn't a Player class; it's a GameObject with a Transform, a Renderer, a Collider, and a PlayerController script.

**Transform Component** — Always on every GameObject. Stores Position (where), Rotation (which way), Scale (how big).

**Active/Inactive** — You can enable/disable GameObjects and components to toggle them on/off without deleting.

---

## Common Components

| Component | Purpose |
|-----------|---------|
| **Transform** | Position, Rotation, Scale (always present) |
| **Mesh Filter** | Defines the 3D shape to render |
| **Mesh Renderer** | Renders the mesh (makes it visible) |
| **Collider** | Detects collisions (Box, Sphere, Capsule, Mesh) |
| **Rigidbody** | Physics simulation (gravity, velocity, forces) |
| **Script** (MonoBehaviour) | Custom C# behavior |
| **Light** | Illuminates the scene (Directional, Point, Spot) |
| **Camera** | Player's viewpoint; renders the game view |

---

## Unity Setup Steps

1. **Create a new 3D scene** (File → New Scene → 3D)
2. **Right-click in Hierarchy:** 3D Object → Cube. A new GameObject appears.
3. **Select the Cube in the Hierarchy**
4. **Look at the Inspector (right panel):** You'll see:
   - Transform component (Position, Rotation, Scale)
   - Mesh Filter (the cube shape)
   - Box Collider (collision boundary)
   - Mesh Renderer (makes it visible)
5. **Add a Rigidbody:** In Inspector, click "Add Component" → Search "Rigidbody" → Click it
6. **In the Rigidbody component, toggle "Use Gravity"** — it should now be checked
7. **Press Play and watch it fall!**

---

## Guided Practice

1. **Create 3 GameObjects:** Cube (ground), Sphere (ball), Cylinder (obstacle)
2. **Add a Rigidbody to the Sphere** (Add Component → Rigidbody)
3. **Position the Cube at Y=0** (ground level)
4. **Position the Sphere high above** (Y=5)
5. **Press Play:** The sphere should fall and land on the cube
6. **Add a Rigidbody to the Cube:** Change "Body Type" to "Kinematic" (it won't move but can block things)

---

## Practice Problems

**Beginner:** Create a scene with 3 objects: a ground cube, a falling sphere, and a wall (tall thin cube). Add Rigidbodies to ground and wall set to "Kinematic". Press Play and describe what happens.

**Intermediate:** Create 5 cubes stacked vertically. Add Rigidbodies to all. Press Play. The tower should topple. Take a screenshot of the unstable result.

**Challenge:** Design a small physics scene: a ramp (rotated cube), a ball at the top, and obstacles at the bottom. Each object should have the right components (Collider, maybe Rigidbody). Press Play and verify the ball rolls correctly.

<details>
<summary>💡 Hints</summary>
- Every visible GameObject needs both a Mesh Filter *and* a Mesh Renderer to show up
- Colliders define collision boundaries; they don't need Rigidbodies
- Rigidbodies enable *physics* — gravity, momentum, collision impulses
- Kinematic Rigidbodies don't fall but can be moved by script and collide with dynamic objects
</details>

<details>
<summary>✅ Sample: Ball and Ramp</summary>

Hierarchy:
- Ground (Cube, scale 10,1,10, Rigidbody as Kinematic)
- Ramp (Cube, scale 1,1,5, rotated 30° on Z, positioned at top, Rigidbody as Kinematic)
- Ball (Sphere, positioned at top of ramp, Rigidbody set to Dynamic)

When Play is pressed, gravity pulls Ball down, Ramp redirects it, and it rolls across Ground.

</details>
