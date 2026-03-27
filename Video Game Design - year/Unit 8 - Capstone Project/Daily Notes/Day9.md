# Day 9: Sprint 1 Check-In — Prototype Demo

**Session Goal:** Demo your playable prototype to the class and receive structured feedback.

---

## Today's Focus

Today every student presents their Sprint 1 prototype. The game doesn't need to be pretty. It needs to be PLAYABLE — someone else can sit down and understand what the game is trying to be. You'll also give feedback to classmates using the form below.

---

## Work Session Agenda

**Minutes 0-5:** Set up your game for demo. Make sure it runs without crashing.

**Minutes 5-40:** Rotating demos — each student/group has ~3 minutes. Classmates observe and fill out feedback forms.

**Minutes 40-55:** Read your feedback forms. Write Sprint 2 plan using feedback + teacher notes.

---

## Demo Presentation Guide

When it's your turn, tell the class:
1. **Game title and type:** "I'm building a 2D platformer called ___."
2. **What works:** "The player can move, jump, and collect coins."
3. **Core loop:** Show someone playing start to finish (or die trying).
4. **One challenge:** "I'm stuck on ___."

You are NOT graded on how polished it looks today. You ARE expected to have a playable game loop.

---

## Peer Feedback Form

```
SPRINT 1 FEEDBACK FORM
Your name: ___________________
Game you're reviewing: ___________________
Developer: ___________________

1. What's working well? (Be specific)

2. What was confusing or unclear as a player?

3. One feature suggestion that fits their current scope:

4. Rating — how fun is the core mechanic right now?
   [ ] Not yet there  [ ] Getting there  [ ] Pretty fun  [ ] Really fun!

5. One encouragement for the developer:
```

---

## Technical Tips

```csharp
// Common Sprint 1 bugs to fix before Sprint 2:

// Bug: Player falls through floor
// Fix: Make sure floor has a Collider2D (not just a Renderer)

// Bug: Enemy kills player instantly (too many triggers per frame)
// Fix: Add a damage cooldown using a float timer:
private float damageCooldown = 0f;
void Update()
{
    if (damageCooldown > 0) damageCooldown -= Time.deltaTime;
}
void OnCollisionEnter2D(Collision2D col)
{
    if (col.CompareTag("Enemy") && damageCooldown <= 0)
    {
        GameManager.instance.TakeDamage(1);
        damageCooldown = 1.5f; // 1.5 second invincibility
    }
}
```

---

## Reflection / Exit Ticket

1. What was the most useful piece of feedback you received today?
2. What are your top 3 Sprint 2 goals?

---

## Progress Checklist

- [ ] Demo completed — game ran in front of class
- [ ] Feedback forms collected (keep them!)
- [ ] Sprint 2 task list drafted based on feedback
- [ ] Sprint 2 "definition of done" written
