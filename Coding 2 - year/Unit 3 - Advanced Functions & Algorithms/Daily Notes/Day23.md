# Day 23: Unit 3 Project Lab - Functional Programming Mini-Project

**Learning Target:** I can apply functional programming concepts (lambdas, higher-order functions, comprehensions) to solve real-world data processing problems.

---

## Project: Data Processing Pipeline

**Scenario:** You're working with a list of student records and need to process and analyze the data using functional programming techniques.

**Starting Dataset:**
```python
students = [
    {"name": "Alice", "grade": 11, "gpa": 3.8, "scores": [92, 95, 88]},
    {"name": "Bob", "grade": 10, "gpa": 3.2, "scores": [78, 82, 79]},
    {"name": "Charlie", "grade": 11, "gpa": 3.9, "scores": [95, 98, 96]},
    {"name": "Diana", "grade": 10, "gpa": 3.5, "scores": [85, 88, 86]},
    {"name": "Eve", "grade": 11, "gpa": 3.6, "scores": [89, 91, 87]},
]
```

---

## Part 1: Data Filtering and Transformation

**Task 1A:** Filter students with GPA >= 3.5 using a list comprehension.

**Task 1B:** Extract just the names of high-performing students (GPA >= 3.7) using map().

**Task 1C:** Create a dictionary mapping student names to their average score.

---

## Part 2: Complex Data Analysis

**Task 2A:** Find the top 3 students by GPA using sorted() with a lambda key.

**Task 2B:** Group students by grade level using a dictionary comprehension.

**Task 2C:** Calculate class average GPA using reduce() from functools.

---

## Part 3: Function Composition

**Task 3A:** Create a pipeline that:
1. Filters students (grade == 11)
2. Maps to just their names
3. Sorts alphabetically

**Task 3B:** Create a closure that generates custom comparison functions (e.g., compare by GPA, compare by grade).

---

## Part 4: Challenge Tasks

**Task 4A:** Create a decorator that timing how long data processing takes.

**Task 4B:** Use generator expressions to lazily process and filter large datasets.

**Task 4C:** Implement a memoized function that calculates statistics on demand.

---

## Starter Code

```python
from functools import reduce
import time

students = [
    {"name": "Alice", "grade": 11, "gpa": 3.8, "scores": [92, 95, 88]},
    {"name": "Bob", "grade": 10, "gpa": 3.2, "scores": [78, 82, 79]},
    {"name": "Charlie", "grade": 11, "gpa": 3.9, "scores": [95, 98, 96]},
    {"name": "Diana", "grade": 10, "gpa": 3.5, "scores": [85, 88, 86]},
    {"name": "Eve", "grade": 11, "gpa": 3.6, "scores": [89, 91, 87]},
]

# Part 1: Data Filtering
print("=== PART 1: Filtering ===")
# Task 1A
high_gpa = [s for s in students if s["gpa"] >= 3.5]
print(f"Students with GPA >= 3.5: {len(high_gpa)}")

# Task 1B
top_names = list(map(lambda s: s["name"], filter(lambda s: s["gpa"] >= 3.7, students)))
print(f"Top students: {top_names}")

# Task 1C
avg_scores = {s["name"]: sum(s["scores"]) / len(s["scores"]) for s in students}
print(f"Average scores: {avg_scores}")

# Part 2: Analysis
print("\n=== PART 2: Analysis ===")
# Task 2A
top_3 = sorted(students, key=lambda s: s["gpa"], reverse=True)[:3]
print(f"Top 3 by GPA: {[s['name'] for s in top_3]}")

# Task 2B
by_grade = {
    grade: [s["name"] for s in students if s["grade"] == grade]
    for grade in set(s["grade"] for s in students)
}
print(f"Students by grade: {by_grade}")

# Task 2C
class_gpa = reduce(lambda acc, s: acc + s["gpa"], students, 0) / len(students)
print(f"Class average GPA: {class_gpa:.2f}")

# Part 3: Composition
print("\n=== PART 3: Composition ===")
# Task 3A
pipeline = sorted(
    map(lambda s: s["name"], filter(lambda s: s["grade"] == 11, students))
)
print(f"Grade 11 students (sorted): {pipeline}")

# Task 3B
def make_comparator(field, descending=False):
    def compare(student):
        value = student[field]
        return value if not descending else -value if isinstance(value, (int, float)) else value
    return compare

# Part 4: Challenge
print("\n=== PART 4: Challenge ===")
# Task 4A
def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} took {elapsed:.4f}s")
        return result
    return wrapper

@timing_decorator
def analyze_students():
    return [s for s in students if s["gpa"] >= 3.7]

analyze_students()
```

---

## Submission Checklist

- [ ] All 12 tasks (1A-1C, 2A-2C, 3A-3B, 4A-4C) completed and tested
- [ ] Code uses appropriate functional programming techniques
- [ ] All functions are documented with clear comments
- [ ] Program runs without errors
- [ ] Results are printed clearly and correctly

---

## Grading Rubric

| Criteria | Points |
|----------|--------|
| Filtering & Mapping (Part 1) | 20 |
| Data Analysis (Part 2) | 20 |
| Function Composition (Part 3) | 20 |
| Challenge Tasks (Part 4) | 20 |
| Code Quality & Comments | 10 |
| **Total** | **90** |

---

## Extensions

1. Add error handling for invalid data
2. Create a sorted menu to select which analysis to run
3. Read student data from a CSV file
4. Implement additional statistics (median, mode, etc.)
5. Create a mini GUI with tkinter to display results

