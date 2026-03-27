# Day 2: Concept Selection & GDD Draft

**Session Goal:** Choose your final project concept and begin drafting your Game Design Document.

---

## Today's Focus

Today you commit to your game idea and start the Game Design Document (GDD) — the blueprint for your entire project. A GDD isn't just busywork: it forces you to think through problems before you hit them in Unity, saving hours of confusion later.

---

## Work Session Agenda

**Minutes 0-5:** Quick stand-up: share your chosen concept in one sentence. Teacher notes any scope concerns.

**Minutes 5-45:** Start filling out the GDD template below. Aim to complete Sections 1–4 today.

**Minutes 45-55:** Save your GDD. Read what you have out loud — does it make sense? What's still unclear?

---

## Game Design Document Template (Draft)

```
GAME DESIGN DOCUMENT — DRAFT
Student Name: ___________________
Project Option: _________________
Date Started: ___________________

SECTION 1: CONCEPT
Game Title: 
One-line pitch (like a movie tagline):
Genre: 
Tone/Aesthetic (dark, cute, retro, sci-fi, etc.):
Inspiration games:

SECTION 2: CORE MECHANIC
What is the ONE core action the player does most? (jump, shoot, slide, rotate):
How does that mechanic create challenge?
What makes YOUR version unique or interesting?

SECTION 3: PLAYER EXPERIENCE
What should the player FEEL while playing? (tense, curious, powerful, clever):
What's the core gameplay loop? (e.g., "Move → Collect coins → Avoid enemies → Reach exit"):
How does the game get harder over time?

SECTION 4: SCOPE (rough estimate)
How many levels/scenes? 
How many enemy types?
How many UI screens (main menu, pause, game over, etc.)?
Estimated complexity (simple / medium / ambitious):

SECTION 5: CONTROLS (fill in Day 3)
SECTION 6: TECHNICAL PLAN (fill in Day 3)
```

---

## Technical Tips

```csharp
// Thinking about your project type? Quick scope checkers:

// 2D Platformer core — how complex is your player controller?
// Simple: left/right + jump (2 scripts)
// Medium: + coyote time, wall jump, double jump (1 bigger script)
// Hard: + dash, slide, animations (multiple scripts + Animator)

// Top-down — how will enemies find the player?
// Simple: move toward player.transform.position each frame
// Medium: NavMesh pathfinding (requires NavMesh baking)

// Always choose SIMPLE for your first pass — you can add later.
```

---

## Reflection / Exit Ticket

1. What is your game's core mechanic in one sentence?
2. Is your current scope for the time available? Circle: Too small / Just right / Too big

---

## Progress Checklist

- [ ] Final concept chosen (no going back after today!)
- [ ] GDD Sections 1–4 drafted
- [ ] Identified at least one "risky" feature (something you're not sure how to build)
- [ ] GDD saved (Google Doc, OneDrive, or paper)
