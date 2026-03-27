# Unit 8: Capstone Project

## Unit Overview

**Duration:** Days 29-36 (8 days)
**Key Concepts:** Game Design Document, MVP planning, prototyping, integration, playtesting, polish, presentation
**Big Idea:** Creating a complete game requires planning, iteration, and feedback. The capstone project brings together all course concepts: design, programming, systems, and user feedback.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Write a comprehensive Game Design Document (GDD)
- [ ] Define MVP (Minimum Viable Product) and scope management
- [ ] Build and iterate on a core game mechanic prototype
- [ ] Integrate multiple systems into a cohesive game
- [ ] Use GetComponent to communicate between systems
- [ ] Create and manage game content (art, audio, particles)
- [ ] Conduct playtesting and gather structured feedback
- [ ] Iterate based on feedback and data
- [ ] Polish games with juicy effects and responsiveness
- [ ] Prepare build settings and export to WebGL
- [ ] Present your game with a demo and reflection

---

## Day-by-Day Content

### Day 29: Game Design Document & Scope

#### Key Concepts
- **Game Design Document (GDD):** Written specification of the game
- **Elevator Pitch:** One-sentence description of the game
- **Core Loop:** The repeating gameplay cycle
- **MVP (Minimum Viable Product):** Smallest feature set to make a playable game
- **Feature List:** All intended features, organized by priority
- **Scope Management:** Deciding what to include and what to cut
- **Prototype Phase:** Testing core mechanics before full development
- **Design vs. Implementation:** Documented design vs. actual code

#### Content
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

#### Annotated Code Example

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

---

### Day 30: Prototyping Core Mechanic

#### Key Concepts
- **Prototype:** Working implementation of the core idea
- **Rapid Iteration:** Quick test-build-feedback cycle
- **Grayboxing:** Minimal visuals, focus on gameplay
- **Playtesting Early:** Test with actual players ASAP
- **Fail Fast:** Discover if the core mechanic is fun quickly
- **Vertical Slice:** Complete (but small) feature set showing full game
- **Mechanics Testing:** Ensuring core mechanic feels good

#### Content
The core mechanic is the most important part. If the core mechanic isn't fun, the game won't be fun. Prototype it first, test it, iterate on it.

**Prototyping Steps:**
1. Implement core mechanic (simplest possible version)
2. Add basic visuals (grayboxing)
3. Test internally (does it feel good?)
4. Get feedback (ask a friend to play)
5. Iterate based on feedback
6. Repeat until core mechanic is fun

**Vertical Slice:**
A small, complete version of the game showing all systems:
- Player movement works
- Enemy AI works
- Scoring works
- Win condition works
- All in one simple level

The vertical slice proves the game's concept works before expanding to more content.

#### Annotated Code Example

```csharp
using UnityEngine;

public class CoreMechanicPrototype : MonoBehaviour
{
    // PROTOTYPE: Minimal implementation of core mechanic
    // Focus: Does the core mechanic FEEL GOOD?
    // Visuals: Grayboxed (simple cubes/spheres)
    // Complexity: Stripped down to bare essentials

    [Header("Core Mechanic Settings")]
    public float moveSpeed = 5f;
    public float rotationSpeed = 100f;
    public int startingHealth = 100;

    [Header("Quick Prototyping")]
    public bool debugMode = true;  // Show debug info
    public bool instantWin = false;  // Skip to win screen (for testing)
    public bool instantLose = false;  // Skip to lose screen (for testing)

    private Rigidbody rb;
    private int currentHealth;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
        currentHealth = startingHealth;

        if (debugMode)
            Debug.Log("PROTOTYPE MODE: Core mechanic test. Focus on feel, not visuals.");
    }

    void Update()
    {
        // Test core mechanic input
        TestCoreInput();

        // Debug shortcuts for rapid iteration
        if (instantWin)
            OnWin();
        if (instantLose)
            OnLose();
    }

    void TestCoreInput()
    {
        // Test movement with arrow keys
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        rb.velocity = new Vector3(horizontal, 0, vertical) * moveSpeed;

        // Test rotation with mouse
        if (Input.GetMouseButton(0))
        {
            Vector3 mouseDir = Input.mousePosition;
            transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
        }

        // Test damage with E key
        if (Input.GetKeyDown(KeyCode.E))
        {
            TakeDamage(10);
        }

        // Test win with W key
        if (Input.GetKeyDown(KeyCode.W))
        {
            OnWin();
        }
    }

    void TakeDamage(int damage)
    {
        currentHealth -= damage;
        Debug.Log("Damage taken. Health: " + currentHealth);

        if (currentHealth <= 0)
        {
            OnLose();
        }
    }

    void OnWin()
    {
        Debug.Log("WIN! Core mechanic feels good!");
        // Load win scene or show message
    }

    void OnLose()
    {
        Debug.Log("LOSE! Ready for next iteration.");
        // Load lose scene or show message
    }

    // Iteration tracking
    public void LogFeedback(string feedback)
    {
        Debug.Log("[FEEDBACK] " + feedback);
        // In a real project, save this to a file for analysis
    }
}
```

