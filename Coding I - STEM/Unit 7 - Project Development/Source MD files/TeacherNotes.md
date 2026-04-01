# Unit 7 - Project Development: Teacher Misconception & Callout Guide

## Overview
Unit 7 is the capstone—where students apply everything they've learned (conditionals, loops, functions, file I/O, debugging) to build a real application. The biggest misconceptions here are **structural** rather than syntactic: (1) students don't plan before coding (they jump in), (2) they write monolithic functions instead of modular ones, (3) they test only happy paths, and (4) they don't document their work or think about maintainability. Unlike earlier units, this unit's failure modes aren't error messages—they're broken designs, incomplete features, and unmaintainable code. This unit rewards **systematic thinking**: problem definition, design, incremental development, and testing. The grade here largely reflects how well students followed the software development process, not just whether code "works." Emphasize planning and design over raw coding speed.

---

## Misconceptions by Topic

### Project Planning & Problem Definition (Days 1)

**⚠️ Misconception:** "Planning is a waste of time; I should just start coding."

**What it looks like in code:**
```python
# Student jumps straight to writing code without a plan
# 30 minutes later: "Wait, what am I trying to do?"
# 2 hours later: "My code is a mess and I don't know how to fix it"
```

**Why students think this:** Coding feels productive; planning feels slow.

**How to address it:** Emphasize: "Code written without a plan is always slower. You'll rewrite it, debug it, and spend hours untangling it. A clear plan takes 20 minutes and saves hours of coding. Professional programmers spend 30% of time planning, 70% executing." Require a written project proposal **before** any coding:
- Problem statement (one sentence)
- Inputs and outputs
- List of functions
- Test cases
- Data structures needed

**STEM priority:** Critical—determines success.

**⚠️ Misconception:** "My project is too simple / too complicated for planning; planning is only for big projects."

**What it looks like in code:**
```python
# Student either:
# A) thinks a simple project doesn't need planning
# B) thinks a complex project is too hard to plan
# Both lead to chaos
```

**Why students think this:** They don't see the value of planning at any scale.

**How to address it:** Clarify: "All programs need planning, regardless of size. Simple ones need simple plans (one page). Complex ones need detailed plans (multiple pages). A plan is your roadmap—without it, you're driving blind." Provide a planning template that scales.

**STEM priority:** Critical—all projects need planning.

**⚠️ Misconception:** "My design is perfect; I don't need to change it once I start coding."

**What it looks like in code:**
```python
# Student designs: "Get input, process, output"
# Starts coding, discovers they need validation
# Realizes the design didn't account for error cases
# Tries to retrofit; it's messy
```

**Why students think this:** They see the plan as fixed.

**How to address it:** Explain: "Plans are flexible. As you code, you'll learn things. If the design doesn't work, update it. The plan is guidance, not a prison. Changing the plan when you discover something is smart, not a failure." Teach the iterative process.

**STEM priority:** Medium—design thinking.

---

### Modular Function Design (Days 1–2)

**⚠️ Misconception:** "I should write one big `main()` function that does everything."

**What it looks like in code:**
```python
def main():
    # Get input
    name = input("Name: ")
    scores = []
    while True:
        s = input("Score: ")
        if s.lower() == "done":
            break
        scores.append(int(s))

    # Calculate
    avg = sum(scores) / len(scores)
    if avg >= 90:
        grade = "A"
    # ... 50 more lines

    # Output
    print(f"{name}: {grade}")

    with open("results.txt", "a") as f:
        f.write(f"{name}: {grade}\n")

main()
```

**Why students think this:** One function feels simpler than multiple.

**How to address it:** Teach: "Big functions are hard to test and understand. Break them into smaller functions, each doing one thing. It looks like more code, but each function is simpler and reusable." Show the modular version:
```python
def get_student_name():
    return input("Name: ").strip()

def get_scores():
    scores = []
    while True:
        s = input("Score (or 'done'): ").strip()
        if s.lower() == "done":
            break
        try:
            scores.append(int(s))
        except ValueError:
            print("Please enter a number")
    return scores

def calculate_average(scores):
    return sum(scores) / len(scores) if scores else 0

def get_grade(average):
    if average >= 90: return "A"
    elif average >= 80: return "B"
    # ...
    return "F"

def save_result(name, grade):
    with open("results.txt", "a") as f:
        f.write(f"{name}: {grade}\n")

def main():
    name = get_student_name()
    scores = get_scores()
    avg = calculate_average(scores)
    grade = get_grade(avg)
    print(f"{name}: {grade}")
    save_result(name, grade)

main()
```

