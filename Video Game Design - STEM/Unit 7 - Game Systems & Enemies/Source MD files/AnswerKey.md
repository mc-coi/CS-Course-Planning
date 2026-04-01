# Unit 7 Answer Key: Game Systems & Enemies

Comprehensive answer key for all 15 practice problems covering AI, game mechanics, and persistence systems.

---

## Problem 1: Simple FSM

### Solution

```csharp
public enum EnemyState { Idle, Patrol, Chase, Attack }

public class Enemy : MonoBehaviour
{
    private EnemyState state = EnemyState.Idle;

    void Update()
    {
        switch(state)
        {
            case EnemyState.Idle:
                IdleBehavior();
                break;
            case EnemyState.Patrol:
                PatrolBehavior();
                break;
            case EnemyState.Chase:
                ChaseBehavior();
                break;
            case EnemyState.Attack:
                AttackBehavior();
                break;
        }
    }

    void IdleBehavior() { /* Stand still */ }
    void PatrolBehavior() { /* Walk between waypoints */ }
    void ChaseBehavior() { /* Move toward player */ }
    void AttackBehavior() { /* Damage player */ }
}
```

### What Success Looks Like
- Enemy has distinct states
- State transitions based on conditions
- Each state has specific behavior
- Clean switch statement structure

### Common Mistakes
- Not initializing state
- Missing break statements (state falls through)
- All states in same method (unorganized)

---

## Problem 2: Patrol Behavior

### Solution

```csharp
Vector3[] waypoints = { new Vector3(-5,0,0), new Vector3(5,0,0) };
int current = 0;
float speed = 2f;

void PatrolBehavior()
{
    transform.position = Vector3.Lerp(transform.position, waypoints[current], speed * Time.deltaTime);
    if (Vector3.Distance(transform.position, waypoints[current]) < 0.1f)
        current = (current + 1) % waypoints.Length;
}
```

### What Success Looks Like
- Enemy walks smoothly between waypoints
- Loops back to first waypoint
- Modulo operator cycles indices properly

### Common Mistakes
- Using transform.position = instead of lerp (jumps)
- No waypoint advancement (stays in place)
- Distance check too large (overshoots waypoint)

---

## Problem 3: Chase Behavior

### Solution

```csharp
float detectionRange = 10f;

void ChaseBehavior()
{
    if (Vector3.Distance(transform.position, player.position) < detectionRange)
    {
        Vector3 dir = (player.position - transform.position).normalized;
        transform.position += dir * chaseSpeed * Time.deltaTime;
        state = EnemyState.Chase;
    }
    else
    {
        state = EnemyState.Patrol;
    }
}
```

### What Success Looks Like
- Enemy detects player within range
- Moves directly toward player
- Returns to patrol when player leaves range

