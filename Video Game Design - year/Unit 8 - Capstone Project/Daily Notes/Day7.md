# Day 7: Sprint 1 — Health System & Game Manager

**Session Goal:** Implement a health system, a GameManager singleton, and a death condition.

---

## Today's Focus

A game needs stakes. Today you add a health system so the player can take damage and die (or lose / fail a level). A GameManager singleton will be the hub for score, health, and scene transitions.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up check-in.

**Minutes 5-45:** Build the GameManager and health system.

**Minutes 45-55:** Make sure taking damage AND dying both work. Save and back up.

---

## Technical Tips

```csharp
// GameManager singleton — central hub for your game state
using UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;
    public int health = 3;

    void Awake()
    {
        if (instance == null) { instance = this; DontDestroyOnLoad(gameObject); }
        else Destroy(gameObject);
    }

    public void AddScore(int amount)
    {
        score += amount;
        UIManager.instance.UpdateScore(score);
    }

    public void TakeDamage(int amount)
    {
        health -= amount;
        UIManager.instance.UpdateHealth(health);
        if (health <= 0) GameOver();
    }

    public void GameOver()
    {
        SceneManager.LoadScene("GameOver");
    }
}

// Player takes damage on enemy contact
void OnCollisionEnter2D(Collision2D col)
{
    if (col.gameObject.CompareTag("Enemy"))
        GameManager.instance.TakeDamage(1);
}
```

---

## Reflection / Exit Ticket

1. Does your player have a health value that decreases on damage? Y / N
2. Does the game transition to a game-over state when health reaches 0? Y / N

---

## Progress Checklist

- [ ] GameManager singleton created
- [ ] Player takes damage from enemy/hazard contact
- [ ] Health reaches 0 → game over scene or respawn
- [ ] Score increments when collecting or defeating enemies
- [ ] Scene saved and backed up
