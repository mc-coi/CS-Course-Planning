# Unit 7 Practice Problems

15 problems covering enemy AI, spawning, health systems, inventory, and persistence.

---

## Problem 1: Simple FSM (Beginner)
Write an enum-based FSM skeleton for an enemy.

<details><summary>Solution</summary>
```csharp
public enum EnemyState { Idle, Patrol, Chase, Attack }
public class Enemy : MonoBehaviour
{
    private EnemyState state = EnemyState.Idle;
    
    void Update()
    {
        switch(state)
        {
            case EnemyState.Idle: break;
            case EnemyState.Patrol: break;
            case EnemyState.Chase: break;
            case EnemyState.Attack: break;
        }
    }
}
```
</details>

---

## Problem 2: Patrol Behavior (Beginner)
Create an enemy that walks between two waypoints.

<details><summary>Solution</summary>
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
</details>

---

## Problem 3: Chase Behavior (Intermediate)
Enemy detects player in range and chases them.

<details><summary>Solution</summary>
```csharp
float detectionRange = 10f;
if (Vector3.Distance(transform.position, player.position) < detectionRange)
{
    Vector3 dir = (player.position - transform.position).normalized;
    transform.position += dir * chaseSpeed * Time.deltaTime;
    state = EnemyState.Chase;
}
```
</details>

---

## Problem 4: Object Pool (Intermediate)
Write an object pool for bullets.

<details><summary>Solution</summary>
```csharp
public class BulletPool : MonoBehaviour
{
    public GameObject bulletPrefab;
    private List<GameObject> pool = new List<GameObject>();
    
    public GameObject Get()
    {
        foreach (GameObject bullet in pool)
            if (!bullet.activeInHierarchy) { bullet.SetActive(true); return bullet; }
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
</details>

---

## Problem 5: Wave Spawner (Challenge)
Create a spawner that increases difficulty each wave.

<details><summary>Solution</summary>
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
</details>

---

## Problem 6: Health Component (Beginner)
Create a reusable Health component with TakeDamage().

<details><summary>Solution</summary>
```csharp
public class Health : MonoBehaviour
{
    public float maxHealth = 100f;
    private float current;
    
    void Start() => current = maxHealth;
    
    public void TakeDamage(float damage)
    {
        current -= damage;
        if (current <= 0) Destroy(gameObject);
    }
}
```
</details>

---

## Problem 7: Damage Interface (Intermediate)
Create an interface so anything can take damage.

<details><summary>Solution</summary>
```csharp
public interface IDamageable
{
    void TakeDamage(float damage);
}

// Usage:
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
</details>

---

## Problem 8: ScriptableObject Item (Beginner)
Create an ItemData ScriptableObject for inventory items.

<details><summary>Solution</summary>
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
</details>

---

## Problem 9: Inventory System (Challenge)
Create an inventory that holds multiple items with quantities.

<details><summary>Solution</summary>
```csharp
[System.Serializable]
public class InventorySlot { public ItemData item; public int quantity; }

public class Inventory : MonoBehaviour
{
    public InventorySlot[] slots = new InventorySlot[10];
    
    public void AddItem(ItemData item)
    {
        foreach (var slot in slots)
            if (slot.item == item && slot.quantity < 99) { slot.quantity++; return; }
        foreach (var slot in slots)
            if (slot.item == null) { slot.item = item; slot.quantity = 1; return; }
    }
}
```
</details>

---

## Problem 10: PlayerPrefs Save (Beginner)
Save and load high score using PlayerPrefs.

<details><summary>Solution</summary>
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
</details>

---

## Problem 11: JSON Save System (Challenge)
Save complex game state to JSON file.

<details><summary>Solution</summary>
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
    GameState state = new GameState { playerHealth = 80, playerPos = transform.position, score = 1000 };
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
</details>

---

## Problem 12: DontDestroyOnLoad (Beginner)
Make a GameManager persist across scenes.

<details><summary>Solution</summary>
```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;
    
    void Awake()
    {
        if (instance != null) Destroy(gameObject);
        else { instance = this; DontDestroyOnLoad(gameObject); }
    }
}
```
</details>

---

## Problem 13: Scene Transitions (Intermediate)
Load a new scene when player reaches the goal.

<details><summary>Solution</summary>
```csharp
void OnTriggerEnter2D(Collider2D col)
{
    if (col.CompareTag("Player"))
    {
        SceneManager.LoadScene("NextLevel");
    }
}
```
</details>

---

## Problem 14: Procedural Generation (Challenge)
Generate random obstacles across a level.

<details><summary>Solution</summary>
```csharp
void GenerateLevel()
{
    for (float x = 0; x < 100; x += 2)
    {
        if (Random.value < 0.6f)
        {
            int height = Random.Range(1, 5);
            Instantiate(obstaclePrefab, new Vector3(x, height, 0), Quaternion.identity);
        }
    }
}
```
</details>

---

## Problem 15: Event System (Intermediate)
Use UnityEvent for loose coupling between systems.

<details><summary>Solution</summary>
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
</details>

---

## Answer Summary

| Problem | Concept |
|---------|---------|
| 1 | FSM enum |
| 2 | Patrol behavior |
| 3 | Chase behavior |
| 4 | Object pooling |
| 5 | Wave spawner |
| 6 | Health component |
| 7 | Damage interface |
| 8 | ScriptableObject |
| 9 | Inventory system |
| 10 | PlayerPrefs |
| 11 | JSON serialization |
| 12 | DontDestroyOnLoad |
| 13 | Scene transitions |
| 14 | Procedural generation |
| 15 | Event system |
