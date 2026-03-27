# Day 8: Sprint 1 — Camera, Scene Polish & Prototype Wrap-Up

**Session Goal:** Polish Sprint 1 to demo-ready state: camera, basic UI, and a complete game loop.

---

## Today's Focus

Tomorrow you demo. Today you make sure the prototype tells a story: player spawns, can move, can interact, can die, and the camera follows. The art can be ugly — but the loop must be complete.

---

## Work Session Agenda

**Minutes 0-5:** Personal sprint review: check every Must-Have item. Mark what's done.

**Minutes 5-40:** Fix remaining Must-Have items. Do NOT add new features.

**Minutes 40-55:** Playtest for 10 minutes. Write down every bug you notice. Fix the top 2.

---

## Technical Tips

```csharp
// Cinemachine camera follow (simplest option):
// 1. Window → Package Manager → Cinemachine → Install
// 2. Cinemachine → Create 2D Camera
// 3. Drag Player into "Follow" field in Virtual Camera component

// Basic UI to show score and health (Unit 5 recap):
using TMPro;
using UnityEngine;

public class UIManager : MonoBehaviour
{
    public static UIManager instance;
    public TextMeshProUGUI scoreText;
    public TextMeshProUGUI healthText;

    void Awake()
    {
        if (instance == null) instance = this;
        else Destroy(gameObject);
    }

    public void UpdateScore(int score) { scoreText.text = "Score: " + score; }
    public void UpdateHealth(int hp) { healthText.text = "HP: " + hp; }
}
```

---

## Reflection / Exit Ticket

1. Write your Sprint 1 demo script in one sentence: "The player can ___, and if ___, then ___."
2. What's the first thing you'll add in Sprint 2?

---

## Progress Checklist

- [ ] Camera follows player smoothly
- [ ] Basic HUD shows score and/or health
- [ ] Full game loop: spawn → play → die → game over
- [ ] Sprint 1 Must-Have checklist 100% done (or nearly)
- [ ] Ready to demo tomorrow — notes written for what to show
- [ ] Scene saved, project backed up
