# Day 13: Sprint 2 Check-In — Peer Playtesting

**Session Goal:** Playtest a classmate's game and receive structured feedback on your own.

---

## Today's Focus

Peer playtesting is one of the most valuable things game developers do. Someone who has never played your game will find problems you're completely blind to — because you've been looking at it for days. Watch without helping. Let them struggle. Take notes.

---

## Work Session Agenda

**Minutes 0-5:** Pair up with someone who is NOT your closest friend (different perspective helps).

**Minutes 5-25:** Partner plays YOUR game for 10 minutes while you silently observe and take notes. Do NOT help them. Do NOT explain the controls.

**Minutes 25-45:** Switch. You play THEIR game silently.

**Minutes 45-55:** Exchange written feedback forms. Read together. Discuss.

---

## Playtesting Observation Sheet

```
PLAYTESTING NOTES (fill out while watching)
Game you're observing: ___________________

CONFUSION: Where did the player get stuck or confused?
(Write down the moment, not just "they were confused")
1.
2.
3.

FRUSTRATION: What made the player visibly frustrated?
1.
2.

DELIGHT: What made the player smile, laugh, or react positively?
1.
2.

BUGS: List every visual bug, crash, or unexpected behavior you saw:
1.
2.
3.

WRITTEN FEEDBACK (give to developer):
"The most important thing to fix before the final is ___."
"One thing that already feels great: ___."
"A small polish suggestion: ___."
```

---

## Technical Tips

```csharp
// Common Sprint 2 bugs to fix this week:

// Bug: Score persists between scene loads (GameManager DontDestroyOnLoad resets needed)
void OnEnable()
{
    // Reset score when new game starts
    score = 0;
    health = maxHealth;
}

// Bug: Player can jump infinitely (ground check not working)
// Fix: Use a layer-based raycast or OverlapCircle for ground detection
private bool IsGrounded()
{
    return Physics2D.OverlapCircle(groundCheck.position, 0.2f, groundLayer);
}
```

---

## Reflection / Exit Ticket

1. What was the most surprising thing you observed during playtesting?
2. What is the ONE thing you will fix/improve first based on today's feedback?

---

## Progress Checklist

- [ ] Playtested a classmate's game for 10+ minutes
- [ ] Filled out observation sheet and feedback form
- [ ] Received and read your feedback forms
- [ ] Sprint 2 remaining task list updated based on feedback
- [ ] Scene saved and backed up