---

### Day 31: Systems Integration

#### Key Concepts
- **Integration:** Connecting multiple systems (player, enemies, UI, scoring)
- **GetComponent:** Accessing other components on the same or different GameObjects
- **References:** Storing references to other GameManager, UI elements, etc.
- **Message Passing:** Systems communicating through method calls
- **Event System:** Loosely coupled communication using C# events
- **Dependency Injection:** Passing dependencies into components
- **Testing Integrated Systems:** Ensuring all systems work together

#### Content
As games grow, many systems need to interact:
- Player shoots bullet
- Bullet hits enemy
- Enemy takes damage
- Enemy dies
- GameManager adds score
- UI updates score display

Each step requires communication between systems.

**Communication Methods:**
1. **Direct References:** Get component and call method
2. **Singletons:** Static GameManager instance
3. **Events:** Loosely coupled communication
4. **Messages:** Send messages between objects

**Integration Checklist:**
- [ ] Player controller communicates with animator
- [ ] Enemies receive damage and die
- [ ] Dying enemies reward points
- [ ] GameManager updates score
- [ ] UI reflects score changes
- [ ] Win/lose conditions are checked
- [ ] All systems work together

#### Annotated Code Example

```csharp
using UnityEngine;

// Integration example: Multiple systems working together

public class IntegratedGameManager : MonoBehaviour
{
    // INTEGRATION: Multiple systems communicating

    public static IntegratedGameManager instance { get; private set; }

    private int score = 0;
    private int enemiesDefeated = 0;
    private PlayerController player;
    private UIManager uiManager;

    void Awake()
    {
        instance = this;
    }

    void Start()
    {
        // Get references to other systems
        player = FindObjectOfType<PlayerController>();
        uiManager = FindObjectOfType<UIManager>();

        if (player == null)
            Debug.LogError("PlayerController not found!");
        if (uiManager == null)
            Debug.LogError("UIManager not found!");
    }

    void Update()
    {
        // Check win condition
        if (enemiesDefeated >= 5)
        {
            Win();
        }

        // Check lose condition
        if (player != null && !player.IsAlive())
        {
            Lose();
        }
    }

    // Called when enemy dies
    public void OnEnemyDefeated()
    {
        enemiesDefeated++;
        AddScore(100);
        Debug.Log("Enemy defeated! Total: " + enemiesDefeated);
    }

    // Called when player collects item
    public void OnItemCollected(int value)
    {
        AddScore(value);
    }

    // Central score management
    public void AddScore(int points)
    {
        score += points;

        // Notify UI to update
        if (uiManager != null)
        {
            uiManager.UpdateScoreDisplay(score);
        }

        Debug.Log("Score: " + score);
    }

    void Win()
    {
        Debug.Log("You Win! Score: " + score);
        // Transition to win scene
    }

    void Lose()
    {
        Debug.Log("Game Over. Final Score: " + score);
        // Transition to lose scene
    }
}

// Player system
public class PlayerController : MonoBehaviour
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();

        // Register health change event
        if (health != null)
        {
            health.OnHealthChanged += HandleHealthChanged;
        }
    }

    void HandleHealthChanged(int newHealth)
    {
        Debug.Log("Player health changed: " + newHealth);
    }

    public bool IsAlive()
    {
        return health != null && health.IsAlive();
    }
}

// Enemy system
public class EnemyController : MonoBehaviour
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();

        // Register death event
        if (health != null)
        {
            health.OnHealthChanged += CheckIfDead;
        }
    }

    void CheckIfDead(int newHealth)
    {
        if (newHealth <= 0)
        {
            // Notify GameManager
            IntegratedGameManager.instance.OnEnemyDefeated();
        }
    }
}

// UI system
public class UIManager : MonoBehaviour
{
    public TMPro.TextMeshProUGUI scoreText;

    public void UpdateScoreDisplay(int newScore)
    {
        if (scoreText != null)
        {
            scoreText.text = "Score: " + newScore;
        }
    }
}
```

