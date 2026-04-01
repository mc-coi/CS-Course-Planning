# Unit 7 - Game Systems & Enemies: Teacher Misconception & Callout Guide

## Overview

This unit teaches students to build game systems—enemy AI with finite state machines (FSMs), a GameManager singleton, object pooling, ScriptableObjects, and coroutines. These are the most architecturally complex concepts in the course, and in a STEM semester the challenge is real: students must implement patterns they've never seen in a compressed timeline. The abstract nature of FSMs, the "why would I pool objects?" question, and the confusion around singletons vs. static classes all need direct, upfront teaching. Unlike the year-long course where students can experiment with FSM variations, STEM students need a working template to customize. Use 🚨 flags to know when to stop everything.

---

## Misconceptions by Topic

### Finite State Machines (Days 1–4)

**⚠️ Misconception:** "I can use a bunch of if/else statements to control my enemy. I don't need a state machine."

**What it looks like:** A student writes nested if/else chains for idle, patrol, chase, and attack behavior. The code becomes 100+ lines of tangled logic with hard-to-find bugs.

**Why students think this:** Simple behavior can be written with if/else. They don't see the problem until it grows.

**How to address it:** Show the FSM pattern. "If/else works for 2 states. By 4 states it's unmaintainable. An FSM uses an enum to represent the current state and a switch statement to run the right behavior. Adding a new state is just adding a new case—no tangled conditionals. Think of it as a flowchart in code."

🚨 **STEM Priority — STOP THE CLASS:** If students are building enemy AI with large if/else chains, stop and introduce the FSM pattern before they build on a broken foundation.

```csharp
// FSM pattern
enum EnemyState { Idle, Patrol, Chase, Attack }
EnemyState currentState = EnemyState.Idle;

void Update()
{
    switch (currentState)
    {
        case EnemyState.Idle:    HandleIdle();    break;
        case EnemyState.Patrol:  HandlePatrol();  break;
        case EnemyState.Chase:   HandleChase();   break;
        case EnemyState.Attack:  HandleAttack();  break;
    }
}
```

---

**⚠️ Misconception:** "My enemy switches between states too quickly—it flickers between Chase and Idle every frame."

**What it looks like:** An enemy enters Chase when the player is within range, but the player is right at the boundary. The enemy alternates Chase ↔ Idle every frame.

**Why students think this:** They use a single threshold for entering AND exiting a state.

**How to address it:** Add hysteresis (separate enter/exit thresholds). "Use a larger exit threshold than enter threshold. Enter Chase at 5 units, exit at 8 units. The enemy won't flickler at the boundary. This is called hysteresis—a dead zone that prevents oscillation."

```csharp
float chaseRange = 5f;    // enter Chase if player closer than this
float loseRange = 8f;     // exit Chase if player farther than this

void HandleIdle()
{
    if (distToPlayer < chaseRange) currentState = EnemyState.Chase;
}

void HandleChase()
{
    if (distToPlayer > loseRange) currentState = EnemyState.Idle;
    // move toward player...
}
```

---

**⚠️ Misconception:** "My enemy patrols between two waypoints but it overshoots and shakes back and forth."

**What it looks like:** An enemy moves toward a waypoint, reaches it (mostly), then snaps to the next one, but overshoots constantly because it's checking exact position equality.

**Why students think this:** They compare `transform.position == waypoint.position`, which rarely equals exactly due to floating point.

**How to address it:** Use distance threshold. "Never compare positions with `==` in floating-point math. Use `Vector3.Distance(transform.position, waypoint.position) < 0.2f` to detect arrival. Adjust the threshold (0.1f–0.5f) based on how precise you need arrival to be."

```csharp
void HandlePatrol()
{
    // Move toward current waypoint
    transform.position = Vector3.MoveTowards(transform.position, waypoints[currentWaypoint].position, speed * Time.deltaTime);

    // Check arrival
    if (Vector3.Distance(transform.position, waypoints[currentWaypoint].position) < 0.2f)
    {
        currentWaypoint = (currentWaypoint + 1) % waypoints.Length; // loop
    }
}
```

---

### GameManager & Singletons (Days 3–5)

**⚠️ Misconception:** "I need to access the score from multiple scripts. I'll make score a public variable on the GameManager and use FindObjectOfType<GameManager>() everywhere."

**What it looks like:** A student calls FindObjectOfType<GameManager>() every frame in multiple scripts. Performance tanks in complex scenes.

**Why students think this:** FindObjectOfType() is the only method they know for getting references across scripts.

