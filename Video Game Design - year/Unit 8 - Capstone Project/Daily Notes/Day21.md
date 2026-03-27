# Day 21: Final Playtesting & Bug Fixing

**Session Goal:** Final round of playtesting — fix the last bugs before the build.

---

## Today's Focus

One more focused playtesting session before you export. Play the game yourself for 20 minutes straight as if you've never seen it. Then let ONE other person play it and watch silently.

---

## Work Session Agenda

**Minutes 0-20:** YOU play your game from title screen to win or game over. No stopping to fix — just write a list.

**Minutes 20-35:** Fix the top 3 items from your list.

**Minutes 35-50:** One partner plays while you observe silently. Note anything they do that surprises you.

**Minutes 50-55:** Save everything, commit any final changes.

---

## Final Bug-Fix Priority Guide

```
PRIORITY 1 — FIX NOW (game-breaking):
- Crashes or freezes
- Cannot complete the game (soft lock)
- Score doesn't count or health doesn't work

PRIORITY 2 — FIX IF TIME ALLOWS (annoying but not breaking):
- Player can walk through walls
- Enemy spawns inside player
- Audio clip plays at wrong moment

PRIORITY 3 — DOCUMENT AND MOVE ON (cosmetic/minor):
- Minor visual z-fighting
- Slightly unbalanced difficulty in level 3
- UI text clips slightly on very small screens
(Add these to your known bugs list instead of fixing)
```

---

## Technical Tips

```csharp
// Last-minute common crash fixes:

// Null Reference Exception when finding player:
// Always check before using FindGameObjectWithTag:
GameObject playerObj = GameObject.FindGameObjectWithTag("Player");
if (playerObj != null)
    player = playerObj.transform;

// OnDestroy cleanup (stop coroutines when object is destroyed):
void OnDestroy()
{
    StopAllCoroutines();
}

// Make sure all AudioClips are assigned in Inspector before build!
```

---

## Reflection / Exit Ticket

1. Is your game completable from start to finish without crashing? Y / N
2. If N — what is the one blocker you must fix before presenting?

---

## Progress Checklist

- [ ] Played own game for 20 minutes start to finish
- [ ] Top 3 bugs fixed
- [ ] Watched one other person play — noted their reactions
- [ ] Known bugs list updated
- [ ] All scenes saved, project backed up
