# Day 2: Game Design Theory—Challenge vs Skill & Flow

**Learning Target:** I can apply challenge scaling to keep players in a flow state.

---

## Key Concepts

**Challenge vs Skill Balance** (Flow Diagram):
- **Too Easy (below skill level)**: Player feels bored, disengaged, will leave
- **Flow Zone (matched to skill)**: Optimal play—focused, satisfied, wants to continue
- **Too Hard (above skill level)**: Player feels frustrated, gives up, loses confidence

**Difficulty Curve**: As players improve (skill rises), challenge must rise too. Failing to scale difficulty leads to boredom in the second half of a game.

**Progression Mechanics**:
- Introduce new enemy types every 5-10 levels
- Increase enemy count gradually
- Add new mechanics (ice-floor, moving platforms) to refresh the challenge
- Reward mastery (speedrun modes, harder difficulties)

**Game Feel in Difficulty**: Make failure *almost* avoidable—player needs to see the winning move, but executing it requires skill. Cheap, unavoidable deaths are frustrating, not challenging.

---

## Code Example

```csharp
using UnityEngine;

public class DifficultyScaler : MonoBehaviour
{
    public int playerLevel = 1;
    private float baseEnemyHealth = 10f;
    private float baseEnemySpeed = 2f;

    // Challenge scales with player progression
    public float GetScaledEnemyHealth()
    {
        // Each level, enemies get slightly tougher
        return baseEnemyHealth + (playerLevel * 2f);
    }

    public float GetScaledEnemySpeed()
    {
        // Speed increases slowly to maintain flow
        return baseEnemySpeed + (playerLevel * 0.3f);
    }

    // Called when player completes a level
    public void LevelUp()
    {
        playerLevel++;
        Debug.Log($"Player leveled up! Difficulty now {playerLevel}");
        // Next enemies will be tougher, but not impossible
    }
}
```

---

## Unity Setup Steps

No new systems today—this is design thinking. But you can set up a simple test:

1. Open a platformer or combat game you've built
2. Note your current score/level progression
3. Does difficulty increase smoothly, or is there a sudden jump?
4. Interview a tester: "Did you ever feel bored? Frustrated?" where?
5. Plan 3 specific difficulty adjustments based on feedback

---

## Guided Practice

1. **Create a Difficulty Chart**: Pick a game you know well (Cuphead, Dark Souls, Mario).
   - Draw a graph: X-axis = time played, Y-axis = challenge level
   - Mark where you felt bored, where you were in flow, where you got frustrated

2. **Identify the mechanic**: What single change caused each difficulty shift?
   - (Example: "At level 5, the game introduced ice floors—suddenly I had to recalibrate timing")

3. **Apply to your game**: Plan 5 difficulty milestones for a 10-level game.
   - Level 1-2: Learn controls (low challenge)
   - Level 3-4: Master basics (medium challenge)
   - Level 5-7: New mechanics introduced (challenge rises)
   - Level 8-10: Mastery test (high challenge, but fair)

---

## Practice Problems

**Beginner:**
You've created a platformer. Players say levels 1-5 are "too easy," but level 6 is "impossible." How would you fix this using challenge scaling?

**Intermediate:**
Design a progression system for an enemy type. Start with "basic goblin" and evolve it over 10 levels. Write out what changes at level 3, 6, and 9.

**Challenge:**
Analyze a mobile game you've played (Candy Crush, Flappy Bird, Subway Surfers). Identify: What's the intended player skill curve? At what point did *you* hit frustration? Could the curve be smoother?

<details><summary>💡 Hints</summary>
- Beginner: You need intermediate difficulty steps between 5 and 6. What if you added levels 5.5?
- Intermediate: Think beyond just health/speed. Add new abilities, new attack patterns, new environmental hazards
- Challenge: Note when new game mechanics are introduced—those are intentional challenge jumps
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:** Add intermediate levels (5.5, 5.7) with gradually increasing challenge. Or redesign level 6 to teach its mechanic before demanding mastery.

**Intermediate:** 
- Level 1-2: Goblin walks, attacks slowly
- Level 3: Goblin has higher health, attacks faster
- Level 6: Goblin has a shield, can dodge
- Level 9: Goblin summons allies, has area attack

**Challenge:** Most games introduce small difficulty jumps every 3-5 plays. When frustration hits, it's often because a NEW mechanic was added without a tutorial level. The curve could be smoother by teaching new enemy types in isolation before combining them.
</details>