**STEM priority:** Critical—modularity is the key skill.

**⚠️ Misconception:** "My functions should modify global variables instead of returning values."

**What it looks like in code:**
```python
scores = []              # Global

def get_scores():
    global scores        # Modifying global
    while True:
        # ... add to scores list
    # No return

# vs. the better way:
def get_scores():
    scores = []
    while True:
        # ... add to scores
    return scores        # Return the value

scores = get_scores()
```

**Why students think this:** Globals feel like a shortcut.

**How to address it:** Warn: "Avoid global variables in functions. Pass data through parameters and return results. This makes functions testable and independent. If every function modifies globals, your code is a tangled mess." Show the difference in testability:
```python
# Hard to test (relies on global state)
scores = []
def add_score(score):
    global scores
    scores.append(score)

# Easy to test (pure function)
def add_score(scores, score):
    return scores + [score]  # or scores.append(score); return scores

scores = add_score(scores, 85)
```

**STEM priority:** Critical—good design practice.

---

### Incremental Development & Testing (Days 2–3)

**⚠️ Misconception:** "I should write all the code first, then test it."

**What it looks like in code:**
```python
# Student writes 100 lines of code
# Then tries to run it
# 20 errors pop up
# No idea where they're coming from or how to fix them
```

**Why students think this:** They see "writing code" and "testing" as separate phases.

**How to address it:** Teach: "Develop incrementally. Write a small piece, test it, move to the next. If each piece works, the whole program works. You catch bugs early when they're easy to fix." Show the process:
1. Write function 1 → Test it alone
2. Write function 2 → Test it alone
3. Integrate functions 1 & 2 → Test together
4. Repeat

Say: "Build the foundation, then add layers. Each layer works before adding the next."

**STEM priority:** Critical—methodology.

**⚠️ Misconception:** "Testing means running the code once and seeing if it works."

**What it looks like in code:**
```python
# Student runs their program once with one input
# It works (happy path)
# They declare it done
# But edge cases break it
```

**Why students think this:** They don't know what comprehensive testing looks like.

**How to address it:** Teach: "Good testing covers happy paths and edge cases. Test with empty input, invalid input, boundary values, very large input. Write test cases before coding (or as you code). Here's a testing template:"
```python
def test_calculate_average():
    assert calculate_average([80, 90, 100]) == 90.0, "Normal case"
    assert calculate_average([]) == 0.0, "Empty list"
    assert calculate_average([50]) == 50.0, "Single value"
    assert calculate_average([0, 0, 0]) == 0.0, "All zeros"
    print("All tests passed!")

test_calculate_average()
```

**STEM priority:** Critical—comprehensive testing.

**⚠️ Misconception:** "If my code runs without errors, it's done."

**What it looks like in code:**
```python
# Program runs, produces output, no crashes
# But: output is wrong, features are missing, edge cases fail
# Student says: "It works!"
```

**Why students think this:** They confuse "runs" with "correct."

**How to address it:** Clarify: "No crashes is table stakes. Correct means it produces the right output for all inputs. Compare your output to expected output. Test edge cases. Make sure all features work." Provide a testing checklist.

**STEM priority:** Critical—correctness matters.

---

### Error Handling & Robustness (Days 2–3)

**⚠️ Misconception:** "Error handling is optional; I'll add it if I have time."

**What it looks like in code:**
```python
# Program crashes if user enters unexpected input
score = int(input("Score: "))  # If user enters "abc", crash!

# Program crashes if file doesn't exist
with open("data.txt") as f:    # If file missing, crash!
    content = f.read()
```

**Why students think this:** They see the "happy path" as the default.

**How to address it:** Teach: "Professional code handles errors gracefully. Users **will** enter unexpected input and files **will** go missing. Plan for it from the start." Make error handling a standard part of the design:
```python
def get_score():
    while True:
        try:
            score = int(input("Score (0-100): "))
            if 0 <= score <= 100:
                return score
            print("Must be 0-100")
        except ValueError:
            print("Please enter a number")

def load_data(filename):
    try:
        with open(filename) as f:
            return f.read()
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
```

**STEM priority:** Critical—professional practice.

**⚠️ Misconception:** "I should catch errors but not tell the user what went wrong."

**What it looks like in code:**
```python
try:
    score = int(input("Score: "))
except ValueError:
    pass                        # Silent failure—user is confused

# Better:
except ValueError:
    print("Please enter a number")
```

**Why students think this:** They don't understand user feedback is part of error handling.

