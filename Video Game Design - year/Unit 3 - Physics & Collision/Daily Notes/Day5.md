# Day 5: OnCollisionEnter & OnCollisionExit

**Learning Target:** I can detect when two Rigidbodies collide and execute code based on collision events.

---

## Key Concepts

**OnCollisionEnter(Collision collision)** — Called when two Rigidbodies first touch. Fires once per collision.

**OnCollisionExit(Collision collision)** — Called when two Rigidbodies stop touching. Fires once per separation.

**OnCollisionStay(Collision collision)** — Called every frame while two Rigidbodies are touching.

**Collision parameter** — Contains info about the collision: `collision.gameObject`, `collision.relativeVelocity`, `collision.contacts[]`.

**Requirements for collision events:**
1. Both objects need a Collider (not marked as trigger)
2. At least one must have a Rigidbody
3. The Rigidbody must not have isKinematic = true

**Real-world examples:**
- **Super Mario:** Jumping on a Goomba triggers OnCollisionEnter, game checks if Mario is above it
- **Crash Bandicoot:** Crashing into a crate calls OnCollisionEnter to damage/destroy it
- **Portal 2:** Objects hitting laser triggers OnCollisionEnter to vaporize them

---

## Code Example

```csharp
using UnityEngine;

public class CollisionDetection : MonoBehaviour
{
    private Rigidbody rb;
    public int health = 3;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    // Called when collision begins
    private void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Hit by: " + collision.gameObject.name);

        // Check what we hit
        if (collision.gameObject.CompareTag("Enemy"))
        {
            TakeDamage(1);
        }

        if (collision.gameObject.CompareTag("Platform"))
        {
            Debug.Log("Landed on platform");
        }

        // Get collision impact info
        float impactForce = collision.relativeVelocity.magnitude;
        Debug.Log("Impact force: " + impactForce);
    }

    // Called when collision ends
    private void OnCollisionExit(Collision collision)
    {
        if (collision.gameObject.CompareTag("Platform"))
        {
            Debug.Log("Left the platform");
        }
    }

    // Called every frame while colliding
    private void OnCollisionStay(Collision collision)
    {
        // Can be used to apply continuous effects
        // Be careful—this fires every frame!
    }

    private void TakeDamage(int damage)
    {
        health -= damage;
        Debug.Log("Health: " + health);
        if (health <= 0)
        {
            Destroy(gameObject);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create Player (Capsule)** with Rigidbody (not isKinematic)
2. **Create Platform (Box)** with BoxCollider. Make Rigidbody Static
3. **Tag the Platform:** Select it → Inspector → Tag dropdown → "Platform"
4. **Create Enemy (Cube)** with Rigidbody (not isKinematic). Tag it "Enemy"
5. **Attach CollisionDetection script to Player**
6. **Press Play:** Walk into the platform and enemy, watch console output

---

## Guided Practice

1. Create a ball and three walls (tagged "Wall1", "Wall2", "Wall3")
2. Add a script that counts collisions: `int hitCount = 0`
3. In OnCollisionEnter, increment hitCount and print it
4. Throw the ball at walls and count bounces in console

---

## Practice Problems

**Beginner:** Create a ball and a target cube. When they collide, print "Hit!" to the console and destroy the target.

**Intermediate:** Build a "lives" system. The player loses a life when hitting an "Enemy" tag. When lives reach 0, display "Game Over" in console.

**Challenge:** Create a "damage on touch" enemy. When the player collides with it, apply knockback force (AddForce in direction away from enemy) and reduce player health.

<details><summary>💡 Hints</summary>
- Use `collision.transform.position` to get the other object's position
- `collision.relativeVelocity.magnitude` tells you how fast objects hit each other
- Tag all objects first, then use `CompareTag()` to identify them
- OnCollisionStay is called every frame—avoid putting heavy code there
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Knockback on enemy collision
public class EnemyDamage : MonoBehaviour
{
    public float knockbackForce = 10f;
    public int damage = 1;

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            Rigidbody playerRb = collision.gameObject.GetComponent<Rigidbody>();
            if (playerRb != null)
            {
                // Knockback away from enemy
                Vector3 knockbackDirection = (collision.transform.position - transform.position).normalized;
                playerRb.AddForce(knockbackDirection * knockbackForce, ForceMode.Impulse);
            }
        }
    }
}
```

</details>
