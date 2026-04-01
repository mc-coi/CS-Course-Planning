# Unit 7 - Capstone Project: Teacher Misconception & Callout Guide

## Overview

Unit 7 is not a traditional unit—it's where students apply everything they've learned to build a substantial, real project. The biggest challenges are project scope, time management, and the shift from "follow instructions" to "make decisions." Students will scope projects too large or too small, procrastinate until the final days, treat planning as "just write code," and struggle with debugging when multiple systems interact. They'll also hit unfamiliar errors, face unclear requirements, and have to troubleshoot problems without a pre-written solution. This unit teaches **professional software development**: planning, iterative building, testing, and presentation.

---

## Misconceptions by Topic

### Project Planning & Scope (Days 1–3)

**⚠️ Misconception:** "I know what I want to build. I'll start coding immediately."

**What it looks like:**
```
Day 1: Student starts coding without a plan
Day 5: They realize the data structure is wrong; refactors 50% of code
Day 15: They've built features but the core logic is fragile
Day 20: Desperate scramble to fix bugs before deadline
```

**Why students think this:** "I have the idea; coding will reveal the rest."

**How to address it:** Enforce **planning before coding**. Show that planning saves time.

```python
# Planning checklist (before writing a single line):
# 1. What is the project? (One sentence)
# 2. Who uses it? (Target user)
# 3. What are core features? (3–5 essential features)
# 4. What data do I need? (What will I store? From where?)
# 5. What's the architecture? (Classes? File structure? Data flow?)
# 6. How will I test it? (What scenarios?)

# Example: Weather Data Analyzer
# 1. What: A tool that fetches weather data and shows trends
# 2. Who: A user who wants to see if temperature is increasing
# 3. Features:
#    - Fetch weather for a city
#    - Store historical data
#    - Show average temperature over time
#    - Display a chart
# 4. Data: City name (input), temps + dates (stored in JSON)
# 5. Architecture:
#    class WeatherData:
#        def __init__(self, city)
#        def fetch_data(self)
#        def compute_trend(self)
#        def plot_trend(self)
# 6. Test: What if API fails? What if no data? What if city doesn't exist?

# With this plan, coding is straightforward!
```

Spend Days 1–3 on planning, not coding. Show that a solid plan cuts development time in half.

---

**⚠️ Misconception:** "I want to build something big and impressive. My project should have 20 features."

**What it looks like:**
```
Student's list:
- User authentication
- Database with 5 tables
- REST API with 50 endpoints
- Web interface
- Mobile app
- Admin dashboard
- Data visualization with 10 chart types
- Recommendation engine
- Real-time notifications
- 3 external APIs

Timeline: 25 days
Reality: Could take 25 weeks
```

**Why students think this:** Ambition + not understanding effort.

**How to address it:** Teach **ruthless prioritization**: MVP (Minimum Viable Product).

```python
# Scope framework: Must Have / Nice to Have / Probably Not

# Example: Student Information System
MUST_HAVE = [
    "Create student record (name, ID, GPA)",
    "Read student by ID or name",
    "Update student GPA",
    "Delete student record",
    "Save/load from JSON file",
    "List all students",
]

NICE_TO_HAVE = [
    "Sort students by GPA",
    "Search by partial name",
    "Calculate class average GPA",
    "Import CSV file",
]

PROBABLY_NOT = [
    "Web interface (too big)",
    "User authentication (scope creep)",
    "Email notifications (external API)",
    "Mobile app (separate project)",
]

# Effort estimation:
# MUST_HAVE: 10–12 days
# NICE_TO_HAVE: 5–7 days (pick 2 features)
# PROBABLY_NOT: Don't do these

# Final scope: MUST_HAVE + 2 NICE_TO_HAVE features = achievable in 25 days
```

Rule: "Build a small project well, not a big project badly. You'll have time for polish and extensions."

---

### Architecture & Code Organization (Days 4–6)

**⚠️ Misconception:** "I'll organize my code as I go. I'll refactor later if needed."

**What it looks like:**
```
Day 10: All code in one file (1000+ lines)
Day 15: Hard to find where to add features
Day 20: No time to refactor; submit messy code
```

**Why students think this:** "Getting it working is the priority."

**How to address it:** Establish **architecture Day 1**. Organize by feature/responsibility.