---

### Day 32: Content Creation & Polish

#### Key Concepts
- **Content:** Art, audio, particles, animations
- **Asset Organization:** Folder structure for clean project
- **Placeholder to Final:** Replace graybox with final visuals
- **Audio Design:** Sound effects and music
- **Particle Effects:** Visual feedback for impact
- **Animation Polish:** Smooth transitions and feedback
- **Color Grading:** Visual style and atmosphere
- **User Feedback:** Visual and audio cues for actions

#### Content
Polish transforms a playable game into a satisfying experience. Polish includes:

1. **Visual Polish:**
   - Replace placeholder graphics with final art
   - Smooth animations and transitions
   - Screen shake, particles, color effects
   - Clean UI with consistent styling

2. **Audio Polish:**
   - Sound effects for all actions (jump, land, attack, collect, etc.)
   - Background music
   - Volume levels and mixing
   - Audio feedback for important events

3. **Feedback:**
   - Particle effects for impact
   - Screen shake on collision
   - Color feedback (flash white on hit, red on low health)
   - Haptic feedback (rumble) on impact

#### Annotated Code Example

```csharp
using UnityEngine;
using UnityEngine.Rendering.PostProcessing;

public class GamePolish : MonoBehaviour
{
    // POLISH: Making the game feel great

    [Header("Visual Polish")]
    public ParticleSystem explosionEffect;
    public ParticleSystem jumpEffect;
    public PostProcessVolume postProcessing;

    [Header("Audio Polish")]
    public AudioClip jumpSound;
    public AudioClip landSound;
    public AudioClip collectSound;
    public AudioClip damageSound;
    public AudioClip victoryMusic;

    [Header("Feedback Settings")]
    public float screenShakeStrength = 0.1f;
    public float screenShakeDuration = 0.2f;
    private Camera mainCamera;
    private Vector3 originalCameraPos;

    void Start()
    {
        mainCamera = Camera.main;
        originalCameraPos = mainCamera.transform.position;
    }

    // Jump with polish
    public void JumpWithFeedback()
    {
        Debug.Log("Jump with feedback!");

        // Visual feedback
        if (jumpEffect != null)
        {
            Instantiate(jumpEffect, transform.position, Quaternion.identity);
        }

        // Audio feedback
        if (jumpSound != null)
        {
            AudioSource.PlayClipAtPoint(jumpSound, transform.position);
        }

        // Screen shake on heavy jump
        StartCoroutine(ScreenShake());
    }

    // Land with polish
    public void LandWithFeedback()
    {
        // Audio feedback
        if (landSound != null)
        {
            AudioSource.PlayClipAtPoint(landSound, transform.position);
        }

        // Screen shake on impact
        StartCoroutine(ScreenShake(screenShakeStrength * 0.5f));
    }

    // Collect item with polish
    public void CollectWithFeedback()
    {
        // Visual pop animation
        transform.localScale = new Vector3(1.2f, 1.2f, 1.2f);
        Invoke("ResetScale", 0.1f);

        // Audio feedback
        if (collectSound != null)
        {
            AudioSource.PlayClipAtPoint(collectSound, transform.position);
        }

        // Particle effect
        if (explosionEffect != null)
        {
            Instantiate(explosionEffect, transform.position, Quaternion.identity);
        }
    }

    // Damage with visual feedback
    public void TakeDamageWithFeedback()
    {
        // Flash red
        StartCoroutine(FlashRed());

        // Screen shake
        StartCoroutine(ScreenShake());

        // Audio feedback
        if (damageSound != null)
        {
            AudioSource.PlayClipAtPoint(damageSound, transform.position);
        }
    }

    System.Collections.IEnumerator ScreenShake(float strength = -1)
    {
        if (strength < 0)
            strength = screenShakeStrength;

        float timer = screenShakeDuration;
        while (timer > 0)
        {
            Vector3 shake = Random.insideUnitSphere * strength;
            mainCamera.transform.position = originalCameraPos + shake;
            timer -= Time.deltaTime;
            yield return null;
        }

        mainCamera.transform.position = originalCameraPos;
    }

    System.Collections.IEnumerator FlashRed()
    {
        SpriteRenderer spriteRenderer = GetComponent<SpriteRenderer>();
        if (spriteRenderer == null)
            yield break;

        spriteRenderer.color = Color.red;
        yield return new WaitForSeconds(0.1f);
        spriteRenderer.color = Color.white;
    }

    void ResetScale()
    {
        transform.localScale = Vector3.one;
    }
}
```

