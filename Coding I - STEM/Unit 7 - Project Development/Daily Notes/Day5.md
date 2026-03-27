# Day 5: Presentations

### How to Present Your Project

A great 5-minute presentation has this structure:

| Section | Time | What to Cover |
|---------|------|--------------|
| **Introduction** | 30 sec | Name your program, state the problem it solves |
| **Demo** | 2 min | Run it live — show normal input, then an edge case |
| **Code Walkthrough** | 1.5 min | Explain 1–2 interesting functions (not line by line) |
| **Challenges** | 45 sec | What was the hardest part? How did you solve it? |
| **Questions** | 30 sec | Invite 1–2 questions |

### Presentation Tips

**Do:**
- Open your code in the editor before you start
- Have your test inputs ready (write them down)
- Speak to the audience, not the screen
- Say "when I call X it does Y" — show the connection
- Be ready for "what happens if the user types nothing?"

**Don't:**
- Read the code line by line (explain the logic instead)
- Say "I didn't get to implement..." (focus on what works)
- Apologize for imperfections (own your work!)
- Rush — it's okay to pause and think

### Sample Presentation Script

```
"Hi, I built a Grade Tracker. The problem: keeping track
of your scores throughout the year is tedious — my program
lets you enter scores, calculates your average, and saves
a report to a file.

Let me show you a demo... [runs program]
I'll enter three scores: 88, 92, 79. The program calculates
the average as 86.3 and assigns a B. Now watch what happens
when I type 'hello' instead of a number... [shows error handling]
It just asks again — no crash.

The most interesting function is get_scores(). It loops until
the user types 'done', but it validates every input with
try/except to catch bad data. Here's the key part... [shows code]

The hardest part was the file saving — I had to make sure it
handled the case where the file couldn't be written.

Any questions?"
```

### Presentation Prep Checklist
- [ ] Program runs without crashing on normal input
- [ ] I know what to type for my live demo
- [ ] I can explain 2 functions in plain English
- [ ] I know what was hardest and how I solved it
- [ ] I've practiced saying my presentation out loud at least once

---