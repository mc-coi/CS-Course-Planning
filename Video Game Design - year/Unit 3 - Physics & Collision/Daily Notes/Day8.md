# Day 8: Trigger Applications — Pickups & Portals

**Learning Target:** I can build game mechanics like pickups and portals using trigger zones.

---

## Key Concepts

**Pickup system** — Trigger zones that destroy or deactivate objects when touched. Used for coins, health packs, ammo.

**Portal system** — Trigger zones that teleport objects to another location. Used for level transitions, secret rooms.

**Teleportation** — Set `transform.position` to move an object instantly.

**Inventory system** — Track collected items using lists or counters.

**Real-world examples:**
- **Mario:** Coins use triggers with Destroy() in OnTriggerEnter
- **Portal 2:** Blue/orange portals are triggers that teleport you between them
- **Zelda:** Chests are triggers that open when you stand on them
- **Minecraft:** Ender portals are triggers that teleport to the End

---

## Code Example

```csharp
using UnityEngine;

public class Pickup : MonoBehaviour
{
    public enum PickupType { Coin, HealthPack, PowerUp }
    public PickupType type = PickupType.Coin;
    public int value = 1; // Amount to add (coins, health, etc)

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            PlayerInventory inventory = other.GetComponent<PlayerInventory>();
            if (inventory != null)
            {
                inventory.Add(type, value);
            }
            Destroy(gameObject);
        }
    }
}

public class PlayerInventory : MonoBehaviour
{
    public int coins = 0;
    public int health = 100;

    public void Add(Pickup.PickupType type, int amount)
    {
        switch (type)
        {
            case Pickup.PickupType.Coin:
                coins += amount;
                Debug.Log("Coins: " + coins);
                break;
            case Pickup.PickupType.HealthPack:
                health = Mathf.Min(health + amount, 100);
                Debug.Log("Health: " + health);
                break;
            case Pickup.PickupType.PowerUp:
                Debug.Log("PowerUp collected!");
                break;
        }
    }
}

public class Portal : MonoBehaviour
{
    public Transform exitPoint;
    private float teleportCooldown = 1f;
    private float lastTeleportTime = 0f;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player") && Time.time - lastTeleportTime > teleportCooldown)
        {
            other.transform.position = exitPoint.position;
            other.transform.rotation = exitPoint.rotation;
            lastTeleportTime = Time.time;
            Debug.Log("Teleported!");
        }
    }
}
```

---

## Unity Setup Steps

**For Pickup System:**
1. Create a coin (sphere, small)
2. Add SphereCollider, enable isTrigger
3. Remove Rigidbody or disable it
4. Attach Pickup script
5. Tag it "Coin"

**For Portal System:**
1. Create two trigger zones (boxes, same size)
2. Make one blue (material), one orange
3. Create empty GameObjects for exitPoints (place where teleported object should appear)
4. Attach Portal script to entrance, set exitPoint to the other portal's exitPoint
5. Set up teleportCooldown to prevent loop teleportation

---

## Guided Practice

1. Create a level with 5 scattered coins
2. Create a player with Rigidbody and tag "Player"
3. Add PlayerInventory script to player
4. Attach Pickup script to each coin
5. Play and collect coins—watch console output
6. Add two portals and test teleportation between them

---

## Practice Problems

**Beginner:** Create 10 coins scattered in a room. When all collected, print "Level Complete!"

**Intermediate:** Build a health pickup system. Collect red crosses to restore health. Hitting enemies costs health. When health reaches 0, print "Game Over".

**Challenge:** Create a puzzle room. Three colored portals (red, blue, green) teleport to different areas. Use a key pickup system where you need to collect specific keys before doors open.

<details><summary>💡 Hints</summary>
- Use `Mathf.Min()` to cap health at maximum
- Create empty GameObjects as portal exit points
- Add cooldown to prevent infinite teleport loops
- Use `GetComponent<>()` to find other scripts on the same object
- For keys/doors, check an inventory list before allowing passage
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Key and door system
public class KeyPickup : MonoBehaviour
{
    public string keyColor = "red";

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            KeyInventory inv = other.GetComponent<KeyInventory>();
            if (inv != null)
            {
                inv.CollectKey(keyColor);
            }
            Destroy(gameObject);
        }
    }
}

public class KeyInventory : MonoBehaviour
{
    public List<string> keys = new List<string>();

    public void CollectKey(string color)
    {
        keys.Add(color);
        Debug.Log("Collected " + color + " key!");
    }

    public bool HasKey(string color)
    {
        return keys.Contains(color);
    }
}

public class Door : MonoBehaviour
{
    public string requiredKeyColor = "red";

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            KeyInventory inv = other.GetComponent<KeyInventory>();
            if (inv != null && inv.HasKey(requiredKeyColor))
            {
                Destroy(gameObject); // Door opens (destroyed)
                Debug.Log("Door opened!");
            }
        }
    }
}
```

</details>
