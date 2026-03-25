# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is the MDA framework, and how does it relate to game design?

2. Name the five main panels in the Unity editor and describe the purpose of each.

3. What is the Transform component, and what three properties does it store?

4. Explain the difference between the Scene view and the Game view.

5. What is the difference between Start() and Update() methods in a MonoBehaviour script?

6. How do you attach a C# script to a GameObject?

7. What does Debug.Log() do, and why is it useful?

8. Explain the parent-child relationship in the Hierarchy and how it affects Transform values.

9. What is a Material, and what are three important properties of the Standard Material?

10. What is Time.deltaTime, and why is it important for game development?

---

**Answers:**

1. The MDA framework stands for Mechanics (rules), Dynamics (interactions), and Aesthetics (emotional response). It's a way to understand and design games by separating what players do (mechanics), how systems interact (dynamics), and how they feel (aesthetics).

2. **Scene View** - A 3D viewport where you arrange and edit GameObjects. **Game View** - Shows what the camera sees (player perspective). **Hierarchy** - Displays all GameObjects in the current scene as a tree. **Inspector** - Shows properties/components of the selected GameObject. **Project Panel** - File browser for all project assets (scripts, prefabs, sprites).

3. The Transform component stores: **Position** (X, Y, Z coordinates in 3D space), **Rotation** (angles around X, Y, Z axes in degrees), and **Scale** (size multipliers for each axis).

4. The **Scene View** is where you edit and arrange GameObjects in the editor. The **Game View** shows what the camera will render during gameplay—this is what players see.

5. **Start()** is called once when the scene begins (good for initialization and setup). **Update()** is called once per frame (good for continuous logic like checking input or moving objects).

6. Right-click in the Project panel and select Create > C# Script. Name it descriptively. Double-click to edit, write your code, save, and then drag the script onto a GameObject in the Hierarchy to attach it. Alternatively, select a GameObject and drag the script into the Inspector.

7. Debug.Log() prints a message to the Console window. It's essential for debugging: print variable values, track code execution, and understand what's happening in your game at runtime.

8. A child GameObject's position is stored in local space relative to its parent. When the parent moves, rotates, or scales, all children move with it while maintaining their relative positions. This is useful for organizing complex objects like vehicles with wheels or characters with limbs.

9. A Material defines how a surface looks (color, texture, reflectivity). It's composed of a Shader (a program) and properties. Three important properties of the Standard Material are: **Albedo** (the base color), **Metallic** (how metal-like the surface is), and **Smoothness** (how shiny the surface is).

10. Time.deltaTime is the time elapsed since the last frame (in seconds). It's important because it makes movement and animation frame-rate independent. Without it, computers running at faster frame rates would move faster, causing inconsistencies across different hardware.

---
