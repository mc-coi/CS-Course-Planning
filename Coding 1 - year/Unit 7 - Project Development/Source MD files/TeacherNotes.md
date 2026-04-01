# Unit 7 - Project Development: Teacher Misconception & Callout Guide

## Overview

Unit 7 is where students apply everything they've learned to build complete, real-world programs from start to finish. Unlike previous units that focus on single concepts, this unit emphasizes software engineering practices: planning before coding, iterative development, systematic testing, and professional communication. The biggest teaching challenges are: (1) students dive into coding before planning, leading to tangled, hard-to-debug programs; (2) they confuse "it works" with "it's well-designed," skipping refactoring and documentation; (3) they test only happy paths, missing edge cases that break their projects; (4) they struggle to manage complexity and don't know how to break large problems into manageable pieces; and (5) they view the software development lifecycle as optional ("that's for professional programmers"), not understanding it prevents chaos. These misconceptions result in projects that are difficult to demo, hard to debug, and impossible to enhance later.

---

## Misconceptions by Topic

### The Software Development Lifecycle (Days 146–150)

**⚠️ Misconception:** "I should just start coding" OR "Planning is a waste of time; real programmers jump in."

**What it looks like:**
```
Student A:
- Opens the code editor immediately
- Writes code, changes mind, deletes it
- Adds features randomly
- Project becomes tangled and hard to debug

Student B:
- Writes down what the program should do
- Plans the major pieces (functions, data structures)
- Codes incrementally, testing as they go
- Project is clean, debuggable, and extensible
```

**Why students think this:** In previous units, the projects were small enough to write directly. They think larger projects work the same way. They also see writing code as "the real work" and planning as busywork.

**How to address it:** **Make planning mandatory and valued.**

Show the SDLC phases:

| Phase | What You Do | Output |
|-------|------------|--------|
| **1. Define** | Understand the problem, write specifications | Problem statement, features list |
| **2. Plan** | Design architecture, pseudocode, flowcharts | Specifications, design document |
| **3. Design** | Design UI, data structures, function signatures | Prototypes, function list |
| **4. Code** | Write code incrementally, test as you go | Working features |
| **5. Test & Polish** | Test systematically, debug, refactor, document | Polished, tested code |
| **6. Present** | Demo, explain design, reflect | Presentation, portfolio |

Explain: "Professional programmers spend 20% of time planning and 80% coding. It sounds backwards, but it's because planning prevents mistakes later. When you jump in without planning, you spend 80% coding and 80% debugging."

Require deliverables for each phase:
- **Phase 1:** One-page problem statement
- **Phase 2:** Pseudocode or flowchart, list of functions
- **Phase 3:** Design document (data structures, function signatures)
- **Phase 4:** Working code (built incrementally)
- **Phase 5:** Test results, refactored code, docstrings
- **Phase 6:** Presentation, README

This changes the mindset from "just code" to "think first, then code."

---

### Scope Creep & Defining the MVP (Days 146–150)

**⚠️ Misconception:** "I should add every feature I think of" OR "More features = better project."

**What it looks like:**
```
Student starts with:
- "I'll build a text-based game with inventory, NPC AI, save/load, multiplayer..."

By mid-project:
- "I'm stuck on the inventory system"
- "I haven't even started the game logic"
- "I have 500 lines of code and it doesn't work"

Better approach:
- MVP (minimum viable product): Simple game with basic commands
- Extra features only if MVP works first
- Each extra feature is a separate phase
```

**Why students think this:** They're excited and ambitious. They don't understand that features interact in complex ways. They haven't experienced the pain of scope creep.

**How to address it:** **Define MVP early and enforce it.**

"An MVP is the smallest version of your project that still works. For a game, that might be: the player can move, enemies can spawn, collision detection works. That's enough. Save/load and AI can come later if you have time."

Show the difference:
```
MVP Features:
- User can enter numbers
- Program calculates average
- Program displays result

Nice-to-Have Features:
- Validation of input
- Support for negative numbers
- Export to file

Won't-Do-But-Cool Features:
- Graphical UI
- Multi-threading
- Database
```

