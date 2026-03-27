# Unit 3: Conditionals — Assessment & Key Questions

Review questions with detailed answers to prepare for assessment.

---

## Section 1: Vocabulary & Concepts (30 points possible)

### Q1: Assignment vs. Comparison
**Question:** What is the difference between `=` and `==`?

**Answer:**
- `=` is the **assignment operator**. It assigns a value to a variable.
  - Example: `x = 5` sets x to 5
- `==` is the **comparison operator**. It checks if two values are equal and returns True or False.
  - Example: `x == 5` checks if x equals 5, returns Boolean

This is a critical distinction. Using `=` in an if statement causes a SyntaxError.

---

### Q2: Conditional Statement Types
**Question:** When should you use `if` vs `elif` vs `else`?

**Answer:**
- **if:** Tests the initial condition. If True, executes block and skips remaining branches.
  - Example: Check first requirement
- **elif** (else if): Tested only if previous if was False. Provides alternative condition.
  - Example: Check second requirement if first wasn't met
- **else:** Has no condition. Catches all remaining cases (when all previous were False).
  - Example: Default case when no conditions matched

**Flow:**
1. Check if (if True, execute and skip rest)
2. If false, check elif (if True, execute and skip rest)
3. If false, execute else (always has default behavior)

Only ONE branch executes. They are mutually exclusive.

---

### Q3: Logical Operators
**Question:** Explain `and`, `or`, and `not` operators.

**Answer:**
- **and:** Returns True only if BOTH conditions are True
  - `True and True` → True
  - `True and False` → False
  - `False and True` → False
  - `False and False` → False
  - Usage: "You must be 18 AND have a license"

- **or:** Returns True if AT LEAST ONE condition is True
  - `True or True` → True
  - `True or False` → True
  - `False or True` → True
  - `False or False` → False
  - Usage: "Monday OR Friday is acceptable"

- **not:** Reverses the Boolean value
  - `not True` → False
  - `not False` → True
  - Usage: "If NOT logged in, show login screen"

---

### Q4: Nested Conditionals
**Question:** What does a nested conditional look like? When would you use it?

**Answer:**
**Structure:**
```python
if condition1:
    # Outer block
    if condition2:
        # Inner block (nested)
        # Code here runs if BOTH conditions are True
    else:
        # Inner else block
    # Code here runs if condition1 True (after inner if/else)
else:
    # Outer else block
```

**When to use:**
- When one decision depends on another
- When you need hierarchical decision-making
- For dependent conditions (inner check only matters if outer is True)

**Example:**
```python
if has_key:  # First check
    if door_locked:  # Second check (only if has_key)
        print("Unlock door")
```

---

### Q5: Indentation Importance
**Question:** Why is indentation important in Python?

**Answer:**
Python uses **indentation** (4 spaces per level) to define code blocks. It determines:

1. **Which code belongs to which statement**
   - Code indented under `if` belongs to that if
   - Code not indented is outside the if

2. **Program logic**
   - Wrong indentation changes program behavior
   - Incorrect indent causes IndentationError

3. **Scope**
   - Variables defined inside if block may only be used there
   - Indentation shows scope visually

**Example:**
```python
if x > 5:
    print("Big")      # INDENTED - part of if
    print("Really")   # INDENTED - part of if
print("Done")         # NOT indented - always runs
```

---

### Q6: Short-Circuit Evaluation
**Question:** Explain short-circuit evaluation and give an example where it prevents errors.

**Answer:**
**Definition:**
Python stops evaluating a Boolean expression as soon as the result is determined.

**With `and`:**
- If first condition is False, second is never checked (result already False)
- Saves time and prevents errors

**With `or`:**
- If first condition is True, second is never checked (result already True)
- Saves time and prevents errors

