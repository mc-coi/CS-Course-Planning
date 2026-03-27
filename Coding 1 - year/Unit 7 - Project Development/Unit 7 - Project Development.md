# Unit 7: Project Development
> Apply everything you've learned to build a complete, professional Python application.

## 📋 Unit Overview
- **Duration:** 35 days / 7 weeks (Days 146–180)
- **Schedule:** Monday–Friday, 55-minute periods
- **Key Concepts:** Software development lifecycle, project planning, iterative development, testing, debugging, documentation, presentation
- **Big Idea:** Real programming is solving real problems systematically — from defining the problem to designing architecture, building incrementally, testing thoroughly, documenting clearly, and presenting professionally
- **TN Standards Addressed:** Computational thinking, problem decomposition, program design, software engineering best practices, technical communication, collaboration

---

## Learning Targets

By the end of Unit 7, I can:

- **Design & Plan:** Define a problem clearly, write specifications, design architecture before coding
- **Develop Incrementally:** Build code in small, testable pieces using bottom-up development
- **Test Systematically:** Unit test individual functions and integration test how pieces work together
- **Debug Professionally:** Identify and fix bugs using error messages, print tracing, and systematic reasoning
- **Code for Quality:** Write clean, readable, well-documented code following industry standards
- **Refactor Confidently:** Improve structure and readability without changing functionality
- **Document Thoroughly:** Write docstrings, comments, README files, and user guides
- **Present Professionally:** Demonstrate projects clearly and explain design choices confidently
- **Reflect & Grow:** Evaluate your learning, recognize growth areas, and plan next steps

---

## Unit 7 Structure (Days 146–180)

### Week 30 (Days 146–150): Software Development Process
**Focus:** Understanding the full lifecycle and planning your project

- **Day 146:** The Software Development Lifecycle (SDLC)
- **Day 147:** Writing a project proposal — problem statement, audience, features
- **Day 148:** Planning with pseudocode and flowcharts
- **Day 149:** Breaking a project into milestones and tasks
- **Day 150:** Peer review of project proposals

### Week 31 (Days 151–155): Design & Prototyping
**Focus:** Designing architecture and building a working MVP

- **Day 151:** User interface design — text-based menus and interaction flow
- **Day 152:** Data design — planning variables, lists, dictionaries, data structures
- **Day 153:** Function design — planning functions and their signatures before coding
- **Day 154:** Building a working prototype (MVP) — core functionality
- **Day 155:** Prototype demo and peer feedback

### Week 32 (Days 156–160): Core Development Sprint 1
**Focus:** Implementing core features with quality and testing

- **Day 156:** Setting up project structure — `main()`, helper functions, organization
- **Day 157:** Core feature development — **work day** (check-in, debugging tips, progress tracking)
- **Day 158:** Core feature development — **work day** (check-in, mini-challenges, peer support)
- **Day 159:** Code review and debugging session — peer review, collaborative debugging
- **Day 160:** Progress check and sprint retrospective

### Week 33 (Days 161–165): Core Development Sprint 2
**Focus:** Adding advanced features and ensuring robustness

- **Day 161:** Additional features development — **work day** (check-in, debugging tips, progress tracking)
- **Day 162:** Additional features development — **work day** (check-in, mini-challenges, peer support)
- **Day 163:** Input validation and error handling — defensive coding
- **Day 164:** File I/O integration — save/load data, persistence
- **Day 165:** Progress check and sprint retrospective

### Week 34 (Days 166–170): Polish & Testing
**Focus:** Ensuring quality, reliability, and user experience

- **Day 166:** Code cleanup — comments, docstrings, variable names, organization
- **Day 167:** Testing — systematic testing with edge cases and stress testing
- **Day 168:** Bug fixing day — addressing testing issues
- **Day 169:** User experience polish — menus, output formatting, clarity
- **Day 170:** Feature freeze — final code review before lock-down

### Week 35 (Days 171–175): Documentation & Presentation Prep
**Focus:** Preparing to share your work

- **Day 171:** Writing project documentation — README, user guide, technical guide
- **Day 172:** Code walkthrough practice — explaining your code clearly
- **Day 173:** Building a presentation — slides, demo plan, narrative
- **Day 174:** Presentation rehearsal — peer feedback, timing, refinement
- **Day 175:** Final project submission

