# Day 6: Transform Properties & Parenting Deep Dive

**Learning Target:** I can manipulate Transform properties (position, rotation, scale) precisely and use parenting to build hierarchies.

---

## Key Concepts

**Position** — XYZ coordinates in world space (or local space if you switch the toggle). X = left/right, Y = up/down, Z = forward/back.

**Rotation** — Euler angles in degrees. X/Y/Z represent rotation around each axis. **Careful:** Rotation order matters (gimbal lock), but for basic design, just think "spin on each axis."

**Scale** — Size multiplier. (1,1,1) = normal; (2,2,2) = twice as big; (0.5,0.5,0.5) = half size. **Negative scales = flip** (ugly for rendering; avoid).

**Parent-Child Relationship** — A child's local position is *relative to its parent*. Moving the parent moves all children.

**Anchor Point** — The origin of an object. Usually the center, but you can offset it (advanced).

---

## Transform Inspector Fields

| Field | Meaning | Example |
|-------|---------|---------|
| Pos X/Y/Z | Position in meters | 5.0 = 5 units right |
| Rot X/Y/Z | Rotation in degrees | 90 = 90° rotation |
| Scale X/Y/Z | Size multiplier | 2.0 = twice as large |

---

## Unity Setup Steps

1. **Create two cubes in the Hierarchy**
2. **Rename them:** "Parent_Cube" and "Child_Cube"
3. **In the Inspector, manually set Parent_Cube position:** X=0, Y=0, Z=0
4. **Set Child_Cube position:** X=2, Y=0, Z=0 (it appears 2 units to the right)
5. **Drag Child_Cube onto Parent_Cube in the Hierarchy** — Child_Cube is now parented
6. **Watch the Inspector:** Child_Cube's position now shows (2,0,0) in *local* space
7. **Move Parent_Cube to X=5:** Both cubes move right by 5 units

---

## Guided Practice

1. **Create a "Robot" parent with "Head", "Body", "Arm_Left", "Arm_Right" cubes as children**
2. **Position each part** (head on top, arms to the sides) using local positions
3. **Rotate the Body 45 degrees** — only the body rotates, not the arms
4. **Scale the Arm_Left to (0.5, 1, 0.5)** — it becomes thinner
5. **Move the Robot parent:** All parts move together; the hierarchy is intact

---

## Practice Problems

**Beginner:** Create a simple parent-child structure (parent cube with 3 children) and move the parent. Verify all children follow.

**Intermediate:** Design a "character" with 5+ body parts. Use parenting to ensure when you rotate the torso, limbs follow correctly. Position and scale each part realistically.

**Challenge:** Build a hierarchical scene: a "Scene Root" containing "Buildings", and Buildings contains "Walls" and "Roof". Demonstrate that scaling Scene Root scales the entire city proportionally.

<details>
<summary>💡 Hints</summary>
- Parenting is *spatial*: children's positions are offsets from the parent's origin
- If you rotate a parent, children rotate *around the parent's center*, not their own center
- Use parenting for organizational clarity AND for gameplay (e.g., parent a sword to a hand so it moves with the hand)
- Reset values: Ctrl-click on any property in Inspector to reset it to default
</details>

<details>
<summary>✅ Sample: Robot Structure</summary>

Hierarchy:
- Robot (position 0,0,0)
  - Body (local pos 0,0,0, scale 1,2,0.5)
  - Head (local pos 0,1.5,0, scale 0.8,0.8,0.8)
  - Arm_Left (local pos -1,0.5,0, scale 0.3,1,0.3)
  - Arm_Right (local pos 1,0.5,0, scale 0.3,1,0.3)
  - Leg_Left (local pos -0.3,-1,0)
  - Leg_Right (local pos 0.3,-1,0)

Rotating Robot rotates the entire figure around its center.

</details>
