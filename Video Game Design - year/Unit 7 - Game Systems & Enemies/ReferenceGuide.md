# Unit 7 Reference Guide: Game Systems & Enemies

## Finite State Machine (FSM) Pattern

### Enum-Based FSM
```csharp
public enum EnemyState { Idle, Patrol, Chase, Attack, Dead }

public class Enemy : MonoBehaviour
{
    private EnemyState currentState = EnemyState.Idle;

    void Update()
    {
        switch(currentState)
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

    void ChangeState(EnemyState newState)
    {
        currentState = newState;
        // Optional: OnStateExit/OnStateEnter callbacks
    }
}
```

### State Transitions
- Check conditions at end of behavior
- Example: "If player in range, ChangeState(EnemyState.Chase)"
- Common transitions: Idle→Patrol, Patrol→Chase, Chase→Attack, Any→Dead

---

## Enemy AI Patterns

### Patrol
```csharp
private Vector3[] waypoints;
private int currentWaypoint = 0;
private float patrolSpeed = 2f;

void PatrolBehavior()
{
    Vector3 targetPos = waypoints[currentWaypoint];
    transform.position = Vector3.Lerp(transform.position, targetPos, patrolSpeed * Time.deltaTime);
    
    if (Vector3.Distance(transform.position, targetPos) < 0.1f)
        currentWaypoint = (currentWaypoint + 1) % waypoints.Length;
}
```

### Chase
```csharp
private Transform playerTransform;
private float detectionRange = 10f;
private float chaseSpeed = 3f;

void ChaseBehavior()
{
    float distToPlayer = Vector3.Distance(transform.position, playerTransform.position);
    
    if (distToPlayer < detectionRange)
    {
        Vector3 direction = (playerTransform.position - transform.position).normalized;
        transform.position += direction * chaseSpeed * Time.deltaTime;
    }
    else
        ChangeState(EnemyState.Patrol);
}
```

### Attack
```csharp
private float attackCooldown = 2f;
private float attackTimer = 0;

void AttackBehavior()
{
    attackTimer -= Time.deltaTime;
    
    if (attackTimer <= 0)
    {
        DealDamage(playerTransform.GetComponent<Health>(), 10);
        attackTimer = attackCooldown;
    }
    
    // Return to chase if player too far
    if (Vector3.Distance(transform.position, playerTransform.position) > 5f)
        ChangeState(EnemyState.Chase);
}
```

---

## Object Pooling

### Pool Manager
```csharp
public class ObjectPool : MonoBehaviour
{
    public GameObject prefab;
    public int poolSize = 10;
    private List<GameObject> pool = new List<GameObject>();

    void Start()
    {
        // Pre-create objects
        for (int i = 0; i < poolSize; i++)
        {
            GameObject obj = Instantiate(prefab);
            obj.SetActive(false);
            pool.Add(obj);
        }
    }

    public GameObject GetObject()
    {
        foreach (GameObject obj in pool)
        {
            if (!obj.activeInHierarchy)
            {
                obj.SetActive(true);
                return obj;
            }
        }
        // If no inactive objects, create new one
        GameObject newObj = Instantiate(prefab);
        pool.Add(newObj);
        return newObj;
    }

    public void ReturnObject(GameObject obj)
    {
        obj.SetActive(false);
    }
}
```

### Benefits
- Avoid Destroy() overhead (expensive)
- Reduce garbage collection pauses
- Reuse objects: bullets, particles, enemies

---

## Spawner Systems

### Wave Spawner
```csharp
public class WaveSpawner : MonoBehaviour
{
    public GameObject[] enemyPrefabs;
    public int enemiesPerWave = 5;
    private int currentWave = 1;

    void Update()
    {
        if (EnemiesDefeated())
            StartNextWave();
    }

    void StartNextWave()
    {
        int enemiesToSpawn = enemiesPerWave + (currentWave - 1) * 2; // Scaling
        
        for (int i = 0; i < enemiesToSpawn; i++)
        {
            Vector3 spawnPos = GetRandomSpawnPoint();
            GameObject enemy = Instantiate(enemyPrefabs[Random.Range(0, enemyPrefabs.Length)], spawnPos, Quaternion.identity);
        }
        currentWave++;
    }
}
```

### Timed Spawner
```csharp
private float spawnInterval = 3f;
private float spawnTimer = 0;

void Update()
{
    spawnTimer -= Time.deltaTime;
    
    if (spawnTimer <= 0)
    {
        SpawnEnemy();
        spawnTimer = spawnInterval;
    }
}
```

