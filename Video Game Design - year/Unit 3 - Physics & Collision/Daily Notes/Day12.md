# Day 12: Raycasting for Shooting & Targeting

**Learning Target:** I can use raycasts to implement shooting systems and target detection.

---

## Key Concepts

**Raycast from camera** — Shoot from player's viewpoint to detect what they're aiming at.

**Instant hit detection** — No projectile needed. Raycast is instant (good for bullets, lasers).

**Raycast with LayerMask** — Only detect specific layer types (enemies, not walls).

**Multiple raycasts** — Spread raycasts for shotgun effect or hitscan weapons.

**Real-world examples:**
- **Halo:** Instant-hit weapons use raycasts from gun barrel
- **Portal 2:** Portal gun uses raycasts to detect valid surfaces
- **Minecraft:** Mining uses raycast to detect block player is looking at
- **CS:GO:** Weapons use raycasts from player position

---

## Code Example

```csharp
using UnityEngine;

public class RaycastShootingSystem : MonoBehaviour
{
    private Camera cam;
    public LayerMask enemyLayer;
    public int damage = 25;
    public float maxDistance = 100f;
    
    // Shotgun spread
    public int pelletsPerShot = 8;
    public float spreadAngle = 15f;

    private void Start()
    {
        cam = GetComponent<Camera>();
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Shoot();
        }
    }

    private void Shoot()
    {
        // Single shot raycast
        RaycastHit hit;
        Vector3 rayOrigin = cam.transform.position;
        Vector3 rayDirection = cam.transform.forward;

        if (Physics.Raycast(rayOrigin, rayDirection, out hit, maxDistance, enemyLayer))
        {
            // We hit an enemy
            Health health = hit.transform.GetComponent<Health>();
            if (health != null)
            {
                health.TakeDamage(damage);
                Debug.Log("Hit " + hit.transform.name + " for " + damage + " damage");
            }

            // Create hit effect at impact point
            InstantiateHitEffect(hit.point, hit.normal);
        }
        else
        {
            Debug.Log("Miss!");
        }

        Debug.DrawLine(rayOrigin, rayOrigin + rayDirection * maxDistance, Color.red, 0.1f);
    }

    public void ShotgunShoot()
    {
        // Multiple raycasts in a spread
        for (int i = 0; i < pelletsPerShot; i++)
        {
            // Random spread around forward direction
            float randomX = Random.Range(-spreadAngle, spreadAngle);
            float randomY = Random.Range(-spreadAngle, spreadAngle);
            
            Vector3 spreadDirection = cam.transform.forward;
            spreadDirection = Quaternion.Euler(randomX, randomY, 0) * spreadDirection;

            RaycastHit hit;
            if (Physics.Raycast(cam.transform.position, spreadDirection, out hit, maxDistance, enemyLayer))
            {
                Health health = hit.transform.GetComponent<Health>();
                if (health != null)
                {
                    health.TakeDamage(damage / 2); // Each pellet does less damage
                }
            }
        }
    }

    private void InstantiateHitEffect(Vector3 position, Vector3 normal)
    {
        // Could instantiate particle effects or decals here
        Debug.Log("Hit effect at " + position);
    }
}

public class Health : MonoBehaviour
{
    public int maxHealth = 100;
    private int currentHealth;

    private void Start()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int amount)
    {
        currentHealth -= amount;
        if (currentHealth <= 0)
        {
            Die();
        }
    }

    private void Die()
    {
        Destroy(gameObject);
    }
}
```

---

## Unity Setup Steps

1. **Create layers:** Player, Enemy, Wall
2. **Create Player (Capsule)** with Camera child object
3. **Create Enemies (Cubes)** with Health scripts, layer = "Enemy"
4. **Attach RaycastShootingSystem to Camera**
5. **Set Enemy Layer** in Inspector shooting script
6. **Press Play:** Click to shoot at enemies

---

## Guided Practice

1. Set up player with camera
2. Create 5 enemy targets
3. Implement single-shot raycast shooting
4. Test aiming at enemies
5. Modify damage amount and test

---

## Practice Problems

**Beginner:** Create a raycast gun that damages enemies. Print hits and misses.

**Intermediate:** Build a shotgun with 8 pellets fired in a spread pattern. Each pellet does less damage.

**Challenge:** Create a beam weapon that fires continuously while mouse is held down. Damage increases if you keep the beam on the same target.

<details><summary>💡 Hints</summary>
- Use `Random.Range()` to spread rays in cone
- `Quaternion.Euler()` rotates direction by angle
- Each pellet should have slightly different damage
- For continuous beams, raycast in Update() while button held
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Beam weapon
public class BeamWeapon : MonoBehaviour
{
    private Camera cam;
    public LayerMask enemyLayer;
    public float damagePerSecond = 50f;
    public float maxDistance = 100f;
    
    private Health currentTarget = null;
    private float timeOnTarget = 0f;

    private void Start()
    {
        cam = GetComponent<Camera>();
    }

    private void Update()
    {
        if (Input.GetMouseButton(0))
        {
            FireBeam();
        }
        else
        {
            timeOnTarget = 0f;
            currentTarget = null;
        }
    }

    private void FireBeam()
    {
        RaycastHit hit;
        Vector3 rayOrigin = cam.transform.position;
        Vector3 rayDirection = cam.transform.forward;

        if (Physics.Raycast(rayOrigin, rayDirection, out hit, maxDistance, enemyLayer))
        {
            Health health = hit.transform.GetComponent<Health>();
            
            if (health == currentTarget)
            {
                timeOnTarget += Time.deltaTime;
            }
            else
            {
                currentTarget = health;
                timeOnTarget = 0f;
            }

            if (currentTarget != null)
            {
                float damageThisFrame = damagePerSecond * Time.deltaTime;
                currentTarget.TakeDamage((int)damageThisFrame);
            }
        }
    }
}
```

</details>
