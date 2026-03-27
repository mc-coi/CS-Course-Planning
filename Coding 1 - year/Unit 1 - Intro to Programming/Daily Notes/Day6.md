# Day 6: Variables — Naming Rules, Assignment & Reassignment
**Learning Target:** I can create variables, assign values, and reassign them correctly.

### Key Concepts
A **variable** is a named container that stores a value in the computer's memory. Think of it like a labeled box—you put something inside and give it a name so you can refer to it later. In Python, creating a variable is simple: `variable_name = value`

**Variable naming rules:**
- Cannot contain spaces; use underscores instead: `first_name` not `first name`
- Cannot start with a number: `age1` is okay, `1age` is not
- Cannot use special characters like `!@#$%`
- Cannot be Python keywords like `print`, `if`, `while`, `for`
- Are case-sensitive: `score` and `Score` are different variables
- Should be descriptive: `student_name` is better than `x`

**Naming conventions** (best practices):
- Use lowercase with underscores: `my_age`, `favorite_color`
- Avoid single letters unless it's a loop counter: use `total_score` not `s`
- Be specific and descriptive: `student_count` is better than `number`

**Assignment** means storing a value in a variable: `name = "Alex"`. The equals sign here is not "equals" mathematically—it means "assign the right side to the left side."

**Reassignment** means changing what a variable holds. A variable can store different values throughout a program: `score = 90; score = 95;` Now score holds 95, and 90 is forgotten.

### Code Examples
```python
# Creating variables and assigning values
name = "Morgan"
age = 17
gpa = 3.85
is_honors = True

print(name)        # Morgan
print(age)         # 17
print(gpa)         # 3.85
print(is_honors)   # True

# Reassigning variables (changing the value)
score = 85
print(score)       # 85
score = 92
print(score)       # 92 (changed!)

# Multiple assignment (assigning multiple variables at once)
first, last, grade = "Jordan", "Smith", 10
print(first, last, grade)  # Jordan Smith 10

# Using variables in output
player = "Alex"
points = 23
print(f"{player} scored {points} points")  # Alex scored 23 points
```

### Guided Practice
Create a program that:
1. Creates 5 variables with different data (your name, age, GPA, favorite subject, and whether you like math)
2. Prints each variable on a separate line
3. Then reassigns at least one variable to a new value
4. Prints the updated value
5. Include at least 2 comments explaining your code

### Practice Problems

**Problem 1 — Beginner:** Declare one variable for each piece of information: your name, your age, your height (as a decimal), and whether you're a student. Then print all of them.

```python
# Starter code
my_name =
my_age =
my_height =
am_student =

print()
```

**Problem 2 — Intermediate:** Create a program that demonstrates variable reassignment. Start with `x = 5`, print it, then change it to `x = 15`, and print it again. Add comments explaining what's happening.

**Problem 3 — Challenge:** Create a program that demonstrates that `score` and `Score` are different variables by assigning different values to each and printing both.

<details>
<summary>💡 Hints</summary>

- Problem 1: Don't forget that some variables need quotes, others don't
- Problem 2: Comments should explain that reassignment changes what the variable holds
- Problem 3: This shows case-sensitivity in Python
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
my_name = "Taylor"
my_age = 16
my_height = 5.75
am_student = True

print(my_name)
print(my_age)
print(my_height)
print(am_student)

# Problem 2 Example
x = 5
print(f"x starts as: {x}")
x = 15
print(f"x is now: {x}")  # Reassignment changes the value

# Problem 3 Example
score = 95
Score = 87
print(f"score = {score}, Score = {Score}")  # Two different variables!
```

</details>

---
