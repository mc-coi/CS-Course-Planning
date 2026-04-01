# Unit 7 - Capstone Project: Teacher Misconception & Callout Guide

## Overview
Unit 7 is where everything from Units 1–6 comes together. The biggest teaching challenges are: (1) students underestimate project scope and panic halfway through, (2) they don't plan before coding and rewrite code multiple times, (3) they write monolithic "God" objects instead of designing proper architecture, (4) they skip testing and debugging, finding bugs too late, (5) they don't document code, making it hard to present, and (6) they think the capstone is *only* about coding when it's really about design, testing, and communication. This unit determines whether students can build *real* software or just scripts. Success here demonstrates mastery of the entire semester; failure reveals gaps from earlier units.

## Misconceptions by Topic

### Project Planning & Scope (Day 1)

**⚠️ Misconception:** "I can start coding immediately; planning is a waste of time."
**What it looks like in code:**
```python
# Student jumps in:
# "I'll make a task manager app"
# Starts coding without requirements, design, or user stories

# 3 days later:
# Realizes they forgot a core feature, architecture is a mess
# Rewrites everything
```
**Why students think this:** In Units 1–6, projects are small and well-defined.
**How to address it:** **Make planning non-negotiable.** "The bigger the project, the more planning matters. Spend Day 1 planning; you'll save days of rewrites later. The rule: if you think you know what you're building, you haven't planned enough."

Show the planning document template:
```
1. PROJECT VISION
   "A task manager app for students to track assignments and deadlines."

2. USER STORIES
   - As a student, I want to add tasks so I don't forget them
   - As a student, I want to see overdue tasks so I prioritize urgent work
   - As a student, I want to mark tasks complete so I track progress

3. SCOPE
   Must-Have:
   - Add/delete/view tasks
   - Save to file
   - Show overdue tasks

   Nice-to-Have:
   - Categories/priorities
   - Recurring tasks
   - Email reminders

   Out-of-Scope:
   - Mobile app
   - Real-time collaboration
   - AI scheduling

4. SUCCESS CRITERIA
   "The app can save 100 tasks, filter by due date, and persist across sessions."
```

---

**⚠️ Misconception:** "I should build every feature I can imagine."
**What it looks like in code:**
```python
# Student's Capstone Idea:
# "A full social network with:
#  - User accounts and authentication
#  - Direct messaging
#  - News feed with likes/comments
#  - Notifications
#  - Search and recommendations
#  - Mobile-responsive frontend"

# For a 2-week unit.
# Student burns out, delivers 20% of this, poorly.
```
**Why students think this:** Ambition is good; scope management is hard.
**How to address it:** **Teach the MVP (Minimum Viable Product) concept.** "Build the smallest useful version first. Get that working. Then add features. For a task manager:
- MVP: Add tasks, save to file, view tasks
- V2: Delete tasks, mark complete
- V3: Filter by priority
- V4: Recurring tasks
- ...

If you don't finish V4, you still have a working V3. Better than spending time on V4 and crashing before V3 is done."

Force scope discipline:
```
You have 6 days of implementation.
Estimate: 1 day per feature, plus 1 day for testing and bugs.
Features you can actually build: ~5

What are your 5 must-haves?
```

---

### Architecture & Design (Day 2)

**⚠️ Misconception:** "I can design architecture while coding. I don't need to plan classes upfront."
**What it looks like in code:**
```python
# Bad: Monolithic design
class App:
    def __init__(self):
        self.tasks = []
        self.users = []
        self.categories = []

    def add_task(self, task): ...
    def delete_task(self, task): ...
    def add_user(self, user): ...
    def authenticate_user(self, user): ...
    def save_to_file(self): ...
    def load_from_file(self): ...
    # ... 20 more methods
    # This class does EVERYTHING

# Good: Proper design
class Task:
    def __init__(self, name, due_date):
        self.name = name
        self.due_date = due_date

class TaskManager:
    def __init__(self):
        self.tasks = []

    def add_task(self, task): ...
    def delete_task(self, task): ...

class Storage:
    def save(self, tasks): ...
    def load(self): ...

class App:
    def __init__(self):
        self.manager = TaskManager()
        self.storage = Storage()

# Each class has ONE responsibility
```
**Why students think this:** They don't know about separation of concerns.
**How to address it:** **Teach the Single Responsibility Principle.** "Each class should do ONE thing:
- `Task`: Represents a task (data)
- `TaskManager`: Manages tasks (business logic)
- `Storage`: Saves/loads (I/O)
- `App`: Coordinates (main controller)