Make students commit to an MVP in their proposal. Require them to prioritize features. This teaches the reality of software development.

---

### Incremental Development & Version Control (Days 156–165)

**⚠️ Misconception:** "I'll build the whole thing, then test it" OR "Version control is for professionals, not students."

**What it looks like:**
```
Bad approach:
- Day 1–5: Write all the code
- Day 6: Test everything
- Day 7: Debug for hours, realize the entire architecture is wrong

Good approach:
- Day 1: Build core feature (player movement)
- Test: Make sure movement works
- Day 2: Add next feature (collision detection)
- Test: Make sure both work together
- Day 3: Add next feature...
- By day 5, you have a working program, not a time bomb
```

**Why students think this:** They think testing means "does it run without crashing?" They don't see testing as part of development. Version control feels like overhead.

**How to address it:** **Require incremental development and frequent commits.**

"Each day, add *one* feature and test it. Commit to Git with a message like 'Add collision detection.' This way, if something breaks, you only have to look at today's changes. It also shows progress."

Teach the practice:
```
Day 1: Core feature (player can move)
- Write code
- Test: Does it work? ✓
- Commit: "Feature: Player movement"

Day 2: Add next feature (enemies spawn)
- Write code
- Test: Does everything still work? ✓
- Commit: "Feature: Enemy spawning"

Day 3: Fix bugs from testing
- Debug
- Test: All features still work? ✓
- Commit: "Bugfix: Collision detection false positives"
```

Show Git as a safety net: "If you break something, you can look at what you changed today. Or you can revert to yesterday and start over."

For Unit 7, don't require Git if it's not in the curriculum, but encourage it. The principle of incremental development is essential.

---

### Testing & Edge Cases at Scale (Days 166–170)

**⚠️ Misconception:** "If my program runs, it's tested" OR "I don't need to test edge cases for my project."

**What it looks like:**
```
Incomplete testing:
- Student tests with one example input
- "It works!"
- Presents project, and it crashes on unexpected input

Comprehensive testing:
- Student tests normal input ✓
- Tests empty/no input ✓
- Tests boundary values ✓
- Tests invalid input ✓
- Creates test cases and documents results
```

**Why students think this:** They haven't built anything large enough to need comprehensive testing. They don't see testing as essential.

**How to address it:** **Make testing a requirement, not an afterthought.**

Require a test plan:

| Scenario | Input | Expected | Actual | Status |
|----------|-------|----------|--------|--------|
| Normal | ... | ... | ... | PASS |
| Empty | ... | ... | ... | PASS |
| Boundary | ... | ... | ... | PASS |
| Invalid | ... | ... | ... | PASS |

Teach stress testing: "Does your program slow down with 100 items? 1,000? Does it handle rapid input changes?"

Show the bugs that testing reveals:
```python
# Program: Find the maximum in a list
def find_max(items):
    max_item = items[0]
    for item in items:
        if item > max_item:
            max_item = item
    return max_item

# Test: Normal case
find_max([3, 1, 4, 1, 5])  # 5 ✓

# Test: Empty list
find_max([])  # IndexError!
# Bug found: Doesn't handle empty lists

# Better version:
def find_max(items):
    if not items:
        return None
    max_item = items[0]
    for item in items:
        if item > max_item:
            max_item = item
    return max_item
```

Students who test systematically produce better projects.

---

### Code Organization & Modularity (Days 156–165)

**⚠️ Misconception:** "I should write everything in main()" OR "Modularity is optional."

**What it looks like:**
```
Bad organization:
def main():
    # 200 lines of code
    # Input handling
    # Game logic
    # Output
    # Everything

Good organization:
def get_user_input():
    # Input validation
    pass

def process_game_logic():
    # Game mechanics
    pass

def display_output():
    # Formatting
    pass

def main():
    # Orchestrates the above
    pass
```

**Why students think this:** They haven't felt the pain of maintaining 200-line functions. They think "it works" is good enough.

**How to address it:** **Enforce function decomposition in projects.**

Requirement: "No function should be longer than 30 lines. If it is, break it into smaller functions."

