# Day 55: Practice Lab — Decision-Based Programs

**Learning Target:** I can build complete programs using if/elif/else to make decisions based on user input.

---

## Learning Summary (Week 11 Review)

This week you mastered:
1. **if statements:** Execute code when condition is True
2. **if/else:** Two-path decisions
3. **if/elif/else:** Multiple-path decisions (only one executes)
4. **Real-world patterns:** Grading, menus, tiered pricing

---

## Practice Lab: Decision-Based Programs

### Project Overview

Build one of these complete programs. Your program must:
- Accept user input
- Use if/elif/else for decisions
- Include at least 4 decision branches
- Provide clear output
- Handle edge cases gracefully

---

## Option A: Advanced Grading System

```
Input: Student name and test score
Output: Letter grade, GPA, commentary
Logic:
  - A (90-100): "Excellent"
  - B (80-89): "Good"
  - C (70-79): "Satisfactory"
  - D (60-69): "Needs improvement"
  - F (0-59): "Failing"
```

**Requirements:**
- [ ] Accept name and score (input validation: 0-100)
- [ ] Calculate grade (A-F)
- [ ] Calculate GPA (4.0, 3.0, 2.0, 1.0, 0.0)
- [ ] Print personalized message based on grade
- [ ] Handle invalid input gracefully

**Starter:**
```python
name = input("Student name: ")
score = int(input("Score (0-100): "))

# Validate
if score < 0 or score > 100:
    print("Invalid score!")
else:
    # Determine grade and GPA
    if score >= 90:
        grade = "A"
        gpa = 4.0
        message = "Excellent work!"
    # ... continue ...

    print(f"{name}: {grade} (GPA: {gpa}) - {message}")
```

---

## Option B: Interactive Menu System

```
Output: Menu with options
Input: User choice
Logic: Execute selected action
```

**Requirements:**
- [ ] Display menu (5+ options)
- [ ] Accept user choice (1-5)
- [ ] Use if/elif/else to handle choices
- [ ] Each choice does something different
- [ ] Handle invalid choice

**Starter:**
```python
print("=== Main Menu ===")
print("1. Calculate area of rectangle")
print("2. Convert temperature")
print("3. Check number properties")
print("4. Play coin flip")
print("5. Exit")

choice = input("Select (1-5): ")

if choice == "1":
    length = float(input("Length: "))
    width = float(input("Width: "))
    area = length * width
    print(f"Area: {area}")
elif choice == "2":
    # ... temperature conversion ...
else:
    print("Invalid choice")
```

---

## Option C: Movie Theater Ticket System

```
Input: Age, day of week
Output: Ticket price (with discounts)
Logic: Age category + weekday discount
```

**Requirements:**
- [ ] Accept age and day of week
- [ ] Determine base price by age:
  - Under 13: $6 (child)
  - 13-17: $8 (student)
  - 18-64: $10 (adult)
  - 65+: $7 (senior)
- [ ] Apply weekday discount:
  - Mon-Thu: 25% off
  - Fri-Sun: 10% off
- [ ] Display breakdown

**Starter:**
```python
age = int(input("Your age: "))
day = input("Day (Mon-Sun): ").lower()

# Base price by age
if age < 13:
    base = 6
elif age < 18:
    base = 8
elif age < 65:
    base = 10
else:
    base = 7

# Discount by day
if day in ["monday", "tuesday", "wednesday", "thursday"]:
    discount = 0.25
else:
    discount = 0.10

final = base * (1 - discount)
print(f"Base: ${base:.2f}")
print(f"Discount: {discount*100:.0f}%")
print(f"Final: ${final:.2f}")
```

---

## Option D: Eligibility Checker

```
Input: Multiple requirements
Output: Approved/Denied with reasons
Logic: All conditions must be met
```

**Example: College Admission**
- [ ] GPA >= 3.0
- [ ] SAT >= 1000
- [ ] Essay submitted
- [ ] No disciplinary issues

**Starter:**
```python
gpa = float(input("GPA: "))
sat = int(input("SAT score: "))
essay = input("Essay submitted? (yes/no): ").lower()
issues = input("Any disciplinary issues? (yes/no): ").lower()

# Check each requirement
if gpa >= 3.0 and sat >= 1000 and essay == "yes" and issues == "no":
    print("✓ APPROVED")
else:
    print("✗ DENIED - Missing requirements:")
    if gpa < 3.0:
        print("  - GPA too low")
    if sat < 1000:
        print("  - SAT too low")
    if essay != "yes":
        print("  - No essay")
    if issues == "yes":
        print("  - Disciplinary issues")
```

---

## Requirements Checklist

Your program must have:
- [ ] Clear user prompts
- [ ] At least 4 decision branches
- [ ] Logical use of if/elif/else
- [ ] Input validation (or at least valid assumptions)
- [ ] Clear, formatted output
- [ ] At least 3 comments explaining logic
- [ ] No syntax errors

---

## Testing Checklist

Before submitting, test:
- [ ] Program runs without crashing
- [ ] All branches execute correctly
- [ ] Output is clear and well-formatted
- [ ] Edge cases work (0, 100, etc.)
- [ ] Invalid input is handled (if applicable)
- [ ] Variable names are descriptive
- [ ] Indentation is consistent

---

## Grading Rubric

| Criteria | Points | Notes |
|----------|--------|-------|
| Functionality | 40 | All branches work; logic is correct |
| Code Quality | 30 | Clear names; good indentation; readable |
| Completeness | 20 | Meets all requirements |
| Documentation | 10 | Comments explain logic |

---

## Challenge Extensions

**If you finish early:**
1. Add input validation (check that age is 0-120, etc.)
2. Add more decision branches
3. Combine multiple programs into one menu-driven system
4. Add file I/O (save results to a file)
5. Create a mini game with decision logic

---

## Reflection Questions

After completing your program:

1. How many different paths can your program take?
2. What happens if the user enters unexpected input?
3. Could you simplify your conditionals using Boolean flags?
4. How would you explain your program's logic to someone else?
5. What improvements would you make?

---

## Key Skills Demonstrated

By completing this lab, you can:
- [ ] Write if/elif/else chains correctly
- [ ] Handle multiple decision paths
- [ ] Accept and validate user input
- [ ] Provide clear program output
- [ ] Use comments effectively
- [ ] Test and debug conditional logic
