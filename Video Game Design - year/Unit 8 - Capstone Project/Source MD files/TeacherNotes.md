# Unit 8 - Capstone Project: Teacher Misconception & Callout Guide

## Overview

The capstone is where students synthesize everything—C#, physics, design, UI, 2D, systems, and polish. This is less about teaching new concepts and more about **mentoring** the game-making process. The biggest challenges are **scope creep** (students bite off more than they can finish), **decision fatigue** (too many design choices paralyze them), and **losing sight of fun** (they polish a broken core mechanic instead of fixing the mechanic). Unlike earlier units, there are no single "misconceptions" here—instead, there are recurring patterns: students who don't playtest, students who over-engineer, students who blame tools instead of iterating, and students who finish something technically impressive but not fun.

---

## Misconceptions by Topic

### Scope & Planning (Days 1–3)

**⚠️ Misconception:** "I'll make a big game with lots of features. Polish comes later. I have 3 weeks."

**What it looks like:** A student designs a game with 10 levels, 5 enemy types, 3 weapon types, bosses, and a narrative. Three weeks later, they have 1 half-finished level and no time to polish.

**Why students think this:** Games look like they have lots of features. Students don't realize how much time each feature takes.

**How to address it:** Enforce a scope document. "Write down exactly what the game will be. Be specific: 'one level, one enemy type, one weapon, one mechanic.' Ask: can this be done in 2 weeks of part-time work? If no, cut features. Always build a 'minimum playable game' first, then add if you have time. Better to ship a polished small game than an unfinished big game."

---

**⚠️ Misconception:** "I have a great idea, but I'm not sure if it's fun. Let me design it fully before building it."**

**What it looks like:** A student spends a week designing a game on paper, then builds it for a week, only to discover the core mechanic isn't fun.

**Why students think this:** They don't understand the power of rapid prototyping.

**How to address it:** Prototype early. "Build a playable version of the core mechanic in 2-3 days. Don't worry about art, sound, or levels. Just the mechanic. Play it. Is it fun? If no, redesign quickly. If yes, then add art and levels. A fast, ugly prototype teaches more than a detailed design document."

---

### Design Iteration & Playtesting (Throughout)

**⚠️ Misconception:** "I finished my game. It's done. I'm happy with it."**

**What it looks like:** A student finishes a prototype but doesn't playtest or iterate.

**Why students think this:** They don't realize how obvious bugs and unfun mechanics are to outside players. The designer is blind to their own game.

**How to address it:** Mandate playtesting. "Before you call it done, let someone else play it. Watch them silently. What do they struggle with? Where do they get stuck? What do they say is unfun? Fix those things. Iterate at least once based on feedback. The best games aren't designed in isolation—they're refined through playtesting."

---

**⚠️ Misconception:** "I playtested my game, and everyone said it was too hard. So I made it easier. Now it's too easy and boring."**

**What it looks like:** A student overreacts to feedback, swinging the difficulty wildly.

**Why students think this:** They take all feedback as equally important.

**How to address it:** Evaluate feedback critically. "Not all feedback is actionable. If one person says it's too hard but five say it's just right, trust the majority. If everyone struggles at level 3 but sails through level 2, the jump is too steep. Make small adjustments (5-10%) and test again. Tuning is iterative."

---

### Core Mechanic vs. Polish (Throughout)

**⚠️ Misconception:** "My game feels flat. I'll add cool visual effects and music to make it better."**

**What it looks like:** A student adds screen shake, particles, and a soundtrack to a game with a broken core mechanic. It looks good but doesn't feel fun.

**Why students think this:** They see polish as visual. They don't realize polish comes from a solid mechanic.

**How to address it:** Prioritize mechanics. "Polish (audio, effects, graphics) enhances a good game. But if the core mechanic isn't fun, polish can't save it. First, make sure jumping feels good, shooting feels responsive, enemies are fair. Then add effects. A polished game with a bad mechanic is still bad. An unpolished game with a great mechanic is fun."

---

### Time Management & Scope Cuts (Throughout)

**⚠️ Misconception:** "I'm halfway through and behind schedule. I'll just skip playtesting and skip polish to save time."**

**What it looks like:** A student sees they're running out of time and cuts playtesting and feedback.

**Why students think this:** They think polish is optional.

**How to address it:** Finish strong. "If you're behind, cut features, not playtesting or polish. Remove a level, reduce enemy types, simplify graphics—but make what remains polished and fun. A small, solid game is better than a large, broken game. Use the last few days for bug fixes and feedback iteration."

---

## Whole-Class Warning Signs

- **Multiple students are stuck redesigning their idea because the first version wasn't fun.** This is normal! Validate: "Many games go through 2-3 redesigns. Iteration is not failure." Help them scope a prototype and rebuild quickly.

- **Everyone's behind schedule and panicking.** Some students over-scoped, others spent too long on art. Remind them that playtesting and bugs always take longer than expected. Help them cut scope before the deadline.

- **A few students are over-engineering (e.g., a complex save system for a 5-minute game).** Gently redirect: "That's cool, but will it make the game more fun?" Many students don't distinguish between "nice to have" and "essential."

- **No one's game feels fun yet, and they're worried.** This is week 1-2; it's normal. Unfinished games feel flat. Reassure them and focus on playtesting feedback.

- **Some students have brilliant ideas but poor execution (bugs, unclear rules, broken controls).** Help them debug and test. Ideas are cheap; execution is hard.

---

## Questions That Reveal Understanding