---

### Day 33: Playtesting & Feedback

#### Key Concepts
- **Playtesting:** Having actual players test your game
- **Feedback Collection:** Structured questions to gather data
- **Quantitative Data:** Measurable metrics (time to win, deaths, score)
- **Qualitative Feedback:** Opinions and feelings
- **A/B Testing:** Testing two versions to see which is better
- **Iteration:** Using feedback to improve the game
- **Bug Reporting:** Documenting issues for fixing
- **Design Validation:** Proving your design choices are correct

#### Content
Playtesting is where you learn if your game is actually fun. You can't know until real players play it.

**Playtesting Questions:**
1. Is the core mechanic fun?
2. Is the difficulty appropriate?
3. Is the goal clear?
4. Is the control responsive?
5. Did you enjoy the experience? (1-10 rating)
6. What was most fun?
7. What was frustrating?
8. Would you recommend this game?

**Playtesting Session:**
1. Brief player on the goal (1 minute)
2. Player plays (5-10 minutes)
3. Observe (don't help or talk)
4. Ask questions
5. Take notes
6. Repeat with 3-5 players

**Data Analysis:**
- Average fun rating
- Common complaints
- Most praised feature
- Difficulty sweet spot

#### Annotated Code Example

```csharp
using UnityEngine;
using System.Collections.Generic;

public class PlaytestingManager : MonoBehaviour
{
    // PLAYTESTING: Collect data and feedback

    [System.Serializable]
    public class PlaytestSession
    {
        public string playerName;
        public float sessionTime;
        public int finalScore;
        public int deathCount;
        public float funRating;  // 1-10
        public string feedback;
        public bool wouldRecommend;
    }

    private List<PlaytestSession> sessions = new List<PlaytestSession>();
    private PlaytestSession currentSession;
    private float sessionStartTime;
    private int deathCount = 0;

    void Start()
    {
        StartNewSession("Player 1");
    }

    void Update()
    {
        // Track session time
        if (currentSession != null)
        {
            currentSession.sessionTime = Time.time - sessionStartTime;
        }
    }

    public void StartNewSession(string playerName)
    {
        currentSession = new PlaytestSession();
        currentSession.playerName = playerName;
        sessionStartTime = Time.time;
        deathCount = 0;

        Debug.Log("Playtesting session started: " + playerName);
    }

    public void RecordDeath()
    {
        deathCount++;
        if (currentSession != null)
        {
            currentSession.deathCount = deathCount;
        }
    }

    public void EndSession(int finalScore)
    {
        if (currentSession == null)
            return;

        currentSession.finalScore = finalScore;
        sessions.Add(currentSession);

        Debug.Log("Session ended for: " + currentSession.playerName);
        AnalyzeSessions();
    }

    public void RecordFeedback(string playerName, float funRating, string feedback, bool wouldRecommend)
    {
        PlaytestSession session = sessions.Find(s => s.playerName == playerName);
        if (session != null)
        {
            session.funRating = funRating;
            session.feedback = feedback;
            session.wouldRecommend = wouldRecommend;

            Debug.Log($"Feedback recorded for {playerName}: {funRating}/10");
        }
    }

    void AnalyzeSessions()
    {
        if (sessions.Count == 0)
            return;

        // Calculate averages
        float avgTime = 0;
        float avgScore = 0;
        float avgDeaths = 0;
        float avgFunRating = 0;
        int recommendCount = 0;

        foreach (PlaytestSession session in sessions)
        {
            avgTime += session.sessionTime;
            avgScore += session.finalScore;
            avgDeaths += session.deathCount;
            avgFunRating += session.funRating;
            if (session.wouldRecommend)
                recommendCount++;
        }

        avgTime /= sessions.Count;
        avgScore /= sessions.Count;
        avgDeaths /= sessions.Count;
        avgFunRating /= sessions.Count;

        // Report results
        Debug.Log("=== PLAYTESTING ANALYSIS ===");
        Debug.Log("Sessions: " + sessions.Count);
        Debug.Log("Avg Time: " + avgTime.ToString("F1") + "s");
        Debug.Log("Avg Score: " + avgScore.ToString("F0"));
        Debug.Log("Avg Deaths: " + avgDeaths.ToString("F1"));
        Debug.Log("Avg Fun Rating: " + avgFunRating.ToString("F1") + "/10");
        Debug.Log("Would Recommend: " + recommendCount + "/" + sessions.Count);

        // Iteration recommendations
        if (avgFunRating < 5)
            Debug.LogWarning("Core mechanic may not be fun. Iterate!");
        if (avgDeaths > 10)
            Debug.LogWarning("Game is too hard. Reduce difficulty.");
        if (avgTime < 60)
            Debug.LogWarning("Game is too short. Add more content.");
    }

    public List<PlaytestSession> GetSessions()
    {
        return sessions;
    }
}

// Playtesting UI for gathering feedback
public class PlaytestingUI : MonoBehaviour
{
    public void SubmitFeedback(string playerName, float funRating, string feedback, bool wouldRecommend)
    {
        PlaytestingManager manager = FindObjectOfType<PlaytestingManager>();
        if (manager != null)
        {
            manager.RecordFeedback(playerName, funRating, feedback, wouldRecommend);
        }
    }
}
```

---

### Days 34-36: Final Polish, Build & Presentation

#### Key Concepts
- **Build Settings:** Configuring project for export
- **WebGL Export:** Building for web browser
- **Scene List:** Organizing all scenes in build
- **Optimization:** Reducing file size and improving performance
- **Presentation:** Showing your work to others
- **Reflection:** Analyzing what you learned
- **Documentation:** README files and guides
- **Retrospective:** What went well, what didn't, what you'd change

#### Content
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

#### Annotated Code Example

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

---

## Practice Problems

### Comprehensive Capstone Tasks

**Task 1:** Write a complete Game Design Document (2-3 pages) for your capstone game.

<details>
<summary>Requirements</summary>
Include: Title, Elevator Pitch, Core Loop, Win/Lose Conditions, Feature List (Must/Should/Nice), Target Audience, Technical Details, Art Style, Estimated Scope.
</details>

---

**Task 2:** Design and implement the MVP (Minimum Viable Product) for your game.

<details>
<summary>Requirements</summary>
Include: Core mechanic only, one level, basic visuals, win condition, lose condition, score system. Should be completable in 2-3 days.
</details>

---

**Task 3:** Implement all major systems (Player, Enemy AI, Health, Scoring, UI) and integrate them.

<details>
<summary>Requirements</summary>
All systems communicate properly. Enemies die when health = 0. Score updates on enemy death. UI reflects game state.
</details>

---

**Task 4:** Playtest with 3-5 players and document feedback.

<details>
<summary>Requirements</summary>
Collect: Fun rating (1-10), What was fun, What was frustrating, Would recommend (yes/no), Session time, Deaths, Final score. Analyze results.
</details>

---

**Task 5:** Iterate based on playtesting feedback.

<details>
<summary>Requirements</summary>
Make at least 3 changes based on player feedback. Document what changed and why.
</details>

---

**Task 6:** Add polish (particles, sounds, screen shake, animations) to enhance game feel.

<details>
<summary>Requirements</summary>
Include feedback for: Jump, Land, Attack, Damage, Collect, Victory, Defeat. Should feel satisfying.
</details>

---

**Task 7:** Prepare build settings and export to WebGL.

<details>
<summary>Requirements</summary>
Game builds without errors. All scenes included. Playable in web browser. File size under 100MB.
</details>

---

**Task 8:** Create presentation and reflection document (1-2 pages).

<details>
<summary>Requirements</summary>
Include: Design highlights, technical challenges, playtesting results, reflection, lessons learned, future roadmap.
</details>

---

## Capstone Evaluation Rubric

### Gameplay (25 points)
- Core mechanic is clear and fun
- Controls are responsive
- Win/lose conditions exist and work
- Appropriate difficulty progression
- Game provides challenge and satisfaction

### Technical Implementation (25 points)
- Clean, organized code
- Uses design patterns (singleton, state machine, etc.)
- Systems integrate properly
- No bugs or crashes
- Performance is acceptable

### Polish & Game Feel (20 points)
- Visual feedback (particles, animations, effects)
- Audio feedback (sounds, music)
- Responsive controls
- Satisfying feedback loops
- Professional presentation

### Design & Scope (15 points)
- Realistic scope (MVP completed)
- Clear design vision
- Playtesting integrated
- Iterations based on feedback
- Documentation complete

### Presentation (15 points)
- Clear demo of gameplay
- Articulate design decisions
- Honest reflection on challenges
- Shows understanding of concepts
- Professional presentation

---

## Final Checklist

- [ ] Game Design Document complete
- [ ] MVP implemented and tested
- [ ] All major systems integrated
- [ ] Playtesting completed with 3+ players
- [ ] Feedback collected and analyzed
- [ ] Iterations made based on feedback
- [ ] Polish added (particles, sounds, effects)
- [ ] No bugs or crashes
- [ ] Build settings configured
- [ ] WebGL export tested
- [ ] All scenes included in build
- [ ] Code clean and documented
- [ ] Presentation prepared
- [ ] Reflection written
- [ ] README/documentation complete

---

## Vocabulary & Quick Reference

### Project Management Terms

| Term | Definition |
|------|-----------|
| **GDD** | Game Design Document; specification of the game |
| **MVP** | Minimum Viable Product; smallest playable version |
| **Scope** | Amount of work to complete the project |
| **Iteration** | Cycle of build → test → feedback → improve |
| **Vertical Slice** | Complete but small version showing all systems |
| **Prototype** | Working implementation of core mechanic |
| **Playtest** | Real players testing your game |
| **Polish** | Final refinement for quality |
| **Build** | Compiled version for distribution |
| **Reflection** | Analysis of what was learned |

### Build & Export Quick Reference

```csharp
// WebGL Build Checklist
/*
1. File > Build Settings
2. Add all scenes (drag from Hierarchy)
3. Select WebGL platform
4. Configure Player Settings:
   - Company Name
   - Product Name
   - Default Icon
   - Resolution
5. Click "Build"
6. Choose output folder
7. Test in web browser
*/

// Common Build Settings for WebGL
public class BuildSettings
{
    /*
    Quality: Balanced (not ultra to reduce file size)
    Resolution: 1280x720 default
    Vsync: Enabled for smooth gameplay
    WebGL: 2.0 (most compatible)
    Compression: Enabled to reduce size
    */
}
```

### Presentation Outline Template

```
GAME PRESENTATION STRUCTURE:

1. Title Slide (10 seconds)
   - Game name
   - Your name
   - Date

2. Gameplay Demo (5 minutes)
   - Play the game
   - Show core mechanic
   - Demonstrate win condition

3. Design (2 minutes)
   - What makes this game unique?
   - Design pillars
   - Target audience

4. Technical (2 minutes)
   - Key systems
   - Design patterns used
   - Challenges overcome

5. Playtesting (1 minute)
   - Number of testers
   - Average fun rating
   - Key feedback
   - Changes made

6. Reflection (2 minutes)
   - What went well?
   - What was hard?
   - What you learned
   - Future improvements

7. Questions & Discussion
```

---

## Additional Resources

- **Game Design Document Template:** Available in course materials
- **Playtesting Guide:** https://www.gamasutra.com/blogs/RyanCreighton/20171205/310275/The_Playtests_That_Save_Games.php
- **WebGL Build Guide:** https://docs.unity3d.com/Manual/webgl-building.html
- **Game Development Postmortem:** https://www.youtube.com/results?search_query=game+dev+postmortem

---

## Summary: Complete Game Development Workflow

**Week 1 (Days 1-4): Planning**
- Write GDD
- Design MVP
- Plan scope

**Week 1-2 (Days 5-8): Core Implementation**
- Prototype core mechanic
- Build vertical slice
- Get initial feedback

**Week 2 (Days 9-14): Systems**
- Integrate all major systems
- Test integration
- Fix bugs

**Week 2-3 (Days 15-20): Polish & Playtesting**
- Add visual/audio feedback
- Playtest with players
- Iterate on feedback

**Week 3 (Days 21-28): Final Development**
- Implement remaining features
- Optimize performance
- Final polish

**Week 4 (Days 29-36): Delivery**
- Final QA and bug fixes
- Build and export
- Create presentation
- Reflect on learning

This 8-unit capstone brings together everything you've learned: design thinking, programming, systems architecture, and game feel. Your capstone project is proof that you can design and build a complete game from scratch.