```python
# Good structure for a capstone project:

project_name/
├── main.py              # Entry point
├── data/
│   ├── __init__.py
│   └── loader.py        # Load/save data
├── models/
│   ├── __init__.py
│   └── student.py       # Student class
├── api/
│   ├── __init__.py
│   └── external.py      # API calls
├── ui/
│   ├── __init__.py
│   └── menu.py          # User interface
├── tests/
│   ├── __init__.py
│   ├── test_models.py
│   └── test_data.py
└── README.md

# Each file has ONE responsibility:
# - models.py: Define classes
# - data.py: Load/save files
# - api.py: External API calls
# - ui.py: User interaction
# - main.py: Tie it together

# Benefits:
# 1. Easy to find code
# 2. Easy to test (each module independently)
# 3. Easy to extend (add features without touching everything)
```

Show this structure Day 1. Enforce it throughout.

---

**⚠️ Misconception:** "I'll write all the code first, then test at the end."

**What it looks like:**
```
Day 20: First time running the full program
Day 20 12:00 PM: Multiple crashes
Day 20 11:59 PM: Still debugging
```

**Why students think this:** "Testing takes time; I'll skip it."

**How to address it:** Teach **incremental development**: Build one feature, test it, then add the next.

```python
# Development cycle (repeat for each feature):

# Day 1: Plan the feature
# "I want: Load student data from JSON file"
# - Read JSON
# - Parse list of dicts
# - Return Student objects
# - Handle missing file

# Day 2: Write the code
def load_students_from_json(filename):
    """Load students from JSON file."""
    try:
        with open(filename) as f:
            data = json.load(f)
        return [Student(**record) for record in data]
    except FileNotFoundError:
        return []

# Day 2: Test immediately
# Test cases to write:
# 1. File exists and has valid data → returns list of students
# 2. File doesn't exist → returns empty list
# 3. File has malformed JSON → handles gracefully
# 4. File has missing fields → handles gracefully

def test_load_students():
    # Test 1: Valid data
    students = load_students_from_json('test_data.json')
    assert len(students) == 3
    assert students[0].name == 'Alice'

    # Test 2: Missing file
    students = load_students_from_json('nonexistent.json')
    assert len(students) == 0

    # Test 3: Malformed JSON
    # (Create a test file with bad JSON)
    students = load_students_from_json('bad_data.json')
    assert isinstance(students, list)

test_load_students()  # Run immediately

# Now move on to the next feature, knowing this one works.
```

Build, test, move on. No surprises on Day 20.

---

### Handling Errors & Edge Cases (Days 7–12)

**⚠️ Misconception:** "Edge cases are rare. I'll handle the happy path first."

**What it looks like:**
```
Student's code:
age = int(input("Enter age: "))
category = age_to_category(age)

# Crashes if user enters "abc" (ValueError)
# Crashes if age is -5 (no validation)
# Crashes if CSV is missing a column (KeyError)
```

**Why students think this:** "Edge cases are details; the main logic matters."

**How to address it:** Show that edge cases are **not rare**; they're the difference between hobby code and production code.

```python
# Robust input handling:

def get_valid_age():
    """Get age from user with validation."""
    while True:
        try:
            age_str = input("Enter your age (0-150): ")
            age = int(age_str)

            if age < 0 or age > 150:
                print("Age must be between 0 and 150")
                continue

            return age
        except ValueError:
            print("Please enter a valid number")

# Test cases:
# 1. Valid age (25) → returns 25 ✓
# 2. Non-number input ("abc") → asks again ✓
# 3. Out-of-range (-5) → asks again ✓
# 4. Float input (25.5) → asks again ✓
# 5. Empty input ("") → asks again ✓

# Robust file handling:

def load_csv_safely(filename):
    """Load CSV with error handling."""
    try:
        with open(filename) as f:
            reader = csv.DictReader(f)
            records = list(reader)
    except FileNotFoundError:
        print(f"Error: File {filename} not found")
        return []
    except csv.Error as e:
        print(f"Error reading CSV: {e}")
        return []

    # Validate records
    valid_records = []
    for i, record in enumerate(records):
        if not all(key in record for key in ['name', 'age', 'gpa']):
            print(f"Warning: Row {i+1} missing required fields; skipping")
            continue
        try:
            record['age'] = int(record['age'])
            record['gpa'] = float(record['gpa'])
            valid_records.append(record)
        except ValueError:
            print(f"Warning: Row {i+1} has invalid types; skipping")

    return valid_records

# Test cases:
# 1. File doesn't exist → returns [], explains why
# 2. CSV is malformed → returns partial list, explains errors
# 3. Missing columns → skips bad rows, continues
# 4. Bad types (age="abc") → skips row, explains why
# 5. File is valid → returns all records
```