If a class does multiple things, refactor it. This makes code easier to test, debug, and extend."

Force design review before coding:
```
"Before you write a line of code, draw a class diagram.
What classes do you need?
What does each do?
How do they interact?"
```

Show the difference:
```python
# Bad: Monolithic
app = App()
app.add_task(...)
app.save_to_file()
# App does too much

# Good: Clean separation
manager = TaskManager()
manager.add_task(...)
storage = Storage()
storage.save(manager.tasks)
# Each class has one job
```

---

**⚠️ Misconception:** "I should use inheritance for everything to avoid code duplication."
**What it looks like in code:**
```python
# Over-engineered:
class Entity:
    def __init__(self, id, created_at):
        self.id = id
        self.created_at = created_at

class Task(Entity):
    def __init__(self, id, created_at, name):
        super().__init__(id, created_at)
        self.name = name

class User(Entity):
    def __init__(self, id, created_at, username):
        super().__init__(id, created_at)
        self.username = username

# For a small project, this is overkill
# Use inheritance when you have 3+ classes with shared behavior
```
**Why students think this:** They learned inheritance in Unit 2 and want to use it.
**How to address it:** **Teach the "three times rule."** "Only create a base class after you have three or more classes with shared code. For a small capstone, inheritance is rarely needed. Use composition or just duplicate a little code—it's okay."

Keep it simple:
```python
# Simple (good for small projects):
class Task:
    def __init__(self, name, due_date):
        self.name = name
        self.due_date = due_date

class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

# No inheritance needed; each is independent
```

---

### Implementation Phase 1 — Core Features (Day 3)

**⚠️ Misconception:** "I should implement everything perfectly the first time."
**What it looks like in code:**
```python
# Student tries to be perfect:
# Spends 8 hours polishing the add_task() method
# - Validation
# - Error messages
# - Logging
# - Input sanitization
# - ...

# By end of day, only one feature is done
# Runs out of time, delivers incomplete project
```
**Why students think this:** They've been taught to write quality code.
**How to address it:** **Teach "rough first, polish later."** "Get features working first, even if rough. Refine later. A half-finished feature is worth nothing; a rough feature that works is worth a lot."

Set a rule:
```
"Day 3-4: Get core features working.
"Don't worry about edge cases, error handling, or perfect style."
"Make it work first."

Day 5: Polish and test.
```

Show the progress curve:
```
Day 1: Plan
Day 2: Design
Day 3-4: Implement (rough)
Day 5: Test, debug, refine
Day 6: Documentation, presentation
```

---

**⚠️ Misconception:** "I don't need to test as I code; I'll test at the end."
**What it looks like in code:**
```python
# Student implements for days without testing
# Day 5: "Let me test this"
# Discovers: crashes, logic errors, missing features
# Doesn't have time to fix

# Better: test after each feature
```
**Why students think this:** Testing feels like extra work.
**How to address it:** **Make testing part of implementation.** "After you write a feature, test it immediately. This catches bugs early. Testing at the end is too late—you don't have time to fix major issues."

Simple testing workflow:
```python
# Implement a feature
def add_task(self, name, due_date):
    task = Task(name, due_date)
    self.tasks.append(task)
    return task

# Test it immediately
manager = TaskManager()
task = manager.add_task("Study", "2024-12-31")
assert task.name == "Study"
assert len(manager.tasks) == 1
print("✓ add_task works")

# Then move to the next feature
```

---

### Implementation Phase 2 — Features & Polish (Day 4)

**⚠️ Misconception:** "I can test my code by just running it and looking at the output."
**What it looks like in code:**
```python
# Weak testing:
app = App()
app.add_task("Task 1")
app.add_task("Task 2")
print(app.tasks)
# Output: [<Task object>, <Task object>]
# "Looks good!"

# But edge cases aren't tested:
# - Empty task name? (crashes)
# - Past due date? (invalid)
# - Duplicate tasks? (unclear behavior)
```
**Why students think this:** Visual output feels like verification.
**How to address it:** **Show the power of systematic testing.** "Write test cases for normal and edge cases:
```python
def test_add_task():
    manager = TaskManager()

    # Normal case
    task = manager.add_task("Buy groceries", "2024-12-25")
    assert len(manager.tasks) == 1

    # Edge case: empty name
    with raises(ValueError):
        manager.add_task("", "2024-12-25")

    # Edge case: past date
    with raises(ValueError):
        manager.add_task("Old task", "2000-01-01")

    print("✓ All tests pass")

test_add_task()
```