**Error Prevention Example:**
```python
# Without short-circuit, this would error if data is empty
if data and data[0] > 5:
    # If data is empty (falsy), the and stops here
    # data[0] is NOT evaluated, no IndexError!

# Without short-circuit:
if len(data) > 0 and data[0] > 5:
    # Both conditions always checked
```

---

### Q7: Input Validation
**Question:** What is input validation and why does it matter?

**Answer:**
**Definition:**
Input validation checks that user input meets requirements BEFORE using it in the program.

**Validation types:**
1. **Type checking:** Is it the right type? (number vs. string)
   ```python
   age = int(input("Age: "))  # Converts to int
   ```

2. **Range checking:** Is it within valid range?
   ```python
   if 0 <= age <= 150:
       print("Valid")
   ```

3. **Format checking:** Does it match expected pattern?
   ```python
   if "@" in email and "." in email:
       print("Valid email format")
   ```

4. **Required fields:** Is it not empty?
   ```python
   if name and name.strip():
       print("Name provided")
   ```

**Why it matters:**
- Prevents crashes (TypeError, ValueError)
- Ensures correct calculations
- Improves user experience (clear error messages)
- Essential in professional software

---

### Q8: Truthy and Falsy Values
**Question:** What are truthy and falsy values in Python?

**Answer:**
In Python, any value can be used in a Boolean context (if statement). They evaluate as True or False.

**Falsy values** (evaluate as False):
- `False` — the Boolean literal
- `0` — integer zero
- `0.0` — float zero
- `""` — empty string
- `[]` — empty list
- `None` — no value

**Truthy values** (evaluate as True):
- `True` — the Boolean literal
- Any non-zero number (1, -5, 3.14, etc.)
- Any non-empty string ("hello", "0", " ", etc.)
- Any non-empty list, dictionary, set, etc.

**Examples:**
```python
if 0:
    print("Won't print")  # 0 is falsy

if 5:
    print("Will print")   # Non-zero is truthy

if "":
    print("Won't print")  # Empty string is falsy

if "hello":
    print("Will print")   # Non-empty string is truthy
```

---

### Q9: Chained Comparisons
**Question:** Explain chained comparisons. Write an example.

**Answer:**
**Definition:**
Chained comparisons let you check multiple conditions in one expression. They're more readable than using `and`.

**Syntax:**
```python
lower_bound <= value <= upper_bound
```

**Equivalent to:**
```python
value >= lower_bound and value <= upper_bound
```

**Examples:**
```python
# Check if score is in valid range
if 0 <= score <= 100:
    print("Valid score")

# Check if age is teen
if 13 <= age <= 19:
    print("Teenager")

# Check if day is weekday
if 1 <= day <= 5:
    print("Weekday")
```

**Advantages:**
- More readable
- More Pythonic
- Easier to understand intent

---

### Q10: Flag Variables
**Question:** What is a flag variable and why use them?

**Answer:**
**Definition:**
A flag variable is a Boolean variable that tracks state or the result of a condition. Flags simplify complex logic.

**Common naming:**
- `is_*`: `is_logged_in`, `is_admin`, `is_valid`
- `has_*`: `has_license`, `has_permission`, `has_error`
- `can_*`: `can_vote`, `can_drive`, `can_edit`

**Example:**
```python
# Without flags (complex)
if age >= 18 and has_license and has_insurance:
    if not on_probation:
        if not suspended:
            print("Can drive")

# With flags (clear)
is_old_enough = age >= 18
is_licensed = has_license
is_insured = has_insurance
is_clear = not on_probation and not suspended

if is_old_enough and is_licensed and is_insured and is_clear:
    print("Can drive")
```

**Benefits:**
- Makes code more readable
- Easier to reuse conditions
- Simplifies debugging
- Represents real-world "status" concepts

---

## Section 2: Code Tracing (35 points possible)

### Trace 1: Simple if
```python
x = 10
if x > 5:
    print("Big")
else:
    print("Small")
print("Done")
```

