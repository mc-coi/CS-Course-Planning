# Unit 7: Capstone Project Assessment
> Complete grading rubrics, evaluation forms, self-assessment, and teacher guidance for the capstone.

---

## Table of Contents
1. [Project Rubric](#project-rubric)
2. [Presentation Rubric](#presentation-rubric)
3. [Student Self-Assessment](#student-self-assessment)
4. [Peer Evaluation](#peer-evaluation-form)
5. [Teacher Grading Guide](#teacher-grading-guide)
6. [Grade Calculation](#grade-calculation)

---

## Project Rubric

**Total: 100 points**

### Category 1: Code Functionality (25 points)

**What this measures:** Does the app work? Are all required features implemented and functional?

| Score | Criteria |
|-------|----------|
| **25** | All required features work perfectly. No crashes. Edge cases handled gracefully. |
| **20** | All required features work. Minor bugs or edge case issues (non-breaking). |
| **15** | Most required features work. Some bugs or missing features. |
| **10** | Some features missing or broken. App crashes in some scenarios. |
| **5** | Major features missing or non-functional. |
| **0** | App does not run or no features work. |

**Teacher Notes:**
- Run the app yourself; try to break it
- Test with sample data and edge cases
- Does it handle errors gracefully or crash?
- Are all 5 core features from the plan implemented?

---

### Category 2: Code Quality & Design (25 points)

**What this measures:** Is the code well-organized, readable, and properly structured using OOP/functions?

| Score | Criteria |
|-------|----------|
| **25** | Excellent OOP design with clear classes/functions. No code duplication. Strong error handling. Variable names are clear and consistent. |
| **20** | Good OOP design. Minor code duplication. Adequate error handling. Variable names mostly clear. |
| **15** | Fair OOP design. Some code duplication. Basic error handling. Some unclear variable names. |
| **10** | Poor design. Minimal OOP structure. Weak error handling. Many unclear variable names. |
| **5** | Very poor design. Little organization. Almost no error handling. |
| **0** | No meaningful code structure. |

**Teacher Notes:**
- Read through the code (not just run it)
- Does it use OOP? Are classes well-designed?
- Is there code duplicated that should be in a function?
- Are variable/function names clear? (e.g., `student` vs. `s`)
- Is error handling present? (try/except, input validation)

---

### Category 3: Documentation & Comments (15 points)

**What this measures:** Is the code documented? Can someone understand it from README and comments?

| Score | Criteria |
|-------|----------|
| **15** | Comprehensive README. Every function has a docstring explaining purpose, args, and returns. Comments explain complex logic and "why" decisions. |
| **12** | Good README. Most functions have docstrings. Adequate comments on complex sections. |
| **9** | Adequate README. Some functions have docstrings. Basic comments. |
| **6** | Poor README. Few docstrings. Minimal comments. |
| **3** | Almost no documentation. |
| **0** | No documentation. |

**Teacher Notes:**
- README should explain: project purpose, how to run, features, project structure, known issues
- Every function needs a docstring with purpose and args
- Complex logic should have inline comments
- Check for dead code or debug print statements to remove

---

### Category 4: Testing & Edge Cases (15 points)

**What this measures:** Has the student tested their app? Do they handle edge cases and errors?

| Score | Criteria |
|-------|----------|
| **15** | Comprehensive testing evident. App handles errors gracefully. Edge cases tested (empty data, invalid input, missing files). |
| **12** | Good testing. Most errors handled. Some edge cases tested. |
| **9** | Basic testing done. Some error handling. Limited edge case coverage. |
| **6** | Minimal testing. Basic error handling. Few edge cases considered. |
| **3** | Very little testing evident. |
| **0** | No evidence of testing. |

**Teacher Notes:**
- Look for try/except blocks around file I/O and user input
- Does app validate input (e.g., GPA 0-4.0)?
- Does it handle missing files, empty lists, invalid data?
- Student should be able to describe their testing approach

---

### Category 5: Presentation (10 points)

**What this measures:** Can the student present their work clearly and answer questions about it?

| Score | Criteria |
|-------|----------|
| **10** | Clear, engaging presentation. Explains code and design decisions. Answers questions confidently. Good pace and communication. |
| **8** | Clear presentation. Explains features and process. Handles most questions well. |
| **6** | Adequate presentation. Some explanation. Answers some questions. |
| **4** | Unclear or rushed presentation. Little explanation. Struggles to answer questions. |
| **2** | Very unclear presentation. Cannot explain code. |
| **0** | No presentation or unintelligible. |

**Teacher Notes:**
- Does the student understand their own code?
- Can they explain design choices?
- Are they confident or defensive when questioned?
- Did they practice the demo?

---

## Presentation Rubric

**Used for Days 23–24 presentations. Total: 50 points**

| Category | Excellent (10) | Good (8) | Adequate (6) | Needs Work (4) | Poor (2) |
|----------|---|---|---|---|---|
| **Clarity** | Crystal clear what project does; easy to follow | Mostly clear; some steps unclear | Somewhat unclear; requires attention to understand | Confusing; hard to follow | Very unclear; confusing throughout |
| **Demo Quality** | App works perfectly; features shown smoothly | App works; minor glitches | App mostly works; some bugs visible | Several issues; some features don't work | App crashes or won't run |
| **Communication** | Speaks clearly, good pace, engages audience | Generally clear; mostly good pace | Adequate clarity; some pacing issues | Often mumbles or too fast/slow | Inaudible or extremely unclear |
| **Understanding** | Clearly understands code; explains design | Good understanding; explains most features | Basic understanding; can explain some features | Limited understanding; vague explanations | Cannot explain code |
| **Time Management** | Perfect pacing; 5–7 minutes; complete demo | Good pacing; near 5–7 minutes | Acceptable timing; slightly over/under | Poor timing; too long or too short | Severely over/under time |

**Total Presentation Score:** Sum of 5 categories (scale 0–50 points)

---

## Student Self-Assessment

**Student Name:** ________________
**Project:** ________________
**Date:** ________________

### Part 1: Functionality

1. **List your 5 core features. Did you implement all of them?**
   - [ ] Feature 1
   - [ ] Feature 2
   - [ ] Feature 3
   - [ ] Feature 4
   - [ ] Feature 5

   All completed: ☐ Yes ☐ Partially ☐ No

2. **Did you test your app? Describe your testing:**
   ________________

3. **What edge cases did you handle?** (e.g., empty data, invalid input)
   ________________

4. **Are there any known bugs or limitations?**
   ________________

### Part 2: Code Quality

5. **Does your code use OOP (classes)? Describe your class structure:**
   ________________

6. **Is your code well-organized? Explain:**
   ________________

7. **Do you have docstrings and comments? Estimate coverage:**
   ☐ 100% ☐ 75–90% ☐ 50–75% ☐ <50% ☐ None

### Part 3: Process & Learning

8. **What was the hardest part of this capstone?**
   ________________

9. **How did you solve that challenge?**
   ________________

10. **What did you learn about software development?**
    ________________

11. **What would you do differently if you did this project again?**
    ________________

### Part 4: Self-Rating

**Rate yourself honestly on a scale of 1–5:**

| Aspect | 1 (Weak) | 2 | 3 (OK) | 4 | 5 (Excellent) |
|--------|----------|---|--------|---|---|
| **Code Functionality** | ☐ | ☐ | ☐ | ☐ | ☐ |
| **Code Quality** | ☐ | ☐ | ☐ | ☐ | ☐ |
| **Documentation** | ☐ | ☐ | ☐ | ☐ | ☐ |
| **Testing & Debugging** | ☐ | ☐ | ☐ | ☐ | ☐ |
| **Presentation** | ☐ | ☐ | ☐ | ☐ | ☐ |
| **Overall Capstone** | ☐ | ☐ | ☐ | ☐ | ☐ |

12. **What grade do you think you deserve, and why?**
    ________________

---

## Peer Evaluation Form

**Evaluator Name:** ________________
**Project Evaluated:** ________________
**Date:** ________________

### Part 1: What You Observed

1. **In 2–3 sentences, what does this project do?**
   ________________

2. **List the features you saw demonstrated:**
   - [ ]
   - [ ]
   - [ ]

3. **Did the app work during the demo?**
   ☐ Yes, all features worked
   ☐ Mostly worked
   ☐ Some features didn't work
   ☐ Crashed or wouldn't run

### Part 2: Strengths

4. **What 3 things did this project do well?**
   1. ________________
   2. ________________
   3. ________________

5. **What was impressive or creative about this project?**
   ________________

### Part 3: Constructive Feedback

6. **What 2 things could be improved?**
   1. ________________
   2. ________________

7. **Do you have any questions about the code or design?**
   ________________

8. **One suggestion for a future enhancement:**
   ________________

### Part 4: Overall Assessment

9. **On a scale of 1–5, how ready is this app for actual use?**
   ☐ 1 (Not ready) ☐ 2 ☐ 3 (OK) ☐ 4 ☐ 5 (Very ready)

10. **One genuine compliment about the project:**
    ________________

---

## Teacher Grading Guide

### Before Grading

- [ ] Student submitted all required files (code, README, sample data)
- [ ] Code runs without critical errors
- [ ] Student completed presentation
- [ ] Self-assessment and peer feedback collected

### Grading Checklist (25 points: Functionality)

**Test the app yourself:**
- [ ] App starts and runs without immediate crashes
- [ ] All 5 core features from plan are implemented
- [ ] Features work correctly (no major bugs)
- [ ] Data persists (save/load works)
- [ ] Error handling present (doesn't crash on bad input)
- [ ] Edge cases handled (empty data, invalid input)

**Questions to answer:**
- Can the student's app be used as intended?
- Are there any critical bugs?
- Does it handle errors gracefully?
- Would you trust this software?

---

### Grading Checklist (25 points: Code Quality)

**Read the code:**
- [ ] Classes are well-designed (not just functions in a class)
- [ ] No significant code duplication
- [ ] Variable names are clear (not `s`, `x`, `thing`)
- [ ] Functions have single, clear purposes
- [ ] Error handling present (try/except, validation)
- [ ] File I/O is safe (doesn't crash if file missing)

**Questions to answer:**
- Is the code organized logically?
- Could another programmer understand it easily?
- Does it follow good OOP design?
- Are there anti-patterns (e.g., global variables, huge functions)?

---

### Grading Checklist (15 points: Documentation)

**Check README:**
- [ ] Explains what project does
- [ ] Has installation/setup instructions
- [ ] Lists features
- [ ] Shows project structure
- [ ] Acknowledges known issues

**Check code:**
- [ ] All functions have docstrings
- [ ] Docstrings explain purpose, args, returns
- [ ] Complex logic has comments
- [ ] No debug print statements left
- [ ] No dead/unused code

---

### Grading Checklist (15 points: Testing)

**From presentation and conversation:**
- [ ] Student describes testing approach
- [ ] App handles invalid input gracefully
- [ ] Edge cases covered (empty, large datasets, etc.)
- [ ] Student aware of limitations

**By observation:**
- [ ] Try to break the app; does it recover?
- [ ] Error messages are helpful
- [ ] No unexpected crashes

---

### Grading Checklist (10 points: Presentation)

**During presentation:**
- [ ] Clear explanation of project
- [ ] Demo runs smoothly (or student handles issues well)
- [ ] Answers questions confidently
- [ ] Shows understanding of code
- [ ] Good pacing and communication

**Questions to ask:**
- "Why did you design it this way?"
- "What was your biggest challenge?"
- "How did you test this feature?"
- "If you had more time, what would you add?"

---

### Common Grading Scenarios

**Scenario: App works but code is messy**
- Functionality: 25/25
- Code Quality: 15/25 (deduct for unclear names, duplication)
- Overall: Still strong if documented and tested

**Scenario: Code is excellent but app has bugs**
- Functionality: 15/25 (deduct for bugs)
- Code Quality: 25/25
- Overall: Decent; address why testing was missed

**Scenario: Student doesn't present**
- Presentation: 0/10
- Subtract 10 from overall grade
- Note: soft policy acceptable? Discuss with student

**Scenario: Excellent project but student can't explain it**
- Project components: Full points
- Presentation: 4–6/10
- Consider: Did student do the work, or did someone else?
- Action: Ask deeper questions; verify understanding

---

## Grade Calculation

### Method 1: Rubric Points (Recommended)

**Total: 100 points**

1. Code Functionality: _______ / 25
2. Code Quality: _______ / 25
3. Documentation: _______ / 15
4. Testing: _______ / 15
5. Presentation: _______ / 10

**Total Score: _______ / 100**

**Letter Grade:**
- 90–100: A (excellent)
- 80–89: B (good)
- 70–79: C (satisfactory)
- 60–69: D (needs improvement)
- <60: F (incomplete)

### Method 2: Rubric + Presentation Separate

**Project Score:**
- Functionality: _______ / 25
- Code Quality: _______ / 25
- Documentation: _______ / 15
- Testing: _______ / 15
- **Subtotal: _______ / 80**

**Presentation Score:**
- (From presentation rubric): _______ / 50

**Combined: _______ / 130**
- Convert to /100: Multiply by (100/130) ≈ 0.77

---

## Grading Notes & Comments

Use this space to record qualitative feedback for the student:

**Student Name:** ________________
**Project:** ________________

**Strengths:**
- Feature that stood out: ________________
- Good design choice: ________________
- Impressive problem-solving: ________________

**Areas for Growth:**
- Code organization could improve by: ________________
- Testing approach: ________________
- Communication during presentation: ________________

**Specific Feedback:**
________________

**Next Steps (if student wants to continue):**
- Could enhance by: ________________
- Could refactor: ________________

**Overall Assessment:**
This student has demonstrated ________________. They will ______________. Grade: ___ / 100

---

## Final Grade Summary

| Category | Points | Grade |
|----------|--------|-------|
| Functionality | ___/25 | |
| Code Quality | ___/25 | |
| Documentation | ___/15 | |
| Testing | ___/15 | |
| Presentation | ___/10 | |
| **TOTAL** | **___/100** | **___** |

---

## Teacher Reflection

After grading all capstones:

1. **Overall Class Performance:** What was the average grade? Were there surprises?

2. **Strongest Projects:** Which project(s) stood out? Why?

3. **Common Issues:** What problems did multiple students face?

4. **Growth Observed:** How much did students improve from Day 1 to Day 25?

5. **Next Time:** What would you change about the capstone unit?

---

**Remember: The capstone is about growth, not perfection. Recognize effort, persistence, and learning. Every student who completes a capstone has achieved something real.**