Test everything systematically, not just happy paths."

---

**⚠️ Misconception:** "Refactoring is a waste of time; my code works."
**What it looks like in code:**
```python
# Working but messy:
def save_tasks():
    # 50 lines of code doing multiple things
    # - Validation
    # - File I/O
    # - Error handling
    # - Logging
    # Hard to understand, hard to test

# Refactored:
def validate_tasks(tasks):
    # 10 lines, one job

def write_file(filename, data):
    # 10 lines, one job

def save_tasks():
    # 5 lines, orchestrates validation and writing
```
**Why students think this:** They have limited time.
**How to address it:** **Show that refactoring saves time in the long run.** "Messy code is hard to debug and extend. You spend hours fixing bugs in tangled code. Clean code is quick to understand and fix. Spend 30 minutes refactoring; save 3 hours debugging later."

Simple refactoring rule: "If a function is >20 lines or does 2+ things, break it up."

---

### Testing & Debugging (Day 5)

**⚠️ Misconception:** "If my code doesn't crash, it works correctly."
**What it looks like in code:**
```python
# Code that runs but produces wrong results:
def calculate_grade(scores):
    return sum(scores) / len(scores)  # Works for normal lists

# But edge case: empty list
result = calculate_grade([])  # ZeroDivisionError!

# Or: returns wrong answer silently
def find_highest_scorer(students):
    best = students[0]
    for student in students:
        if student.grade > best.grade:
            best = student
        # Missing: update best!
    return best  # Returns first student always!
```
**Why students think this:** It runs without crashing.
**How to address it:** **Distinguish between "works" and "correct."** "Code can run without crashing but produce wrong answers. Test the *output*, not just that it doesn't crash."

```python
def test_calculate_grade():
    # Normal case
    assert calculate_grade([90, 80, 100]) == 90

    # Edge case: empty list
    with raises(ValueError):
        calculate_grade([])  # Should raise, not crash silently

    # Edge case: single score
    assert calculate_grade([95]) == 95

test_calculate_grade()
```

---

**⚠️ Misconception:** "Debugging means adding print() statements everywhere."
**What it looks like in code:**
```python
# Poor debugging:
def add_task(self, name):
    print(f"Adding task: {name}")
    task = Task(name)
    print(f"Task created: {task}")
    self.tasks.append(task)
    print(f"Tasks list: {self.tasks}")
    return task
    print("Task added")  # Unreachable!

# Better: use a debugger or systematic logic
```
**Why students think this:** Print statements are simple.
**How to address it:** **Teach logical debugging.** "Print statements help, but better: understand the code flow, write tests, and use a debugger (Python has `pdb`). Systematic debugging finds root causes faster than random printing."

Show the approach:
```python
# 1. Understand what SHOULD happen
# add_task should: create Task, add to list, return Task

# 2. Write a test
def test_add_task():
    m = TaskManager()
    t = m.add_task("Study")
    assert t.name == "Study"
    assert len(m.tasks) == 1

# 3. Run the test; see where it fails
# 4. Inspect that part of the code
# 5. Fix the bug

# Use `assert` statements to verify assumptions:
def add_task(self, name):
    assert name, "Name cannot be empty"
    task = Task(name)
    assert task.name == name, "Task name not set"
    self.tasks.append(task)
    assert task in self.tasks, "Task not added to list"
    return task
```

---

### Documentation & Presentation (Day 6)

**⚠️ Misconception:** "Documentation is optional if the code is 'self-explanatory.'"
**What it looks like in code:**
```python
# No documentation:
def proc(d):
    r = []
    for k, v in d.items():
        if v > 50:
            r.append((k, v))
    return r

# Two weeks later, what does this do? No idea!
```
**Why students think this:** They assume code is obvious.
**How to address it:** **Require documentation before submission.** "Code is read 10x more than written. Document so others (and future you) understand. Every project module needs:
1. Module-level docstring (what does this module do?)
2. Function/method docstrings (what does this do? what are inputs/outputs?)
3. Complex logic gets comments

