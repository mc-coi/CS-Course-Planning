# Day 19: Sprint 3 — Final Polish & Bug Hunt

**Session Goal:** Polish every corner of the game and systematically squash bugs.

---

## Today's Focus

"Polish" is the difference between a school project and something you'd show at a game fair. Today you play your game like a stranger would — looking for anything that feels rough, broken, or confusing — and you fix it.

---

## Work Session Agenda

**Minutes 0-5:** Create a bug list (paper or digital doc). Every bug gets written down.

**Minutes 5-30:** Fix the most noticeable bugs first (crashes > visual glitches > balancing).

**Minutes 30-45:** Polish pass: consistent art style, no placeholder text, balanced audio.

**Minutes 45-55:** Save, build (Ctrl+B), confirm the build runs.

---

## Polish Checklist

```
VISUAL POLISH:
[ ] All text uses correct font and size (no default white Arial on black)
[ ] No "New Game Object" or placeholder names visible in game
[ ] Consistent art style (all sprites same resolution/style)
[ ] Background fills the screen at 16:9
[ ] UI elements properly anchored (don't float off-screen)

AUDIO POLISH:
[ ] No jarring audio transitions
[ ] Music volume is appropriate (not overpowering SFX)
[ ] No missing audio warnings in console

GAMEPLAY POLISH:
[ ] Player can complete the game without getting irreversibly stuck
[ ] No infinite score exploits or easy cheese
[ ] Camera never shows outside the level (add Camera Confiner if needed)
[ ] Death respawn works correctly every time

TECHNICAL POLISH:
[ ] No errors in Console during normal play
[ ] Frame rate is stable (no major drops)
```

---

## Technical Tips

```csharp
// Camera confiner (keeps camera inside level bounds)
// 1. Add Cinemachine → CinemachineConfiner2D to your Virtual Camera
// 2. Create an empty GameObject with a Polygon Collider 2D outlining your level
// 3. Assign it to the Confiner component's "Bounding Shape 2D"

// Object pooling for performance (spawning many bullets/particles)
// Instead of Instantiate/Destroy, deactivate and reactivate from a pool
// Helps prevent frame rate drops in endless runner or shooter games
```

---

## Reflection / Exit Ticket

1. How many bugs did you fix today?
2. What is the most important remaining issue?

---

## Progress Checklist

- [ ] Bug list created with priorities
- [ ] Critical bugs (crashes, soft-locks) fixed
- [ ] Visual and audio polish applied
- [ ] Game runs smoothly without console errors
- [ ] Scene saved and backed up