### Week 36 (Days 176–180): Presentations & Course Wrap-Up
**Focus:** Sharing your achievements and reflecting on growth

- **Day 176:** Project presentations — Group A (first half of class)
- **Day 177:** Project presentations — Group B (second half of class)
- **Day 178:** Course reflection — looking back on growth, celebrating learning
- **Day 179:** Looking ahead — CS career paths, Coding II preview, next steps
- **Day 180:** End-of-year celebration and portfolio review

---

## 📂 Unit 7 Resources

### Core Files in This Unit
1. **Daily Notes (Day 146–180):** Detailed lesson plans for each day
2. **ReferenceGuide.md:** SDLC framework, planning templates, documentation standards
3. **UnitPractice.md:** 15 project practice problems across difficulty levels
4. **UnitAssessment.md:** Project rubric and self-evaluation

### Key Concepts

#### The Software Development Lifecycle (SDLC)

Great software starts on paper, not in the code editor. Follow these six phases:

| Phase | What You Do | Output | Days |
|-------|------------|--------|------|
| **1. Define** | Understand the problem; identify users and needs | Problem statement | 146–147 |
| **2. Plan** | Design architecture; write pseudocode; break into tasks | Specifications, pseudocode, flowcharts | 148–150 |
| **3. Design** | Design UI, data structures, and functions | Prototypes, design docs | 151–155 |
| **4. Code** | Write code incrementally, test as you go | Working features | 156–165 |
| **5. Test & Polish** | Systematic testing, debugging, refactoring, documentation | Polished, tested code | 166–172 |
| **6. Present** | Demo, explain, reflect, celebrate | Presentation, portfolio | 173–180 |

#### Project Proposal Template

Fill this out **before** writing any code:

```
PROJECT TITLE: ___________________________

PROBLEM STATEMENT:
What problem does this program solve?
Who would use it?
Why is it important?

TARGET AUDIENCE:
Who are your users? What do they need?

CORE FEATURES (must-haves):
1.
2.
3.

NICE-TO-HAVE FEATURES:
1.
2.

INPUTS:
What data does the program take in?
(user input, files, data sources, etc.)

OUTPUTS:
What does the program produce?
(printed results, files, visualizations, etc.)

TECHNOLOGY & DATA STRUCTURES:
What Python features will you use?
(lists, dictionaries, file I/O, loops, functions, etc.)

FUNCTION LIST:
Function name         | What it does              | Parameters | Return value
--------------------- | ----------------------- | ---------- | -----------
main()                | Orchestrate the program |            |
...                   |                         |            |

TEST CASES:
Input → Expected Output
[normal case]  →
[edge case]    →
[error case]   →
```

#### Pseudocode Structure

Write logic in plain English first — no Python syntax:

```
PROGRAM: Grade Calculator

1. Show welcome message
2. Ask for student's name
3. Loop until user types "done":
   a. Ask for a score
   b. Validate the score (must be 0-100)
   c. Add to scores list
   d. Show confirmation
4. Calculate average of all scores
5. Convert average to letter grade
6. Display formatted report
7. Ask if user wants to save report to file
   a. If yes, write report to file
   b. Show success/error message
8. Ask if they want to process another student
```

#### Breaking Problems into Functions

Look at your pseudocode and ask "what is each step doing?" — each major step becomes a function.

```python
# From the pseudocode above:

def display_welcome():
    """Show opening message."""
    pass

def get_student_name():
    """Prompt for and validate student name."""
    pass

def get_scores():
    """Collect scores from user with validation."""
    pass

def calculate_average(scores):
    """Return the mean of a list of scores."""
    pass

def letter_grade(average):
    """Convert average to letter grade A-F."""
    pass

def display_report(name, scores, average, grade):
    """Print a formatted grade report."""
    pass

def save_report(filename, name, scores, average, grade):
    """Save report to a text file."""
    pass

def main():
    """Orchestrate the entire program."""
    display_welcome()
    name = get_student_name()
    scores = get_scores()
    avg = calculate_average(scores)
    grade = letter_grade(avg)
    display_report(name, scores, avg, grade)

    save_choice = input("\nSave report to file? (y/n): ").lower()
    if save_choice == "y":
        filename = f"{name.replace(' ', '_')}_report.txt"
        save_report(filename, name, scores, avg, grade)

    print("Thank you for using Grade Tracker!")

if __name__ == "__main__":
    main()
```

