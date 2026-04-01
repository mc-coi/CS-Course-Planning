# Unit 7 - Game Systems & Enemies: Teacher Misconception & Callout Guide

## Overview

This unit is where students build **intelligent** games. Enemies have to behave (follow paths, patrol, respond to player proximity), and game systems have to coordinate (spawn waves, track state, manage data). The biggest challenge is **complexity**: students juggle multiple systems and lose track of which variable controls what. They also struggle with **finite state machines** (FSMs)—an abstract pattern that's powerful but hard to visualize. Additionally, they don't understand why object pooling matters (spawning and destroying GameObjects is slow) until they profiling. For a year-long course, students can experiment with simple AI and build systems iteratively. For a semester course, provide FSM templates and pre-built systems to customize.

---

## Misconceptions by Topic

### Finite State Machines & AI Behavior (Throughout)

**⚠️ Misconception:** "My enemy just walks around randomly. I want it to patrol, chase when it sees the player, then give up. But the behavior is too complicated to code."**

**What it looks like:** A student tries to hardcode enemy logic with tons of if statements, and it becomes a jumbled mess.

**Why students think this:** FSMs aren't an obvious pattern. They're used to linear scripts, not state-based logic.

**How to address it:** Teach FSMs explicitly. "Enemies have states: Patrol, Chase, Stunned, Dead. Each state has code that runs while in that state. You transition between states based on conditions (see player → Chase, timer runs out → Patrol). Structure it:
```csharp
enum EnemyState { Patrol, Chase, Stunned }
EnemyState currentState = EnemyState.Patrol;

void Update()
{
    switch(currentState)
    {
        case EnemyState.Patrol:
            Patrol();
            if(CanSeePlayer()) currentState = EnemyState.Chase;
            break;
        case EnemyState.Chase:
            Chase();
            if(!CanSeePlayer()) currentState = EnemyState.Patrol;
            break;
    }
}
```
This scales to 5, 10, or 20 states without becoming a mess."

---

**⚠️ Misconception:** "I wrote an FSM, but the enemy's state doesn't transition. The logic must be broken."**

**What it looks like:** A student writes condition checks that never evaluate to true, so the state never changes.

**Why students think this:** The condition is probably correct, but the code structure has a bug (e.g., checking the condition at the wrong time, or the condition uses `==` when it should use `!=`).

**How to address it:** Debug with logging. "Add `Debug.Log()` to print the current state and what conditions are being checked:
```csharp
Debug.Log("State: " + currentState);
if(CanSeePlayer())
{
    Debug.Log("Player spotted!");
    currentState = EnemyState.Chase;
}
```
Run the game and watch the Console. If it never prints 'Player spotted!', the condition is false. Check if `CanSeePlayer()` is implemented correctly."

---

### Enemy Behavior & Pathfinding (Throughout)

**⚠️ Misconception:** "I want my enemy to patrol along a path. I created waypoints, but the enemy doesn't go to them."**

**What it looks like:** A student has Transform objects placed as waypoints but no code to move the enemy between them.

**Why students think this:** They think waypoints automatically guide movement. Actually, the code has to read waypoint positions and move the enemy.

**How to address it:** Implement path following. "Store waypoints in an array:
```csharp
Transform[] waypoints;
int currentWaypoint = 0;

void Patrol()
{
    Vector3 target = waypoints[currentWaypoint].position;
    transform.position = Vector3.MoveTowards(transform.position, target, speed * Time.deltaTime);

    if(Vector3.Distance(transform.position, target) < 0.5f)
    {
        currentWaypoint = (currentWaypoint + 1) % waypoints.Length;
    }
}
```
Assign waypoint Transforms in the Inspector. The enemy now walks from point to point."

---

**⚠️ Misconception:** "My enemy chases the player, but it moves in a straight line and gets stuck on walls. How do I make it smarter?"**

**What it looks like:** A student's enemy does `transform.position += (player.position - transform.position).normalized * speed * Time.deltaTime;` and ignores obstacles.

**Why students think this:** Pathfinding is a complex topic. They think moving toward the player is enough.

**How to address it:** Introduce alternatives. "For simple games: (1) Use raycasting to detect walls and move around them. (2) Use NavMesh (built-in pathfinding, advanced). (3) For top-down games, use grid-based movement (move one grid cell at a time, detect collisions). Don't worry about smart pathfinding yet—just don't move into walls. Check for collisions before moving."

