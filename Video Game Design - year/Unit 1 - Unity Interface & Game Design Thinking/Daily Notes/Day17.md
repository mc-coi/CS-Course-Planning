# Day 17: Mini-Project — Static 3D Scene

**Learning Target:** I can design and build a complete 3D scene using GameObjects, prefabs, materials, and lighting.

---

## Project Brief

**Your Task:** Build a cohesive 3D environment (e.g., a park, a small city block, a fantasy shrine, a laboratory). The scene should:

1. **Use 30+ GameObjects** (cubes, spheres, cylinders, etc.)
2. **Include at least 3 custom materials** (different colors and finishes)
3. **Use prefabs for repetitive elements** (trees, benches, lamps, etc.)
4. **Have proper lighting** (at least 1 Directional Light + 1-2 Point Lights)
5. **Demonstrate hierarchy and parenting** (groups of objects under parent containers)
6. **Be visually coherent** (design makes sense; not random objects scattered)

---

## Suggested Themes (Pick One or Create Your Own)

- **Zen Garden:** Sand (flat plane), rocks, water (blue planes), stepping stones, lanterns
- **Street Corner:** Buildings, lampposts, benches, sidewalk, street
- **Fantasy Temple:** Main structure, pillars, altar, torches, decorative statues
- **Playground:** Equipment (swings, slide, seesaw), benches, trash bins, trees
- **Laboratory:** Tables, equipment (cylinders/spheres as "machines"), shelves, lights

---

## Requirements Checklist

- [ ] 30+ GameObjects placed in the scene
- [ ] 3+ unique materials created and applied
- [ ] At least 2 prefabs created (used 2+ times each)
- [ ] Proper lighting (1 Directional, 1-2 Point lights, sensible Intensity/Range)
- [ ] Parent-child hierarchy visible (Scene Root with organized children)
- [ ] All objects named meaningfully (not "Cube", "Cube1", etc.)
- [ ] Scene saved as "Unit1_MiniProject"
- [ ] No errors in Console

---

## Workflow Steps

1. **Plan your theme** and sketch it (even rough drawings help)
2. **Create base elements** (ground, walls, main structures)
3. **Add detail objects** (decorations, smaller props)
4. **Create 2-3 prefabs** for repeating elements (trees, poles, benches)
5. **Set up lighting** (position directional light, add point lights for local illumination)
6. **Organize hierarchy** — Create empty GameObjects as "folders" (Environment, Props, Lights, etc.)
7. **Create materials** for visual variety (wood, stone, metal, etc.)
8. **Adjust camera** for a nice default view of your scene
9. **Review and refine** — take screenshots, verify names are clear, check for z-fighting or holes

---

## Guided Practice (Workflow Demo)

1. **Create a "Ground" plane** (large flat cube or use a Plane primitive)
2. **Create a "Building" prefab** (a house-like structure with walls, door, windows)
3. **Instantiate Building 3 times** at different positions
4. **Create a "Tree" prefab** (cylinder trunk + sphere foliage)
5. **Place Trees around** the buildings
6. **Add a Directional Light** (sun) and adjust rotation
7. **Add a Point Light** (streetlamp) at each building
8. **Organize everything** under a "Scene Root" empty GameObject

---

## Success Criteria

- **Visual Coherence:** Scene tells a story; objects belong together
- **Technical Quality:** No errors, proper naming, organized hierarchy
- **Asset Reuse:** Prefabs are used multiple times (demonstrates efficiency)
- **Lighting:** Scene is well-lit; shadows add depth

---

## Deliverables

Save your scene as **"Unit1_MiniProject.unity"** in the Scenes folder.

Optional: Take 2-3 screenshots from different camera angles (save as PNG) showing your scene.

---

## Hints & Tips

- Use layers to temporarily hide elements while building (e.g., hide Trees while placing Buildings)
- Vertex snapping (Cmd/Ctrl+Shift + drag) aligns objects perfectly
- Press `F` frequently to frame your selection and verify alignment
- Color-code materials to visually organize object types
- Name objects in a hierarchical pattern: "Building_Main", "Building_Entrance", "Building_Roof", etc.
- Test: press Play and walk around (if you add a simple camera controller script)
