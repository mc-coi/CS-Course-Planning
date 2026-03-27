# Day 1: Game Design Vocabulary & Unity Panels

**Learning Target:** I can define key game design terms and navigate the five main Unity editor panels.

## Key Concepts

- **Game Design:** The art and science of defining game rules, systems, and player experiences
- **MDA Framework:** Mechanics (rules) → Dynamics (behavior) → Aesthetics (player feeling)
- **Mechanics:** The rules and systems that govern gameplay (jumping, collecting coins, health)
- **Dynamics:** How mechanics interact during play (collecting coins gets faster, enemies adapt)
- **Aesthetics:** The emotional response players have (fun, tension, satisfaction)
- **Unity Editor:** A visual development environment for creating games
- **Scene:** A container for GameObjects and their relationships

The Unity editor is divided into five main panels:
1. **Scene View** – A 3D viewport where you arrange and edit GameObjects
2. **Game View** – Shows what the camera sees (player perspective)
3. **Hierarchy Panel** – Displays all GameObjects in the current scene as a tree
4. **Inspector Panel** – Shows properties/components of the selected GameObject
5. **Project Panel** – File browser for all project assets (scripts, prefabs, sprites)

GameObjects are the fundamental building blocks in Unity. Each scene contains GameObjects, and each GameObject has components attached to it. The **Transform** component is the most essential—it stores position, rotation, and scale.

## Code Examples

```csharp
using UnityEngine;

// MonoBehaviour is the base class for all scripts attached to GameObjects
public class GameManager : MonoBehaviour
{
    // This method runs once when the scene starts
    void Start()
    {
        // Print a debug message to the Console window
        Debug.Log("Game started!");
    }

    // This method runs once per frame
    void Update()
    {
        // We'll add gameplay logic here later
    }
}
```

## Guided Practice

1. Open Unity and create a new 3D scene
2. Right-click in the Hierarchy and create a new GameObject
3. In the Inspector, observe the Transform component showing x, y, z position
4. Drag the GameObject in the Scene view to move it
5. Open the Game view tab to see what the camera sees

## Practice Problems

**Problem 1 — Beginner:** Explain the MDA framework and give an example from a game you know.

**Problem 2 — Intermediate:** Create a new scene with a Cube and a Plane. Move the Cube above the Plane using the Move tool (W key). What are the Transform coordinates of the Cube?

**Problem 3 — Challenge:** Design a simple game concept (one paragraph) using the MDA framework. Describe the mechanics, dynamics, and aesthetics.

<details>
<summary>Hints</summary>

**Problem 1:** MDA stands for Mechanics, Dynamics, Aesthetics. Think about how the rules (mechanics) create interactions (dynamics) that make players feel something (aesthetics).

**Problem 2:** Use the Scene view to visually position the Cube. Look at the Transform component in the Inspector to see the X, Y, Z values. The Y value should be greater than 0 to be above the Plane.

**Problem 3:** Start with a core mechanic (e.g., "dodge falling objects"), then describe how that mechanic creates interesting interactions (dynamics), and finally describe the emotional experience (aesthetics).
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:** **MDA Framework:** Mechanics are the rules and systems (e.g., in Mario, the ability to jump, collect coins, defeat enemies). Dynamics are how those mechanics interact during play (e.g., jumping over obstacles and collecting coins creates a challenging rhythm). Aesthetics are the emotional response (e.g., players feel excited, accomplished, or challenged). **Example:** In Super Mario Bros, the mechanic of "press jump to jump higher the longer you hold" creates the dynamic of responsive control, giving players the aesthetic of empowerment and satisfaction.

**Problem 2:** Answers will vary, but an example would be: Plane position: (0, 0, 0), Cube position: (0, 2, 0) or similar. The Y coordinate must be higher than the Plane's Y coordinate to be visually above it.

**Problem 3:** **Example Game: "Dodge Blocks"** **Mechanics:** The player controls a square that moves left/right on the screen. Blocks fall from the top. When the player's square touches a block, they lose a life. Collecting a gold square adds a life. **Dynamics:** As the game continues, blocks fall faster, creating increasing pressure. The player must react quickly and anticipate where blocks will land. **Aesthetics:** Players experience tension and urgency. When they dodge a block, they feel relief. Collecting gold feels rewarding. The overall experience is one of focused, fast-paced challenge.
</details>