**How to address it:** Use the Singleton pattern. "A Singleton gives you one global instance without searching every frame. Set it up once in Awake(): `public static GameManager Instance;`. Any script can then access it directly: `GameManager.Instance.score`. No searching every frame, no null references."

🚨 **STEM Priority — STOP THE CLASS:** Teach the Singleton pattern before students build interconnected systems. It's used in nearly every game.

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager Instance;
    public int score = 0;

    void Awake()
    {
        if (Instance == null)
        {
            Instance = this;
            DontDestroyOnLoad(gameObject); // survive scene loads
        }
        else
        {
            Destroy(gameObject); // enforce one instance
        }
    }
}

// Access from any other script:
GameManager.Instance.score += 10;
```

---

**⚠️ Misconception:** "I added DontDestroyOnLoad to my GameManager, but when I restart the game there are two GameManagers and the score doubles."

**What it looks like:** A student loads the opening scene again (restart) and a second GameManager instance appears. Score and values are applied twice.

**Why students think this:** DontDestroyOnLoad keeps the object—loading the scene again adds another one.

**How to address it:** Enforce one instance in Awake(). "The standard Singleton Awake() checks: `if (Instance != null && Instance != this) { Destroy(gameObject); return; }`. This destroys any duplicate that appears when the scene reloads. Only the first-ever instance survives."

---

**⚠️ Misconception:** "Why can't I just use a static variable for the score? Why do I need a whole GameManager class?"

**What it looks like:** A student puts `public static int score = 0;` on a random script and accesses it everywhere. It works—until the game resets and the static variable doesn't.

**Why students think this:** Static variables are simpler than a Singleton class.

**How to address it:** Explain the trade-off. "Static variables work for simple cases. But a GameManager GameObject can be seen in the Inspector, can have methods, can hold references to UI components, and can be reset cleanly by resetting its values. Static variables are invisible in the editor, can't be reset by destroying the object, and get messy for complex state. Use static variables for simple constants; use a Singleton class for game state."

---

### Object Pooling (Days 5–6)

**⚠️ Misconception:** "I'm Instantiating and Destroying bullets every time. Performance seems fine."

**What it looks like:** A student Instantiates bullets on fire and Destroys them on hit. At low fire rates it's fine; during intense gameplay it spikes.

**Why students think this:** The performance cost of Instantiate/Destroy isn't visible in normal gameplay until it spikes at the wrong moment.

**How to address it:** Introduce object pooling. "Instantiate() and Destroy() allocate and free memory—expensive operations that cause garbage collection spikes (hitches in gameplay). Object pooling pre-creates objects at scene start and reuses them by toggling SetActive(). No allocations at runtime = no hitches. For bullets, projectiles, particle effects, and enemies—always pool."

🚨 **STEM Priority — Monitor:** For STEM courses, introduce the concept with a simple pool. If students ask why game feel drops during heavy action, this is usually the cause.

```csharp
// Simple bullet pool
public class BulletPool : MonoBehaviour
{
    [SerializeField] GameObject bulletPrefab;
    [SerializeField] int poolSize = 20;
    List<GameObject> pool = new List<GameObject>();

    void Start()
    {
        for (int i = 0; i < poolSize; i++)
        {
            GameObject b = Instantiate(bulletPrefab);
            b.SetActive(false);
            pool.Add(b);
        }
    }

    public GameObject GetBullet()
    {
        foreach (var b in pool)
        {
            if (!b.activeInHierarchy) return b;
        }
        return null; // pool exhausted
    }
}
```

---

### ScriptableObjects (Days 6–7)

**⚠️ Misconception:** "I need different enemy types with different stats. I'll make a separate script for each enemy type."

**What it looks like:** A student creates EnemyBasic.cs, EnemyFast.cs, EnemyTank.cs—each nearly identical but with different values hard-coded.

**Why students think this:** Subclassing or copy-paste is the most obvious approach to variation.

**How to address it:** Use ScriptableObjects. "ScriptableObjects are data containers you create in the Project panel—no GameObject needed. Define stats (health, speed, damage) once in a ScriptableObject class, then create multiple instances in the Project panel with different values. One EnemyBase.cs script reads from a ScriptableObject. Change stats without touching code."

```csharp
[CreateAssetMenu(fileName = "EnemyData", menuName = "Game/EnemyData")]
public class EnemyData : ScriptableObject
{
    public float maxHealth;
    public float speed;
    public float damage;
    public Sprite sprite;
}

// On the Enemy script:
public EnemyData data;