---

### Game State & Persistence (Throughout)

**⚠️ Misconception:** "I'm tracking the player's health, ammo, and inventory with separate variables in different scripts. But when I load a new scene, they all reset."**

**What it looks like:** A student has `Player.cs` with health, `WeaponManager.cs` with ammo, and `Inventory.cs` with items. When the scene changes, all are lost.

**Why students think this:** They didn't plan for persistence. Data is scattered across scripts.

**How to address it:** Centralize state. "Create a `GameManager` singleton that persists across scenes:
```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;
    public int health = 100;
    public int ammo = 30;

    void Awake()
    {
        if(instance == null)
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
        }
        else Destroy(gameObject);
    }
}
```
Now access it from any script: `GameManager.instance.health -= 10;`. Data persists between scenes."

---

### Object Pooling (Throughout)

**⚠️ Misconception:** "I'm spawning projectiles with `Instantiate()` and destroying them with `Destroy()`. The game runs fine, so object pooling isn't necessary."**

**What it looks like:** A student spawns bullets/enemies freely and notices no lag until late game when hundreds are spawned/destroyed.

**Why students think this:** Instantiate/Destroy work but are slow. The lag is invisible until you have a lot of objects.

**How to address it:** Teach pooling. "Instantiate and Destroy allocate and free memory, which is slow. Object pooling pre-creates a pool of objects and reuses them (disable/enable instead of create/destroy):
```csharp
// Pool setup
GameObject[] bulletPool = new GameObject[100];
for(int i = 0; i < 100; i++) bulletPool[i] = Instantiate(bulletPrefab);
bulletPool[i].SetActive(false);

// Spawn
void SpawnBullet()
{
    foreach(GameObject bullet in bulletPool)
    {
        if(!bullet.activeInHierarchy)
        {
            bullet.SetActive(true);
            bullet.transform.position = transform.position;
            break;
        }
    }
}

// Destroy (return to pool)
bullet.SetActive(false);
```
This is much faster than Instantiate/Destroy."

---

**⚠️ Misconception:** "I implemented object pooling, but disabling GameObjects causes problems with scripts. They don't run."**

**What it looks like:** A student disables pooled objects, but when reactivated, they don't behave correctly.

**Why students think this:** Disabled GameObjects skip Update(). Scripts on disabled objects don't run.

**How to address it:** Plan for reuse. "When you disable an object, its scripts don't run. When you re-enable it, scripts resume—they don't reset state. For pooling to work, reset object state when reactivating:
```csharp
void OnEnable()
{
    health = maxHealth;
    animator.SetTrigger('Spawn');
}

void OnDisable()
{
    // Cleanup if needed
}
```
Use OnEnable/OnDisable instead of Start/Destroy."

---

### ScriptableObjects & Data Management (Throughout)

**⚠️ Misconception:** "I created a ScriptableObject for enemy stats, but I can't see the data in the Inspector."**

**What it looks like:** A student creates a ScriptableObject class but doesn't see serialized fields in the Inspector.

**Why students think this:** They didn't make the class public or didn't mark fields with [SerializeField].

**How to address it:** Set up correctly. "ScriptableObjects work like this:
```csharp
[CreateAssetMenu(fileName = 'EnemyStats', menuName = 'Enemies/Stats')]
public class EnemyStats : ScriptableObject
{
    public int health = 100;
    public float speed = 5f;
    public Sprite sprite;
}
```
Make the class public. Fields are serialized by default. Right-click in Project panel → Create → Enemies → Stats to create an instance. Edit it in the Inspector, and all enemies using it get the same stats."

---

### Waves & Spawning (Throughout)

**⚠️ Misconception:** "I want to spawn a wave of 10 enemies, but I'm doing it in a loop, and they all spawn at the same position. They overlap."**

**What it looks like:** A student writes:
```csharp
for(int i = 0; i < 10; i++)
{
    Instantiate(enemyPrefab, spawnPoint, Quaternion.identity);
}
```
All enemies spawn at the same spot.

**Why students think this:** They didn't offset spawn positions. Actually spawning at the same spot is the problem.

**How to address it:** Offset positions. "Spawn at different positions:
```csharp
for(int i = 0; i < 10; i++)
{
    Vector3 randomOffset = new Vector3(Random.Range(-5f, 5f), 0, Random.Range(-5f, 5f));
    Instantiate(enemyPrefab, spawnPoint + randomOffset, Quaternion.identity);
}
```
Now enemies spread out. Or spawn them one at a time with a delay using coroutines."