Benefits:
- **Testability:** Test each function independently
- **Readability:** Each function does one thing
- **Reusability:** Use functions in other programs
- **Debuggability:** Find bugs faster in smaller functions

Show the organization pattern:
```python
def main():
    """Orchestrate the program."""
    setup()
    while game_running:
        player_input = get_input()
        update_game_state(player_input)
        display_state()
    cleanup()

def get_input():
    """Get and validate user input."""
    pass

def update_game_state(player_input):
    """Update game based on player action."""
    pass

def display_state():
    """Display current game state."""
    pass
```

This teaches professional organization.

---

### Documentation & README (Days 171–175)

**⚠️ Misconception:** "Documentation is optional" OR "Good code documents itself."

**What it looks like:**
```
No documentation:
- Project has no README
- Functions have no docstrings
- No explanation of how to use it
- Someone else (or you later) can't figure it out

Good documentation:
- README with overview, how to run, examples
- Docstrings for all functions
- Comments explaining non-obvious logic
- Code is clear and well-organized
```

**Why students think this:** They haven't maintained code they wrote months ago. They don't realize how quickly they forget their own reasoning.

**How to address it:** **Require documentation as part of the project.**

Require a README with:
- **Overview:** What does your project do?
- **How to run:** Step-by-step instructions
- **Features:** What can the user do?
- **Known limitations:** What doesn't work?
- **Future improvements:** What could be added?

Example:
```markdown
# Dice Game

A command-line dice game where you roll dice and try to reach 21 without going over.

## How to Run

1. Open terminal
2. Navigate to project folder
3. Run: python game.py

## Features

- Roll one die or multiple dice
- Track your score
- Compare against dealer
- Play multiple rounds

## Known Limitations

- No graphics (text-based only)
- No save/load between sessions
- Dealer strategy is simple

## Future Improvements

- Add betting system
- Implement save/load
- Add AI difficulty levels
```

Require docstrings for all functions:
```python
def roll_dice(num_dice=1):
    """Simulate rolling dice and return the total.

    Args:
        num_dice (int): Number of dice to roll (default 1)

    Returns:
        int: Total of all dice rolls
    """
    pass
```

This teaches students to think like maintainers, not just coders.

---

### Refactoring & Code Quality (Days 166–170)

**⚠️ Misconception:** "Refactoring is polishing; it's not important" OR "If it works, don't touch it."

**What it looks like:**
```
Before refactoring:
- Repeated code (copy-paste)
- Long functions
- Unclear variable names
- No comments
- Hard to change

After refactoring:
- DRY (Don't Repeat Yourself)
- Short functions with single responsibility
- Clear, meaningful names
- Comments explaining why
- Easy to change and extend
```

**Why students think this:** They've been taught "if it works, you're done." They don't see the difference between "working" and "well-designed."

**How to address it:** **Make refactoring a phase in the SDLC.**

Teach refactoring techniques:
1. **Extract repeated code into functions**
2. **Rename for clarity**
3. **Break long functions into smaller ones**
4. **Remove unused code**

Show the improvement:
```python
# Before: Repeated code
x = int(input("Number: "))
if x < 0:
    print("Invalid")
    x = int(input("Number: "))

y = int(input("Number: "))
if y < 0:
    print("Invalid")
    y = int(input("Number: "))

# After: Extracted function
def get_positive_number(prompt):
    while True:
        x = int(input(prompt))
        if x >= 0:
            return x
        print("Invalid")

x = get_positive_number("X: ")
y = get_positive_number("Y: ")
```

Refactoring is where students learn design thinking. It's not polish; it's essential.

---

### Handling Complexity & Debugging Large Projects (Days 156–170)

**⚠️ Misconception:** "I can debug large projects the same way I debug small ones" OR "If something's wrong, I'll rewrite it."

**What it looks like:**
```
Small project debugging:
- Add a print statement
- See what's wrong
- Fix it

Large project debugging:
- Hundreds of lines of code
- Multiple functions calling each other
- Hard to know where the problem is
- Random rewrites don't help
```

**Why students think this:** They haven't worked on large projects where random changes make things worse.

**How to address it:** **Teach systematic debugging for large projects.**

