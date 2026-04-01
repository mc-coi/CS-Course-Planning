# Unit 8 - Capstone Project: Teacher Misconception & Callout Guide

## Overview

The capstone is where students synthesize everything—C#, physics, design, UI, 2D systems, FSMs, and polish. In a STEM semester course, the timeline is compressed: students have 2–3 weeks instead of 3–4. This makes scope management even more critical than in the year-long version. The same recurring patterns appear, but faster and harder: scope creep (they design a game that would take 3 months), decision paralysis (too many design choices), and polish before core mechanic (they add screen shake to a game where jumping is broken). The teacher's job in this unit is less about instruction and more about mentoring: redirecting, cutting scope, enforcing playtesting, and keeping students moving forward. Unlike earlier units, there's no "wrong answer" to teach—only patterns to watch for.

---

## Misconceptions by Topic

### Scope & Planning (Days 1–2)

**⚠️ Misconception:** "I have 3 weeks, so I can make a game with 3 levels, multiple enemy types, a boss, cutscenes, and a full story."

**What it looks like:** A student's scope document lists 15+ features. Three weeks later, they have one buggy level and no time for polish.

**Why students think this:** Students see finished games and don't realize how long each feature takes. Three weeks sounds like a lot.

**How to address it:** Enforce the MVP scope document. "In a STEM capstone, you have roughly 60-75 hours of class and homework time. Each feature costs more than you think. Rule: write down your absolute minimum playable game—one level, one mechanic, one enemy type. Build that first. Can you build it in ONE week? If no, cut features. Better to ship a polished small game than an unfinished ambitious one."

🚨 **STEM Priority — STOP THE CLASS:** Do a whole-class scope-cutting exercise on Day 1. Take a student's ambitious idea and publicly scope it down to what's achievable. This sets expectations for everyone.

**Scope Document Template (fill out Day 1):**
- Core mechanic (one sentence): ___
- Genre: ___
- Number of levels: ___ (max 2 for STEM)
- Enemy types: ___ (max 2)
- Win/lose condition: ___
- Week 1 deliverable (playable prototype): ___
- Week 2 deliverable (full game, unpolished): ___
- Week 3 deliverable (polished, bug-fixed build): ___

---

**⚠️ Misconception:** "I have a great idea, but I'm not sure if it's fun. Let me spend the first week designing it on paper."

**What it looks like:** A student spends 3–5 days writing game design documents and planning levels. By the time they build it, there's no time to iterate.

**Why students think this:** Design before building feels methodical and safe. They don't understand rapid prototyping.

**How to address it:** Prototype in 2 days. "In a STEM course, you must have something playable in 2 days—not 2 weeks. Use placeholder art (colored cubes), ignore sound, skip menus. Just make the core mechanic work. Is it fun? If no, redesign IMMEDIATELY. A 2-day prototype teaches more than a week of design docs."

---

### Design Iteration & Playtesting (Throughout)

**⚠️ Misconception:** "My game is technically complete. I'm done."

**What it looks like:** A student finishes implementing features but never shows it to anyone else. Bugs that are obvious to outside players go unfixed.

**Why students think this:** The developer is blind to their own game. What's obvious to them is confusing to others.

**How to address it:** Mandate playtesting. "Before you call it done, have ONE other person play it while you watch silently. You cannot talk. Watch where they get confused, where they die unfairly, where they stop having fun. That's your bug list. Fix those things first. In a STEM course, you should playtest at least twice: once at the halfway point and once in the final week."

🚨 **STEM Priority — STOP THE CLASS:** If it's Day 7 and no one has playtested anything, stop all work and do a whole-class playtesting session. Pair students, give them 5 minutes each, and debrief.

---

**⚠️ Misconception:** "My playtester said the game was too hard. I made it much easier. Now it's boring."

**What it looks like:** A student swings from "too hard" to "trivially easy" in one revision.

**Why students think this:** They take all feedback as equally important and make maximal changes.

**How to address it:** Make small, measured adjustments. "Not all feedback is equal. One person saying it's hard doesn't mean it is. Five people saying it's hard means it is. Make small adjustments: reduce enemy health by 10%, increase player speed by 5%. Test again. Tuning is iterative—small moves, retest, small moves, retest. Don't swing wildly based on one tester."

---

### Core Mechanic vs. Polish (Throughout)

**⚠️ Misconception:** "My game is boring. I'll add screen shake, particles, and music to make it feel better."

**What it looks like:** A student adds visual effects to a game with a broken or boring core mechanic. It looks better but still isn't fun.

**Why students think this:** Polish is visible and satisfying to add. They don't realize polish enhances a good mechanic but can't save a bad one.

