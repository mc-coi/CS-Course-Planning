# Day 6: Sprint 1 — Core Mechanics (Work Day 2)

**Session Goal:** Build enemy behavior and collectibles / core interaction.

---

## Today's Focus

Yesterday the player moved. Today the world responds. Add at least one enemy or obstacle, and one form of player interaction (collecting, destroying, avoiding). Keep it simple — a cube that moves back and forth is a valid enemy placeholder.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up: "Yesterday I finished ___. Today I'm building ___."

**Minutes 5-45:** Build from your Sprint 1 checklist — focus on enemies and core interaction.

**Minutes 45-55:** Test it. Break it. Fix it. Save everything.

---

## Today's Build Focus Areas

**For 2D Platformers:**
- Enemy patrol behavior (back and forth between two points)
- Collectibles (coins) that disappear on trigger and add to score

**For Top-Down Shooters:**
- Bullet prefab: spawns at player position, moves in aim direction
- Enemy that chases the player

**For Puzzle Games:**
- Core mechanic fully playable (even if ugly)
- Feedback when puzzle is solved (particle, sound, or color change)

**For Endless Runner:**
- Obstacle spawner (create obstacle prefab, spawn off-screen, move left, destroy)
- Collision with obstacle ends the run

---

## Technical Tips

```csharp
// Enemy patrol between two points
public class EnemyPatrol : MonoBehaviour
{
    public Transform pointA;
    public Transform pointB;
    public float speed = 3f;
    private Transform target;

    void Start() { target = pointB; }

    void Update()
    {
        transform.position = Vector2.MoveTowards(
            transform.position, target.position, speed * Time.deltaTime);

        if (Vector2.Distance(transform.position, target.position) < 0.1f)
            target = (target == pointA) ? pointB : pointA;
    }
}

// Collectible pickup
public class Collectible : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            GameManager.instance.AddScore(10);
            Destroy(gameObject);
        }
    }
}
```

---

## Reflection / Exit Ticket

1. Does your game have at least one enemy or obstacle? Y / N
2. Is there something to DO besides moving? Y / N

---

## Progress Checklist

- [ ] Enemy or obstacle exists in scene
- [ ] Player can interact with something (collect, avoid, destroy)
- [ ] No console errors when pressing Play
- [ ] Scene saved and backed up
