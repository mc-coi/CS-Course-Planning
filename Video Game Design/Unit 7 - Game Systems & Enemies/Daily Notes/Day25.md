# Day 25: Health Components & Modular Design

**Learning Target:** Design and implement modular health/damage systems that can be reused across different entity types.

### Key Concepts

- **Health System:** Tracks entity health and handles damage
- **Modular Design:** Breaking code into independent, reusable components
- **Damage Method:** Public method for taking damage
- **Death Handler:** Cleanup and effects when health reaches 0
- **Damage Types:** Different damage sources (weapon, hazard, poison)
- **Knockback:** Pushing entity away on impact
- **Invulnerability Frames:** Temporary immunity to damage

### Content

A health system is essential for games with enemies and damage. Instead of each script handling damage independently, create a reusable Health component.

**Health Component Benefits:**
- Consistency: All entities with health behave the same way
- Reusability: Add to player, enemies, destructible objects
- Maintainability: Changes to health logic happen in one place

**Modular Design Pattern:**
Instead of one big script doing everything:
- Create a Health component (handles damage, death)
- Create an Enemy component (handles AI)
- Create a Weapon component (handles attacks)
- Create a GameManager component (coordinates everything)

Each component is independent and can be reused.

### Code Examples

```csharp
using UnityEngine;

// Reusable health component
public class Health : MonoBehaviour
{
    [Header("Health Settings")]
    public int maxHealth = 100;
    public int currentHealth;

    [Header("Damage Settings")]
    public float invulnerabilityDuration = 0.2f;
    private float invulnerabilityTimer = 0f;

    [Header("References")]
    public GameObject deathEffectPrefab;
    public AudioClip damageSound;
    public AudioClip deathSound;

    // Events for other systems to listen to
    public delegate void HealthChangedEvent(int newHealth);
    public event HealthChangedEvent OnHealthChanged;

    void Start()
    {
        currentHealth = maxHealth;
        OnHealthChanged?.Invoke(currentHealth);
    }

    void Update()
    {
        // Decrease invulnerability timer
        if (invulnerabilityTimer > 0)
        {
            invulnerabilityTimer -= Time.deltaTime;
        }
    }

    // Public method for taking damage
    public void TakeDamage(int damageAmount)
    {
        // Don't take damage if invulnerable
        if (invulnerabilityTimer > 0)
        {
            Debug.Log("Invulnerable! Ignoring damage.");
            return;
        }

        currentHealth -= damageAmount;
        invulnerabilityTimer = invulnerabilityDuration;

        Debug.Log(gameObject.name + " took " + damageAmount + " damage. Health: " + currentHealth);

        // Clamp health to 0
        if (currentHealth < 0)
            currentHealth = 0;

        // Invoke event so UI and other systems update
        OnHealthChanged?.Invoke(currentHealth);

        // Play damage sound
        if (damageSound != null)
        {
            AudioSource.PlayClipAtPoint(damageSound, transform.position);
        }

        // Check if dead
        if (currentHealth <= 0)
        {
            Die();
        }
    }

    public void Heal(int healAmount)
    {
        currentHealth += healAmount;
        if (currentHealth > maxHealth)
            currentHealth = maxHealth;

        Debug.Log("Healed " + healAmount + " health. Current: " + currentHealth);
        OnHealthChanged?.Invoke(currentHealth);
    }

    void Die()
    {
        Debug.Log(gameObject.name + " died!");

        // Play death effect
        if (deathEffectPrefab != null)
        {
            Instantiate(deathEffectPrefab, transform.position, Quaternion.identity);
        }

        // Play death sound
        if (deathSound != null)
        {
            AudioSource.PlayClipAtPoint(deathSound, transform.position);
        }

        // Notify other systems
        GetComponent<IDeathHandler>()?.OnDeath();

        // Remove from scene
        Destroy(gameObject);
    }

    public bool IsAlive()
    {
        return currentHealth > 0;
    }

    public float GetHealthPercent()
    {
        return (float)currentHealth / maxHealth;
    }
}

// Interface for death handling
public interface IDeathHandler
{
    void OnDeath();
}

// Example: Enemy that implements IDeathHandler
public class Enemy : MonoBehaviour, IDeathHandler
{
    private Health health;

    void Start()
    {
        health = GetComponent<Health>();
    }

    public void OnDeath()
    {
        Debug.Log("Enemy died! Award points.");
        GameManager.instance.AddScore(100);
    }
}
```

### Guided Practice

1. Create a new script called `Health.cs` and attach it to an enemy GameObject
2. Set maxHealth to 100 in the Inspector
3. Create a simple collision script that calls `TakeDamage(10)` when the player touches the enemy
4. Test by colliding with the enemy and watching health decrease
5. Verify the enemy is destroyed when health reaches 0

### Practice Problems

**Problem 1 — Beginner:** Create a Health component and attach it to an enemy. Make the enemy take damage on collision with the player.

**Problem 2 — Intermediate:** Implement invulnerability frames so the player flashes white after taking damage and can't take damage for 0.5 seconds.

**Problem 3 — Challenge:** Create a damage feedback system that displays floating damage numbers above the enemy's head when they take damage.

<details>
<summary>Hints</summary>

**Problem 1:** Create Health.cs component. In OnCollisionEnter(), call TakeDamage(). Verify health decreases and enemy dies at 0 health.

**Problem 2:** Track invulnerability timer and return early from TakeDamage if timer > 0. Use SpriteRenderer.color to flash.

**Problem 3:** Instantiate a prefab with a TextMeshPro component. Have it display damage amount, fade out, and destroy itself after 1 second.

</details>

<details>
<summary>Sample Answers</summary>

See the Annotated Code Example in the Key Concepts section above for the complete Health class implementation.

For invulnerability frames, the Health class already includes this:
```csharp
if (invulnerabilityTimer > 0)
{
    Debug.Log("Invulnerable! Ignoring damage.");
    return;
}
```

For floating damage numbers, create a DamagePopup prefab and instantiate it in the TakeDamage method:
```csharp
if (deathEffectPrefab != null)
{
    Instantiate(deathEffectPrefab, transform.position, Quaternion.identity);
}
```

</details>
