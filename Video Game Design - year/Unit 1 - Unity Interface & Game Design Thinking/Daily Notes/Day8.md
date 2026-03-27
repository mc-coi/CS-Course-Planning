# Day 8: Lighting Basics

**Learning Target:** I can set up basic lighting in a scene and understand how light affects materials and visibility.

---

## Key Concepts

**Light Component** — Illuminates the scene. Without lights, materials appear black/very dark.

**Directional Light** — Simulates the sun. Parallel rays from one direction. **For:** Overall scene lighting.

**Point Light** — Like a light bulb. Radiates in all directions from a point. **For:** Lamps, fires, explosions.

**Spotlight** — Cone of light from a direction. **For:** Flashlights, stage lights.

**Intensity** — How bright (0-2+ are common; above 1 is very bright).

**Ambient Light** — Flat, directional-less lighting that fills shadows. **Where:** Window → Rendering → Lighting Settings.

---

## Light Properties

| Property | Default | Range | Use |
|----------|---------|-------|-----|
| Intensity | 1 | 0-2+ | How bright |
| Color | White | Any | Warm/cool tone |
| Range (Point/Spot) | 10 | 0+ | How far it reaches |
| Angle (Spot) | 30 | 0-180 | Cone width |

---

## Unity Setup Steps

1. **Create a new 3D scene**
2. **Create a few cubes and spheres** in random positions
3. **Look at the Hierarchy:** You should see a "Directional Light" (the sun) already there
4. **Select the Directional Light** and look at Inspector
5. **Change its Rotation Y to 90:** The light direction changes, shadows move
6. **In Hierarchy, right-click:** Create Empty → name it "Lights"
7. **Right-click Lights folder:** Light → Point Light → Name it "Lamp1"
8. **Position Lamp1 above a cube:** It illuminates nearby objects with a warm glow
9. **Adjust Lamp1's Range:** (Inspector → Range = 20) — light spreads further
10. **Create a Spotlight:** Lights → Light (Spot) → Position it pointing at an object

---

## Guided Practice

1. **Delete the default Directional Light** (or move it far away)
2. **Create a Point Light positioned at (0, 3, 0)** (above center)
3. **Create 5 cubes around the light** at varying distances
4. **Adjust the Point Light's Intensity:** 1.0, then 2.0 — notice brightness change
5. **Change the light's color to blue:** Window → Rendering → Lighting → Ambient Light → change to blue tint
6. **Create a Spotlight pointing downward** at one of the cubes

---

## Practice Problems

**Beginner:** Create a scene with 1 Directional Light and 5 objects. Rotate the light 90° on the Y axis. Take a screenshot showing shadows.

**Intermediate:** Build a room with 4 walls (cubes), a floor (flat cube), and 2 Point Lights inside. Adjust light properties so the room feels naturally lit.

**Challenge:** Design a moody scene: dim Directional Light, a blue Point Light on the left, a warm Point Light on the right, and 3+ objects. Make it feel atmospheric (like a game scene).

<details>
<summary>💡 Hints</summary>
- One Directional Light is usually enough (it's the "sun")
- Point Lights are expensive (performance cost) — use sparingly
- Increase Intensity for brighter light, decrease Range to save performance
- Bake lighting (advanced) for better performance on static scenes
- Without ANY light, scenes appear almost completely black
</details>

<details>
<summary>✅ Sample: Lit Scene</summary>

Hierarchy:
- Directional Light (Rotation Y=45, Intensity=1)
  - Cube (ground, material: Gray Matte)
  - Sphere (position 0,1,0, material: Red Matte)
  - Cube (position 3,1,0, material: Blue Metallic)
- Point Light (position 0,5,0, Range=15, Color=warm white, Intensity=1.5)
- Spotlight (position -5,3,-2, pointing at center, Intensity=0.8)

Result: Well-lit scene with directional shadows + ambient from Point Light + dramatic Spotlight.

</details>
