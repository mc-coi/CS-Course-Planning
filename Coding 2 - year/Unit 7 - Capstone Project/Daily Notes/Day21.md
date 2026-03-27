# Day 21: Final Polish & Submission Preparation

**Session Goal:** Final touches, ensure everything is ready for presentation.

---

## Today's Focus

You have working code and documentation. Today is about final polish—double-checking everything, creating sample data, and getting ready to present. By end of day, you should feel confident and excited about showing your work.

---

## Work Session Agenda

**Minutes 0-5:** **Final Checklist Review**
- Teacher: what will graders / evaluators look for?
- Students: review submission requirements
- Q&A about presentation format and expectations

**Minutes 5-50:** **Final Polish & Preparation**

1. **Code final check** (5 min)
   - Run app one more time
   - Verify no errors, crashes, or strange behavior
   - Check: all features work as intended

2. **Sample data creation** (10 min)
   - Create example data files students/evaluators can use
   - Example: `data/sample_students.json` with 5–10 records
   - Makes it easy to demo your app

3. **Presentation prep** (15 min)
   - Create a demo script or outline (see below)
   - Plan what you'll show: features, design, process
   - Prepare backup plan if something crashes

4. **Final code review** (10 min)
   - Scan code one more time for typos, dead code
   - Verify all files are included in submission
   - Check: no hardcoded passwords, API keys, or personal info

5. **Submission verification** (5 min)
   - File list created (all code, README, data samples)
   - Everything saved and committed
   - Final commit message clear

**Minutes 50-55:** **Celebration & Readiness**
- You've built something real!
- Rest of sprint: deliver presentations

---

## Sample Data Creation

Create realistic example data for your project:

**For Student System:** `data/sample_students.json`
```json
[
    {
        "name": "Alice Smith",
        "student_id": 1001,
        "gpa": 3.85,
        "courses": ["Math 101", "Physics 201", "English 101"]
    },
    {
        "name": "Bob Johnson",
        "student_id": 1002,
        "gpa": 3.45,
        "courses": ["Math 101", "Chemistry 201"]
    },
    {
        "name": "Carol White",
        "student_id": 1003,
        "gpa": 3.92,
        "courses": ["Physics 201", "English 101", "History 101"]
    }
]
```

**For Data Analyzer:** `data/sample_weather.csv`
```csv
date,temperature,humidity,condition
2024-01-01,45,60,Cloudy
2024-01-02,48,55,Sunny
2024-01-03,42,75,Rainy
2024-01-04,50,50,Sunny
```

**For API App:** Add a `SETUP.md` with API key instructions and cached sample responses

---

## Demo Script

Write down what you'll demo and in what order:

```
DEMO SCRIPT: Student Information System

[Approx. 5-7 minutes]

1. INTRO (30 sec)
   "I built a student information system that lets you manage student
    records with search, sort, and persistent storage."

2. STARTUP (30 sec)
   [Run: python main.py]
   "The app starts with an empty list and shows a menu."

3. ADD FEATURE (1 min)
   [Pick: 1]
   [Add Alice Smith, ID 1001, GPA 3.85]
   "Here I'm adding a student. The app validates input—if I tried
    to enter a GPA > 4.0, it would reject it."

4. ADD MORE (30 sec)
   [Add 1-2 more students]

5. SEARCH FEATURE (1 min)
   [Pick: 3]
   [Search for "alice"]
   "Now I'll search for Alice. The search is case-insensitive and
    supports partial matches."

6. SORT FEATURE (30 sec)
   [Pick: 4]
   "Sort by GPA shows students highest to lowest."

7. SAVE & LOAD (1 min)
   [Pick: 5, exit]
   [Show students.json created]
   [Restart app, loads students automatically]
   "When I exit, the data saves to JSON. When I restart, it loads
    automatically."

8. ARCHITECTURE (1 min)
   [Show code structure]
   "The code uses OOP: Student class for individual records,
    StudentSystem class for managing collections. File I/O uses
    JSON for persistence."

9. Q&A (remaining time)
   "Any questions?"
```

---

## Pre-Presentation Checklist

- [ ] App runs without errors from fresh start
- [ ] All features work as expected
- [ ] Sample data files created
- [ ] Demo script written and practiced
- [ ] Code is clean (no debug prints, dead code)
- [ ] README is comprehensive
- [ ] All files are saved and committed
- [ ] Know how long your demo takes (target: 5–7 min)
- [ ] Have a backup plan if something crashes (e.g., "Let me show you the code instead")

---

## What Graders Will Look For

Be aware:

1. **Does it work?** — App runs, features function (Functionality)
2. **Is the code well-written?** — Clear names, good design (Quality)
3. **Is it documented?** — README, docstrings, comments (Documentation)
4. **Is it tested?** — Works in normal and edge cases (Testing)
5. **Can you explain it?** — You understand your code (Presentation)

Your grade depends on ALL of these, not just "did it work."

---

## Handling Presentation Nerves

Normal to feel anxious. Remember:

- You've spent 3 weeks on this. You know it better than anyone.
- Everyone is supportive—classmates want to hear about your project.
- If something crashes during demo, it's okay: "Let me show you the code instead."
- You're not being judged as a person; just on the work you did.

---

## Reflection / Exit Ticket

1. What are you most proud of in your capstone?
2. What would you do differently if you could start over?
3. How ready do you feel to present?

---

## Progress Checklist

- [ ] Final code review completed
- [ ] Sample data created
- [ ] Demo script written and practiced
- [ ] All files organized and ready for submission
- [ ] README and documentation finalized
- [ ] Backup plan prepared (if demo fails)
- [ ] Ready to present on Days 23-24
