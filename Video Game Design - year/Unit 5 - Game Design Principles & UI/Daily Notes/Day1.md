# Day 1: Game Design Theory—MDA Framework

**Learning Target:** I can identify and apply the MDA (Mechanics, Dynamics, Aesthetics) framework to analyze game design.

---

## Key Concepts

**MDA Framework** breaks down games into three layers:
- **Mechanics**: The rules and systems (jump height, enemy spawn rate, damage formula)
- **Dynamics**: What happens when mechanics interact (players experiment with jump timing to avoid enemies)
- **Aesthetics**: The emotional experience (tension, accomplishment, surprise, fun)

The key insight: *designers control mechanics, but players experience aesthetics through dynamics*. A small tweak to jump height (mechanic) changes how a player feels (aesthetic) because it changes how they play (dynamic).

**Flow State** (Csikszentmihalyi): Players perform best when challenge matches skill. Too easy = boredom. Too hard = frustration. Perfect = flow.

**Player Motivation** (Bartle taxonomy):
- Achievers: want to win, reach goals, get high scores
- Explorers: want to discover secrets, see what's in the world
- Socializers: want to play with others, cooperate
- Killers: want to dominate, show skill over others

---

## Code Example

```csharp
using UnityEngine;

// Not actual game code—but this shows how a mechanic affects dynamics/aesthetics
public class JumpMechanicsDemo : MonoBehaviour
{
    public float jumpForce = 5f;        // MECHANIC: designer controls
    private bool isGrounded = true;

    // In Update(), we CONTROL the mechanic
    // But the DYNAMIC is how the player feels when using it
    // And the AESTHETIC is whether it feels satisfying

    public void Jump()
    {
        if (isGrounded)
        {
            // Increasing jumpForce changes the dynamic (higher jump = more air control)
            // Which changes the aesthetic (feels floatier, more "Super Mario-ish")
            GetComponent<Rigidbody2D>().velocity = Vector2.up * jumpForce;
            isGrounded = false;
        }
    }
}
```

---

## Unity Setup Steps

This is a theory day—no new Unity systems. But let's think like a designer:

1. Open a recent game project
2. Play for 5 minutes, noting:
   - What's one mechanic you interact with every second?
   - How does that mechanic make you feel?
   - Is it challenging, easy, or perfect?
3. Identify: What would change in dynamics if the designer tweaked that mechanic by 50%?

---

## Guided Practice

1. **Analyze Flappy Bird**:
   - Mechanics: Gravity, jump force, pipe gaps
   - Dynamics: Rapid decision-making, tension
   - Aesthetics: Frustration, urgency, quick victories

2. **Modify the dynamic**: What if gravity was 50% weaker?
   - The mechanic changed slightly, but what dynamics change?
   - What would the new aesthetic feel like? (Answer: more forgiving, less urgency)

3. **Apply to your own game**: Pick one mechanic from a project you've worked on.
   - Write it down (e.g., "enemy patrol speed = 3 units/sec")
   - Predict: if I doubled it, what dynamics change?
   - Predict: would it be more fun? Why?

---

## Practice Problems

**Beginner:**
In Mario, the jump is not instantaneous—you hold the button longer for a higher jump. Is this a mechanic or dynamic? Why?

**Intermediate:**
Design a game where the only mechanic is "player moves left/right" and "enemies spawn randomly." Write out 3 different aesthetics you could create by changing dynamics (not mechanics).

**Challenge:**
Take a mobile game you've played. Identify one monetization mechanic (like energy/stamina). How does that mechanic create dynamics that push players toward buying? What aesthetic experience are they trying to create?

<details><summary>💡 Hints</summary>
- Beginner: Is it something the designer directly controls, or is it what the player experiences?
- Intermediate: Think about spawn rate, enemy color, enemy speed—these aren't new mechanics, just different dynamics from the same rules
- Challenge: What feeling do they want you to have when you run out of energy?
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:** It's a mechanic—the designer controls jump height through button press duration. The dynamic is that players learn to time their press. The aesthetic is satisfying control.

**Intermediate:** Same mechanics, three aesthetics:
1. Slow spawn, weak enemies → peaceful exploration
2. Fast spawn, strong enemies → survival horror
3. Random spawns with visual tells → puzzle-solving (predicting patterns)

**Challenge:** The stamina mechanic creates a dynamic where players hit a hard stop. The aesthetic is FOMO (fear of missing out) + frustration, which pushes monetization. They want you to feel like you're "wasting" the game's potential while waiting.
</details>