void Start()
{
    health = data.maxHealth;
    GetComponent<SpriteRenderer>().sprite = data.sprite;
}
```

---

### Coroutines (Days 7–8)

**⚠️ Misconception:** "I want to wait 2 seconds before spawning the next wave. I'll use a while(true) loop with a counter inside Update()."

**What it looks like:** A student tries to create a delay by counting frames or using a counter in Update(). It's overly complex and often breaks.

**Why students think this:** They don't know coroutines exist, and Update() is their only tool.

**How to address it:** Use coroutines. "A coroutine is a method that can pause and resume. Use `yield return new WaitForSeconds(2f)` to wait 2 seconds without blocking everything else. Start it with `StartCoroutine(SpawnWave())`. It's the correct tool for timed sequences, delayed events, and wave spawning."

```csharp
IEnumerator SpawnWave()
{
    yield return new WaitForSeconds(3f);   // wait 3 seconds
    for (int i = 0; i < 5; i++)
    {
        Instantiate(enemyPrefab, spawnPoint.position, Quaternion.identity);
        yield return new WaitForSeconds(0.5f); // 0.5s between spawns
    }
}

// Call with:
StartCoroutine(SpawnWave());
```

---

**⚠️ Misconception:** "I called StartCoroutine(SpawnWave()) but the method runs instantly without any delay."

**What it looks like:** A student defines a coroutine returning void or IEnumerable instead of IEnumerator. The yield return is ignored.

**Why students think this:** The syntax is easy to get slightly wrong.

**How to address it:** Check the return type. "A coroutine MUST return IEnumerator (not void, not IEnumerable). If the return type is wrong, Unity ignores the yield statements and runs the code immediately. Also check that you're calling StartCoroutine(MethodName()) not MethodName() directly—calling directly bypasses coroutine behavior."

---

## Whole-Class Warning Signs

- **Everyone's enemy AI is a giant if/else chain.** Stop and introduce the FSM enum/switch pattern. It's one of the most important patterns in game programming and needs to be taught, not discovered.

- **Multiple students can't access variables across scripts.** They're not using the Singleton pattern. Teach GameManager.Instance once and enforce it as the class standard for cross-script state.

- **Instantiate/Destroy calls spike and the game hitches.** Object pooling time. A quick demo of pool vs. no-pool is convincing. Even a simple manual pool (SetActive) is enough for the capstone.

- **Students making separate scripts for every enemy type.** Show ScriptableObjects—a 15-minute demo replaces the copy-paste approach for the entire class.

- **Wave spawning not working—students can't figure out timing.** Coroutines are the answer. Demo WaitForSeconds once; the whole class benefits.

---

## Questions That Reveal Understanding

1. **"Explain an FSM in one sentence. Then give a concrete example from a game."**
   - Good answer: "An FSM tracks a current state and runs different behavior based on that state. Example: A guard enemy that Patrols → chases if player detected → attacks if in range → returns to patrol if player escapes."
   - Red flag: "It's a way to organize code." (True but shows no understanding of state transitions.)

2. **"What's the Singleton pattern and when do you use it?"**
   - Good answer: "One global instance of a class, accessed via a static Instance property. Use it for managers (GameManager, AudioManager, UIManager) that need to be accessed from multiple scripts without FindObjectOfType."
   - Red flag: "A static class." (Partially correct but static classes can't use MonoBehaviour, serialize fields, or appear in Inspector.)

3. **"Why does object pooling improve performance over Instantiate/Destroy?"**
   - Good answer: "Instantiate allocates memory; Destroy frees it. Frequent allocation/deallocation triggers garbage collection, which causes frame hitches. Pooling reuses objects with SetActive, eliminating allocations at runtime."
   - Red flag: "It's faster because the objects already exist." (Directionally correct but doesn't explain GC spikes.)

4. **"What does a ScriptableObject do and how is it different from a MonoBehaviour?"**
   - Good answer: "ScriptableObjects are data containers that live in the Project panel—they're assets, not GameObjects. MonoBehaviours are components on GameObjects. Use ScriptableObjects to define shared data (enemy stats, item definitions) once and reference them from many scripts."
   - Red flag: "They're like static classes." (Incorrect—ScriptableObjects are serialized assets with Inspector support.)

5. **"Your coroutine runs immediately without waiting. What's wrong?"**
   - Good answer: "Check the return type—it must be IEnumerator, not void or IEnumerable. Also make sure you're calling StartCoroutine(MethodName()) not MethodName() directly."
   - Red flag: "The yield return syntax is wrong." (Partially—return type is the more common root cause.)

---

## Common Student Questions & How to Answer Them

**Q1: "My enemy chases the player even through walls. How do I make it path around them?"**

*A:* "True pathfinding uses Unity's NavMesh system (AI package). For simple 2D games, use A* Pathfinding Project (free on the Unity Asset Store). For a quick workaround: check if there's a wall between enemy and player with a raycast before chasing. If a wall is hit, fall back to Patrol instead of Chase. Full pathfinding is a STEM capstone stretch goal."

---

**Q2: "I want enemies to spawn in waves. How do I set that up?"**

*A:* "Use a coroutine for wave timing. In a WaveManager: `StartCoroutine(RunWaves());`. Each wave waits `WaitForSeconds(waveDelay)`, then spawns enemies using a loop with `WaitForSeconds(spawnDelay)` between each. Track active enemies with a counter: increment on spawn, decrement in the enemy's OnDestroy(). When counter == 0, start the next wave."

---

**Q3: "How do I make a health system that works for both the player and enemies?"**

*A:* "Create a reusable Health script: `public float currentHealth; public float maxHealth;`. Add methods: `TakeDamage(float amount)` and `Die()`. Attach it to both the player and enemies. Call `GetComponent<Health>().TakeDamage(damage)` from any projectile or attack. Override Die() behavior in subclasses or use UnityEvents to trigger custom on-death behavior."

---

**Q4: "My GameManager survives scene loads (DontDestroyOnLoad), but I want to reset all game state when the player restarts. How?"**

*A:* "Add a Reset() method to GameManager that resets all values: `public void Reset() { score = 0; lives = 3; currentLevel = 0; }`. Call it when the player clicks Restart before loading the first scene. Don't destroy the GameManager—just reset its values."

---

**Q5: "Can I use multiple coroutines at once? I want a boss that shoots, moves, and charges simultaneously."**

*A:* "Yes—StartCoroutine() is non-blocking. Each call runs independently. `StartCoroutine(ShootPattern()); StartCoroutine(MovementPattern()); StartCoroutine(ChargeAttack());` all run simultaneously. They're like parallel tracks. Coroutines don't block each other unless you use yield to wait for another coroutine."

---

## Analogies That Work

1. **"A finite state machine is like a traffic light. The light is always in one state: Red, Yellow, or Green. Each state has rules (Red = cars stop, Green = cars go). The light transitions between states on a timer. It can't be in two states at once. Your enemy AI is the same—one state at a time, with rules for switching."**
   - Makes FSM immediately intuitive and the single-active-state rule clear.

2. **"Object pooling is like a library. Instead of buying a new book every time you read one (Instantiate) and burning it when done (Destroy), you borrow from the library and return it when finished (SetActive true/false). The library's collection stays constant. No waste."**
   - Makes pooling feel obvious and efficient.

3. **"ScriptableObjects are like index cards in a recipe box. Each card has the same fields (ingredients, steps) but different values. The chef (Enemy script) reads from whatever card you hand them. You can have 100 enemy types using one script and 100 ScriptableObject cards."**
   - Makes the data-driven design principle stick.

---

## Unity-Specific Gotchas

- **Coroutines stop when the GameObject is disabled or destroyed.** If you call `SetActive(false)` on a pooled enemy with a running coroutine, the coroutine stops silently. Store coroutine references and call `StopCoroutine()` before disabling if needed.

- **Static Instance persists between Play mode sessions in the editor.** After stopping Play mode, `GameManager.Instance` still holds the old reference. This causes NullReferenceExceptions on re-enter. The singleton Awake() pattern with null check handles this—make sure Instance is set in Awake(), not Start().

- **ScriptableObjects in Resources/ folder must be loaded with Resources.Load().** If you place ScriptableObjects in a Resources folder, load them via `Resources.Load<EnemyData>("EnemyBasic")`. If they're referenced by a field in the Inspector, just drag them—no Resources.Load needed. Prefer Inspector references for STEM simplicity.

- **IEnumerator vs IEnumerable** — coroutines need `IEnumerator`, not `IEnumerable`. The compiler won't flag this as an error, but `yield return` won't work correctly. This is the most common coroutine bug in student code.

- **Vector3.MoveTowards vs Lerp for enemy movement** — `MoveTowards` moves at a fixed speed and won't overshoot the target. `Lerp` moves proportionally (slows as it approaches). For patrol points, use `MoveTowards`. For smooth follow (camera, homing missiles), use `Lerp`.

- **FindObjectOfType() is O(n) over all scene objects.** Never call it in Update(). Cache references in Start() or use the Singleton pattern. In a scene with 100+ objects, per-frame FindObjectOfType() is measurably slow.

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
