# Day 30: Prototyping Core Mechanic

**Learning Target:** Build and iterate on a core game mechanic prototype through rapid testing and feedback.

### Key Concepts

- **Prototype:** Working implementation of the core idea
- **Rapid Iteration:** Quick test-build-feedback cycle
- **Grayboxing:** Minimal visuals, focus on gameplay
- **Playtesting Early:** Test with actual players ASAP
- **Fail Fast:** Discover if the core mechanic is fun quickly
- **Vertical Slice:** Complete (but small) feature set showing full game
- **Mechanics Testing:** Ensuring core mechanic feels good

### Content

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

### Code Examples

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

### Guided Practice

1. Implement the simplest version of your core mechanic
2. Use graybox graphics (cubes, spheres, basic shapes)
3. Focus on feel, not visuals
4. Test internally: Does it feel good?
5. Add debug shortcuts (instant win, instant lose, quick damage)
6. Get feedback from a friend or classmate
7. Document what feels good and what feels bad
8. Iterate: Make changes based on feedback

### Practice Problems

**Problem 1 — Beginner:** Build a simple prototype of your core mechanic with basic controls and immediate feedback.

**Problem 2 — Intermediate:** Create a vertical slice with player movement, enemy AI, and win condition working together.

**Problem 3 — Challenge:** Playtest your prototype with 2-3 people and document their feedback on what feels fun and what feels bad.

<details>
<summary>Hints</summary>

**Problem 1:** Start very simple: just player movement and one action (jump, shoot, collect, etc.). Iterate from there.

**Problem 2:** Integrate player movement, a simple enemy, collision detection, and a win condition. Don't worry about polish.

**Problem 3:** Ask: Is the core mechanic fun? What was most fun? What was frustrating? Would you play more?

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:** Create a simple player controller that moves with arrow keys and jumps with spacebar. Add a cube to jump on. Test and iterate.

**Problem 2:** Add an enemy that chases the player. Add health. Create a win condition (reach the goal, defeat enemies, etc.). Test together.

**Problem 3:** Create a feedback form:
- Fun rating (1-10)
- What was most fun?
- What was frustrating?
- Would you play the full game?

Document responses and look for patterns.

</details>