**How to address it:** Teach: "When you catch an error, tell the user clearly what went wrong and what they should do. Silence confuses them. Make error messages helpful." Show examples:
```python
# BAD: silent failure
except ValueError:
    pass

# GOOD: inform user
except ValueError:
    print("Please enter a valid number")

# GREAT: guide user
except ValueError:
    print("Invalid input. Please enter a number between 0 and 100")
```

**STEM priority:** Medium—user experience design.

---

### Documentation & Code Quality (Days 3–4)

**⚠️ Misconception:** "Documentation is for when I'm done; I'll add it at the end."

**What it looks like in code:**
```python
# Student writes code for a week
# Promises to add comments and docstrings
# Never gets around to it
# Code is delivered undocumented
```

**Why students think this:** Documentation feels like busywork.

**How to address it:** Teach: "Document as you code. Add docstrings right after defining functions. Add inline comments for non-obvious logic. This ensures documentation exists and reflects your current thinking." Make it a grade requirement: "20% of your grade is documentation."

**STEM priority:** Critical—documentation is deliverable.

**⚠️ Misconception:** "Comments should explain what the code does, line by line."

**What it looks like in code:**
```python
# BAD: repeating code
x = 5
# Set x to 5
for i in range(x):
    # Loop i from 0 to x-1
    print(i)
    # Print i
```

**Why students think this:** They've seen bad comments and copied the style.

**How to address it:** Teach: "Comments explain **why**, not what. The code shows what. A good comment answers: Why did you write it this way? What assumption are you making?" Show good examples:
```python
# GOOD: explains intent
PENALTY_THRESHOLD = 5
# Penalize users if they fail more than 5 times (based on user research)
for i in range(threshold):
    # ...
```

**STEM priority:** Low—style, but improves code quality.

**⚠️ Misconception:** "My code works; it's good enough."

**What it looks like in code:**
```python
# Working but:
# - Variable names unclear (x, temp, data)
# - Functions do too much
# - No docstrings
# - Magic numbers (5, 100) without explanation
# - Repeated code (copy-pasted)
```

**Why students think this:** They conflate "works" with "quality."

