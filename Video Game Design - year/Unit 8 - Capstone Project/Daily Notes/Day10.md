# Day 10: Sprint 2 — Adding Enemies & AI

**Session Goal:** Add a second enemy type or improve existing enemy AI with new behaviors.

---

## Today's Focus

Sprint 2 is about layering. Your prototype works — now make it interesting. Today: enemies get smarter and more varied. Players should feel a real challenge emerging.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up: Sprint 2 goal, first task today.

**Minutes 5-45:** Implement one new or upgraded enemy behavior.

**Minutes 45-55:** Playtest with your new enemy. Is it fair? Is it interesting? Adjust values.

---

## Technical Tips

```csharp
// Enemy that chases the player
using UnityEngine;

public class EnemyChase : MonoBehaviour
{
    public float speed = 4f;
    public float detectionRange = 8f;
    private Transform player;

    void Start()
    {
        player = GameObject.FindGameObjectWithTag("Player").transform;
    }

    void Update()
    {
        float dist = Vector2.Distance(transform.position, player.position);
        if (dist < detectionRange)
        {
            transform.position = Vector2.MoveTowards(
                transform.position, player.position, speed * Time.deltaTime);
        }
    }
}

// Enemy that shoots projectiles at the player
public class ShootingEnemy : MonoBehaviour
{
    public GameObject bulletPrefab;
    public float fireRate = 2f;
    private float fireTimer;
    private Transform player;

    void Start() { player = GameObject.FindGameObjectWithTag("Player").transform; }

    void Update()
    {
        fireTimer -= Time.deltaTime;
        if (fireTimer <= 0f)
        {
            fireTimer = fireRate;
            Shoot();
        }
    }

    void Shoot()
    {
        GameObject b = Instantiate(bulletPrefab, transform.position, Quaternion.identity);
        Vector2 dir = (player.position - transform.position).normalized;
        b.GetComponent<Rigidbody2D>().velocity = dir * 6f;
        Destroy(b, 3f);
    }
}
```

---

## Reflection / Exit Ticket

1. Does your game now have two meaningfully different challenges/enemies? Y / N
2. What's the balance feel like — too easy, too hard, or about right?

---

## Progress Checklist

- [ ] At least two different enemy behaviors in the game
- [ ] Enemies are fair — player has time to react
- [ ] No new console errors
- [ ] Scene saved and backed up