---

### Coroutines & Delayed Actions (Throughout)

**⚠️ Misconception:** "I used a coroutine with `yield return new WaitForSeconds(2f)`, but it ran immediately. Coroutines don't work."**

**What it looks like:** A student writes a coroutine that should delay an action but it doesn't.

**Why students think this:** They forgot to call `StartCoroutine()`, so the coroutine was never started.

**How to address it:** Use StartCoroutine(). "Coroutines must be started with `StartCoroutine()`:
```csharp
void SpawnWave()
{
    StartCoroutine(SpawnWaveCoroutine());
}

IEnumerator SpawnWaveCoroutine()
{
    for(int i = 0; i < 10; i++)
    {
        Instantiate(enemyPrefab, ...);
        yield return new WaitForSeconds(1f);  // Delay 1 second between spawns
    }
}
```
Without `StartCoroutine()`, the coroutine isn't executed."

---

## Whole-Class Warning Signs

- **Multiple students' enemies get stuck in walls or each other.** They're not checking collisions before moving. Have them add a raycast or overlap check before moving.

- **Everyone's game gets slower as enemies spawn.** They're using Instantiate/Destroy. Introduce object pooling early.

- **Several students have GameManager singletons that conflict (creating multiple instances).** They didn't implement the null check. Provide a template GameManager with proper singleton pattern.

- **Enemy states aren't transitioning correctly.** They're checking conditions at the wrong time or using the wrong operators (`=` instead of `==`). Teach them to debug with Console output.

- **ScriptableObjects seem pointless to beginners.** Show them the benefit: change enemy stats once, all enemies using that asset change instantly. No need to reprogram.

---

## Questions That Reveal Understanding

1. **"Draw a state diagram for an enemy that patrols, chases the player, and flees when health is low."**
   - Good answer: A diagram with circles (Patrol, Chase, Flee) and arrows showing transitions: Patrol → Chase (see player), Chase → Flee (low health), Flee → Patrol (far away), etc.
   - Red flag: A linear diagram or no transitions between states.

2. **"Why use an object pool instead of Instantiate/Destroy?"**
   - Good answer: "Allocating and freeing memory is slow. Pooling pre-creates objects and reuses them (disable/enable), which is much faster. Important for games with many objects (bullets, particles, enemies)."
   - Red flag: "Because the teacher said to" or "It's faster" (without understanding why).

3. **"You have 100 enemies on screen, each with a script that runs Update(). How would you optimize?"**
   - Good answer: "Use object pooling for enemies. Disable distant enemies. Use spatial partitioning or quadtrees to avoid checking all 100 enemies every frame. Reduce the complexity of each enemy's Update() (cache GetComponent calls, use simpler AI)."
   - Red flag: "Buy a better computer" or "Nothing can be optimized." (Not thinking systematically.)