1. **"What's the smallest version of your game that you can build in one week?"**
   - Good answer: "One level, one enemy type, one weapon, one mechanic. All playable and fun."
   - Red flag: "I have to include all the features I planned" (they don't understand MVP).

2. **"You playtested your game and people said jumping feels floaty. How do you fix it?"**
   - Good answer: "Test different jump heights, gravity values, and coyote time. Watch playtesters and see when they're frustrated. Tweak until it feels good."
   - Red flag: "I'll add a particle effect to make jumping look better" (they're conflating mechanic with visual polish).

3. **"You're two weeks in and behind schedule. What's your next move?"**
   - Good answer: "Cut scope. Remove levels, features, or enemy types. Keep the core mechanic solid and polish it. Finish on time with something playable."
   - Red flag: "I'll stay up late to catch up" or "I'll skip playtesting to save time" (unsustainable).

---

## Common Student Questions & How to Answer Them

**Q1: "My game is done, but it doesn't feel fun. What do I do?"**

*A:* "Playtest it with someone who hasn't seen it before. Watch them play without talking. Where do they struggle? What do they complain about? That's your roadmap. Fix the top 3 issues. Playtest again. Iterate."

---

**Q2: "I have lots of ideas but I'm not sure which one to build. How do I choose?"**

*A:* "Pick the idea you're most excited about. Build a one-week prototype of the core mechanic. Is it fun? If yes, expand it. If no, try idea #2. The idea that's fun to build and fun to play is the winner."

---

**Q3: "My game is almost done but there are still bugs. Should I fix them or add more features?"**

*A:* "Fix bugs first. A polished game with fewer features beats a buggy game with more features. Players notice bugs more than missing features. Polish what you have."

---

**Q4: "How do I balance difficulty? My playtesters said it was too hard, but some said too easy."**

*A:* "If feedback is mixed, you're probably in the right ballpark. Make small adjustments. Reduce enemy health by 5%, increase player damage by 10%. Test. Repeat. Don't swing wildly. Also, consider difficulty options (easy/medium/hard)."

---

**Q5: "I want to add a save system, in-game menus, controller support, and mobile touch controls. Do I have time?"**

*A:* "Probably not, unless those are essential to the game. Build the game without them first. If you finish with time, add them as polish. Don't spend a week on a save system if your core mechanic isn't fun yet."

---

## Analogies That Work

1. **"Building a game is like cooking a meal. First, make sure the main dish (core mechanic) tastes good. Don't spend time plating and garnishing until you've fixed the recipe. Once the main is perfect, then you plate it beautifully (polish)."**
   - This prioritizes the right things.

2. **"Scope is like a project budget. You have 3 weeks (the budget). Each feature costs time. Playtesting costs time. Polish costs time. Plan carefully or you'll run out of time. Cut features if you have to, but don't skip playtesting."**
   - This makes time/scope trade-offs concrete.

3. **"Playtesting is like debugging. You wouldn't ship code without testing it. Don't ship a game without playtesting it. What's obvious to you (the designer) is often confusing to players."**
   - This validates the playtesting process.

---

## Mentoring Strategies

**Week 1-2: Prototype & Validate**
- Help students build a playable core mechanic as fast as possible.
- Playtest immediately, even if it's ugly.
- Is the core fun? If no, redesign. If yes, move to implementation.

**Week 2-3: Implement & Iterate**
- Help with specific technical issues (physics tuning, animation syncing, UI wiring).
- Keep playtesting every 2-3 days.
- Make design decisions based on feedback, not hunches.
- Watch for scope creep; push back on "nice-to-haves."

**Week 3-4: Polish & Bug Fix**
- Help with known issues.
- Playtesting for final feedback.
- Final balance tweaks.
- Audio and visual polish (if time allows).

---

## Red Flags to Watch

- **Student hasn't playtested by day 5.** They're avoiding feedback. Encourage them to show it to a friend.
- **Student is spending days on art before the mechanic works.** They're prioritizing the wrong thing. Gently redirect.
- **Student's game has 3 levels but level 1 is broken.** They're not debugging. Show them how to use Console, breakpoints, or Debug.Log().
- **Student says "The game is finished" on day 7 of a 15-day project.** They might be burned out or not testing thoroughly. Offer support.
- **Student is asking to scope up (add features) instead of down.** They don't realize they're behind. Have a frank conversation about what's realistic.

---

## Success Criteria for Capstone

A successful capstone game:
1. **Is playable start-to-finish** without game-breaking bugs.
2. **Has a clear, fun core mechanic** that's easy to understand.
3. **Is playtested and iterated** based on feedback.
4. **Has polish** (UI, audio, visual feedback) appropriate to scope.
5. **Shows mastery** of Units 1-7 (C#, physics, design, systems, etc.).
6. **Was delivered on time** with a realistic scope.

It does NOT have to:
- Be graphically beautiful (placeholder art is fine).
- Have all originally planned features.
- Be a novel idea (clones and remakes are great learning).
- Be perfectly balanced (close is good enough).

---

## Grading Considerations

**Technical (40%):**
- Code quality and organization.
- Physics and collision handling.
- UI and system design.
- Polish and bug fixes.

**Design (30%):**
- Core mechanic is clear and fun.
- Playtesting was done and incorporated.
- Scope is appropriate to time.

**Presentation (20%):**
- Game is playable and has a clear goal.
- Audio and visual feedback work.
- Controls are intuitive.

**Process (10%):**
- Student iterated based on feedback.
- Documented decisions and changes.
- Managed time effectively.

---

## Post-Capstone

After students finish, have them:
1. **Write a retrospective:** What went well? What would you do differently?
2. **Playtest someone else's game** and give constructive feedback.
3. **Extend their game** with a new feature or level (optional polish).
4. **Present to the class** in 2-3 minutes.

This closure loop helps them reflect and learn from the process.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
