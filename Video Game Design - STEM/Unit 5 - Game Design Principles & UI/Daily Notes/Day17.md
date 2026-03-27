# Day 17: MDA Framework & Game Loop

**Learning Target:** Understand the MDA framework (Mechanics, Dynamics, Aesthetics) and the core game loop that drives all games.

### Key Concepts

- **MDA Framework:** Mechanics (rules), Dynamics (interactions), Aesthetics (emotions)
- **Core Game Loop:** The repeating sequence: Feedback → Input → Resolution → Repeat
- **Mechanics:** The rules and systems (jump, collect, defeat)
- **Dynamics:** How mechanics interact (increasing difficulty, chaining actions)
- **Aesthetics:** The emotional response (fun, tension, satisfaction)
- **Bartle Types:** Four player motivations (Achiever, Explorer, Socializer, Killer)
- **Player Motivation:** Why players play (challenge, exploration, story, competition)

### Content

Every game can be analyzed through the MDA framework:

**Mechanics:** The rules. In Mario, you can jump, move, and collect coins.

**Dynamics:** How rules create interactions. Jumping over obstacles while collecting coins creates a rhythm. Enemies force you to dodge while collecting—increasing pressure.

**Aesthetics:** How interactions make players *feel*. The combination of jumping, collecting, and dodging creates tension and relief. Players feel accomplished when they beat a level.

**Core Game Loop:**
Every game has a repeating loop:
1. Player receives feedback (visual/audio)
2. Player makes decision (input)
3. Game responds (mechanics resolve)
4. Loop repeats

Example: In Pac-Man:
- See pellets and ghosts (feedback)
- Move with arrow keys (decision)
- Eat pellet, check if ghost touched you (mechanics)
- Repeat

**Bartle Types** describe player motivations:
- **Achiever:** Wants to overcome challenges, earn rewards, reach goals
- **Explorer:** Wants to discover secrets, understand systems, learn the world
- **Socializer:** Wants to interact with others, collaborate, tell stories
- **Killer:** Wants to compete, dominate, challenge other players

Different games appeal to different types. Many players exhibit multiple motivations.

### Code Examples

```csharp
using UnityEngine;

public class GameLoopManager : MonoBehaviour
{
    [System.Serializable]
    public class GameState
    {
        public int score = 0;
        public int health = 100;
        public int level = 1;
        public bool isPaused = false;
    }

    public GameState gameState = new GameState();

    // Simulating the core game loop:
    // 1. Feedback (UI update)
    // 2. Input (player decision)
    // 3. Resolution (mechanics)
    // 4. Repeat

    void Update()
    {
        if (gameState.isPaused)
            return;

        // Step 1: Provide feedback
        UpdateUI();

        // Step 2: Get player input
        HandleInput();

        // Step 3: Resolve mechanics
        UpdateGameMechanics();

        // Step 4: Repeat (Update() calls itself every frame)
    }

    void UpdateUI()
    {
        // Show current score, health, etc.
        Debug.Log($"Score: {gameState.score} | Health: {gameState.health} | Level: {gameState.level}");
    }

    void HandleInput()
    {
        // Player makes decisions
        if (Input.GetKeyDown(KeyCode.Space))
        {
            OnPlayerAction("Jump");
        }
    }

    void UpdateGameMechanics()
    {
        // Game responds to input
        // (Could damage player, collect items, etc.)
    }

    void OnPlayerAction(string action)
    {
        Debug.Log("Player performed: " + action);
        // Trigger feedback (particles, sounds, visual feedback)
    }

    public void AddScore(int points)
    {
        gameState.score += points;
    }

    public void TakeDamage(int damage)
    {
        gameState.health -= damage;
        if (gameState.health <= 0)
        {
            GameOver();
        }
    }

    void GameOver()
    {
        Debug.Log("Game Over! Final Score: " + gameState.score);
        gameState.isPaused = true;
    }
}
```

### Guided Practice

**Activity:** Analyze a game you know (Mario, Pac-Man, Tetris, etc.) using the MDA framework:
1. List 3 mechanics (rules the game has)
2. Describe 2 dynamics (how those mechanics interact)
3. Write 2-3 adjectives describing the aesthetics (how the game makes you feel)
4. Identify which Bartle Types your game appeals to most

Example (Mario):
- **Mechanics:** Jump, move left/right, collect coins
- **Dynamics:** Enemies force you to jump carefully while collecting coins
- **Aesthetics:** Tension, satisfaction, accomplishment
- **Bartle Types:** Achiever (reach the goal), Explorer (find secrets)

### Practice Problems

**Problem 1 — Beginner:** Pick a simple game (Snake, Flappy Bird, etc.) and identify 1 mechanic, 1 dynamic, and how it makes you feel.

**Problem 2 — Intermediate:** Analyze a game using all 4 Bartle Types. How does the game appeal to each type of player?

**Problem 3 — Challenge:** Design a simple mechanic (e.g., "jump on platforms") and predict what dynamics and aesthetics it will create.

<details>
<summary>Hints</summary>

**Problem 1:** Think simple. A mechanic is a rule. A dynamic is how rules interact. Aesthetics are emotions.

**Problem 2:** Not all games appeal equally to all types. Some games are heavily Achiever-focused; others cater to Explorers with secrets.

**Problem 3:** Consider how a player would experience your mechanic repeatedly. What would make it fun or frustrating?

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1 Example (Flappy Bird):**
- **Mechanic:** Tap to make bird go up; gravity pulls down
- **Dynamic:** Avoiding pipes while staying alive
- **Aesthetics:** Frustration, tension, short bursts of triumph

**Problem 2 Example (Minecraft):**
- **Achiever:** Survival mode has goals (defeat Ender Dragon)
- **Explorer:** Creative mode lets you discover and build freely
- **Socializer:** Multiplayer servers and shared worlds
- **Killer:** PvP modes and competitive servers

**Problem 3 Example:**
- **Mechanic:** "Jump on platforms that disappear 2 seconds after landing"
- **Dynamics:** Player must move quickly, can't stay on one platform; forces constant forward momentum
- **Aesthetics:** Panic, urgency, adrenaline

</details>