4. **"What's the difference between a scene-specific GameManager and a persistent GameManager?"**
   - Good answer: "Scene-specific: created each scene, destroyed when scene changes (good for per-level data). Persistent: survives scene changes using DontDestroyOnLoad (good for game-wide state like health, score, settings)."
   - Red flag: "They're the same thing" or "I don't know." (They haven't designed for persistence.)

---

## Common Student Questions & How to Answer Them

**Q1: "My enemy FSM has lots of states. How do I avoid the switch statement becoming unmanageable?"**

*A:* "Switch statements scale okay up to 5-10 states. For more, consider an abstract State class:
```csharp
abstract class EnemyState { public abstract void Enter(); public abstract void Update(); public abstract void Exit(); }
class PatrolState : EnemyState { ... }
currentState.Update();  // Works for any state
```
This scales to 20+ states cleanly."

---

**Q2: "I want enemies to respawn after being killed, but not all at once. How?"**

*A:* "Use a coroutine:
```csharp
if(isDead)
{
    StartCoroutine(RespawnCoroutine());
    isDead = false;
}

IEnumerator RespawnCoroutine()
{
    yield return new WaitForSeconds(3f);  // Wait 3 seconds
    Instantiate(enemyPrefab, spawnPoint, Quaternion.identity);
}
```
Or use object pooling: disable the enemy, wait 3 seconds, re-enable it."

---

**Q3: "How do I detect when the player enters an enemy's detection range?"**

*A:* "Use a trigger collider:
```csharp
void OnTriggerEnter(Collider other)
{
    if(other.CompareTag('Player'))
    {
        detectedPlayer = true;
    }
}
```
Or use Physics.OverlapSphere for more control:
```csharp
Collider[] hits = Physics.OverlapSphere(transform.position, detectionRange);
foreach(Collider hit in hits)
{
    if(hit.CompareTag('Player')) detectedPlayer = true;
}
```"

---

**Q4: "My ScriptableObject has default values, but I want each instance to have different values. Is this normal?"**

*A:* "Yes, that's the point! Create a ScriptableObject asset (Right-click → Create → Enemy Stats). Edit it in the Inspector. The asset stores those values. Create multiple assets (EnemyStats_Goblin, EnemyStats_Orc). Reference them in prefabs or code, and each enemy has different stats."

---

**Q5: "How do I spawn a wave of 5 enemies, 1 every 2 seconds?"**

*A:* "Use a coroutine:
```csharp
StartCoroutine(SpawnWave());

IEnumerator SpawnWave()
{
    for(int i = 0; i < 5; i++)
    {
        Instantiate(enemyPrefab, spawnPoint, Quaternion.identity);
        yield return new WaitForSeconds(2f);
    }
}
```
Or loop and track time:
```csharp
float spawnTimer = 0;
for(int i = 0; i < 5; i++)
{
    if(spawnTimer <= 0)
    {
        Instantiate(enemyPrefab, ...);
        spawnTimer = 2f;
    }
    spawnTimer -= Time.deltaTime;
}
```"

---

## Analogies That Work

1. **"An FSM is like a traffic light. The light has states: Red, Yellow, Green. In each state, the light does something (Red: stop traffic, Green: go). It transitions between states on a timer. Your enemy FSM works the same: Patrol, Chase, Flee are like the colored lights, and transitions happen when conditions are met."**
   - This makes FSMs concrete and relatable.

2. **"Object pooling is like a deck of cards. Instead of creating and destroying cards constantly, you keep a full deck and mark cards as 'in use' or 'available.' When you need a card, you grab an available one. When you're done, you mark it available again. Much faster than printing and burning cards."**
   - This makes the efficiency gain intuitive.

3. **"A ScriptableObject is like a recipe card. You write the recipe once. Many people can follow the same recipe. If you change the recipe, everyone using it cooks differently. Without it, each person would have to memorize the recipe."**
   - This explains data reuse.

---

## Unity-Specific Gotchas

- **Coroutines stop if the GameObject or script is disabled.** If you disable an enemy while a coroutine is running, the coroutine pauses. Re-enable it and the coroutine resumes. Use `StopCoroutine()` if you want to stop it explicitly.

- **`DontDestroyOnLoad` persists even in Play mode's editor.** If you load a scene twice without stopping the editor, you get two instances. Use a singleton check to prevent duplicates.

- **NavMesh needs to be baked for each scene.** Using Unity's NavMesh pathfinding requires baking the scene. This is a one-time setup but students often forget it.

- **Physics queries are slow inside nested loops.** OverlapSphere on every enemy checking every frame is expensive. Cache results or use spatial partitioning.

- **Coroutines use `Time.deltaTime`, so they respect Time.timeScale.** If you pause the game (Time.timeScale = 0), coroutines with `WaitForSeconds` pause. Use `WaitForSecondsRealtime` if you want coroutines to ignore timeScale (useful for pause menus).

- **Random.seed affects all Random calls.** Setting a seed for debugging is good, but if you forget to unset it, all random behavior is predictable. Useful for debugging but remember to unset.

- **Destroys don't happen immediately; they're queued until end of frame.** If you Destroy an enemy and then check if it still exists, it exists. Use `activeInHierarchy` or mark it as destroyed instead of relying on immediate destruction.

---

## Year-Long Differentiators

For year-long courses:
- Let students build AI enemies with simple FSMs first (Patrol, Chase), then add complexity (Flee, Attack, Stun). Iteration builds understanding.
- Introduce optimization (pooling, spatial queries) when they notice lag, not preemptively. Learning from a problem they observe sticks better.
- Have them build a GameManager once in Unit 5, then extend it in Unit 7. Reusing a system reinforces its design.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