```python
# Good documentation
\"\"\"
module: task_manager.py
Handles task creation, storage, and retrieval.
\"\"\"

def filter_high_priority(tasks):
    \"\"\"
    Return tasks with priority >= 8.

    Args:
        tasks (list): List of Task objects

    Returns:
        list: Filtered tasks, sorted by due date

    Raises:
        TypeError: If tasks is not a list
    \"\"\"
    if not isinstance(tasks, list):
        raise TypeError("tasks must be a list")

    filtered = [t for t in tasks if t.priority >= 8]
    return sorted(filtered, key=lambda t: t.due_date)
```

---

**⚠️ Misconception:** "I should present my code in the capstone demo."
**What it looks like in code:**
```python
# Student shows:
# "Here's my main.py"
# [Scrolls through 200 lines of code]
# "Um, this is where I add tasks... and here's where I save..."
# Audience asleep.

# Better: show the APP, not the code
```
**Why students think this:** They spent days coding; they want credit for it.
**How to address it:** **Teach presentation vs. demo.** "Your presentation should show *what* the app does, not *how* it works. Demonstrate features, not code. Unless they ask 'how does this work?', don't show code."

Presentation structure:
```
1. Problem: "Students forget assignments."
2. Solution: "My task manager app."
3. Features:
   - Add and track tasks ✓
   - Set due dates and priorities ✓
   - Filter overdue tasks ✓
4. Demo: [Use the app]
5. Technical:
   - Built with Python, uses OOP and file I/O
   - ~500 lines of code in 5 classes
6. Challenges: [What was hard?]
7. Future: [What would you add?]
```

---

## Whole-Class Warning Signs

- Students starting to code immediately without planning
- Monolithic "God" classes that do everything
- No tests until the last day; many bugs discovered too late
- Code with no documentation; student can't explain their own code
- Halfway through, realizing scope is too large, panic
- Features half-finished when time runs out
- Demo shows code instead of the running app
- No version control; can't recover from mistakes
- Presentation is "Here's my code" instead of "Here's what my app does"
- Students complaining that the project is too hard (usually due to poor planning)

---

## Questions That Reveal Understanding

1. **"Explain your project's architecture. What classes do you have and what does each do?"**
   - Good answer: Clear separation of concerns. Each class has one responsibility. Diagram or list.
   - Red flag: "I have one big class that does everything" or can't explain the design.

2. **"How did you test your code? What test cases did you write?"**
   - Good answer: "I tested normal cases, edge cases, and error conditions. I write tests after each feature."
   - Red flag: "I just ran it and looked at the output" or "I didn't have time to test."

3. **"Walk me through the most challenging part of your project. How did you solve it?"**
   - Good answer: Clear explanation of the problem and the solution. Shows problem-solving.
   - Red flag: "I don't remember" or vague explanation.

4. **"If you had more time, what would you add to your project?"**
   - Good answer: Specific features, clear priority, understand why they didn't fit in scope.
   - Red flag: "I don't know" or unrealistic ideas.

5. **"Show me your code. Can you explain what this function does?"**
   - Good answer: Clear explanation, good variable names, documented, easy to follow.
   - Red flag: Poor variable names (`x`, `temp`, `thing`), no comments, convoluted logic.

6. **"How did you manage your time? What did you do Day 1, Day 2, etc.?"**
   - Good answer: Plan, design, implement, test, polish. Structured and intentional.
   - Red flag: "I just started coding" or "I ran out of time."

---

## Common Student Questions & How to Answer Them

**Q: "I have too many ideas. How do I pick a project?"**
A: "Pick one that solves a real problem you have—doesn't have to be huge. A simple project done well is better than an ambitious project half-finished. Ask: 'What's the smallest useful version?' Start there."

**Q: "How much documentation is enough?"**
A: "Every public function/method gets a docstring (one sentence + inputs/outputs). Complex sections get comments. Don't document obvious code (`x = x + 1` doesn't need a comment). Aim for 10-20% of your code to be documentation."