**Trace:**
1. Set x = 10
2. Is 10 > 5? YES (True)
3. Print "Big"
4. Skip else block
5. Print "Done"

**Output:**
```
Big
Done
```

---

### Trace 2: if/elif/else
```python
score = 75
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```

**Trace:**
1. Set score = 75
2. Is 75 >= 90? NO (False) → skip
3. Is 75 >= 80? NO (False) → skip
4. Is 75 >= 70? YES (True) → execute!
5. Print "C"
6. Skip remaining branches

**Output:**
```
C
```

---

### Trace 3: Nested Conditionals
```python
age = 20
if age >= 18:
    print("Adult")
    if age >= 65:
        print("Senior")
else:
    print("Minor")
```

**Trace:**
1. Set age = 20
2. Is 20 >= 18? YES (True)
3. Print "Adult"
4. Is 20 >= 65? NO (False)
5. Skip nested print
6. Skip else block

**Output:**
```
Adult
```

---

### Trace 4: Logical Operators
```python
x = 5
y = 10
if x > 0 and y > 5:
    print("Both true")
else:
    print("Not both")
```

**Trace:**
1. Set x = 5, y = 10
2. Evaluate: Is 5 > 0? YES (True)
3. AND: Check second: Is 10 > 5? YES (True)
4. True and True = True
5. Print "Both true"

**Output:**
```
Both true
```

---

### Trace 5: Complex Conditions
```python
score = 85
if score > 90:
    print("A")
elif score > 80:
    print("B")
else:
    print("C")
```

**Trace:**
1. Set score = 85
2. Is 85 > 90? NO (False) → skip
3. Is 85 > 80? YES (True) → execute!
4. Print "B"
5. Skip else

**Output:**
```
B
```

---

## Section 3: Key Concepts Summary

### Boolean Expressions
A Boolean expression evaluates to True or False using:
- Comparison operators (==, !=, <, >, <=, >=)
- Logical operators (and, or, not)
- Boolean literals (True, False)

### Control Flow
- **if:** Execute if condition True
- **if/else:** Two paths, one always executes
- **if/elif/else:** Multiple paths, only first True executes
- **Nested:** Dependent decisions, check one then another

### Best Practices
1. Use descriptive variable names
2. Validate all user input
3. Use flags for clarity
4. Check conditions from most to least specific in elif
5. Use and/or instead of nesting when conditions are independent
6. Comment complex logic
7. Test all branches and edge cases

---

## Assessment Preparation Checklist

Before the assessment:
- [ ] Understand all 10 vocabulary questions
- [ ] Can trace code without running it
- [ ] Can write if/elif/else correctly
- [ ] Know when to use and vs or
- [ ] Know what truthy/falsy means
- [ ] Can validate input
- [ ] Understand nested conditionals
- [ ] Know how to debug common errors
- [ ] Can explain your code clearly

---

## Practice Assessment Questions

**1. Code Trace (Write Output):**
```python
name = "alice"
if name == "Alice":
    print("Found Alice")
elif name == "alice":
    print("Found alice")
else:
    print("Not found")
```
**Output:** `Found alice`

---

**2. Write Code:**
Check if a person can vote:
- Must be 18+
- Must be a citizen
Print "✓ Can vote" or "✗ Cannot vote"

**Answer:**
```python
age = int(input("Age: "))
is_citizen = input("Citizen? (yes/no): ").lower() == "yes"

if age >= 18 and is_citizen:
    print("✓ Can vote")
else:
    print("✗ Cannot vote")
```

---

**3. Short Answer:**
Why would short-circuit evaluation prevent an error in this code?
```python
if numbers and numbers[0] > 5:
```

**Answer:**
If `numbers` is an empty list (falsy), the `and` operator stops evaluating at that point. `numbers[0]` is never attempted, so no IndexError occurs. Without short-circuit, both conditions would be checked and crash on empty list.

---

*You're ready! Trust your preparation and do your best on the assessment.*
