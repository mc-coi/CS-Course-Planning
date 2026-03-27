# Day 7: Data Types — int, float, str, bool & the type() Function
**Learning Target:** I can identify and work with Python's four basic data types.

### Key Concepts
Python has four main basic data types:

1. **str (string):** Text, enclosed in quotes. Examples: `"Alice"`, `'hello'`, `"123 Main St"`
   - Strings are for any text, including numbers that shouldn't be calculated
   - Both single and double quotes work, but be consistent in a program

2. **int (integer):** Whole numbers without decimals. Examples: `42`, `-7`, `0`, `1000000`
   - Can be positive, negative, or zero
   - Used for counting, ages, scores, etc.

3. **float (floating-point):** Numbers with decimals. Examples: `3.14`, `-0.5`, `99.99`, `2.0`
   - Used for measurements, prices, ratings, etc.
   - Even `5.0` is a float because it has a decimal point

4. **bool (boolean):** True or False (always capitalized in Python)
   - Used for yes/no, on/off, enrolled/not enrolled situations
   - Only two possible values: True or False

The `type()` function tells you what data type a value is. It returns a response like `<class 'str'>` or `<class 'int'>`.

### Code Examples
```python
# String variables
name = "Alex"
city = "Nashville"
print(name)           # Alex
print(type(name))     # <class 'str'>

# Integer variables
age = 17
score = 95
print(age)            # 17
print(type(age))      # <class 'int'>

# Float variables
gpa = 3.85
price = 19.99
print(gpa)            # 3.85
print(type(gpa))      # <class 'float'>

# Boolean variables
is_enrolled = True
is_absent = False
print(is_enrolled)    # True
print(type(is_enrolled))  # <class 'bool'>

# Checking types
print(type("hello"))     # <class 'str'>
print(type(42))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type(True))        # <class 'bool'>

# Important: "5" and 5 are different!
text_number = "5"        # String (text)
actual_number = 5        # Integer (number)
print(type(text_number))     # <class 'str'>
print(type(actual_number))   # <class 'int'>
```

### Guided Practice
Create a program that:
1. Creates variables of all four data types
2. Prints each variable with its type
3. Explains in comments what each type is used for
4. Shows the difference between `"17"` and `17`

### Practice Problems

**Problem 1 — Beginner:** Declare one variable of each data type (str, int, float, bool) about yourself and print them all.

```python
# Starter code
name =
age =
height =
is_student =

print()  # Print all variables here
```

**Problem 2 — Intermediate:** Create variables for a student profile (name, age, GPA, and whether they're on honor roll). Print each variable with its type.

**Problem 3 — Challenge:** Write code to demonstrate that `type("3.14")` returns `<class 'str'>` while `type(3.14)` returns `<class 'float'>`. Explain in comments why this matters.

<details>
<summary>💡 Hints</summary>

- Problem 1: Strings need quotes, booleans are True or False (capitalized)
- Problem 2: GPA should be a float, name should be a string
- Problem 3: Quotes make anything a string, including numbers
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = "Jordan"
age = 16
height = 5.75
is_student = True

print(name, type(name))
print(age, type(age))
print(height, type(height))
print(is_student, type(is_student))

# Problem 2 Example
student_name = "Sam"
student_age = 17
student_gpa = 3.9
is_honors = True

print(f"{student_name}: {type(student_name)}")
print(f"{student_age}: {type(student_age)}")
print(f"{student_gpa}: {type(student_gpa)}")
print(f"Honors: {type(is_honors)}")

# Problem 3 Example
as_text = "3.14"
as_number = 3.14
print(type(as_text))      # <class 'str'>
print(type(as_number))    # <class 'float'>
# Quotes make it text; without quotes it's a number
```

</details>

---
