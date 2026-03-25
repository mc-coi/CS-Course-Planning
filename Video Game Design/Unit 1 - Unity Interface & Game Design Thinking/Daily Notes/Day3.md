# Day 3: Materials, Lighting & Scene Building

**Learning Target:** I can create materials and lights to build visually appealing scenes in Unity.

## Key Concepts

- **Material:** Defines how a surface looks (color, texture, shininess)
- **Shader:** A program that tells the GPU how to render a material
- **Light:** An object that illuminates the scene
- **Standard Material:** Unity's default physically-based material
- **Albedo:** The base color of a material
- **Metallic & Smoothness:** Properties that control reflections and specularity
- **Ambient Light:** Overall light in the scene from all directions

Every mesh needs a material to be visible. Materials are created in the Project panel and assigned to Renderer components on GameObjects. The **Standard Material** shader is the default and supports:
- **Albedo:** The main color texture or color
- **Metallic:** How metal-like the surface is (0 = non-metal, 1 = pure metal)
- **Smoothness:** How shiny the surface is (0 = rough, 1 = mirror-like)

Lights are essential for visibility. Common light types:
- **Directional Light:** Simulates sunlight; illuminates everything equally
- **Point Light:** Emits light from a position in all directions
- **Spot Light:** A cone of light from a position, like a flashlight

To build a simple scene:
1. Create a Plane (GameObject > 3D Object > Plane) for the ground
2. Create a Cube and move it above the plane
3. Adjust the scale and position of objects
4. Create a Directional Light or use the default one
5. Assign different materials to objects to see how they look

## Code Examples

```csharp
using UnityEngine;

public class SceneBuilder : MonoBehaviour
{
    // Reference to the material to change color
    private Renderer meshRenderer;

    void Start()
    {
        // Get the Renderer component attached to this GameObject
        meshRenderer = GetComponent<Renderer>();

        // Change the albedo (base color) of the material
        // Note: Create a new material instance so we don't modify the original
        meshRenderer.material.color = new Color(1f, 0.5f, 0f); // Orange
    }

    void Update()
    {
        // Optional: Animate the color over time
        float hue = Time.time % 1f; // Cycles from 0 to 1
        meshRenderer.material.color = Color.HSVToRGB(hue, 1f, 1f);
    }
}
```

## Guided Practice

1. Create a Plane and a Cube in your scene
2. In the Project panel, right-click and create a new Material
3. In the Inspector, change the Albedo color to a custom color (e.g., red)
4. Drag the material onto the Cube in the scene or hierarchy
5. Create a Directional Light and adjust its intensity to see how it affects the scene
6. Create a Point Light and place it near the Cube to see local lighting
7. Experiment with Metallic and Smoothness values on the material

## Practice Problems

**Problem 1 — Beginner:** Create a material with a custom color and assign it to a Sphere. What color did you choose and why?

**Problem 2 — Intermediate:** Create a scene with a Cube, Sphere, and Plane. Assign different materials to each and adjust their Metallic and Smoothness values. Describe the visual differences.

**Problem 3 — Challenge:** Build a simple scene with 5 objects, 2 lights, and different materials. Take a screenshot of the Game view and explain your design choices.

<details>
<summary>Hints</summary>

**Problem 1:** Right-click in the Project panel and select Create > Material. Click on it and change the color in the Inspector. Drag it onto your Sphere.

**Problem 2:** Make one material metallic (Metallic = 1, Smoothness = 0.9), one material rough (Metallic = 0, Smoothness = 0.2), and one in between. Observe how light reflects differently.

**Problem 3:** Think about composition and lighting. Where does light come from? How do materials enhance the scene? Consider using warm and cool colors.
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:** Answers will vary. Example: A bright red material (#FF0000) was chosen because it's eye-catching and could represent an important object like a power-up or hazard in a game.

**Problem 2:** The metallic material with high smoothness should look shiny and reflective like polished metal. The rough material (low smoothness) should appear dull and matte. The material in between shows a balance between reflection and diffusion.

**Problem 3:** A good scene design uses lighting to create depth and mood. For example: a Directional Light simulates sunlight, a Point Light adds local illumination near key objects, and materials with varying properties help distinguish different objects in the scene.
</details>
