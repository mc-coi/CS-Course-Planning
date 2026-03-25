# Day 24: Prefabs & Complete Systems

**Learning Target:** Create reusable prefab templates and build a complete 2D game system with enemy spawning and object management.

### Key Concepts

- **Prefab:** A template GameObject that can be instantiated multiple times
- **Prefab Asset:** The template file in the Project folder
- **Prefab Instance:** A copy of the prefab in the scene
- **Overrides:** Changes to a prefab instance that differ from the template
- **Instantiate():** Creates a copy of a prefab at runtime
- **Destroy():** Removes a GameObject from the scene
- **Object Pooling:** Reusing objects instead of creating/destroying (optimization)

### Content

Prefabs are essential for game development. Instead of recreating the same GameObject repeatedly, create it once as a prefab, then instantiate copies.

**Creating Prefabs:**
1. Build a complete GameObject (with all components, scripts, etc.)
2. Drag it from the Hierarchy into the Project folder
3. A blue prefab icon appears in the Project
4. Delete the instance from the Hierarchy
5. Drag the prefab back to instantiate copies

**Using Prefabs in Code:**
```csharp
public GameObject enemyPrefab;
Instantiate(enemyPrefab, spawnPosition, Quaternion.identity);
```

**Benefits:**
- Consistency: All enemies behave identically
- Efficiency: Change the prefab once, all copies update
- Performance: Efficient memory management

### Code Examples

```csharp
using UnityEngine;

public class EnemySpawner : MonoBehaviour
{
    public GameObject enemyPrefab;
    public Transform[] spawnPoints;
    public int enemyCount = 5;

    void Start()
    {
        SpawnEnemies();
    }

    void SpawnEnemies()
    {
        for (int i = 0; i < enemyCount; i++)
        {
            // Pick a random spawn point
            Transform spawnPoint = spawnPoints[Random.Range(0, spawnPoints.Length)];

            // Instantiate a copy of the enemy prefab
            GameObject newEnemy = Instantiate(
                enemyPrefab,
                spawnPoint.position,
                Quaternion.identity
            );

            // Optional: name the instance
            newEnemy.name = "Enemy_" + i;

            // Optional: set as child of spawner
            newEnemy.transform.parent = transform;
        }
    }
}

public class Enemy : MonoBehaviour
{
    public float speed = 2f;
    public int health = 10;
    public GameObject deathEffectPrefab;

    void Update()
    {
        // Simple patrolling
        transform.Translate(speed * Time.deltaTime, 0, 0);
    }

    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        // Instantiate death effect
        if (deathEffectPrefab != null)
        {
            Instantiate(deathEffectPrefab, transform.position, Quaternion.identity);
        }

        // Remove this enemy
        Destroy(gameObject);
    }
}

// Object Pooling example (optimization for frequent instantiation)
public class BulletPool : MonoBehaviour
{
    public GameObject bulletPrefab;
    private Queue<GameObject> bulletPool = new Queue<GameObject>();

    void Start()
    {
        // Pre-create bullets
        for (int i = 0; i < 20; i++)
        {
            GameObject bullet = Instantiate(bulletPrefab);
            bullet.SetActive(false);
            bulletPool.Enqueue(bullet);
        }
    }

    public GameObject GetBullet(Vector3 position)
    {
        GameObject bullet;

        if (bulletPool.Count > 0)
        {
            // Reuse pooled bullet
            bullet = bulletPool.Dequeue();
            bullet.SetActive(true);
            bullet.transform.position = position;
        }
        else
        {
            // Create new if pool is empty
            bullet = Instantiate(bulletPrefab, position, Quaternion.identity);
        }

        return bullet;
    }

    public void ReturnBullet(GameObject bullet)
    {
        bullet.SetActive(false);
        bulletPool.Enqueue(bullet);
    }
}
```

### Guided Practice

**Activity:** Create and use an enemy prefab

1. Create an Enemy GameObject with:
   - Sprite Renderer (enemy sprite)
   - BoxCollider2D
   - Rigidbody2D (Body Type: Dynamic)
   - Enemy script
2. Drag it to the Project folder to create a prefab
3. Delete the scene instance
4. Create an EnemySpawner GameObject with the EnemySpawner script
5. Assign the prefab to the spawner's public field
6. Run and watch enemies spawn

### Practice Problems

**Problem 1 — Beginner:** Import a sprite image and display it using Sprite Renderer. Change its sorting order and color.

**Problem 2 — Intermediate:** Create an enemy prefab that spawns multiple instances at different positions.

**Problem 3 — Challenge:** Create a complete 2D game with player movement, enemies, collectibles, and score system using prefabs.

<details>
<summary>Hints</summary>

**Problem 1:** Import PNG, set Texture Type to "Sprite". Drag onto GameObject. Access SpriteRenderer in Inspector or script.

**Problem 2:** Build a complete enemy GameObject. Drag it to Project to create a prefab. Use Instantiate() to spawn copies.

**Problem 3:** Combine: 2D movement, sprite animation, prefabs for enemies/coins, collision detection, score UI.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
using UnityEngine;

public class SpriteDisplay : MonoBehaviour
{
    void Start()
    {
        SpriteRenderer sr = GetComponent<SpriteRenderer>();
        sr.sortingOrder = 5;
        sr.color = new Color(1, 0.5f, 0);  // Orange
    }
}
```

**Problem 2:**
See EnemySpawner code example above.

**Problem 3:**
Combine code from Days 22, 23, and 24. Add collision detection for coin collection:
```csharp
void OnTriggerEnter2D(Collider2D collision)
{
    if (collision.CompareTag("Coin"))
    {
        score += 10;
        Destroy(collision.gameObject);
    }
}
```

</details>