---

## Health & Damage System

### Health Component
```csharp
public interface IDamageable
{
    void TakeDamage(float damage);
}

public class Health : MonoBehaviour, IDamageable
{
    public float maxHealth = 100f;
    private float currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(float damage)
    {
        currentHealth -= damage;
        if (currentHealth <= 0)
            Die();
    }

    private void Die()
    {
        Destroy(gameObject);
    }
}

// Usage:
Health health = enemy.GetComponent<Health>();
health.TakeDamage(20);
```

---

## ScriptableObject Pattern

### Item Definition
```csharp
[CreateAssetMenu(menuName = "Items/New Item")]
public class ItemData : ScriptableObject
{
    public string itemName = "Item";
    public Sprite icon;
    public int stackLimit = 99;
    public string description = "";
}

// Create in Inspector: Right-click Project → Create → Items → New Item
```

### Inventory
```csharp
[System.Serializable]
public class InventorySlot
{
    public ItemData item;
    public int quantity = 0;
}

public class Inventory : MonoBehaviour
{
    public InventorySlot[] slots = new InventorySlot[10];

    public void AddItem(ItemData item)
    {
        foreach (InventorySlot slot in slots)
        {
            if (slot.item == item && slot.quantity < item.stackLimit)
            {
                slot.quantity++;
                return;
            }
        }
        
        // Find empty slot
        foreach (InventorySlot slot in slots)
        {
            if (slot.item == null)
            {
                slot.item = item;
                slot.quantity = 1;
                return;
            }
        }
    }
}
```

---

## Save System Patterns

### Simple PlayerPrefs
```csharp
public void SaveGame()
{
    PlayerPrefs.SetInt("Level", currentLevel);
    PlayerPrefs.SetFloat("Health", health);
    PlayerPrefs.SetString("PlayerName", playerName);
    PlayerPrefs.Save();
}

public void LoadGame()
{
    currentLevel = PlayerPrefs.GetInt("Level", 1);
    health = PlayerPrefs.GetFloat("Health", 100);
    playerName = PlayerPrefs.GetString("PlayerName", "Player");
}
```

### JSON Serialization (Complex Data)
```csharp
[System.Serializable]
public class GameState
{
    public float playerHealth;
    public Vector3 playerPosition;
    public int score;
}

public void SaveToJSON()
{
    GameState state = new GameState { /* populate */ };
    string json = JsonUtility.ToJson(state);
    System.IO.File.WriteAllText("savegame.json", json);
}

public void LoadFromJSON()
{
    string json = System.IO.File.ReadAllText("savegame.json");
    GameState state = JsonUtility.FromJson<GameState>(json);
}
```

---

## Scene Management

### DontDestroyOnLoad
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
            DontDestroyOnLoad(gameObject); // Persists across scenes
        }
    }
}
```

### Scene Loading
```csharp
using UnityEngine.SceneManagement;

SceneManager.LoadScene("GameScene");
SceneManager.LoadSceneAsync("GameScene"); // Async load

// Get current scene info
string currentScene = SceneManager.GetActiveScene().name;
int sceneIndex = SceneManager.GetActiveScene().buildIndex;
```

---

## Procedural Generation

### Random Obstacle Spawning
```csharp
void GenerateLevel()
{
    for (float x = 0; x < levelWidth; x += 2)
    {
        if (Random.value < 0.6f) // 60% chance
        {
            int height = Random.Range(1, 5);
            Vector3 pos = new Vector3(x, height, 0);
            Instantiate(obstaclePrefab, pos, Quaternion.identity);
        }
    }
}
```

### Perlin Noise Terrain
```csharp
void GenerateTerrainWithPerlin()
{
    for (int x = 0; x < levelWidth; x++)
    {
        float height = Mathf.PerlinNoise(x * 0.1f, seed) * maxHeight;
        Vector3 pos = new Vector3(x, height, 0);
        Instantiate(tilePrefab, pos, Quaternion.identity);
    }
}
```

---

## Event System

### Unity Events
```csharp
using UnityEngine.Events;

public class Player : MonoBehaviour
{
    public UnityEvent OnPlayerDamaged = new UnityEvent();
    public UnityEvent OnPlayerHealed = new UnityEvent();

    public void TakeDamage(float damage)
    {
        health -= damage;
        OnPlayerDamaged.Invoke();
    }

    public void Heal(float amount)
    {
        health += amount;
        OnPlayerHealed.Invoke();
    }
}

// Subscribe to events
player.OnPlayerDamaged.AddListener(PlayDamageSound);
```
