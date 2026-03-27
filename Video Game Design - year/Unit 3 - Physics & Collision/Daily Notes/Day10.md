# Day 10: Physics.CheckSphere & Overlap Detection

**Learning Target:** I can detect all objects within a radius using Physics.OverlapSphere and Physics.CheckSphere.

---

## Key Concepts

**Physics.OverlapSphere(Vector3 position, float radius)** — Returns array of all Colliders touching a sphere at position.

**Physics.CheckSphere(Vector3 position, float radius)** — Returns true if any collider touches the sphere (faster, no array).

**Physics.OverlapBox, Physics.OverlapCapsule** — Same concept but for box/capsule shapes.

**LayerMask filtering** — All Physics functions accept a LayerMask parameter to filter results.

**Real-world examples:**
- **Minecraft:** Check sphere to detect blocks near player
- **Dark Souls:** Check sphere around enemy to detect players in aggro range
- **Pokémon:** Check sphere to detect nearby wild Pokémon
- **Explosion damage:** OverlapSphere centered at explosion point damages all enemies nearby

---

## Code Example

```csharp
using UnityEngine;

public class ExplosionDamage : MonoBehaviour
{
    public float explosionRadius = 5f;
    public int damage = 50;
    public LayerMask damageLayer; // Set to "Enemy" layer in Inspector

    public void Explode()
    {
        // Get all enemies in radius
        Collider[] hitColliders = Physics.OverlapSphere(transform.position, explosionRadius, damageLayer);

        foreach (Collider hitCollider in hitColliders)
        {
            // Get Health component and damage it
            Health health = hitCollider.GetComponent<Health>();
            if (health != null)
            {
                // Calculate falloff damage (closer = more damage)
                float distance = Vector3.Distance(transform.position, hitCollider.transform.position);
                float damageMultiplier = 1f - (distance / explosionRadius);
                int actualDamage = Mathf.RoundToInt(damage * damageMultiplier);

                health.TakeDamage(actualDamage);
                Debug.Log("Hit " + hitCollider.gameObject.name + " for " + actualDamage + " damage");
            }

            // Apply knockback
            Rigidbody rb = hitCollider.GetComponent<Rigidbody>();
            if (rb != null)
            {
                Vector3 explosionDirection = (hitCollider.transform.position - transform.position).normalized;
                rb.AddForce(explosionDirection * 10f, ForceMode.Impulse);
            }
        }

        Destroy(gameObject);
    }

    private void OnDrawGizmosSelected()
    {
        // Visualize explosion radius in editor
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position, explosionRadius);
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
        Debug.Log(gameObject.name + " health: " + currentHealth);
        if (currentHealth <= 0)
        {
            Die();
        }
    }

    private void Die()
    {
        Debug.Log(gameObject.name + " died!");
        Destroy(gameObject);
    }
}
```

---

## Unity Setup Steps

1. **Create layers:** Enemy, Player, Explosion (see Day 9)
2. **Create a bomb (sphere)** with the ExplosionDamage script
3. **Create 5 enemies (cubes)** with Health scripts, layer set to "Enemy"
4. **In Inspector, set Damage Layer** to "Enemy" on the bomb
5. **Add a trigger zone** to the bomb that calls Explode() when touched
6. **Press Play:** Trigger the bomb and watch enemies take damage

---

## Guided Practice

1. Create a radial damage system
2. Place bomb in center, enemies around it
3. Trigger bomb and confirm damage falloff (closer enemies take more damage)
4. Adjust explosionRadius and verify it only damages objects nearby
5. Add visual indication (growing sphere gizmo) of explosion radius

---

## Practice Problems

**Beginner:** Create a "heal pulse" ability. Center on player, heal all allies within 5 units.

**Intermediate:** Build an "aggro system." Enemies detect player using OverlapSphere. When player enters radius, enemies chase and attack.

**Challenge:** Create a "shockwave" that expands outward. Use OverlapSphere with increasing radius to push objects away in expanding waves.

<details><summary>💡 Hints</summary>
- Use OnDrawGizmosSelected() to visualize sphere in editor (not at runtime)
- Store OverlapSphere result in array and iterate through
- Distance falloff: `1 - (distance / maxDistance)` creates smooth reduction
- CheckSphere is faster if you only need true/false
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Expanding shockwave
public class Shockwave : MonoBehaviour
{
    public float maxRadius = 10f;
    public float expandSpeed = 5f;
    public LayerMask objectLayer;
    
    private float currentRadius = 0f;

    private void Update()
    {
        currentRadius += expandSpeed * Time.deltaTime;

        if (currentRadius >= maxRadius)
        {
            Destroy(gameObject);
            return;
        }

        Collider[] hit = Physics.OverlapSphere(transform.position, currentRadius, objectLayer);
        
        foreach (Collider obj in hit)
        {
            Rigidbody rb = obj.GetComponent<Rigidbody>();
            if (rb != null)
            {
                Vector3 pushDir = (obj.transform.position - transform.position).normalized;
                rb.velocity = pushDir * 10f;
            }
        }
    }

    private void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.yellow;
        Gizmos.DrawWireSphere(transform.position, currentRadius);
    }
}
```

</details>