**How to address it:** Prioritize core mechanic first. "Polish (effects, sound, animation) amplifies what's already there. If jumping feels bad, screen shake makes bad jumping look flashy. First make jumping feel good. Then add effects. Ask: 'Is the core mechanic fun with no art or sound?' If yes, polish it. If no, fix the mechanic before adding anything else."

---

**⚠️ Misconception:** "I'm behind schedule. I'll skip playtesting and bug fixing to add more features."

**What it looks like:** A student sees the deadline approaching and adds features instead of polishing what exists.

**Why students think this:** They think more features = better game. They don't prioritize polish.

**How to address it:** Cut features, not playtesting. "If you're behind, cut features—not playtesting or bug fixes. Remove a level, simplify an enemy type, skip the boss. But make what remains work correctly and feel polished. A small, solid game with no bugs beats a large, broken game every time. In a STEM course with 2-3 weeks, scope is everything."

---

### Time Management (Throughout)

**⚠️ Misconception:** "I'll finish the core mechanic this week and polish next week. I have plenty of time."

**What it looks like:** A student doesn't account for debugging time. The "simple" feature takes 3 days instead of 1. They run out of time.

**Why students think this:** They underestimate debugging and integration time.

**How to address it:** Build in buffer time. "Double your time estimates. If you think something takes 2 hours, plan for 4. Debug and integration always take longer than expected. Also, playtesting always reveals bugs. Leave at least 2 full days at the end for bug fixing. In a STEM capstone, your schedule should be: Week 1 = prototype, Week 2 = implementation, Week 3 = playtesting and polish ONLY—no new features."

---

## Whole-Class Warning Signs

- **Multiple students have never playtested by the end of Week 1.** This is a critical red flag. Force a class playtesting session immediately. Pair all students, 5 minutes each. The feedback students get from watching someone else play their game is irreplaceable.

- **Everyone's behind schedule and panicking in Week 2.** They over-scoped or spent too long on art/menus. Remind them: cut features. Help them identify the 2-3 things that are essential and cut everything else. Done is better than ambitious.

- **Several students are spending days on art before the core mechanic works.** Placeholder art is fine. Direct them: "Get the core mechanic working first. Art is the last 10% of the game."

- **Students have technically complete games that aren't fun.** Common for STEM students who prioritize correctness over feel. Play each student's game and give direct, specific feedback: "The jump is too slow. Make it 20% faster and test."

- **A few students say 'I'm done' in Week 1 of a 3-week capstone.** Either they under-scoped, aren't testing thoroughly, or are burned out. Have a conversation: walk through the success criteria together. Are all 6 criteria met? If yes, help them scope UP with an optional extension (new level, new enemy, leaderboard).

---

## Questions That Reveal Understanding