**How to address it:** Teach: "Code has two readers: the computer and humans (future you, teammates). Make it readable. Use clear variable names, small functions, docstrings, no copy-paste. Code that works but is unreadable is actually broken." Provide a code quality checklist:
- [ ] Variable names are clear
- [ ] Functions are small (< 20 lines)
- [ ] Docstrings explain purpose, parameters, return
- [ ] No repeated code (DRY: Don't Repeat Yourself)
- [ ] No magic numbers
- [ ] Comments explain non-obvious logic
- [ ] Tests cover happy path and edge cases

**STEM priority:** Medium—professional practice.

---

### Presentation & Reflection (Days 5–6)

**⚠️ Misconception:** "Presentation is separate from coding; it's just talking about the code."

**What it looks like in code:**
```python
# Student finishes code but hasn't thought about how to explain it
# Presents awkwardly, can't articulate design decisions
```

**Why students think this:** They separate "doing" from "explaining."

**How to address it:** Teach: "Presentation is part of the project. Plan it as you design. Be ready to explain: What problem does it solve? What's your design? Why did you make those choices? What would you do differently? How did you test it?" Require a demo + 2-minute walkthrough.

**STEM priority:** Medium—communication skill.

**⚠️ Misconception:** "Reflection is busywork; I should focus on the code."

**What it looks like in code:**
```python
# Student finishes project and moves on
# Doesn't think about what they learned or would do differently
```

**Why students think this:** Reflection doesn't produce code.

**How to address it:** Teach: "Reflection is how you grow. Ask yourself: What worked well? What was hard? What would I do differently? What did I learn?" Make reflection required:
- Write a 1-page reflection after finishing
- Include: successes, challenges, lessons, improvements

**STEM priority:** Medium—metacognitive skill.

---

## Whole-Class Warning Signs

- **Students starting to code before planning** — Stop them. Require a written plan first. Make it a checkpoint.
- **Monolithic main() function** — Insist on breaking it into smaller functions. Teach the "one sentence" rule.
- **No error handling** — Crash on invalid input. Require try/except for user input and file operations.
- **No testing; only happy path works** — Teach edge case testing. Require test cases in the design.
- **Undocumented code** — Missing docstrings, comments, README. Make documentation 20% of the grade.
- **Code that works by accident** — No clear design, copied/modified examples without understanding. Push them to explain it.
- **Presentation lacks clarity** — Can't explain design decisions. Practice the explanation beforehand.

---

## Questions That Reveal Understanding

1. **"Describe your project in one sentence. What problem does it solve?"**
   - Good answer: Clear, concise, specific. Example: "A grade tracker that lets teachers record student scores and generates reports."
   - What it reveals: Do they understand the core purpose?

2. **"Walk me through your design. What functions do you have? What does each do?"**
   - Good answer: Lists functions with clear purposes. Example: `get_scores()` collects input, `calculate_average()` computes the mean, `save_to_file()` writes output.
   - What it reveals: Is the design modular? Can they explain it?

3. **"What edge cases did you test? Show me one test case."**
   - Good answer: Lists edge cases (empty input, zero, large numbers, invalid input) and shows how they tested them.
   - What it reveals: Do they think about robustness? Did they test systematically?

4. **"If I enter invalid input, what happens? Does your program crash?"**
   - Good answer: "No, it catches the error and asks me to try again." (Shows try/except)
   - What it reveals: Did they handle errors?

5. **"Read me the docstring for your main function. What does it say?"**
   - Good answer: Clear explanation of what the function does, with parameter and return info if applicable.
   - What it reveals: Did they document their code?

6. **"What would you do differently if you built this again?"**
   - Good answer: Reflective. Example: "I'd plan more upfront to avoid rewriting. I'd make functions smaller. I'd test more edge cases."
   - What it reveals: Did they reflect? Did they learn?

---

## Common Student Questions & How to Answer Them

**Q: "I don't know where to start. How do I begin?"**
A: "Start with planning, not coding. Write: (1) What problem are you solving? (2) What data do you need? (3) What are the main steps? (4) What functions will you need? Answer these first. Then start with the simplest function and test it. Build up from there."

**Q: "Should I make one big function or many small ones?"**
A: "Many small ones. Each function should do one thing. If you can describe it in one sentence without saying 'and', it's probably the right size. Small functions are easier to test and reuse."

**Q: "How much error handling do I need?"**
A: "Anywhere a user provides input or you interact with files. Always wrap user input in try/except. Always handle FileNotFoundError. Always validate input before using it."

**Q: "Do I have to comment every line?"**
A: "No! Comment the non-obvious stuff. Explain why you did something, not what you did. Most code is self-explanatory if variable names are clear. One good comment per function is often enough."

**Q: "How do I know if my code is good?"**
A: "Check: Does it work (all features)? Does it handle errors? Is it readable (clear names, small functions)? Is it documented? Can you explain your design choices? If yes to all, it's good."

---

## Analogies That Work

**1. Planning as a Blueprint:**
"Before building a house, you draw blueprints. You don't just start laying bricks. A project blueprint (design document) saves you from building the wrong thing. It takes 20 minutes to draw, saves hours of rebuilding."

**2. Modular Functions as Building Blocks:**
"Build your program like Legos. Each block (function) has one job. You test each block, then click them together. If one breaks, you replace just that block, not the whole structure."

**3. Testing as Quality Assurance:**
"Testing is like checking a car before it leaves the factory. You don't just turn it on and drive. You test the brakes, lights, engine, doors, edge cases. Only after all tests pass does it ship to customers."

---

## STEM-Specific Notes

**Pacing:** Unit 7 is 6 days / 2 weeks. This is tight for a full project. Use the time wisely:
- **Day 1 (Planning & Design):** Checkpoint. Require written plan before coding.
- **Days 2–3 (Development Session 1 & 2):** Build & test incrementally.
- **Days 4–5 (Refinement & Documentation):** Polish code, add docs, test edge cases.
- **Day 6 (Presentation):** Demo and walkthrough.

**Grading Rubric (Suggested):**
- Design & Planning: 20%
- Code Quality & Modularity: 20%
- Functionality (Features Work): 20%
- Testing & Error Handling: 15%
- Documentation: 15%
- Presentation & Explanation: 10%

This weighting values design and process over raw features. A well-designed, fully documented, thoroughly tested program with simpler features beats a feature-rich but chaotic program.

**Acceleration Path:** For advanced students, add constraints or extensions:
- Implement a feature using a design pattern (e.g., factory, strategy)
- Build a GUI (using tkinter or similar)
- Extend the project with additional features
- Refactor for performance or scalability

**Support Path:** Provide templates and scaffolding:
- Planning template
- Function signature template
- Testing template
- Documentation template

Provide check-ins: Plan (Day 1), Progress (Day 3), Polish (Day 5). Early feedback prevents last-minute disasters.

---
