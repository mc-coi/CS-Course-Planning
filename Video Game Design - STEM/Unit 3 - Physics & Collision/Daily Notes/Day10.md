# Day 10: Colliders & Collision Detection

**Learning Target:** Detect and respond to collisions between GameObjects using collision callbacks.

### Key Concepts

- **Collider:** A shape that defines an object's physical boundaries
- **Box Collider:** Rectangular collision shape (good for cubes, blocks)
- **Sphere Collider:** Circular collision shape (good for balls, spheres)
- **Capsule Collider:** Elongated rounded shape (good for characters)
- **OnCollisionEnter():** Called when two colliders first touch
- **OnCollisionStay():** Called every frame while colliders are touching
- **OnCollisionExit():** Called when colliders stop touching
- **Tag:** A label for identifying GameObjects
- **CompareTag():** Efficiently checks if an object has a specific tag
- **Rigidbody Requirement:** OnCollision methods require a Rigidbody on at least one object

### Content

Colliders define the physical shape of objects. Most GameObjects need a collider to interact with physics and detect collisions.

**Collider Types:**
- **Box Collider:** Perfect for rectangular objects. Set Size to match the GameObject's visual dimensions.
- **Sphere Collider:** Perfect for round objects. Set Radius to match visual size.
- **Capsule Collider:** Good for character bodies. Typically oriented along the Y axis.

**Collision Detection Callbacks:**
These methods are called automatically by Unity when collisions happen:

```csharp
void OnCollisionEnter(Collision collision)
{
    // Called once when collision begins
    // collision contains info about the other object
}

void OnCollisionStay(Collision collision)
{
    // Called every frame while colliding
}

void OnCollisionExit(Collision collision)
{
    // Called once when collision ends
}
```

**Tags:**
Tags are string labels for GameObjects. Create tags in Tags & Layers (top right of Inspector):
1. Click "Add Tag"
2. Create a new tag name (e.g., "Enemy", "Coin", "Platform")
3. Assign tags to GameObjects
4. Check tags with CompareTag() (more efficient than == comparison)

### Code Examples

```csharp
using UnityEngine;

public class CollisionDetector : MonoBehaviour
{
    public int damageOnImpact = 10;
    private int timesCollided = 0;

    void Start()
    {
        // Add a tag "Hazard" in the Tags & Layers menu first
        gameObject.tag = "Hazard";
    }

    // Called when this object collides with another
    void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Collided with: " + collision.gameObject.name);
        timesCollided++;

        // Check if the colliding object is an enemy
        if (collision.gameObject.CompareTag("Enemy"))
        {
            Debug.Log("Hit an enemy!");
            // Could damage the enemy here

            // Get a component from the collided object
            Health enemyHealth = collision.gameObject.GetComponent<Health>();
            if (enemyHealth != null)
            {
                enemyHealth.TakeDamage(damageOnImpact);
            }
        }

        // Get collision information
        Vector3 collisionPoint = collision.contacts[0].point;
        Vector3 collisionNormal = collision.contacts[0].normal;
        Debug.Log("Collision point: " + collisionPoint);
    }

    void OnCollisionStay(Collision collision)
    {
        // This object is touching another every frame
        // Could be used for sliding friction effects
    }

    void OnCollisionExit(Collision collision)
    {
        Debug.Log("Stopped colliding with: " + collision.gameObject.name);
    }
}

// Example Health component
public class Health : MonoBehaviour
{
    public int maxHealth = 100;
    private int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        Debug.Log("Health: " + currentHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log(gameObject.name + " died!");
        Destroy(gameObject);
    }
}
```

### Guided Practice

1. Create a Cube and a Sphere in your scene
2. Add a Rigidbody to the Cube and Sphere
3. Add Box and Sphere colliders respectively
4. Create a script that prints "Collision!" when they touch
5. Attach the script to one of the objects
6. Press Play and drop the Cube onto the Sphere
7. Watch the Console for collision messages
8. Experiment: What happens if you remove the Rigidbody from one object?

### Practice Problems

**Problem 1 — Beginner:** Add a Box Collider to a Cube and a Plane. Create a simple collision detection script that prints "Collision!" when they touch.

**Problem 2 — Intermediate:** Create a damage system where colliding with a hazard tagged object reduces player health by 10.

**Problem 3 — Challenge:** Create a collision system that detects different object types (Enemy, Coin, Wall) and responds differently to each (damage, score, bounce).

<details>
<summary>Hints</summary>

**Hint 1:** Both objects need colliders. At least one needs a Rigidbody for OnCollisionEnter() to trigger.

**Hint 2:** Use `collision.gameObject.CompareTag()` to check what you hit. Create tags in the Inspector.

**Hint 3:** You can access collision information like the contact point and normal from the Collision parameter.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void OnCollisionEnter(Collision collision)
{
    Debug.Log("Collision!");
}
```
Attach this to the Cube. The Cube needs a Rigidbody; the Plane needs a Box Collider.

**Answer 2:**
```csharp
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.CompareTag("Hazard"))
    {
        health -= 10;
    }
}
```

**Answer 3:** Use multiple collision callbacks with tag checks to differentiate behavior.

</details>