### Common Mistakes
- Not normalizing direction (speed varies with distance)
- Using absolute position instead of += (doesn't preserve existing movement)
- No range limit (chases forever)

---

## Problem 4: Object Pool

### Solution

```csharp
public class BulletPool : MonoBehaviour
{
    public GameObject bulletPrefab;
    private List<GameObject> pool = new List<GameObject>();

    public GameObject Get()
    {
        foreach (GameObject bullet in pool)
            if (!bullet.activeInHierarchy)
            {
                bullet.SetActive(true);
                return bullet;
            }
        GameObject newBullet = Instantiate(bulletPrefab);
        pool.Add(newBullet);
        return newBullet;
    }

    public void Return(GameObject bullet)
    {
        bullet.SetActive(false);
    }
}
```

### What Success Looks Like
- Reuses bullets instead of destroying
- No garbage collection spikes
- Efficient memory usage
- Better performance than constant Instantiate/Destroy

### Common Mistakes
- Creating unlimited bullets (defeats pooling purpose)
- Not checking activeInHierarchy (activates same bullet twice)
- Not returning bullets to pool

---

## Problem 5: Wave Spawner

### Solution

```csharp
int currentWave = 1;

void SpawnWave()
{
    int count = 5 + currentWave * 2; // Scales with wave
    for (int i = 0; i < count; i++)
        Instantiate(enemyPrefab, GetRandomSpawnPoint(), Quaternion.identity);
    currentWave++;
}
```

### What Success Looks Like
- Wave 1: 7 enemies
- Wave 2: 9 enemies
- Wave 3: 11 enemies
- Difficulty increases progressively

### Common Mistakes
- Linear growth too fast (unbalanced)
- No maximum cap (impossible later waves)
- Spawning in same location (overlap)

---

## Problem 6: Health Component

### Solution

```csharp
public class Health : MonoBehaviour
{
    public float maxHealth = 100f;
    private float current;

    void Start() => current = maxHealth;

    public void TakeDamage(float damage)
    {
        current -= damage;
        if (current <= 0)
            Destroy(gameObject);
    }
}
```

### What Success Looks Like
- Reusable on any GameObject
- Takes damage and dies
- Simple and clean interface

### Common Mistakes
- No max health (can't heal)
- Not destroying object (dead entity still exists)
- Negative health values possible

---

## Problem 7: Damage Interface

### Solution

```csharp
public interface IDamageable
{
    void TakeDamage(float damage);
}

public class Bullet : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D col)
    {
        IDamageable damageable = col.GetComponent<IDamageable>();
        if (damageable != null)
            damageable.TakeDamage(10);
    }
}
```

### What Success Looks Like
- Any object implementing IDamageable takes damage
- Decoupled: bullets don't know about enemy implementation
- Extensible: new damageable types easily added

### Common Mistakes
- Not checking if null (exception on incompatible objects)
- Casting instead of interface (tightly coupled)
- Destroying before damage applied

---

## Problem 8: ScriptableObject Item

### Solution

```csharp
[CreateAssetMenu(menuName = "Items/NewItem")]
public class ItemData : ScriptableObject
{
    public string itemName;
    public Sprite icon;
    public string description;
}
// Create in Inspector: Right-click → Create → Items → NewItem
```

### What Success Looks Like
- Items created as ScriptableObjects
- Menu option appears in context menu
- Data easily accessible and reusable

### Common Mistakes
- Missing [CreateAssetMenu] attribute (no menu option)
- Wrong menu path (hard to find)
- Not serializing fields (can't edit in Inspector)

---

## Problem 9: Inventory System

### Solution

```csharp
[System.Serializable]
public class InventorySlot { public ItemData item; public int quantity; }

public class Inventory : MonoBehaviour
{
    public InventorySlot[] slots = new InventorySlot[10];

    public void AddItem(ItemData item)
    {
        // Try to add to existing stack
        foreach (var slot in slots)
            if (slot.item == item && slot.quantity < 99)
            {
                slot.quantity++;
                return;
            }
        // Add to empty slot
        foreach (var slot in slots)
            if (slot.item == null)
            {
                slot.item = item;
                slot.quantity = 1;
                return;
            }
    }
}
```

### What Success Looks Like
- Items stack up to 99
- Fills first empty slot
- Can hold 10 items maximum
- Stacking priority respected

### Common Mistakes
- Not checking max quantity (infinite stacking)
- Adding multiple items to same slot
- No full inventory warning

---

## Problem 10: PlayerPrefs Save

### Solution

```csharp
void SaveHighScore(int score)
{
    int highScore = PlayerPrefs.GetInt("HighScore", 0);
    if (score > highScore)
    {
        PlayerPrefs.SetInt("HighScore", score);
        PlayerPrefs.Save();
    }
}

int LoadHighScore() => PlayerPrefs.GetInt("HighScore", 0);
```

### What Success Looks Like
- High score persists between sessions
- Only updates if score is higher
- Default value used if key missing

### Common Mistakes
- Forgetting PlayerPrefs.Save() (doesn't persist)
- Overwriting every score
- No default value (crashes on first run)

---

## Problem 11: JSON Save System

### Solution

```csharp
[System.Serializable]
public class GameState
{
    public float playerHealth;
    public Vector3 playerPos;
    public int score;
}

void SaveGame()
{
    GameState state = new GameState
    {
        playerHealth = 80,
        playerPos = transform.position,
        score = 1000
    };
    string json = JsonUtility.ToJson(state);
    System.IO.File.WriteAllText("save.json", json);
}

void LoadGame()
{
    string json = System.IO.File.ReadAllText("save.json");
    GameState state = JsonUtility.FromJson<GameState>(json);
    // Apply state...
}
```

### What Success Looks Like
- Complex game state saved to file
- Human-readable JSON format
- Data restored from file correctly

### Common Mistakes
- Not marking class Serializable (JSON fails)
- File path wrong (file not found)
- Not checking if file exists (exception on load)

---

## Problem 12: DontDestroyOnLoad

### Solution

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    void Awake()
    {
        if (instance != null)
            Destroy(gameObject);
        else
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
        }
    }
}
```

### What Success Looks Like
- GameManager persists across scene loads
- Only one instance exists
- Accessible from anywhere via GameManager.instance

### Common Mistakes
- Not checking if instance exists (multiple managers)
- Destroying wrong object
- Not calling Awake (check happens too late)

---

## Problem 13: Scene Transitions

### Solution

```csharp
void OnTriggerEnter2D(Collider2D col)
{
    if (col.CompareTag("Player"))
    {
        SceneManager.LoadScene("NextLevel");
    }
}
```

### What Success Looks Like
- Walking into trigger loads next scene
- Scene transitions smoothly
- Previous scene unloaded

### Common Mistakes
- Using wrong tag
- Scene not added to Build Settings (fails)
- No trigger collider (OnTrigger doesn't fire)

---

## Problem 14: Procedural Generation

### Solution

```csharp
void GenerateLevel()
{
    for (float x = 0; x < 100; x += 2)
    {
        if (Random.value < 0.6f)  // 60% spawn chance
        {
            int height = Random.Range(1, 5);
            Instantiate(obstaclePrefab, new Vector3(x, height, 0), Quaternion.identity);
        }
    }
}
```

### What Success Looks Like
- Random obstacle pattern each run
- Difficulty varies
- Layout feels natural, not random

### Common Mistakes
- Random seed not set (same level every time)
- Spawn chance wrong (too sparse or too dense)
- Obstacles overlapping (unrealistic)

---

## Problem 15: Event System

### Solution

```csharp
public class Player : MonoBehaviour
{
    public UnityEvent<int> OnDamaged = new UnityEvent<int>();

    public void TakeDamage(int damage)
    {
        health -= damage;
        OnDamaged.Invoke(damage);
    }
}

// Subscribe:
player.OnDamaged.AddListener((damage) => PlayHitSound());
```

### What Success Looks Like
- Multiple systems respond to damage event
- Loose coupling between systems
- Easy to add new responses without modifying Player

### Common Mistakes
- Not unsubscribing (memory leaks)
- Invoking with wrong parameter type
- No one subscribed (event silent)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | Finite State Machine | Beginner |
| 2 | Patrol Behavior | Beginner |
| 3 | Chase Behavior | Intermediate |
| 4 | Object Pooling | Intermediate |
| 5 | Wave Spawning | Intermediate |
| 6 | Health Component | Beginner |
| 7 | Interface Usage | Intermediate |
| 8 | ScriptableObject | Beginner |
| 9 | Inventory System | Advanced |
| 10 | PlayerPrefs | Beginner |
| 11 | JSON Serialization | Advanced |
| 12 | Singleton Persistence | Intermediate |
| 13 | Scene Management | Beginner |
| 14 | Procedural Generation | Advanced |
| 15 | Event System | Intermediate |
