# Days 34-36: Final Polish, Build & Presentation

**Learning Target:** Finalize your game, prepare it for distribution, and deliver a professional presentation.

### Key Concepts

- **Build Settings:** Configuring project for export
- **WebGL Export:** Building for web browser
- **Scene List:** Organizing all scenes in build
- **Optimization:** Reducing file size and improving performance
- **Presentation:** Showing your work to others
- **Reflection:** Analyzing what you learned
- **Documentation:** README files and guides
- **Retrospective:** What went well, what didn't, what you'd change

### Content

**Build Settings:**
1. File > Build Settings
2. Add all scenes to build
3. Set initial scene to menu
4. Choose WebGL platform
5. Configure player settings (game name, icon, etc.)
6. Build and test

**Optimization:**
- Remove unused assets
- Compress textures
- Limit particle effects
- Use object pooling
- Profile with Profiler window

**Presentation Outline:**
1. **Title Slide** – Game name, your name, date
2. **Gameplay Demo** – Play the game
3. **Design Highlights** – What makes this game unique
4. **Technical Challenges** – What was hard, how you solved it
5. **Playtesting Results** – What players said
6. **Reflection** – What you learned, what you'd change
7. **Code Example** – Show interesting code (state machine, health system, etc.)
8. **Future Plans** – What you'd add with more time

### Code Examples

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class BuildAndDeployManager : MonoBehaviour
{
    // BUILD & DEPLOYMENT: Prepare game for final submission

    /*
    BUILD CHECKLIST:
    [ ] All scenes added to Build Settings
    [ ] Splash screen configured
    [ ] Game icon set
    [ ] Initial scene set to MainMenu
    [ ] WebGL quality settings configured
    [ ] All bugs fixed and tested
    [ ] Performance profiled and optimized
    [ ] Audio levels balanced
    [ ] Pause menu works
    [ ] Settings persist (PlayerPrefs)
    [ ] High score persists
    [ ] Game has clear win/lose conditions
    [ ] Controls are responsive
    [ ] No console errors
    */

    public static void BuildChecklist()
    {
        Debug.Log("BUILD CHECKLIST:");
        Debug.Log("[ ] All scenes organized in Build Settings");
        Debug.Log("[ ] WebGL export configured");
        Debug.Log("[ ] All assets optimized");
        Debug.Log("[ ] No memory leaks");
        Debug.Log("[ ] Playtested and polished");
        Debug.Log("[ ] Documentation complete");
        Debug.Log("[ ] Build successful and tested");
    }
}

// Example Game Design Document for presentation
public class CapstoneProjectGDD : MonoBehaviour
{
    /*
    CAPSTONE PROJECT PRESENTATION STRUCTURE
    ========================================

    GAME: "My Game Title"
    DEVELOPER: [Your Name]
    DATE: [Current Date]

    1. OVERVIEW
    -----------
    Brief description of the game in 2-3 sentences.

    2. DESIGN PILLARS
    -----------------
    - What makes this game special?
    - Core mechanic
    - Target audience

    3. TECHNICAL IMPLEMENTATION
    ---------------------------
    - Key systems (Health, AI, Physics, UI)
    - Design patterns used (Singleton, State Machine, etc.)
    - Challenges faced and solutions

    4. PLAYTESTING RESULTS
    ----------------------
    - Average fun rating: _/10
    - Most enjoyed feature:
    - Main feedback:
    - Iterations made:

    5. REFLECTION
    -------------
    - What went well?
    - What was challenging?
    - What would you improve?
    - What did you learn?

    6. FUTURE ROADMAP
    -----------------
    - Features to add
    - Optimizations to make
    - Polish improvements
    */

    public string gameTitle = "My Capstone Game";
    public string developerName = "[Your Name]";

    public string[] designPillars = new string[]
    {
        "Fast-paced gameplay",
        "Satisfying feedback",
        "Progressive difficulty"
    };

    public string[] achievements = new string[]
    {
        "Implemented state machine for enemy AI",
        "Created modular health system",
        "Built complete UI system",
        "Playtested with 5+ players"
    };

    public string[] lessonsLearned = new string[]
    {
        "Scope management is critical",
        "Playtesting feedback is invaluable",
        "Polish matters more than features",
        "Code organization prevents bugs"
    };

    public void PrintPresentation()
    {
        Debug.Log("=== CAPSTONE PROJECT PRESENTATION ===");
        Debug.Log("Game: " + gameTitle);
        Debug.Log("Developer: " + developerName);
        Debug.Log("");

        Debug.Log("DESIGN PILLARS:");
        foreach (string pillar in designPillars)
        {
            Debug.Log("  - " + pillar);
        }

        Debug.Log("");
        Debug.Log("KEY ACHIEVEMENTS:");
        foreach (string achievement in achievements)
        {
            Debug.Log("  - " + achievement);
        }

        Debug.Log("");
        Debug.Log("LESSONS LEARNED:");
        foreach (string lesson in lessonsLearned)
        {
            Debug.Log("  - " + lesson);
        }
    }
}
```

### Guided Practice

1. Complete the build checklist
2. Configure Build Settings (add scenes, set initial scene)
3. Profile your game for performance issues
4. Fix any remaining bugs
5. Test the WebGL build thoroughly
6. Create presentation slides
7. Practice your presentation
8. Write reflection document

### Practice Problems

**Task 1:** Complete all items in the build checklist and prepare a clean build.

**Task 2:** Create a presentation with all 8 sections covering your game design and technical implementation.

**Task 3:** Write a 1-2 page reflection document on your capstone project.

<details>
<summary>Hints</summary>

**Task 1:** Go through each checklist item methodically. Fix any issues before building.

**Task 2:** Create visual slides showing gameplay, design decisions, and technical challenges. Include code examples and playtesting data.

**Task 3:** Reflect on: What went well? What was hard? What would you do differently? What did you learn? What would you add?

</details>

<details>
<summary>Sample Answers</summary>

**Sample Presentation Outline:**
1. Title: "Asteroid Blast" by [Name]
2. Gameplay demo (30 seconds of actual play)
3. Design: Fast-paced arcade action, simple controls, escalating difficulty
4. Technical: State machine for enemy AI, Health system, GameManager singleton
5. Playtesting: 5 players, avg 7.2/10 fun rating, feedback: "needs more levels"
6. Reflection: Learned scope management, playtesting value, importance of polish
7. Code: Show state machine example
8. Future: Multiple difficulty levels, power-ups, leaderboard

**Sample Reflection:**
- Best decision: Built MVP first, then added features
- Hardest part: Balancing difficulty
- What I'd change: More playtesting earlier
- Most important lesson: Polish matters more than features

</details>
