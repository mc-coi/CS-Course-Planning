# Day 13: Sprint 2 Check-In – Peer Code Review

**Session Goal:** Review your code with a peer; give and receive constructive feedback on design and implementation.

---

## Today's Focus

Professional developers review each other's code before it ships. Today you'll do the same. You'll learn from seeing how peers solved problems, and they'll give you feedback on your work. This isn't about finding mistakes—it's about improving together.

---

## Work Session Agenda

**Minutes 0-10:** **Introduction to Code Review**
- Teacher: what is code review? (quality gate, learning opportunity, not criticism)
- Review guidelines: be kind, be specific, ask questions
- How to read code: follow the logic, understand the design, look for clarity

**Minutes 10-50:** **Peer Code Review Pairs (20 min per pair)**
- Pair up with another student (can be different project)
- Reviewer #1 reviews Reviewer #2's code using the **Code Review Form** (below)
- Then swap: Reviewer #2 reviews Reviewer #1's code
- Both fill out forms and discuss

**Minutes 50-55:** **Debrief & Reflection**
- Share: What did you learn from your peer's code?
- Discuss: What will you change based on feedback?
- Teacher: key takeaways

---

## Code Review Form

**Reviewer Name:** ________________
**Developer Name:** ________________
**Project:** ________________
**Date:** ________________

### Code Overview
1. In 2–3 sentences, what does this project do?

### Strengths
What are 3 things this code does well?
- [e.g., "Clear function names", "Good error handling", "Well-organized file structure"]
-
-

### Questions
List 2–3 things you don't understand or want to know more about:
- Q1:
- Q2:
- Q3:

### Suggestions for Improvement
List 2–3 specific suggestions. Be constructive:
- Suggestion 1: [Why: ...] (What: ... How: ...)
- Suggestion 2:
- Suggestion 3:

### One Compliment
Give one specific, genuine compliment about the code or the project:


---

## Code Review Tips for Reviewers

**Do:**
- Ask questions if you don't understand something
- Point out things you like
- Give specific examples: "The `load_from_json()` function is really clean because..."
- Suggest one way to improve, not 10

**Don't:**
- Judge the person; critique the code
- Say "this is wrong"—say "I'm not sure what this does"
- Suggest major rewrites if a small tweak works
- Focus on style preferences (tabs vs. spaces)

**Questions to ask:**
- Why did you use a list here instead of a dictionary?
- What happens if the user enters invalid data?
- How do you handle missing files?
- Can you walk me through this function?

---

## Code Review Checklist (for Reviewer)

As you review, check:

- [ ] **Functionality** — Does the code do what it claims?
- [ ] **Readability** — Can I understand it without asking?
- [ ] **Documentation** — Are functions documented?
- [ ] **Error Handling** — What happens if things go wrong?
- [ ] **Design** — Is the code organized logically?
- [ ] **Testing** — Have they tested edge cases?

---

## Developer Tips: Receiving Feedback

- **Listen** without defending. Feedback is a gift.
- **Ask clarifying questions.** "Can you show me an example?"
- **Say thank you.** Even if you disagree, someone spent time helping.
- **Don't change everything.** Use feedback wisely; you own your code.
- **Note it.** Write down feedback; decide later what to apply.

---

## Example Code Review Feedback

**Developer's Code:**
```python
def add_student(self, n, i, g):
    s = Student(n, i, g)
    self.students.append(s)
```

**Reviewer's Comments:**
```
Q: Why do you use single-letter variable names here? (n, i, g, s)

Suggestion: Use full names for clarity. Example:
def add_student(self, name, student_id, gpa):
    student = Student(name, student_id, gpa)
    self.students.append(student)

This makes it easier to understand at a glance.
Also: what happens if student_id is negative? Should you validate?
```

---

## After Code Review

1. Thank your reviewer
2. Note feedback you want to apply
3. Decide: will you change anything before Sprint 3?
4. Plan improvements for Days 14–16

---

## Reflection / Exit Ticket

1. What was one piece of feedback that surprised you?
2. What was one thing you liked about your peer's code?
3. What change will you make based on feedback?

---

## Progress Checklist

- [ ] Peer code review completed
- [ ] Code Review Form filled out and received
- [ ] Feedback discussed with peer
- [ ] Key improvements identified for Sprint 3