**Q: "Should I use OOP or just functions?"**
A: "If you have 2+ classes with attributes and methods, use OOP. If it's just functions, that's fine. Don't force OOP; use it when it makes sense."

**Q: "My code works but it's messy. Should I refactor?"**
A: "If it works and time is running out, ship it. If you have time, refactor—clean code is easier to debug. Priority: working code > clean code > perfect code."

**Q: "I found a bug two days before the deadline. Should I try to fix it?"**
A: "Depends: is it a showstopper? If the app crashes, fix it. If it's cosmetic, leave it and document it in the presentation: 'Known issue: [...]. Here's why: [...].' Honesty is better than panic."

---

## Analogies That Work

1. **Planning as "Building Blueprints"**
   "You wouldn't build a house without a blueprint. You'd run out of materials, miss structural issues, waste time. A project blueprint (design doc) saves you days of rework."

2. **Separation of Concerns as "Dividing Responsibilities"**
   "A restaurant has a chef, a server, a cashier. Each does their job. A monolithic class is one person doing everything—messy and slow. Separate concerns, separate classes."

3. **Testing as "Trying Before Selling"**
   "Before you sell a car, you test it. You don't wait until a customer drives it off a cliff to discover brakes don't work. Test as you build."

4. **Refactoring as "Reorganizing Your Room"**
   "A messy room works (stuff is there) but it's hard to find things. Organizing takes time but makes life easier. Code refactoring is similar."

5. **Documentation as "Leaving Notes for Yourself"**
   "You'll forget what your code does. Leave notes (docstrings, comments) so future you understands. It's a gift to your future self."

---

## Coding 1 Gaps to Watch For

**Gap: No experience with large projects**
- **What it looks like:** Students underestimate scope, don't plan, panic halfway through.
- **Quick patch:** Force planning. Make them write a 1-page design doc before coding starts.

**Gap: Poor problem-solving and debugging skills**
- **What it looks like:** Students get stuck, restart, waste time.
- **Quick patch:** Teach systematic debugging: write tests, use assertions, understand the problem before fixing.

**Gap: Weak communication and presentation skills**
- **What it looks like:** Students can't explain their code or demo it clearly.
- **Quick patch:** Have them present in class before the final. Give feedback on clarity and demo.

---

## Critical Misconceptions to Stop for (vs. Handle 1-on-1)

**STOP for:**
- **Starting to code without planning** — This leads to chaos. Make planning Day 1.
- **No testing** — Bugs discovered at the end are catastrophic. Test as you code.
- **Monolithic "God" classes** — This makes code unmaintainable. Require design review.

**Handle 1-on-1:**
- Struggling with a specific feature — help them debug logically.
- Unsure about refactoring — help them identify what to refactor.
- Presentation anxiety — help them practice, focus on the app not the code.

---

## Grading Rubric (Guidance)

Consider these categories:

**Planning & Design (20%)**
- Clear requirements and user stories
- Sensible architecture with proper separation of concerns
- Evidence of upfront design (diagram or design doc)

**Implementation (30%)**
- Core features work correctly
- Code is reasonably clean and readable
- Appropriate use of OOP, data structures, and algorithms from Units 1–6

**Testing & Debugging (20%)**
- Evidence of testing (test cases written, bugs found and fixed)
- Edge cases handled
- No major crashes or data loss

**Documentation (15%)**
- Code has docstrings for functions/classes
- README explains how to use the app
- Comments for complex logic
- Student can explain their code

**Presentation (15%)**
- Demo shows app working
- Student explains problem, solution, and challenges
- Clear communication
- Honest about limitations

---

## Final Note for Teachers

Unit 7 isn't just about code—it's about *software engineering*. Students learn:
- How to plan before coding
- How to design systems
- How to test systematically
- How to document and communicate
- How to deliver on a deadline

These skills matter more than perfect code. A rough but well-planned app beats a beautiful but disorganized mess.

**Your role is to guide without solving.** Don't let them code themselves into a corner, but don't do the thinking for them. Ask questions:
- "What's your MVP?"
- "How will you test this?"
- "Can you explain this class?"
- "What's your biggest risk?"

Push them to think like engineers, not just coders. The capstone is their chance to show they can build real software. Make it count.

By the end of Unit 7, students should deliver a **complete, working, documented project** that demonstrates mastery of the entire semester. That's the goal.
