# Unit 7 Assessment Prep — Capstone Project

**Review Questions:** Answer these to prepare for your final project and course reflection.

1. What are the five phases of the software development life cycle?
2. What is a user story? Write one example for a to-do list app.
3. What does "refactoring" mean, and why is it important?
4. What is the difference between a unit test and an integration test?
5. Why should you write documentation as you code rather than at the end?
6. What is a docstring? Write one for a function that calculates a student's GPA.
7. Describe the MVC (Model-View-Controller) pattern in your own words.
8. Why should you validate user input, and how do you do it in Python?
9. What makes code "readable"? List at least four practices.
10. Explain how you would present a technical project to a non-technical audience.

---

**Answers:**

1. Planning → Implementation → Testing → Refactoring → Documentation (and Presentation).
2. A user story describes a feature from the user's perspective. Example: "As a student, I want to add tasks to a list so I can track what I need to complete."
3. Refactoring means improving the structure of code without changing what it does — removing duplication, renaming variables for clarity, breaking large functions into smaller ones.
4. A unit test checks a single function or class in isolation; an integration test checks how multiple components work together.
5. Writing documentation as you code is faster and more accurate — you remember the intent immediately. Documentation written later is often incomplete or incorrect.
6. A docstring is a string literal at the start of a function that explains what it does.
```python
def calculate_gpa(grades):
    """
    Calculate a student's GPA from a list of grade points.

    Args:
        grades (list): List of numeric grade points (0.0-4.0)
    Returns:
        float: Average GPA rounded to 2 decimal places
    """
    return round(sum(grades) / len(grades), 2)
```
7. MVC separates an application into Model (data/logic), View (display), and Controller (handles input/connects M and V). This keeps code organized and maintainable.
8. You should validate input to prevent crashes and unexpected behavior. Use `try/except`, `isinstance()`, or conditional checks before processing user data.
9. Readable code uses: descriptive variable/function names, consistent indentation, comments for non-obvious logic, short focused functions, and whitespace between logical sections.
10. Focus on the problem you solved, show a live demo, avoid jargon, explain impact/use cases, and invite questions.