1. **"What's the minimum game you could build in one week that demonstrates your core mechanic?"**
   - Good answer: "One level, one enemy type, basic player movement and attack, a win and lose condition. Playable start to finish."
   - Red flag: "I have to include [3+ features]." (They don't understand MVP.)

2. **"You're halfway through the capstone and behind schedule. What's your next move?"**
   - Good answer: "Cut a feature. Identify what's not essential and remove it. Keep the core mechanic solid. Use remaining time for polish and bug fixes."
   - Red flag: "Stay late and catch up" or "Skip playtesting." (Unsustainable and prioritizes wrong things.)

3. **"Your playtester says the game is too hard. What do you do?"**
   - Good answer: "Make one small adjustment (reduce enemy damage by 10%). Test again. Repeat. Don't overhaul the game based on one tester."
   - Red flag: "Make it much easier" or "Ignore the feedback." (Either extreme is wrong.)

4. **"Your core mechanic is working but feels flat. What do you add first?"**
   - Good answer: "Game feel improvements to the mechanic itself—better jump physics, snappier controls, responsive collision feedback. Then sound effects. Then visual polish."
   - Red flag: "Particle effects and screen shake." (Not wrong, but jumping straight to effects without fixing the mechanic first is the wrong order.)

5. **"What are the six success criteria for a capstone game?"**
   - Good answer: "Playable start-to-finish, clear and fun core mechanic, playtested and iterated, has polish appropriate to scope, shows mastery of course concepts, and delivered on time."
   - Red flag: Listing features instead of criteria. (They're thinking about output, not quality.)

---

## Common Student Questions & How to Answer Them

**Q1: "My game is done, but it doesn't feel fun. What do I do?"**

*A:* "Playtest it with someone who hasn't seen it. Watch them play without talking. Where do they die unfairly? Where do they seem bored? What do they say out loud? Fix the top 3 issues. Then ask: is the core mechanic fun in isolation? Try playing for 60 seconds—is it engaging? If no, the mechanic needs work. If yes, the problem is somewhere else (level design, difficulty, pacing)."

---

**Q2: "I have a lot of ideas but can't decide which game to build."**

*A:* "Pick the one you're most excited about. Build a 2-day prototype. Is it fun? If yes, build it. If no, try the next idea. The only way to know if an idea is fun is to build a prototype. Don't spend more than 2 days prototyping—pick something and commit."

---

**Q3: "My game has a bug I can't fix. Should I keep trying or work around it?"**

*A:* "Spend 30 minutes max on a single bug before asking for help. After 30 minutes: explain the bug to me or a classmate (rubber duck debugging often reveals the solution). If it's still broken after asking: consider if you can cut the feature and still have a complete game. Never spend 2 days on a single bug with a deadline approaching."

---

**Q4: "How do I balance difficulty? Some playtesters say it's too hard and some say it's fine."**

*A:* "Mixed feedback means you're probably close. Make one small adjustment and test with more people. Also consider adding difficulty options if time allows: an Easy mode that reduces enemy health or increases player damage. 5-10% adjustments at a time—never overhaul difficulty based on 1-2 testers."

---

**Q5: "I want to add [feature] but I'm not sure if I have time."**

*A:* "Estimate how long it will take, then double it. If the doubled estimate fits before your deadline with 2 days left for polish, add it. If not, cut it. No new features in the last 2 days—use that time for bug fixes and polish only."

---

## Mentoring Strategies

**Week 1: Prototype & Validate**
- Day 1: Scope document. One mechanic, one level, clear win/lose. Enforce it.
- Days 2-3: Playable prototype. Ugly is fine—does the core mechanic work?
- Days 4-5: Playtest with a partner. Is the mechanic fun? Redesign if not.
- Watch for: students who haven't started, students who are drawing art instead of coding.

**Week 2: Implement & Iterate**
- Focus on wiring everything together: player, enemies, level, UI, win/lose.
- Playtest every 2-3 days. Fix the top issue from each session.
- Watch for: scope creep (adding features instead of finishing existing ones).
- Key question: "If class ended today, would your game be submittable? If no, what's the most important thing to finish?"

**Week 3: Polish & Bug Fix**
- No new features after Day 1 of Week 3.
- Bug fix, playtesting, UI polish, audio, final balance.
- Final playtest session 2 days before deadline.
- Watch for: students still adding features instead of polishing.

---

## Success Criteria for Capstone (STEM Version)

A successful capstone game:
1. **Is playable start-to-finish** without game-breaking bugs.
2. **Has a clear, fun core mechanic** that players understand within 30 seconds.
3. **Has been playtested** with at least 2 outside players and iterated based on feedback.
4. **Has appropriate polish** (UI, audio, visual feedback) for its scope.
5. **Demonstrates mastery** of at least 4 of the 7 units (C#, physics, controls, UI, 2D, systems, design).
6. **Was delivered on time** with a realistic scope.

It does NOT have to:
- Be graphically impressive (placeholder art is fine).
- Have all originally planned features (scope cuts are expected).
- Be a novel idea (remakes and clones are great for learning).
- Be perfectly balanced.

---

## Grading Considerations (STEM Capstone)

**Technical (40%):**
- Code quality and organization (use of functions, no redundancy).
- Physics and collision working correctly.
- UI functional and readable.
- No game-breaking bugs.

**Design (30%):**
- Core mechanic is clear and engaging.
- Evidence of playtesting (playtest log or iteration notes).
- Scope was appropriate to time.

**Presentation (20%):**
- Game is playable with a clear goal.
- Player feedback (sound, visual) is present.
- Controls are intuitive without explanation.

**Process (10%):**
- Student iterated based on feedback.
- Scope document matches delivered game.
- Time was managed effectively (no "it's not done" as final submission).

---

## Analogies That Work

1. **"Scope is a budget. You have 3 weeks (your budget). Each feature costs time. Playtesting costs time. Polish costs time. Overspend and you ship nothing. Cut ruthlessly and ship something great."**
   - Makes the scope-cutting conversation feel practical, not punitive.

2. **"Building a game without playtesting is like writing code without running it. You'd never ship code you haven't tested. Don't ship a game you haven't watched someone else play."**
   - Resonates immediately with STEM students who understand code testing.

3. **"Polish is the frosting on a cake. Great frosting on a bad cake is still a bad cake. Make the cake first. A plain cake that tastes good is better than a beautiful cake that tastes wrong."**
   - Keeps core mechanic first in students' minds.

---

## Post-Capstone

After submission, have students:
1. **Write a 1-page retrospective:** What went well? What would you do differently? What feature didn't make the cut and why?
2. **Playtest someone else's game** and write 3 pieces of constructive feedback.
3. **Present to the class** in 2 minutes: show the game, explain the core mechanic, and share one thing they'd change.

This closure loop is especially valuable in STEM courses where students learn as much from reflection as from building.

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