Strategy:
1. **Isolate the problem:** Which function is failing?
2. **Test the function alone:** Call it with known inputs
3. **Check inputs and outputs:** Use print statements or a debugger
4. **Trace through the logic:** Step through by hand
5. **Fix the root cause:** Don't just patch symptoms

Show the tool: Python debugger (pdb)
```python
import pdb

def complex_function(a, b):
    result = a * b
    pdb.set_trace()  # Program pauses here; you can inspect variables
    return result
```

Students often resort to rewriting everything when they get stuck. Teaching them to debug methodically builds confidence.

---

### Presenting & Communicating Design Decisions (Days 173–180)

**⚠️ Misconception:** "I just need to show that my code works" OR "Explaining design is unnecessary."

**What it looks like:**
```
Bad presentation:
- "Here's my code. It works."
- No explanation of design
- Audience doesn't understand the approach
- Can't answer questions about why you did something

Good presentation:
- "Here's the problem I solved..."
- "I designed it with these main functions..."
- "I chose this approach because..."
- Can answer questions about design and tradeoffs
```

**Why students think this:** They're focused on the product, not the process. They don't see communication as part of development.

**How to address it:** **Require thoughtful presentations.**

Presentation structure:
1. **Problem:** What did you build? For whom?
2. **Design:** How did you break it into pieces?
3. **Challenges:** What was hard? How did you solve it?
4. **Demo:** Show the program working (happy path and edge cases)
5. **Reflection:** What did you learn? What would you do differently?

