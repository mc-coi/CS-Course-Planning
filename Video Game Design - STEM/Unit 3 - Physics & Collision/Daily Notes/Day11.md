# Day 11: Triggers & Object Management

**Learning Target:** Use trigger colliders to detect area-based events and manage object lifecycles.

### Key Concepts

- **Trigger Collider:** A collider that doesn't physically collide; instead, it detects when objects enter/exit it
- **Is Trigger:** A checkbox on colliders that makes them triggers instead of solid colliders
- **OnTriggerEnter():** Called when an object enters a trigger
- **OnTriggerStay():** Called every frame while inside a trigger
- **OnTriggerExit():** Called when an object leaves a trigger
- **Rigidbody Requirement:** At least one object must have a Rigidbody for trigger detection
- **SetActive():** Enables or disables a GameObject and its components
- **GameObject.Find():** Finds an object by name (slow; use sparingly)
- **Instantiate():** Creates a copy of a GameObject at runtime
- **Destroy():** Removes a GameObject from the scene

### Content

Triggers are useful for area-based events: entering a door, collecting an item, entering a hazard zone, etc.

**Setting Up Triggers:**
1. Add a collider to a GameObject
2. Check the "Is Trigger" checkbox
3. Add a Rigidbody to the same object (set it to Kinematic if you don't want it affected by gravity)
4. In a script, implement OnTriggerEnter() to detect when something enters

**Key Difference from Collision:**
- **Collision:** OnCollisionEnter requires both objects to have Rigidbodies. Physical collision happens.
- **Trigger:** OnTriggerEnter works if at least one has a Rigidbody. No physical collision.

**SetActive() for Object Management:**
```csharp
gameObject.SetActive(false);  // Disable and hide
gameObject.SetActive(true);   // Enable and show
```

### Code Examples

```csharp
using UnityEngine;

public class TriggerDetector : MonoBehaviour
{
    public int coinValue = 10;
    public ParticleSystem collectEffect;
    private int coinsCollected = 0;

    void Start()
    {
        gameObject.tag = "Collectible";
    }

    // Called when an object enters this trigger
    void OnTriggerEnter(Collider other)
    {
        Debug.Log("Something entered the trigger: " + other.name);

        // Check if it's the player
        if (other.CompareTag("Player"))
        {
            CollectCoin(other.gameObject);
        }
    }

    void OnTriggerStay(Collider other)
    {
        // Could apply effects while inside (e.g., slow player down)
    }

    void OnTriggerExit(Collider other)
    {
        Debug.Log("Something left the trigger: " + other.name);
    }

    void CollectCoin(GameObject collector)
    {
        Debug.Log("Coin collected!");
        coinsCollected++;

        // Play particle effect at coin position
        if (collectEffect != null)
        {
            Instantiate(collectEffect, transform.position, Quaternion.identity);
        }

        // Add score to player (if they have a score component)
        ScoreManager scoreManager = collector.GetComponent<ScoreManager>();
        if (scoreManager != null)
        {
            scoreManager.AddScore(coinValue);
        }

        // Disable or destroy the coin
        gameObject.SetActive(false);  // Just disable it
        // Or: Destroy(gameObject);  // Completely remove it
    }
}

// Simple score manager for the player
public class ScoreManager : MonoBehaviour
{
    private int score = 0;

    public void AddScore(int points)
    {
        score += points;
        Debug.Log("Score: " + score);
    }

    public int GetScore()
    {
        return score;
    }
}
```

### Guided Practice

1. Create a Cube and a Sphere in your scene
2. On the Cube, add a Box Collider and check "Is Trigger"
3. Add a Rigidbody to the Cube (set to Kinematic)
4. On the Sphere, add a Rigidbody
5. Create a script with OnTriggerEnter() that prints a message
6. Press Play and move the Sphere through the Cube
7. Observe the messages in the Console
8. Try using SetActive(false) to disable the trigger after it's touched

### Practice Problems

**Problem 1 — Beginner:** Create a trigger zone that prints "Entered!" when the player walks through it.

**Problem 2 — Intermediate:** Create a coin collectible that disappears when the player touches it and adds 10 points to a score.

**Problem 3 — Challenge:** Create a damage zone that damages the player while they're inside it, and heals them when they leave.

<details>
<summary>Hints</summary>

**Hint 1:** Make sure the collider has "Is Trigger" checked. Also, at least one object must have a Rigidbody.

**Hint 2:** Use SetActive(false) to disable objects instead of destroying them for better performance (object pooling).

**Hint 3:** You can track when an object enters and exits with separate variables to manage state.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void OnTriggerEnter(Collider other)
{
    Debug.Log("Entered!");
}
```
Attach to a trigger collider. When any object with a Rigidbody enters, "Entered!" prints to the Console.

**Answer 2:**
```csharp
void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Player"))
    {
        ScoreManager scoreManager = other.GetComponent<ScoreManager>();
        if (scoreManager != null)
        {
            scoreManager.AddScore(10);
        }
        Destroy(gameObject);
    }
}
```

**Answer 3:** Use OnTriggerStay() to apply damage while inside, and OnTriggerExit() to heal. Track the duration with a coroutine.

</details>
