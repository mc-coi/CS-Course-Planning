# Day 7: OnTriggerEnter & OnTriggerExit

**Learning Target:** I can use trigger zones to detect when objects enter/exit areas without physical collision.

---

## Key Concepts

**Trigger zone** — A collider with isTrigger = true. Objects pass through instead of bouncing off.

**OnTriggerEnter(Collider collider)** — Fires when an object enters the trigger zone.

**OnTriggerExit(Collider collider)** — Fires when an object leaves the trigger zone.

**OnTriggerStay(Collider collider)** — Fires every frame while in the zone.

**Key difference from collision:**
- No bouncing or physical response
- No Collision object—just a Collider reference
- One object MUST have a Rigidbody (non-kinematic)

**Requirements:**
1. The trigger must have a Collider with isTrigger = true
2. The other object must have a Collider and at least one object needs a Rigidbody
3. Physics layer settings must allow the interaction

**Real-world examples:**
- **Mario:** Coins are trigger zones that disappear when Mario touches them
- **Portal 2:** Portal surfaces are triggers that detect when objects enter
- **Cuphead:** Damage zones are triggers that reduce health
- **Zelda:** Chests are triggers that open when you stand in range

---

## Code Example

```csharp
using UnityEngine;

public class TriggerZone : MonoBehaviour
{
    // Called when something enters the trigger
    private void OnTriggerEnter(Collider other)
    {
        Debug.Log(other.gameObject.name + " entered trigger");

        if (other.CompareTag("Player"))
        {
            Debug.Log("Player entered!");
        }

        if (other.CompareTag("Coin"))
        {
            // Destroy coin and add score
            Destroy(other.gameObject);
            Debug.Log("Coin collected!");
        }
    }

    // Called when something exits the trigger
    private void OnTriggerExit(Collider other)
    {
        Debug.Log(other.gameObject.name + " left trigger");
    }

    // Called every frame while in trigger
    private void OnTriggerStay(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            // Continuous effect (heal, damage, buff)
            // Debug.Log("Player is in zone");
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a trigger zone:** Cube at Y=1 (so player walks through it)
2. **Add BoxCollider:** Inspector → Add Component → Physics → Box Collider
3. **Enable isTrigger:** Inspector → Box Collider → Check "Is Trigger"
4. **Remove Rigidbody** from the trigger (or keep it and set Body Type to Static)
5. **Create Player (Capsule)** with Rigidbody (not kinematic)
6. **Tag Player:** Select → Inspector → Tag dropdown → "Player"
7. **Attach TriggerZone script to trigger**
8. **Press Play:** Walk player through trigger and watch console

---

## Guided Practice

1. Create a trigger zone (invisible cube, isTrigger = true)
2. Create a player (capsule with Rigidbody)
3. Write script that prints "Entered" on OnTriggerEnter, "Exited" on OnTriggerExit
4. Walk player through multiple times
5. Scale the trigger zone larger—easier to hit

---

## Practice Problems

**Beginner:** Create a pickup coin. When player touches it, print "Coin!" and destroy the coin.

**Intermediate:** Build a "healing zone." When player is inside (OnTriggerStay), slowly restore health. Print remaining health.

**Challenge:** Create a "checkpoint" trigger. When player enters, save their position. If they fall off the map, teleport them back to the last checkpoint.

<details><summary>💡 Hints</summary>
- Triggers don't require Rigidbody to have gravity—set Body Type to Static to save performance
- Use `other.bounds.center` to find center of the object in the trigger
- Triggers pass through objects but still detect them—perfect for pickups
- OnTriggerStay fires every FixedUpdate, so use cooldowns to prevent spam
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Checkpoint system
public class Checkpoint : MonoBehaviour
{
    public static Vector3 lastCheckpoint = new Vector3(0, 1, 0);

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            lastCheckpoint = other.transform.position;
            Debug.Log("Checkpoint saved at: " + lastCheckpoint);
        }
    }
}

public class PlayerRespawn : MonoBehaviour
{
    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        // Fall off map
        if (transform.position.y < -5)
        {
            transform.position = Checkpoint.lastCheckpoint;
            rb.velocity = Vector3.zero;
        }
    }
}
```

</details>
