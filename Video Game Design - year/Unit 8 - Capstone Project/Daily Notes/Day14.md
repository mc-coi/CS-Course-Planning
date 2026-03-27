# Day 14: Sprint 2 — Implementing Feedback & Level Design

**Session Goal:** Act on playtesting feedback and build/refine your level design.

---

## Today's Focus

Take the top 3 items from yesterday's feedback and fix or implement them today. Then focus on level design — making your existing content feel intentional: clear starting area, escalating challenge, satisfying goal.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up: "From feedback, I'm fixing ___."

**Minutes 5-30:** Address top feedback items.

**Minutes 30-45:** Level design work — refine level 1, or block out level 2.

**Minutes 45-55:** Playtest your changes. Save and back up.

---

## Technical Tips

```csharp
// Level design principles in Unity:
// 1. Safe start: Player starts in a safe area with no immediate threats
// 2. Teach with geometry: Low platform teaches jumping before gaps appear
// 3. Visual language: Red objects = dangerous. Bright objects = collectible.
// 4. Checkpoint system: Save player position so death isn't punishing

public class Checkpoint : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            // Store spawn position for respawning
            PlayerController.instance.spawnPoint = transform.position;
            GetComponent<SpriteRenderer>().color = Color.green; // visual feedback
        }
    }
}
```

---

## Reflection / Exit Ticket

1. What feedback item had the biggest positive impact when fixed?
2. Is level 1 completable by someone who has never played your game?

---

## Progress Checklist

- [ ] Top 3 feedback items addressed
- [ ] Level 1 completable from start to finish
- [ ] Level difficulty feels appropriately gradual
- [ ] Scene saved and backed up