#### Bottom-Up Development Strategy

**Why bottom-up?**
- Each piece is easy to test in isolation
- Bugs are easier to find when scope is small
- You build confidence as each piece works
- Integration is cleaner when pieces are already tested

**Development order:**
1. Write and test the simplest, most basic function first
2. Test it immediately (don't wait!)
3. Add the next layer
4. Integrate gradually
5. Refactor as patterns emerge

#### Unit Testing Your Functions

Before connecting everything, test each function alone:

```python
def calculate_average(scores):
    """Return the mean of a list of scores."""
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def letter_grade(average):
    """Convert average to letter grade."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

# Test each function BEFORE connecting them
print("Testing calculate_average:")
print(calculate_average([90, 85, 92]))   # Expected: 89.0
print(calculate_average([70, 70, 70]))   # Expected: 70.0
print(calculate_average([]))             # Expected: 0.0

print("\nTesting letter_grade:")
print(letter_grade(95))   # Expected: A
print(letter_grade(83))   # Expected: B
print(letter_grade(55))   # Expected: F

# Add a simple test runner for larger projects
def test_calculate_average():
    assert calculate_average([100, 90, 80]) == 90.0, "Test 1 failed"
    assert calculate_average([70, 70]) == 70.0, "Test 2 failed"
    assert calculate_average([]) == 0.0, "Test 3 failed"
    print("✓ calculate_average: All tests passed")

def test_letter_grade():
    assert letter_grade(95) == "A", "Test 1 failed"
    assert letter_grade(85) == "B", "Test 2 failed"
    assert letter_grade(50) == "F", "Test 3 failed"
    print("✓ letter_grade: All tests passed")

if __name__ == "__main__":
    test_calculate_average()
    test_letter_grade()
```

#### Code Quality Checklist

**Function Quality**
- [ ] Every function has a clear, descriptive name (verb-noun: `calculate_average`, `get_user_input`)
- [ ] Every function has a docstring explaining what it does
- [ ] Every function does exactly one job (single responsibility)
- [ ] No function is longer than ~20–30 lines
- [ ] Functions have clear parameters and return values

**Error Handling**
- [ ] All `input()` calls handle non-numeric input with `try/except`
- [ ] File operations use `try/except` for IOError
- [ ] Division checks for zero
- [ ] List access checks length first or catches IndexError
- [ ] Data validation is done at the point of input

**Code Style**
- [ ] Consistent indentation (4 spaces)
- [ ] Blank lines between functions
- [ ] Module-level docstring at top of file
- [ ] No commented-out dead code
- [ ] Variables use snake_case, constants use UPPER_CASE
- [ ] Line length stays under 80 characters where practical

**Documentation**
- [ ] Module docstring explains the program's purpose
- [ ] Each function has a docstring with purpose, parameters, and return value
- [ ] Complex logic has inline comments explaining "why," not "what"
- [ ] README file explains how to run the program
- [ ] README includes usage examples

**Testing**
- [ ] Each function unit-tested individually
- [ ] Edge cases tested (empty, 0, max values, invalid input)
- [ ] Full program run-through on normal input
- [ ] Full program run-through on bad input (no crashes)
- [ ] Integration points verified (data flows correctly between functions)

---

## Project Ideas by Category

Choose one or create your own!

### Productivity Tools
- Grade tracker / GPA calculator
- Daily to-do list with file persistence
- Unit converter (length, weight, temperature, currency)
- Simple budget tracker with category breakdown
- Study schedule planner
- Book or movie rating tracker

### Games
- Number guessing game with difficulty levels
- Hangman with word list and difficulty
- Rock-Paper-Scissors with win/loss tracking and statistics
- Quiz bowl (read questions from file, track scores)
- Simple text adventure game
- Trivia game with timer and scoring

### Data Programs
- Weather data analyzer (read from CSV, calculate stats)
- Student grade report generator
- Word frequency counter / text analyzer
- Survey results processor with statistics
- Sales/inventory tracker
- Fitness log analyzer

### Utilities
- Password strength checker
- Contact book with file storage (save/load)
- Grocery list manager with price tracking
- Simple note-taking app with search
- File organizer (rename/move files based on patterns)
- Simple calculator with operation history

### Community/Creative
- Event scheduling system
- Simple chat/message logger
- Book club reading tracker
- Personal diary with date/search
- Recipe box with ingredient list
- Family budget planner

---

## Project Selection Criteria

When choosing your project, ensure it:

1. **Uses Core Skills:** Lists, dictionaries, loops, functions, file I/O, error handling, conditionals
2. **Has Clear Scope:** Can be completed in ~4 weeks without being trivial
3. **Has Testing Opportunities:** Has edge cases and validation needs
4. **Interests You:** You'll spend 35 days on this — pick something you care about!
5. **Has a Real User:** You should be able to imagine someone using this

---

## Development Milestones & Checkpoints

Track your progress through these key milestones:

### Milestone 1: Project Proposal (Day 147)
- [ ] Problem statement written and approved
- [ ] Audience identified
- [ ] Core features listed
- [ ] Function list sketched

### Milestone 2: Design Complete (Day 150)
- [ ] Pseudocode written
- [ ] Data structures designed
- [ ] UI flow documented
- [ ] Prototype plan outlined

### Milestone 3: Prototype Done (Day 155)
- [ ] Core MVP working
- [ ] Basic functions implemented
- [ ] Feedback from peers collected
- [ ] Plan for sprint 1 finalized

### Milestone 4: Sprint 1 Complete (Day 160)
- [ ] Core features fully implemented
- [ ] Code reviewed by peer
- [ ] All functions have docstrings
- [ ] Unit tests written and passing

### Milestone 5: Sprint 2 Complete (Day 165)
- [ ] Additional features working
- [ ] Error handling implemented
- [ ] File I/O working
- [ ] Code quality reviewed

### Milestone 6: Polish Complete (Day 170)
- [ ] All tests passing
- [ ] Code cleanup done (comments, naming, style)
- [ ] Edge cases handled
- [ ] User experience polished
- [ ] Feature freeze — no more new features

### Milestone 7: Ready to Present (Day 175)
- [ ] Documentation complete (README, user guide)
- [ ] Presentation ready
- [ ] Code walkthrough practiced
- [ ] Project submitted

### Milestone 8: Presentation Complete (Day 177)
- [ ] Project presented to class
- [ ] Feedback received
- [ ] Reflection completed

---

## Presentation Guidelines

### Structure of a 5–7 Minute Presentation

| Section | Time | What to Cover |
|---------|------|--------------|
| **Introduction** | 30 sec | Project title, problem it solves, who uses it |
| **Demo** | 2–3 min | Run it live — show normal use, then edge case |
| **Code Walkthrough** | 1.5–2 min | Explain 1–2 key functions (not line-by-line) |
| **Challenges & Solutions** | 45 sec | What was hardest? How did you solve it? |
| **Key Learnings** | 30 sec | What did you learn? |
| **Questions** | 1 min | Invite questions |

### Presentation Tips

**Do:**
- Open your code in an editor before you start
- Have test inputs written down and ready
- Speak to the audience, not the screen
- Say "when I enter X, the program does Y"
- Be ready to explain: "What if the user types nothing?"
- Show at least one edge case in your demo
- Pause and think — silence is okay
- Own your work and be proud of it

**Don't:**
- Read code line-by-line (explain the logic instead)
- Say "I didn't get to implement..." (focus on what works)
- Apologize for imperfections (every program has them)
- Rush through your explanation
- Wait until the last second to practice

### Sample Presentation Script

```
"Hi, I built Grade Tracker. The problem: keeping track of your
scores throughout the year is tedious, and calculating your
average by hand is error-prone. My program lets you enter
scores, automatically calculates your average and letter grade,
and saves a detailed report to a file.

Let me show you a demo. [Runs program] I'll enter three scores:
88, 92, 79. The program calculates the average as 86.3 and
assigns a B grade. Now watch what happens when I type 'hello'
instead of a number... [shows error handling] It catches the
error and asks again — no crash, no crash messages.

The most interesting part of the code is the get_scores()
function. It validates every input using try/except, so even if
the user types invalid data, the program handles it gracefully.
Here's the logic: [shows code] We loop until they type 'done',
and inside the loop, we try to convert their input to a float.
If it works AND it's between 0 and 100, we add it. If not, we
ask again.

The hardest part was file saving. I had to handle the case where
the file couldn't be written — maybe they don't have permission.
So I wrapped the file operations in try/except and give the user
a clear error message if something goes wrong.

What I'm most proud of is the error handling. This program won't
crash no matter what the user throws at it. I tested it with empty
input, invalid numbers, way-too-big numbers, all of it.

Any questions?"
```

### Presentation Prep Checklist
- [ ] Program runs without crashing on normal input
- [ ] I have specific inputs written down for my demo
- [ ] I can explain what each major function does
- [ ] I know what was hardest and how I solved it
- [ ] I've practiced saying my presentation out loud at least twice
- [ ] I'm ready for questions (practiced edge case responses)
- [ ] I have my code open in an editor and ready to show

---

## Common Development Pitfalls & How to Avoid Them

| Pitfall | Why It Happens | How to Avoid | Fix If It Happens |
|---------|---------------|-------------|------------------|
| Starting to code without planning | Excited to get started | Spend 30 min on proposal/design first | Stop, write pseudocode, refactor |
| Writing everything at once | Feels faster; avoids "wasted time" | Build one function, test it, repeat | Isolate functions, test individually |
| Never testing until the end | Testing feels like busywork | Test every function the moment it's written | Run unit tests now; debug piece by piece |
| Functions that do too much | No design phase, kept adding | Each function = one job, max ~20 lines | Extract logic into separate functions |
| No error handling | Forgot / didn't think about it | Every `input()` and `open()` needs protection | Add try/except blocks; validate inputs |
| Confusing variable names | Used `x`, `temp`, `stuff` | Name the data: `student_score`, `file_path` | Rename variables for clarity |
| Copy-pasting code instead of functions | Seems faster in the moment | If you copy-paste, extract it to a function | Refactor duplicated code |
| Giving up when stuck | Frustration; feeling lost | Debug systematically: print values, isolate | Add print statements; trace execution |
| Missing docstrings | Added last (or never) | Write docstrings as you write functions | Go back and add them before submission |
| Skipping edge cases | Seems like extra work | Always test: empty input, 0, huge numbers | Write test cases for edge cases |

---

## Helpful Debugging Strategies

### The Print Trace Method

When your code isn't working:

```python
def process_data(numbers):
    print(f"[DEBUG] Received numbers: {numbers}")
    total = 0
    for num in numbers:
        print(f"[DEBUG] Adding {num} to total")
        total += num
    print(f"[DEBUG] Final total: {total}")
    avg = total / len(numbers)
    print(f"[DEBUG] Average: {avg}")
    return avg

# Add prints at key points to trace execution
result = process_data([10, 20, 30])
```

### Systematic Debugging Checklist

1. **Read the error message carefully** — it usually tells you exactly what's wrong
2. **Identify the line number** where the error occurred
3. **Understand the type of error:**
   - `ValueError`: Type mismatch (can't convert string to int)
   - `IndexError`: Accessing list element that doesn't exist
   - `KeyError`: Accessing dictionary key that doesn't exist
   - `NameError`: Using variable that wasn't defined
   - `TypeError`: Wrong type for operation (adding string + number)
4. **Add print statements** to trace the variable values at that point
5. **Check your assumptions:** What did you think would happen? What actually happened?
6. **Test in isolation:** Does this function work on its own?
7. **Check the inputs:** Are they the type/value you expected?
8. **Ask a peer:** Sometimes explaining the problem to someone else reveals the fix

### Common Python Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `ValueError: invalid literal for int()` | Trying to convert non-numeric string to int | Check input with `try/except` or validate first |
| `IndexError: list index out of range` | Accessing list element beyond its length | Check list length before accessing; use `if index < len(list):` |
| `KeyError: 'key_name'` | Accessing dict key that doesn't exist | Check key exists first: `if 'key' in my_dict:` |
| `TypeError: unsupported operand type(s)` | Operating on incompatible types (e.g., `"5" + 5`) | Convert types: `int("5") + 5` |
| `NameError: name 'variable' is not defined` | Using variable before defining it | Define variable before using it |
| `FileNotFoundError` | Trying to open file that doesn't exist | Check file path, use try/except, create file if needed |

---

## Assessment Overview

Your final project will be assessed on a **100-point rubric** across five categories:

### Functionality (20 points)
- Does the program work as specified?
- Are all core features implemented and working?
- Does it handle edge cases and invalid input?

### Code Quality (20 points)
- Is the code well-organized and modular?
- Are variable names clear and descriptive?
- Do functions have docstrings?
- Is there error handling throughout?

### Testing & Debugging (20 points)
- Is the code tested thoroughly (unit and integration)?
- Are edge cases handled?
- Is the program stable and crash-resistant?

### Documentation (20 points)
- Is there a clear README?
- Are all functions documented?
- Is the code easy to understand and modify?

### Presentation & Communication (20 points)
- Is the presentation clear and organized?
- Can you explain your design choices?
- Do you demonstrate understanding of your own code?

See **UnitAssessment.md** for the detailed rubric.

---

## Weekly Schedule Overview

**Week 30 (Days 146–150): Planning & Proposal**
- Understand SDLC, write proposal, plan architecture, peer review

**Week 31 (Days 151–155): Design & Prototype**
- Design UI and data structures, build MVP, get feedback

**Week 32 (Days 156–160): Sprint 1 — Core Features**
- Implement core functionality, test, review, retrospective

**Week 33 (Days 161–165): Sprint 2 — Additional Features**
- Add features, error handling, file I/O, retrospective

**Week 34 (Days 166–170): Polish & Testing**
- Code cleanup, systematic testing, bug fixes, feature freeze

**Week 35 (Days 171–175): Documentation & Prep**
- Write documentation, practice presentation, submit

**Week 36 (Days 176–180): Presentations & Wrap-Up**
- Present to class, reflect on growth, celebrate

---

## Resources for Success

### In This Unit
- **Daily Notes:** See `Daily Notes/Day146.md` through `Day180.md`
- **Reference Guide:** See `ReferenceGuide.md` for templates and detailed guidance
- **Practice Problems:** See `UnitPractice.md` for 15 starter projects
- **Assessment Rubric:** See `UnitAssessment.md` for grading criteria

### External Resources
- Python Official Documentation: https://docs.python.org/3/
- Style Guide (PEP 8): https://www.python.org/dev/peps/pep-0008/
- Git for version control (optional): https://git-scm.com/

---

## Important Reminders

1. **Start with a plan.** Spending 30 minutes on design saves hours of debugging.
2. **Build incrementally.** Write one function, test it, move to the next.
3. **Test as you go.** Don't wait until the end to find bugs.
4. **Read error messages.** They are your friends—they tell you exactly what's wrong.
5. **Ask for help.** Peer review and collaboration make you better.
6. **Document as you go.** Writing docstrings while writing code is easier than adding them later.
7. **Own your work.** You learned a lot—be proud of what you built!

---

## What's Next?

After Coding I, you're ready for:

- **Coding II (Advanced Python):** OOP, data structures, algorithms
- **Data Science:** pandas, NumPy, Matplotlib, analysis
- **Web Development:** HTML/CSS, JavaScript, Flask/Django
- **Game Development:** pygame, game logic, graphics
- **Cybersecurity:** Networks, ethical hacking, system administration
- **Machine Learning:** scikit-learn, TensorFlow, AI applications
- **App Development:** Mobile apps, APIs, databases

---

## Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **SDLC** | Software Development Lifecycle: Define, Plan, Design, Code, Test, Present |
| **Pseudocode** | Logic written in plain English, not code syntax |
| **Specification** | Document describing inputs, outputs, and functions |
| **Bottom-up development** | Building helpers first, then connecting to main |
| **Unit testing** | Testing a single function in isolation |
| **Integration testing** | Testing how multiple functions work together |
| **Edge case** | Unusual input that might expose bugs (0, empty, max) |
| **Refactoring** | Improving code structure without changing behavior |
| **Single responsibility** | Each function does exactly one job |
| **Incremental development** | Building and testing small pieces at a time |
| **Bug** | An error causing incorrect behavior |
| **Debug** | The process of finding and fixing bugs |
| **Modular** | Code organized into small, reusable, single-purpose functions |
| **Code review** | Examining code for correctness, readability, and style |
| **Docstring** | Documentation string at the start of a function/module |
| **MVP** | Minimum Viable Product: core features only, no extras |
| **Sprint** | A focused development cycle (1–2 weeks) with a goal |
| **Retrospective** | Looking back on a sprint to identify what went well and what to improve |

---

**Congratulations on reaching Unit 7!** You've learned the foundations of programming. Now it's time to apply everything in a real project. Start with a plan, be patient with yourself, and remember: every professional programmer started where you are. You've got this!

*Keep building. Stay curious. Make cool stuff.*
