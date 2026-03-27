# Day 29: Game Design Document & Scope

**Learning Target:** Write a comprehensive Game Design Document and define MVP scope for your capstone project.

### Key Concepts

- **Game Design Document (GDD):** Written specification of the game
- **Elevator Pitch:** One-sentence description of the game
- **Core Loop:** The repeating gameplay cycle
- **MVP (Minimum Viable Product):** Smallest feature set to make a playable game
- **Feature List:** All intended features, organized by priority
- **Scope Management:** Deciding what to include and what to cut
- **Prototype Phase:** Testing core mechanics before full development
- **Design vs. Implementation:** Documented design vs. actual code

### Content

A Game Design Document guides development. It answers:
- What is the game?
- Who is the player?
- What is the core mechanic?
- What is the progression?
- What are win/lose conditions?

**GDD Structure:**
1. **Title & Overview** – One-paragraph summary
2. **Elevator Pitch** – One sentence describing the game
3. **Core Gameplay Loop** – How the game plays each cycle
4. **Win/Lose Conditions** – How the player wins or loses
5. **Player Motivation** – Why the player plays
6. **Feature List** – All features, organized as Must-Have, Should-Have, Nice-to-Have
7. **Target Audience** – Who will play
8. **Technical Details** – Platform, art style, estimated scope

**MVP Planning:**
Focus on the absolute minimum to make the game playable:
- Core mechanic works
- One level
- Basic visuals
- Win condition

Everything else is added after MVP is solid.

### Code Examples

```csharp
using UnityEngine;

// Example GDD as a game design document

/*
GAME DESIGN DOCUMENT
====================

TITLE: "Asteroid Blast"

ELEVATOR PITCH:
A fast-paced arcade game where you control a spaceship, destroy asteroids,
and survive as long as possible while your score increases.

CORE GAMEPLAY LOOP:
1. Player sees asteroids approaching
2. Player rotates and shoots asteroids
3. Asteroids break into smaller pieces or disappear
4. Score increases
5. Repeat until hit by asteroid (lose) or survive timer (win)

CORE MECHANIC:
- Control spaceship with arrow keys
- Shoot with spacebar
- Destroy asteroids before they hit you

WIN CONDITION:
- Survive for 3 minutes without being hit

LOSE CONDITION:
- Hit by an asteroid (health = 0)

MVP FEATURES (Must-Have):
- Player spaceship with rotation and movement
- Asteroid spawning and movement
- Shooting mechanic
- Collision detection (bullet-asteroid, asteroid-player)
- Score display
- Simple UI (score, health, timer)
- One difficulty level

SHOULD-HAVE FEATURES:
- Multiple difficulty levels
- Sound effects
- Particle effects for explosions
- Leaderboard
- Pause menu

NICE-TO-HAVE FEATURES:
- Power-ups
- Multiple player ships to choose
- Enemy saucers
- Background music
- Achievements

TARGET AUDIENCE:
Casual players, ages 10+, enjoy arcade games

TECHNICAL DETAILS:
Platform: WebGL
Art Style: Simple 2D geometric shapes
Scope: 2-3 weeks for MVP
*/

// This structure is a template for your capstone game
public class ProjectTemplate : MonoBehaviour
{
    // Use this script as a reference for organizing your game

    [Header("Game Configuration")]
    public string gameTitle = "My Game";
    public int mvpDurationDays = 7;

    [Header("Core Features")]
    public bool hasPlayerMovement = true;
    public bool hasEnemies = true;
    public bool hasCollectibles = true;
    public bool hasScoring = true;

    [Header("MVP Requirements")]
    public bool playerCanMove = true;
    public bool coreMechanicWorks = false;  // Set to true when core mechanic is implemented
    public bool winConditionExists = false;
    public bool loseConditionExists = false;
    public bool basicUIExists = false;
}
```

### Guided Practice

1. Choose a game concept (avoid something too big!)
2. Write a one-sentence elevator pitch
3. Define the core gameplay loop (4-5 steps)
4. List MVP features (5-8 items maximum)
5. Define win and lose conditions clearly
6. Estimate scope: Can you build this in 1-2 weeks?
7. Create a simple GDD document

### Practice Problems

**Problem 1 — Beginner:** Write an elevator pitch and core loop for a simple game concept.

**Problem 2 — Intermediate:** Create a complete GDD with all sections (overview, elevator pitch, core loop, MVP, etc.).

**Problem 3 — Challenge:** Define MVP features and prioritize them into Must-Have, Should-Have, and Nice-to-Have lists.

<details>
<summary>Hints</summary>

**Problem 1:** Elevator pitch should be 1-2 sentences. Core loop should have 4-5 clear steps that repeat.

**Problem 2:** Use the GDD structure in the code example above. Fill in all sections with specific details.

**Problem 3:** Must-Have features are critical for gameplay. Should-Have features enhance it. Nice-to-Have are extras if time allows.

</details>

<details>
<summary>Sample Answers</summary>

**Sample Elevator Pitch:** "A puzzle game where you rotate blocks to create lines, with increasing difficulty and a high score leaderboard."

**Sample Core Loop:**
1. Block falls from top
2. Player rotates block with arrow keys
3. Block lands and fills grid
4. Complete lines disappear
5. Score increases
6. Next block appears

**Sample MVP Features:**
- Must-Have: Block falling, rotation, line clearing, score
- Should-Have: Difficulty levels, sound effects
- Nice-to-Have: Leaderboard, achievements

</details>
