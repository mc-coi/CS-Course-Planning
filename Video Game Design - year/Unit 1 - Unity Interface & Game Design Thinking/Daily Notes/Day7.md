# Day 7: Materials and Colors

**Learning Target:** I can create materials, assign colors, and apply them to GameObjects to customize appearance.

---

## Key Concepts

**Material** — A reusable asset that defines how a surface looks: color, texture, reflectivity, shader. **Where:** Create in Project window.

**Shader** — A program that calculates how light interacts with a surface. **Standard Shader** handles most cases. **Unlit Shader** ignores lighting (for UI, HUD, etc.).

**Albedo** — The "color" of the material without lighting effects. Most visible property.

**Metallic & Smoothness** — Metallic (0-1: how shiny) and Smoothness (0-1: how reflective). Chrome is high metallic + high smoothness.

**Mesh Renderer** — The component that displays a mesh using a material. **Where:** Inspector of any visible GameObject.

---

## Material Properties (Standard Shader)

| Property | Default | What it does |
|----------|---------|--------------|
| Albedo | White | Base color |
| Metallic | 0 | How reflective (0=matte, 1=chrome) |
| Smoothness | 0.5 | How shiny (0=rough, 1=glossy) |
| Normal Map | (none) | Surface detail without geometry |

---

## Unity Setup Steps

1. **Create a new folder in Project window:** Right-click → Folder → name it "Materials"
2. **Inside Materials folder, create a material:** Right-click → Material → name it "Red_Matte"
3. **Select Red_Matte in Project (don't need to open it)**
4. **In Inspector, find Albedo color:** It's white by default
5. **Click the white square** to open the color picker
6. **Set it to red** (move the vertical bar to red, then pick a shade)
7. **Create a cube in your scene**
8. **Drag Red_Matte onto the Cube** in either the Scene View or the Inspector's Mesh Renderer material slot

---

## Guided Practice

1. **Create 5 materials:** Red, Blue, Green, Yellow, Metal
2. **For each, set the Albedo color** and adjust Metallic/Smoothness
3. **Create 5 cubes** in your scene
4. **Drag one material to each cube** — they should all look different
5. **Tweak one material's properties:** Notice all cubes using it update in real-time

---

## Practice Problems

**Beginner:** Create 3 materials (red matte, blue metallic, green reflective) and apply each to a different cube.

**Intermediate:** Design a material for "wood" (brownish, slightly shiny), "stone" (gray, rough), and "gold" (yellow, very reflective). Create 3 cubes and apply them.

**Challenge:** Create a scene with 10+ objects, each with a unique material. Think about realism: what would be metallic? What would be matte? Can you use 5 materials total and apply them to all 10 objects?

<details>
<summary>💡 Hints</summary>
- Colors are RGB: Red=(1,0,0), Green=(0,1,0), Blue=(0,0,1), White=(1,1,1), Black=(0,0,0)
- Alpha (transparency) is tricky; you'll handle it later with different shaders
- Metallic 0 = no metal. Metallic 1 = full metal. Values between are gradients
- Smoothness: 0 = matte/rough. 1 = glossy/shiny. Most materials are 0.3-0.7
- Materials are reusable: one material can be on 100 objects
</details>

<details>
<summary>✅ Sample: Common Materials</summary>

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

</details>
