# Day 3: Level Design Principles—Safe, Challenge, Reward Loop

**Learning Target:** I can apply the safe→challenge→reward loop to design engaging levels.

---

## Key Concepts

**Safe → Challenge → Reward Loop**: Every level should cycle through:
1. **Safe Zone**: Player catches breath, understands new mechanic in isolation
2. **Challenge Zone**: Player applies the mechanic in a dangerous scenario
3. **Reward Zone**: Victory, next level, story reveal, loot—the payoff

This loop repeats multiple times per level. Too much safety = boring. Too much challenge = frustrating. Perfect balance keeps players engaged.

**Tutorial Design**:
- Show mechanic in isolation (safe zone)
- Let player practice without consequence
- Then introduce the challenge
- Never dump 5 mechanics at once

**Visual Language**: Danger should LOOK dangerous (red, sharp edges, scary sounds). Safety should look safe (bright, smooth, calm sounds).

---

## Code Example

```csharp
using UnityEngine;

public class LevelZoneManager : MonoBehaviour
{
    // Conceptually, a level is divided into zones
    public enum ZoneType { Safe, Challenge, Reward }
    
    public class LevelZone
    {
        public ZoneType type;
        public Transform startPoint;
        public Transform endPoint;
        public string description; // "Learn to jump" vs "Dodge enemies"
    }

    private LevelZone[] zones = new LevelZone[3];

    // In design, you'd structure a level like:
    // Zone 0: Safe - introduce jump mechanic, no enemies
    // Zone 1: Challenge - use jump to avoid moving platforms
    // Zone 2: Reward - reach the goal, play victory animation
}
```

---

## Unity Setup Steps

1. Open or create a simple 2D level
2. Divide the level into 3 sections on paper:
   - **Safe**: First 30 seconds, teach one new mechanic
   - **Challenge**: Middle section, force the player to use it under pressure
   - **Reward**: End section, clear path to victory
3. Place visual markers (colored cubes, sprites) at zone boundaries
4. Test: Do new players understand the mechanic by the challenge zone?

---

## Guided Practice

1. **Analyze a Level You Know**: Play through a level from a game you enjoy.
   - Mark where you see Safe → Challenge → Reward zones
   - How many loops are there per level?

2. **Design a Level**: Create a simple platformer level on paper.
   - Safe Zone (10 seconds): Platform with one jump, no enemies
   - Challenge Zone (30 seconds): Use jump to avoid enemies on moving platforms
   - Reward Zone (10 seconds): Jump to goal

3. **Implement Checkpoints**: Add a waypoint at each zone boundary.
   - Use empty GameObjects as markers
   - Confirm the pacing feels right

---

## Practice Problems

**Beginner:**
A level teaches the "dash" mechanic in a safe zone. But then the challenge zone requires dashing AND jumping. Is this good design? Why or why not?

**Intermediate:**
Design the first 3 zones of a game that teaches: (1) movement, (2) jumping, (3) enemy avoidance. Write 2-3 sentences for each zone.

**Challenge:**
Analyze a game tutorial level. Identify where it could cause frustration. How would you redesign it to keep the challenge curve smoother?

<details><summary>💡 Hints</summary>
- Beginner: One new mechanic per safe zone. Combining two mechanics means players are learning both simultaneously—that's Challenge, not Safe
- Intermediate: Each zone should feel like a complete "loop" before moving to the next
- Challenge: Look for moments where multiple new concepts are introduced without practice
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:** Not great design. The challenge zone should practice dash FIRST, then add jumping later. Combining both means the player is learning two things at once.

**Intermediate:**
- Zone 1 (Safe): Open area, no enemies. Press arrow keys to move. Goal: reach the right side
- Zone 2 (Challenge): Platforms with gaps. Use jump to cross. No enemies yet. Goal: reach the top
- Zone 3 (Reward): One slow enemy walks back and forth. Player must time a jump to dodge it. Goal: reach the exit

**Challenge:** Many tutorials fail because they teach too much before letting players play. A better design: teach movement in isolation (safe), then add one enemy (challenge), then give victory (reward)—all in the first level.
</details>
