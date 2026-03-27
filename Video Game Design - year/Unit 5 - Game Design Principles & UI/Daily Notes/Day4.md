# Day 4: Level Design—Visual Language & Tutorial Design

**Learning Target:** I can use visual language and structured tutorials to guide players without text.

---

## Key Concepts

**Visual Language**: Colors, shapes, and sounds communicate meaning:
- **Safe**: Bright colors (green, blue), smooth geometry, calm music
- **Dangerous**: Red, sharp edges, spikes, intense music
- **Interactive**: Glowing, highlighted, buttons with visual feedback
- **Hidden**: Slightly darker, requires exploration to find

**Tutorials**: Show, don't tell.
- Demo the mechanic (player watches)
- Let player practice consequence-free
- Gradually introduce risk
- Remove training wheels only when players are ready

**Level Gating**: Block access to dangerous areas until player masters the safe zone. Use visual barriers (locked doors, cliffs, lava) that aren't arbitrary.

---

## Code Example

```csharp
using UnityEngine;

public class VisualLanguageSystem : MonoBehaviour
{
    public enum Hazard { Spike, Lava, Enemy, Unknown }
    
    public class VisualElement
    {
        public Hazard type;
        public Color warningColor;
        public AudioClip warningSound;
        public ParticleSystem warningEffect;
    }

    // In practice, you'd set these in the Inspector or asset definitions
    public void SetupVisualLanguage()
    {
        // Spikes: Red, sharp shape, piercing sound
        // Lava: Orange/Red, wavy animation, crackling sound
        // Enemy: Red eyes, threatening stance, growling sound
        
        // The VISUAL tells the player "danger" before they interact with it
    }
}
```

---

## Unity Setup Steps

1. Create a simple level with safe and dangerous areas
2. **Safe zone**:
   - Use bright green material for floor
   - No enemies
   - Place a simple tutorial marker (text or image)
3. **Danger zone**:
   - Use red material for hazards (spikes, lava)
   - Add a particle effect (sparks, bubbles) to indicate danger
   - Place an enemy with obvious visual threat (color, animation)
4. Test: Does a new player instantly understand which areas are safe?

---

## Guided Practice

1. **Color Code a Level**: Open a level you've built.
   - Recolor all safe zones bright green
   - Recolor all dangerous zones red
   - Does it feel intuitive?

2. **Design a Tutorial Sequence**: Create a simple tutorial that teaches "jump."
   - Platform 1: Static ground. Player can't fall off. Demo: show jump height
   - Platform 2: Jump over a small gap (not deadly—landing in gap just slides player back)
   - Platform 3: Jump over a real gap (fail = restart from checkpoint)
   - Platform 4: Chain jumps to reach the goal

3. **Add Audio Cues**: For each zone, assign a different tone:
   - Safe zone: calm, melodic
   - Challenge: tense, rhythmic
   - Reward: celebratory

---

## Practice Problems

**Beginner:**
You've created a spike trap. How would you visually signal to a player (without text) that it's dangerous?

**Intermediate:**
Design a tutorial for the "shield" mechanic. Write out 4 steps where player learns progressively with increasing risk.

**Challenge:**
Analyze the opening tutorial of a game you know (Zelda, Celeste, Mario). How does it balance showing, letting player practice, and avoiding text? What would make it better?

<details><summary>💡 Hints</summary>
- Beginner: Think of real-world danger signals (red, spikes, movement, sound, particles)
- Intermediate: No risk → low risk → medium risk → high risk. Each step should teach, not punish
- Challenge: Good tutorials are invisible—players don't realize they're learning
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:** Red color, pointy geometry, particle effect (sparks), harsh sound effect, animation (pulsing or rotating). Maybe an NPC pointing and saying "ouch!" once.

**Intermediate:**
1. Safe: Shield appears on player, no enemies, message: "You have a shield!"
2. Low risk: One weak enemy approaches slowly, player can raise shield (button demo)
3. Medium risk: Enemy attacks, block and counter
4. High risk: Multiple fast enemies, player must manage shield durability

**Challenge:** Most good tutorials are integrated into level design. Instead of a "tutorial level," the first level teaches as you play. The best remove all guidance once players prove they understand.
</details>