Students should write these test cases BEFORE handling errors. This drives the design.

---

### Feature Integration (Days 13–18)

**⚠️ Misconception:** "I built all the features separately. They'll work together automatically."

**What it looks like:**
```
Student built:
- Student class ✓
- Load/save JSON ✓
- Search function ✓
- Sort function ✓

Then integrated them:
student_list = load_students('data.json')
search_results = search(student_list, 'Alice')
sorted_results = sort(search_results)
# Error: sort() expects a list of ints, got a list of Student objects
```

**Why students think this:** They tested each part; assumption is they work together.

**How to address it:** Teach **integration testing**: Test features together.

```python
# Integration test: Load → Search → Sort

def test_full_workflow():
    """Test loading, searching, sorting together."""
    # Setup: Create test data
    test_students = [
        Student('Alice', 1, 3.9),
        Student('Bob', 2, 3.5),
        Student('Charlie', 3, 3.7),
    ]

    # Mock the load function to return test data
    def mock_load(filename):
        return test_students

    # Test the workflow
    students = mock_load('test.json')
    search_results = search(students, 'a')  # Should find Alice and Charlie
    assert len(search_results) == 2

    sorted_results = sort_by_gpa(search_results)
    assert sorted_results[0].gpa == 3.9  # Alice
    assert sorted_results[1].gpa == 3.7  # Charlie

test_full_workflow()
```

Integration tests catch **interface mismatches**: expecting list of ints when you get list of Student objects.

---

### Debugging & Problem-Solving (Days 14–20)

**⚠️ Misconception:** "When something breaks, I'll add print statements everywhere until I find the bug."

**What it looks like:**
```python
# Student's debugging approach:
def process_data(data):
    print("Starting process_data")
    result = transform(data)
    print("After transform:", result)
    for item in result:
        print("Processing:", item)
        item.update()
        print("After update:", item)
    print("Done")
    return result

# Output: 100 print statements, no useful information
```

**Why students think this:** Print is the first tool they learned.

**How to address it:** Teach **systematic debugging**:

```python
# Better approach: Hypothesis testing

# Symptom: student_list is empty when it shouldn't be

# Hypothesis 1: File doesn't exist
assert os.path.exists('data.json'), "File not found"

# Hypothesis 2: File is empty
with open('data.json') as f:
    content = f.read()
    assert len(content) > 0, "File is empty"

# Hypothesis 3: JSON parsing fails
import json
try:
    data = json.loads(content)
    print("JSON parsed successfully:", data)
except json.JSONDecodeError as e:
    raise AssertionError(f"JSON parsing failed: {e}")

# Hypothesis 4: Data structure is wrong
assert isinstance(data, list), f"Expected list, got {type(data)}"
assert len(data) > 0, "JSON is empty list"

# Hypothesis 5: Student object creation fails
try:
    students = [Student(**record) for record in data]
except Exception as e:
    raise AssertionError(f"Student creation failed: {e}")

# Now we've isolated the problem!
```

Teach the **scientific method**: Hypothesis → Test → Result.

---

**⚠️ Misconception:** "I debugged my code in Python. It works. But when someone runs it differently, it breaks."

**What it looks like:**
```
Student's computer:
- File: /Users/student/projects/capstone/data.json
- Code: open('data.json')  ✓ Works

Teacher's computer:
- File: Not found (wrong path)
- Error: FileNotFoundError

Issue: Hardcoded paths, machine-specific assumptions
```

**Why students think this:** "It works on my machine!"

**How to address it:** Teach **defensive coding for deployment**:

```python
# Avoid machine-specific assumptions

# BAD: Hardcoded path
data_file = '/Users/student/projects/capstone/data.json'

# BETTER: Relative to script location
import os
script_dir = os.path.dirname(os.path.abspath(__file__))
data_file = os.path.join(script_dir, 'data', 'data.json')

# BEST: Allow configuration
import os
from pathlib import Path

DATA_DIR = Path(__file__).parent / 'data'
data_file = DATA_DIR / 'data.json'

if not data_file.exists():
    raise FileNotFoundError(f"Data file not found: {data_file}")

# Also test on different machines:
# 1. Your computer
# 2. Teacher's computer (or at least different directory)
# 3. Different operating system (Windows vs. Mac vs. Linux)
```

Have students submit a test that runs on different paths.

---

