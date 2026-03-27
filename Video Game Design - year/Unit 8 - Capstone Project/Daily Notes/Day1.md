# Day 1: Capstone Introduction — Project Options & Rubric

**Session Goal:** Understand the capstone requirements, explore project options, and begin thinking about your game concept.

---

## Today's Focus

Welcome to the capstone unit — the biggest project of the year! Over the next 25 days you will design, build, test, and present a complete, original video game using everything you've learned in Units 1–7. Today is about understanding what's expected and starting to dream big (then scoping it down).

---

## Work Session Agenda

**Minutes 0-10:** Teacher introduces capstone overview. Class discussion: "What makes a game actually fun to finish making?"

**Minutes 10-40:** Read through all five project options and the full rubric below. Browse examples of each type on itch.io (if internet available). Begin brainstorming your concept — write down at least 3 game ideas with a one-sentence description each.

**Minutes 40-55:** Share your top idea with a partner. Partner gives one positive and one "scope check" (is it achievable in ~15 work days?). Record partner feedback.

---

## Project Options

### Option 1: 2D Platformer
A side-scrolling game where the player jumps between platforms, avoids or defeats enemies, and reaches a goal.

**Minimum Requirements:**
- Player movement: run left/right, jump (with coyote time or jump buffer)
- At least 3 enemies with basic AI (patrol or chase)
- At least 2 complete levels + a main menu
- Collectibles (coins, stars) with a score or counter
- Health system with UI health bar
- Win and lose conditions (reach exit = win; health = 0 = lose/respawn)

### Option 2: Top-Down Shooter / Adventure
Player moves in 8 directions, exploring or surviving wave-based combat.

**Minimum Requirements:**
- 8-directional movement with animation
- At least 2 enemy types with different behaviors
- Shooting mechanic with visual feedback (muzzle flash, impact particles)
- Score system and HUD
- At least 3 waves or 2 explorable areas
- Health system with UI

### Option 3: Puzzle Game
An original puzzle mechanic applied across multiple levels with increasing difficulty.

**Minimum Requirements:**
- Clear, original core mechanic (not just a clone — add a twist)
- At least 5 puzzle levels
- Visual feedback for correct/incorrect actions
- Level select or progression menu
- Win screen for each level + overall completion screen
- At least one "aha moment" difficulty spike

### Option 4: Endless Runner
A continuously scrolling game where obstacles are generated procedurally.

**Minimum Requirements:**
- Procedural obstacle spawning with object pooling
- Progressive difficulty (speed increases over time)
- High score system saved with PlayerPrefs
- At least 3 obstacle types
- Particle effects for death/milestone
- Main menu and game-over screen

### Option 5: Custom Concept
Your own original idea — requires teacher approval.

**Minimum Requirements:**
- Meets complexity of Option 1–4 (not simpler)
- GDD submitted and approved by Day 4
- At least 2 scenes, working win/lose, UI, and some form of enemies/challenges

---

## Full Project Rubric (100 Points)

| Category | Points | What Graders Look For |
|---|---|---|
| **Technical Implementation** | 40 | Player movement, physics, collision, scripts working correctly |
| **Game Design Quality** | 25 | Fun to play, clear rules, balanced challenge, feedback to player |
| **Polish & Presentation** | 20 | Audio, particles, menus, art consistency, build runs without errors |
| **Documentation** | 15 | Code comments, GDD, in-editor README, known bugs list |

---

## Technical Tips

```csharp
// This capstone builds on everything! Quick reminder of core patterns:

// Movement (Unit 4)
rb.velocity = new Vector2(moveInput * speed, rb.velocity.y);

// Collision detection (Unit 3)
void OnCollisionEnter2D(Collision2D col) {
    if (col.gameObject.CompareTag("Enemy")) TakeDamage(1);
}

// UI update (Unit 5)
scoreText.text = "Score: " + score;

// Scene loading (Unit 5)
SceneManager.LoadScene("GameOver");
```

---

## Reflection / Exit Ticket

1. Which project option are you leaning toward? Why?
2. What's one feature you're excited to build? What's one you're worried about?

---

## Progress Checklist

- [ ] Read all 5 project options
- [ ] Read the full rubric
- [ ] Wrote down 3 game ideas
- [ ] Got partner feedback on your top concept
- [ ] Narrowed to 1–2 favorites