Teach them to prepare:
- Write a script (don't memorize, but know your talking points)
- Practice the demo (make sure it works!)
- Prepare for questions ("Why did you choose this approach?")

This teaches communication skills that are essential in real work.

---

## Whole-Class Warning Signs

Watch for these patterns—if you see them, **stop and re-teach**:

- **Students jumping into code without a plan:** If you see code that seems tangled or students keep rewriting sections, they skipped planning. Have them write pseudocode before continuing.

- **Testing only happy paths:** If students say "I tested it, it works," ask them to test with empty input, invalid input, boundary values. Often something breaks.

- **100+ line functions:** If you see functions longer than 30 lines, require them to break it into smaller functions. This is a teachable moment about decomposition.

- **No documentation:** If docstrings are missing or comments are minimal, require them before the project is done. Documentation is not optional.

- **Scope creep disasters:** If a student is trying to implement 10 features and nothing works, have them cut back to MVP and get that working first.

- **Refactoring paralysis:** If a student keeps changing code without testing, teach them to refactor in small, testable chunks.

---

## Questions That Reveal Understanding

Ask these to assess real vs. surface-level understanding:

1. **"Why is planning important? Wouldn't you just code faster?"**
   - Good answer: "Planning prevents mistakes. If you plan wrong, you fix it on paper, not after writing 500 lines of code. Planning saves time overall."
   - Surface answer: "Teachers say so?" (Doesn't see the value.)

2. **"What's an MVP? Why not just build the whole thing?"**
   - Good answer: "MVP is the smallest working version. You build it first, make sure it works, then add features. This prevents getting stuck on complex features."
   - Surface answer: "Minimum Viable Product?" (Correct term, doesn't explain why it matters.)

3. **"How would you test a complex program?"**
   - Good answer: "Test each function independently. Test normal cases, empty cases, boundary values, and invalid input. Document test results to make sure everything passes."
   - Surface answer: "Run it and see if it works?" (Doesn't understand systematic testing.)

4. **"Why should you refactor if your code works?"**
   - Good answer: "Refactoring makes code clearer, easier to maintain, and easier to extend. Working code is not the same as good code."
   - Surface answer: "It makes it pretty?" (Misses the real benefits.)

5. **"What should your presentation cover?"**
   - Good answer: "The problem you solved, your design (how you broke it into pieces), challenges you faced, a demo, and what you learned."
   - Surface answer: "Show the code?" (Doesn't understand that communication matters.)

6. **"How long should functions be?"**
   - Good answer: "Around 10–20 lines ideally. If longer, break into smaller functions. One function should do one thing."
   - Surface answer: "As long as needed?" (Doesn't understand modularity.)

---

## Common Student Questions & How to Answer Them

### Q1: "Should I plan my whole project before coding?"

**Good answer:** "Plan the MVP and the architecture (main functions, data structures). That's maybe 30% planning. Then code incrementally, testing as you go. You'll discover details as you build, but the big picture should be clear first."

**Why this works:** It balances planning and coding, showing that both matter.

---

### Q2: "My program is getting really complex. How do I manage it?"

**Good answer:** "Break it into smaller functions, each doing one thing. Test each function independently. Use print statements to trace what's happening. Commit your changes to Git frequently so you can revert if something breaks."

**Why this works:** It gives concrete tools for managing complexity.

---

### Q3: "I'm stuck on a bug. Should I rewrite everything?"

**Good answer:** "No. Instead, isolate the problem. Which function is failing? Test it in isolation with known inputs. Use print statements to see what values variables have. Trace through the logic by hand. Usually, you'll find a small fix, not a rewrite."

**Why this works:** It teaches systematic debugging instead of panic-driven rewrites.

---

### Q4: "What if I don't have time to implement all my features?"

**Good answer:** "That's why you define MVP first. If you run out of time, you still have a working MVP. Document what you didn't do in your README. In real jobs, this is how software is built—you get the core working, then add features later."

**Why this works:** It reframes scope creep as normal and MVP as a safety net.

---

### Q5: "Should I comment every line of code?"

**Good answer:** "No. Comment the why, not the what. If you have a complex algorithm or a non-obvious decision, explain it. If the code is obvious, no comment needed. Aim for 2–5 meaningful comments per function."

**Why this works:** It gives them a balance between no comments and over-commenting.

---

## Analogies That Work

### Analogy 1: Building a House vs. Building a Program

**When to use:** When explaining why planning matters.

**The analogy:** "Building a house without a blueprint is a nightmare. You pour the foundation, realize the walls don't fit, tear it out, start over. With a blueprint, the architect makes sure everything works before the first nail is hammered. Programming is the same. Your blueprint is pseudocode and design. It prevents building in the wrong direction."

**Why it works:** It shows planning as insurance against catastrophic mistakes.

---

### Analogy 2: MVP as the First Draft

**When to use:** When teaching scope management and iteration.

**The analogy:** "Writing a novel: you don't wait until it's perfectly written to share it. You write a first draft, see what works, then revise. Software is the same. Your MVP is the first draft. Get it working, then enhance. Trying to write the perfect first draft takes forever."

**Why it works:** It removes the pressure to be perfect the first time.

---

### Analogy 3: Refactoring as Cleaning Your Room

**When to use:** When teaching that refactoring is important.

**The analogy:** "Your code works, but it's messy. Refactoring is like cleaning your room. It doesn't add new features, but it makes everything easier to find and use. A messy room is hard to live in; messy code is hard to maintain."

**Why it works:** It frames refactoring as maintaining, not polishing.

---

## Summary of Teaching Priorities

In order of importance (most cascading-confusion first):

1. **Plan before coding** – Prevents architecture disasters and scope creep.
2. **Define MVP early** – Keeps students focused and prevents overwhelm.
3. **Incremental development** – Builds working code daily, not a time bomb on day 7.
4. **Systematic testing** – Catches bugs before presentation.
5. **Code organization & modularity** – Makes code testable and maintainable.
6. **Refactoring** – Transforms "working" into "well-designed."
7. **Documentation** – Allows others (and yourself) to understand your work.
8. **Presenting & communicating design** – Shows professionalism and understanding.

Focus energy on items 1–4. Mastery here results in projects that actually work. Items 5–8 are the polish that makes projects professional.

## Final Note

Unit 7 is where students transition from "writing code" to "software development." They learn that programming is 20% coding and 80% thinking, planning, testing, and refactoring. This mindset shift is more important than any specific technique. A student who plans, tests, and refactors will produce better work than one who just codes, even if they're equally skilled coders.

Model this mindset in every lesson. Show your own projects going through the phases. Share your own debugging stories. Let them see that real programmers follow processes, not just intuition.