### Presentation & Documentation (Days 21–24)

**⚠️ Misconception:** "Documentation and presentation are extras. The code speaks for itself."

**What it looks like:**
```
Student's submission:
- Code is complex and poorly commented
- No README
- No explanation of how to use it
- No discussion of design choices
- Presentation: "Um, I made a thing. It works."

Grade: C+ (it works, but no communication)
```

**Why students think this:** Code is the deliverable; documentation feels secondary.

**How to address it:** Teach that **communication is the deliverable**. Code is just evidence.

```python
# Good documentation structure:

# README.md
"""
# Weather Analyzer

## What is it?
A tool that fetches weather data and shows temperature trends.

## How to use it:
1. Install: pip install -r requirements.txt
2. Set up: Add API key to .env (see .env.example)
3. Run: python main.py
4. Enter city name when prompted

## Features:
- Fetch live weather data from OpenWeatherMap API
- Store historical data in data/weather.json
- Compute 7-day average temperature
- Generate trend plot (chart.png)

## Design decisions:
- Used JSON for storage (simple, human-readable)
- Used WeatherData class to encapsulate API calls
- Cached data locally to reduce API calls

## Limitations:
- Free API key has rate limits (60 calls/minute)
- Data only stored locally (not a database)
- Plotting is static (not interactive)

## Known issues:
- Slow on first run (API call takes 2-3 seconds)
- Doesn't handle network timeouts gracefully (future improvement)
"""

# Code comments:
def compute_trend(temperatures):
    """
    Compute temperature trend (linear fit).

    Args:
        temperatures (list): List of float temperatures

    Returns:
        tuple: (slope, intercept) of trend line
               Positive slope = warming trend
    """
    import numpy as np

    if len(temperatures) < 2:
        return 0, 0  # Can't compute trend with < 2 points

    x = np.arange(len(temperatures))
    y = np.array(temperatures)

    # Linear regression: y = mx + b
    coeffs = np.polyfit(x, y, 1)  # Degree 1 = linear
    return coeffs[0], coeffs[1]  # (slope, intercept)

# Presentation outline:
# 1. Problem: "Weather data is hard to visualize. My tool makes it easy."
# 2. Solution: "I built a tool that fetches, stores, and plots weather data."
# 3. Architecture: "The app has 3 parts: API client, data storage, visualization."
# 4. Demo: Show the tool running (actual video or live demo)
# 5. Challenges: "I struggled with API rate limits. I fixed it with caching."
# 6. Future work: "I'd like to add multi-city comparison and an interactive dashboard."
```

Documentation and presentation are **part of the grade**. Make it explicit.

---

## Whole-Class Warning Signs

- **Students haven't done any planning by Day 3** — they're behind. Enforce planning before code.
- **Student's project scope is obviously too big** — help them trim it. Better to finish 70% than 20%.
- **Code is all in one file; hard to navigate** — enforce file structure Day 1.
- **Student is debugging on Day 20 instead of testing all along** — emphasize incremental development.
- **Student hardcodes paths, API keys, or configuration** — teach environment variables and relative paths.
- **Integration test fails** — student didn't test features together. Catch this early.
- **No documentation or unclear how to run the code** — make README.md a requirement; grade it.
- **Presentation is apologetic ("I know it's not great")** — coach them to explain design decisions confidently.

---

## Questions That Reveal Understanding

1. **"Explain your project's architecture in 5 minutes."** (Answer: They should identify major components and explain how they connect. If they can't explain it, they don't understand their own design.)

2. **"Walk me through how data flows from input to output."** (Answer: Trace a complete user interaction. Shows they understand the integration.)

3. **"What was the hardest part of your project? How did you solve it?"** (Answer: Shows problem-solving, debugging skills, and resilience. Canned answers are a red flag.)

