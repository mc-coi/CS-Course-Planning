# Day 3: Development Session 2 — Integration

### Key Concepts

**Integration:** Connecting your tested helper functions into a working program.

**Integration testing:** Testing how the pieces work *together* (vs. unit testing — testing each piece alone).

### Integration Checklist

Before integrating two functions:
- [ ] Both functions work correctly on their own
- [ ] The output type of function A matches what function B expects
- [ ] Edge cases have been handled

### Code Examples — Full Integration

```python
"""
grade_tracker.py
A complete grade tracking application.
Demonstrates full integration of functions built across multiple sessions.
"""

import os

# ── HELPER FUNCTIONS (built and tested individually) ───────

def get_student_name():
    """Prompt for and return the student's name."""
    name = input("Student name: ").strip()
    while not name:
        print("Name cannot be empty.")
        name = input("Student name: ").strip()
    return name

def get_scores():
    """Collect scores from user until 'done' is entered.

    Returns:
        list of float: Valid scores in range 0-100.
    """
    scores = []
    print("Enter scores one at a time. Type 'done' when finished.")
    while True:
        entry = input(f"Score {len(scores)+1} (or 'done'): ").strip()
        if entry.lower() == "done":
            if not scores:
                print("Please enter at least one score.")
                continue
            break
        try:
            score = float(entry)
            if 0 <= score <= 100:
                scores.append(score)
            else:
                print("Score must be between 0 and 100.")
        except ValueError:
            print("Please enter a number.")
    return scores

def calculate_average(scores):
    """Return the arithmetic mean of a list of scores."""
    if not scores:
        return 0.0
    return sum(scores) / len(scores)

def letter_grade(average):
    """Convert a numeric average to a letter grade (A-F)."""
    if average >= 90: return "A"
    if average >= 80: return "B"
    if average >= 70: return "C"
    if average >= 60: return "D"
    return "F"

def display_report(name, scores, average, grade):
    """Print a formatted grade report to the console."""
    border = "=" * 40
    print(f"\n{border}")
    print(f"  Grade Report: {name}")
    print(border)
    print(f"  Scores:   {[round(s, 1) for s in scores]}")
    print(f"  Average:  {average:.1f}")
    print(f"  Grade:    {grade}")
    status = "PASSING" if average >= 70 else "FAILING"
    print(f"  Status:   {status}")
    print(border)

def save_report(filename, name, scores, average, grade):
    """Save the grade report to a text file.

    Args:
        filename (str): Output file path.
        name, scores, average, grade: Report data.
    """
    try:
        with open(filename, "w") as f:
            f.write(f"Grade Report: {name}\n")
            f.write(f"Scores: {scores}\n")
            f.write(f"Average: {average:.1f}\n")
            f.write(f"Grade: {grade}\n")
        print(f"Report saved to '{filename}'")
    except IOError as e:
        print(f"Could not save file: {e}")

# ── MAIN (integration point) ───────────────────────────────

def main():
    """Run the grade tracking program."""
    print("=" * 40)
    print("   Welcome to Grade Tracker")
    print("=" * 40 + "\n")

    name = get_student_name()
    scores = get_scores()
    average = calculate_average(scores)
    grade = letter_grade(average)

    display_report(name, scores, average, grade)

    save_choice = input("\nSave report to file? (y/n): ").lower()
    if save_choice == "y":
        filename = f"{name.replace(' ', '_')}_report.txt"
        save_report(filename, name, scores, average, grade)

    print("\nThanks for using Grade Tracker!")

main()
```

### Integration Debugging Strategy

When integrated code doesn't work:
1. **Check the pipeline:** Trace data flowing from function to function — is it the right type?
2. **Print at connection points:** `print(f"After get_scores, got: {scores}")` between calls
3. **Isolate which function is failing:** Comment out later steps to narrow it down
4. **Check edge cases in integration:** Does `letter_grade` handle the `0.0` returned by `calculate_average([])`?

---