# Day 18: Level Design & Grayboxing

**Learning Target:** Apply level design principles to create engaging challenges that teach players through play without explicit instructions.

### Key Concepts

- **Level Design:** Creating challenges and teaching players through play
- **Onboarding:** Teaching mechanics early without tutorials
- **Grayboxing:** Using simple placeholder shapes to prototype level layouts
- **Pacing:** Varying difficulty to maintain engagement
- **Progression:** Gradually introducing new challenges
- **Learning Curve:** How quickly players master mechanics
- **Feedback:** Clear signals for what's allowed/forbidden
- **Safe Zone:** Area where players can practice without punishment

### Content

Great level design teaches through play. Players learn by doing, not by reading.

**Teaching Through Play:**
- First level: Introduce jumping
- Second level: Combine jumping + obstacles
- Third level: Add enemies; avoid while jumping
- Fourth level: Combine all mechanics; increase pressure

Players learn by experiencing consequences. A hazard spike teaches "don't touch!" without explanation.

**Grayboxing:**
Grayboxing is building levels with placeholder geometry (gray cubes, boxes) before adding final art. This lets you:
- Test gameplay quickly
- Adjust difficulty and pacing
- Iterate without waiting for artists
- Focus on mechanics, not visuals

Create a level with:
1. A safe starting area
2. Introduce one mechanic
3. Practice zone
4. Challenge zone
5. Safe end area

**Pacing:**
Vary difficulty to maintain engagement:
- Easy section to relax
- Medium section to engage
- Hard section for challenge
- Easy section to celebrate victory

### Code Examples

```csharp
using UnityEngine;

public class LevelManager : MonoBehaviour
{
    [System.Serializable]
    public class LevelProgression
    {
        public int levelNumber = 1;
        public float baseEnemySpeed = 2f;
        public int numEnemies = 1;
        public float timeLimit = 60f;
    }

    public LevelProgression[] levels;
    private int currentLevelIndex = 0;

    void Start()
    {
        LoadLevel(0);
    }

    void LoadLevel(int index)
    {
        if (index >= levels.Length)
        {
            Debug.Log("All levels complete!");
            return;
        }

        currentLevelIndex = index;
        LevelProgression levelData = levels[index];

        Debug.Log($"Loading Level {levelData.levelNumber}");
        Debug.Log($"Difficulty: {levelData.baseEnemySpeed}x speed, {levelData.numEnemies} enemies");
        Debug.Log($"Time limit: {levelData.timeLimit} seconds");

        // Spawn enemies based on level difficulty
        SpawnEnemies(levelData.numEnemies, levelData.baseEnemySpeed);
    }

    void SpawnEnemies(int count, float speed)
    {
        for (int i = 0; i < count; i++)
        {
            Debug.Log($"Spawning enemy {i + 1} with speed {speed}");
            // In a real game, instantiate enemy prefab here
        }
    }

    public void CompleteLevel()
    {
        Debug.Log("Level complete!");
        if (currentLevelIndex < levels.Length - 1)
        {
            LoadLevel(currentLevelIndex + 1);
        }
        else
        {
            Debug.Log("Game complete!");
        }
    }

    // Graybox level structure:
    // 1. Safe starting zone (player learns controls)
    // 2. Tutorial zone (single mechanic practiced)
    // 3. Challenge zone (increased difficulty)
    // 4. Mastery zone (all mechanics combined)
    // 5. Safe ending zone (celebration)
}
```

### Guided Practice

**Activity:** Design a graybox level layout on paper

Create a simple platformer level with 5 sections:
1. **Safe Start** — Flat area for movement practice (1 second to cross)
2. **Jump Tutorial** — 2 small gaps to jump over
3. **Practice** — 3 medium gaps with increasing spacing
4. **Challenge** — 2 large gaps + 1 enemy to avoid
5. **Safe End** — Platform with exit door

Sketch this on paper or describe it with coordinates. Write how each section teaches or challenges the player.

### Practice Problems

**Problem 1 — Beginner:** Create a 3-section level (Start → Practice → Challenge) that teaches jumping without words.

**Problem 2 — Intermediate:** Design a level that teaches 2 mechanics: jumping AND collecting items. Show how each section builds on the previous.

**Problem 3 — Challenge:** Write a detailed level design document for a 5-section platformer level, explaining the learning progression and pacing.

<details>
<summary>Hints</summary>

**Problem 1:** Think simple. Start: empty floor. Practice: one gap. Challenge: two gaps closer together.

**Problem 2:** Separate the mechanics. One section for each. Then combine them.

**Problem 3:** Describe each section with: goal, difficulty, what players learn, what could be frustrating. Include a pacing description.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
- **Start Section:** Flat platform with no obstacles. Player learns to move left/right.
- **Practice Section:** 3 small gaps (1 unit wide) with time to recover between each.
- **Challenge Section:** 2 larger gaps (2 units wide) close together. Player must chain jumps.

**Problem 2:**
- **Section 1:** Flat floor with coins scattered. Learn collecting (no jumping yet).
- **Section 2:** Small platforms with no coins. Learn jumping.
- **Section 3:** Platforms with coins. Jump to reach coins. Combine both mechanics.
- **Section 4:** Multiple gaps with coins hard to reach. Challenge section.

**Problem 3:**
See the "Graybox level structure" comment in the code example above. Expand it with specifics about enemy placement, item locations, timing requirements, and explicit learning goals for each zone.

</details>