4. **"Show me a test that validates edge cases."** (Answer: They should have tests for missing files, bad input, etc. If they say "I didn't have time to test," they didn't prioritize correctly.)

5. **"What would you do differently if you were to rebuild this?"** (Answer: Shows reflection and learning. They should identify architectural improvements or features they'd add.)

6. **"Explain a design decision you made (e.g., why you used JSON instead of a database)."** (Answer: Should be thoughtful, not random. Shows they considered tradeoffs.)

7. **"How would you extend your project with a new feature?"** (Answer: They should explain where they'd add it in the architecture, what tests they'd write, etc. Shows code is extensible.)

---

## Common Student Questions & How to Answer Them

**Q: "Can I change my project idea mid-way?"**
A: "Only if necessary. If your original idea is truly infeasible, we can pivot, but you'll be behind. Better to scope down an ambitious idea than to switch. If you're thinking of switching, let's first talk about scaling back the current one."

---

**Q: "How much time should I spend on documentation?"**
A: "Documentation should be ~10% of your time. Write it as you go—don't leave it for the end. A good README takes 1 hour. Comments in code should be natural (1-2 lines per function). Don't over-document; assume the reader knows Python."

---

**Q: "My code works, but it's messy. Should I refactor?"**
A: "If you have time (Days 22–24), yes. If you're still fixing bugs, finish features first. A complete messy project scores higher than an incomplete clean project. That said, refactoring while coding (as you go) prevents the mess."

---

**Q: "I hit a bug I can't figure out. What should I do?"**
A: "Take a step back. Use systematic debugging: (1) Identify the symptom. (2) Form a hypothesis. (3) Test the hypothesis. (4) Repeat. Don't add random code or print statements everywhere. Also, ask for help—pair with a classmate or talk to me during office hours."

---

**Q: "I have too many features and won't finish. What do I do?"**
A: "Cut features immediately. Finish the MVP (core features) well, then add nice-to-haves. Submitting 70% complete with polish is better than 100% incomplete and broken. Pick 1–2 features to drop."

---

## Analogies That Work

**1. Project Planning as Blueprint:**
"Building a house without a blueprint is chaos—contractors rebuild walls, electrical rewiring, budget overruns. Software is the same. A good plan (architecture diagram, feature list, data model) saves massive rework."

---

**2. Testing as Safety Net:**
"Testing is a safety net for a trapeze artist. You can practice your routine fearlessly knowing you won't crash. Without tests, you're afraid to change anything."

---

**3. Documentation as a Letter to Your Future Self:**
"Write documentation for someone who knows Python but doesn't know your project—that person is you in 3 months. Be kind to future-you."

---

**4. Debugging as Detective Work:**
"Don't randomly sprinkle print statements like breadcrumbs hoping to find the criminal. Be systematic: form a hypothesis, test it, narrow the search. A detective gathers evidence methodically, not randomly."

---

**5. Integration as Connecting Puzzle Pieces:**
"You can build each puzzle piece perfectly, but they might not fit together. Integration is where you discover misaligned edges. Test pieces together early."

---

## Capstone Project Rubric Reminders

Remind students that they're graded on:

1. **Functionality (30%):** Does it work? Does it do what was planned?
2. **Code Quality (20%):** Is it clean, organized, and readable? Are there tests?
3. **Design (20%):** Is the architecture sound? Can you extend it?
4. **Documentation (15%):** Can someone else understand and run it? Is the README clear?
5. **Presentation (15%):** Can you explain your project clearly and confidently?

Missing one of these tanks the grade. A project that works but has no documentation loses 15% easy. Emphasize **balance**.

---

## Common Pitfalls & How to Avoid Them

| Pitfall | Symptom | Prevention |
|---------|---------|-----------|
| **Scope creep** | Adding features constantly; never finishing | Finalize MUST_HAVE list Day 1; say no to anything else |
| **No testing** | Debugging chaos on Day 20 | Test each feature before moving to next |
| **Hardcoded values** | Code breaks on teacher's machine | Use relative paths, environment variables, configs |
| **No documentation** | Presentation is "Um... it works?" | Write README as you go; practice presentation |
| **Monolithic code** | 1000-line file; impossible to debug | Organize by feature/responsibility Day 1 |
| **Ignoring edge cases** | Works on happy path; crashes on bad input | Write tests for missing files, bad input, etc. |
| **Skipping integration** | Parts work separately; fail together | Test features together; don't wait until Day 20 |
| **Procrastination** | Last 5 days are chaos | Incremental development; demo every 3 days |

---

## Helpful Milestones to Enforce

- **Day 3:** Planning complete. Architecture designed. No code yet.
- **Day 6:** File structure set up. Classes defined (empty methods). Tests written.
- **Day 9:** Core features working. Integration tests passing.
- **Day 12:** All features implemented. 80% of tests passing.
- **Day 15:** All tests passing. Code review / refactoring.
- **Day 18:** Documentation complete. README written. Demo ready.
- **Day 21:** Final polish. Performance optimization. Edge cases handled.
- **Day 24:** Presentation rehearsal. Final submission.

Regular checkpoints prevent last-minute disasters.

