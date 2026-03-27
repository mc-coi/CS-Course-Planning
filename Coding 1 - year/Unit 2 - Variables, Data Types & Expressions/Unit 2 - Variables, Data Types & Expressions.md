# Unit 2: Variables, Data Types & Expressions
> **Duration:** Days 21-45 (25 days / 5 weeks at 55 min per period)
> Master Python's data types, string manipulation, and expressions to build powerful, flexible programs.

## Unit Overview
This unit builds on Unit 1's foundation with a deep exploration of Python's data types and how to work with them effectively. Students will spend two weeks mastering strings, then move into type conversion, Boolean logic, advanced expressions, and real-world applications. The unit culminates in mini-projects and comprehensive assessment.

**Key Concepts:**
- Variable assignment and compound assignment operators
- Numeric types (int/float) and arithmetic operations
- Strings: indexing, slicing, methods, and formatting
- Type conversion and Boolean data type
- Expressions combining multiple operations
- Math module for scientific computing
- F-string formatting for professional output
- Building complete interactive programs

**Big Idea:**
Different data types and operators allow you to store, manipulate, and display information in powerful and flexible ways. Understanding types deeply gives you control over your programs' behavior.

---

## Learning Targets

By the end of Unit 2, students will be able to:

1. Declare and reassign variables using assignment and compound assignment operators (`=`, `+=`, `-=`, etc.)
2. Perform accurate arithmetic with integers and floats, understanding the distinction between `/` and `//`
3. Create strings and perform operations: concatenation, repetition, indexing, slicing, and method chaining
4. Apply common string methods (`.upper()`, `.lower()`, `.strip()`, `.replace()`, `.find()`, `.count()`) to analyze and transform text
5. Evaluate Boolean expressions and use comparison operators correctly
6. Convert between different data types using `int()`, `float()`, `str()`, and `bool()`
7. Write complex expressions that combine arithmetic, strings, and type operations
8. Use the math module (`math.sqrt()`, `math.pi`, `math.ceil()`, `math.floor()`) for scientific calculations
9. Format output professionally using f-strings with alignment and decimal precision
10. Write complete interactive programs that validate input, perform multi-step calculations, and display results
11. Apply best practices: meaningful variable names, constants (UPPER_CASE), and clear code organization

---

## Unit Structure: 5 Weeks

### Week 5: Deep Dive into Data Types (Days 21-25)
Focus: Understanding the core data types—numbers and strings—in depth.

### Week 6: Type Conversion & Boolean Logic (Days 26-30)
Focus: Converting between types and introducing Boolean values and comparison operators.

### Week 7: Advanced Expressions (Days 31-35)
Focus: Combining operators, string formatting, multiple assignment, and the math module.

### Week 8: Real-World Applications (Days 36-40)
Focus: Building complete programs with input validation, money handling, and meaningful projects.

### Week 9: Review & Assessment (Days 41-45)
Focus: Consolidating learning, identifying common mistakes, and formal assessment.

---

## Practice Problems (Unit Bank)

### Tier 1: Beginner (Problems 1-10)

1. **Variable Basics:** Declare a variable `temperature`, assign it 72, reassign it to 75, and print it.

2. **Arithmetic:** Given `x = 20` and `y = 3`, print the results of `+`, `-`, `*`, `/`, `//`, and `%`.

3. **String Creation:** Create a string that says "Hello, [Your Name]!" using concatenation with a variable.

4. **Indexing:** Given `word = "Python"`, print the first character, the last character, and the middle character.

5. **String Methods:** Use `.upper()`, `.lower()`, and `.replace()` on the phrase "Python is awesome".

6. **Length:** Ask the user for a word and print how many characters it has.

7. **Type Conversion:** Convert the string "42" to an integer, add 8 to it, and print the result.

8. **Slicing:** Given `text = "Hello, World!"`, print "Hello" and "World" using slicing.

9. **Compound Assignment:** Start with `score = 100`, then use `+=`, `-=`, `*=` to modify it. Print after each.

10. **Simple Boolean:** Print the result of `10 > 5`, `"apple" == "apple"`, and `3 != 3`.

### Tier 2: Intermediate (Problems 11-20)

11. **Circle Area:** Ask the user for a radius and calculate the area of a circle (π × r²).

12. **Palindrome Check:** Ask for a word and determine if it's a palindrome using string slicing.

13. **String Slicing with Step:** Predict the output of `"Python"[0:5:2]` and explain what step does.

14. **Chained Methods:** Clean user input by chaining `.strip()`, `.lower()`, and `.title()`.

15. **Formatted Output:** Use an f-string to display a number with exactly 2 decimal places.

16. **Multiple Assignment:** Swap the values of three variables using `a, b, c = c, b, a`.

17. **Money Calculation:** Ask for a price and quantity, calculate total, and display with 2 decimal places.

18. **Distance Formula:** Calculate distance between two points using `math.sqrt()`.

19. **Character Count:** Ask for a sentence and count how many times a specific letter appears.

20. **Type Checking:** Write a program that asks for input and prints its type using `type()`.

### Tier 3: Challenge (Problems 21-25)

21. **Grade Calculator:** Ask for test scores (multiple), calculate average, and assign a letter grade using Boolean logic.

22. **String Analysis:** Given a sentence, find the longest word, count total characters, and list unique first letters.

23. **Compound Expressions:** Calculate compound interest: A = P(1 + r/n)^(nt) with formatted output.

24. **Input Validation Loop:** Ask for a positive integer, validate it, and only proceed when valid input is received.

25. **Mini-Project (Payroll):** Given hourly wage and hours worked, calculate gross pay, taxes, and net pay with detailed output.

---

## Common Mistakes & Misconceptions (12+)

1. **Confusing `=` and `==`**
   `=` is assignment, `==` is comparison. Using `if x = 5` will error; use `if x == 5`.

2. **Division Always Returns Float**
   Students expect `10 / 2` to equal `5` (int) but it equals `5.0` (float). Use `//` for integer division.

3. **String Indexing Starts at 0**
   `"hello"[1]` is `"e"`, not `"h"`. The first character is always at index 0.

4. **Negative Indices Confuse Students**
   `"hello"[-1]` is `"o"` (last). Negative indices count from the end: -1 is last, -2 is second-to-last.

5. **Slice Stop is Exclusive**
   `"hello"[0:3]` gives `"hel"`, not `"hell"`. The stop index is NOT included.

6. **Can't Modify Strings with Indexing**
   Strings are immutable. `s[0] = "x"` will error. Must reassign: `s = "x" + s[1:]`.

7. **Type Mismatch in Concatenation**
   `"Score: " + 42` will error. Must convert: `"Score: " + str(42)`.

8. **Forgetting `.strip()` with Input**
   `input()` includes the newline. `input().strip()` removes whitespace. Compare with equality using cleaned input.

9. **Method Chaining Confusion**
   Methods return values. `"HELLO".lower()` returns `"hello"`, and you can chain: `"HELLO".lower().capitalize()`.

10. **Float Precision Issues**
    `0.1 + 0.2 == 0.3` is `False` due to floating-point rounding. Round for comparisons or use `round()`.

11. **Boolean Values Capitalization**
    Python uses `True` and `False` (capitalized), not `true` and `false`.

12. **Operator Precedence**
    `10 + 2 * 3` is `16`, not `36`. Multiplication happens before addition. Use parentheses to clarify.

13. **Misunderstanding the `in` Operator**
    `"a" in "banana"` is `True`, but this is taught in Unit 3 and can confuse students if introduced early.

---

## Assessment Prep (15 Q&A)

### Short Answer (7 questions, 2-3 sentences each)

1. **Q: Explain the difference between `=` and `==`. Give an example of each.**
   A: `=` is the assignment operator used to give a variable a value. `==` is the comparison operator that checks if two values are equal and returns True or False. Example: `x = 5` assigns 5 to x; `x == 5` checks if x equals 5.

2. **Q: Why does `10 / 2` return `5.0` instead of `5`?**
   A: In Python 3, the `/` operator always performs floating-point division, which returns a float type. To get an integer result, use `//` (floor division): `10 // 2` returns `5`.

3. **Q: What is string indexing, and what does "index starts at 0" mean?**
   A: String indexing accesses individual characters in a string using brackets. Index 0 is the first character, index 1 is the second, and so on. For "hello", `"hello"[0]` is `"h"` and `"hello"[4]` is `"o"`.

4. **Q: Describe what slicing does and explain what `[start:stop:step]` means.**
   A: Slicing extracts a portion of a string. Start is inclusive, stop is exclusive, and step determines the interval. `"Python"[0:4:1]` gives `"Pyth"` (indices 0, 1, 2, 3); `"Python"[0:6:2]` gives `"Pto"` (every 2nd character).

5. **Q: What are three string methods and what do they do?**
   A: `.upper()` converts to uppercase, `.lower()` converts to lowercase, `.strip()` removes leading/trailing whitespace, `.replace(old, new)` swaps occurrences. Example: `"Hello".upper()` returns `"HELLO"`.

6. **Q: What is type conversion, and why is it necessary?**
   A: Type conversion changes a value from one type to another using functions like `int()`, `float()`, `str()`, and `bool()`. It's necessary because operations like concatenation require matching types: `str(42)` converts the integer 42 to the string "42" so it can be concatenated.

7. **Q: What does an f-string do, and write an example that formats a number to 2 decimal places.**
   A: An f-string (formatted string literal) allows you to embed variables and expressions directly in strings using `f"..."` syntax. Example: `price = 9.5; print(f"Total: ${price:.2f}")` outputs "Total: $9.50".

### Code Tracing (5 questions)

8. **Trace this code and predict the output:**
   ```python
   x = 10
   y = 3
   print(x // y)
   print(x % y)
   print(x / y)
   ```
   A: Output is `3`, then `1`, then `3.3333333...`. Floor division gives 3, remainder is 1, true division is a float.

9. **What does this print?**
   ```python
   word = "programming"
   print(word[2:8])
   print(word[-3:])
   ```
   A: First line prints `ogrammm` (indices 2-7), second line prints `ing` (last 3 characters).

10. **Trace this:**
    ```python
    name = "ALICE"
    clean = name.strip().lower().title()
    print(clean)
    ```
    A: Prints `"Alice"`. `.strip()` does nothing (no whitespace), `.lower()` converts to "alice", `.title()` capitalizes first letter.

11. **What are the values after this runs?**
    ```python
    a, b = 5, 10
    a, b = b, a
    print(a, b)
    ```
    A: Prints `10 5`. The values are swapped using multiple assignment.

12. **Predict the output:**
    ```python
    print(5 > 3)
    print("apple" < "banana")
    print(10 == 10)
    ```
    A: `True`, `True`, `True`. Comparisons work on numbers and strings (alphabetically).

### Conceptual (3 questions)

13. **Explain why you cannot do `x[0] = "new"` on a string. What would you do instead?**
    A: Strings are immutable (unchangeable) in Python. You cannot modify a character at an index. Instead, reassign the variable: `x = "new" + x[1:]` or use string methods like `.replace()`.

14. **When should you use f-strings instead of simple concatenation? Give an example.**
    A: Use f-strings when embedding variables or formatting numbers. Concatenation with `+` requires type conversion and is harder to read: `"Price: " + str(9.5)` vs. `f"Price: {9.5}"`. F-strings also allow formatting: `f"Price: ${9.5:.2f}"`.

15. **A student writes `total = 10.5 + 20.3` and expects `30.8`, but gets `30.799999...`. Why, and how would you fix it?**
    A: This is a floating-point precision issue (computers store decimals imperfectly). Fix it by rounding when displaying: `print(round(total, 2))` or using f-strings: `f"{total:.2f}"`.

---

## Vocabulary & Quick Reference

### Data Types
- **int** (integer): Whole numbers like -5, 0, 42
- **float** (floating-point): Decimals like 3.14, -0.5, 2.0
- **str** (string): Text in quotes like "hello" or 'world'
- **bool** (boolean): True or False (capitalized)

### Operators
- **Arithmetic:** `+`, `-`, `*`, `/` (float division), `//` (integer division), `%` (modulo/remainder), `**` (exponentiation)
- **Assignment:** `=` (assign), `+=`, `-=`, `*=`, `/=`, `//=`, `%=` (compound assignment)
- **Comparison:** `==`, `!=`, `>`, `<`, `>=`, `<=` (return Boolean)

### String Operations
- **Concatenation:** `"hello" + "world"` = `"helloworld"`
- **Repetition:** `"ha" * 3` = `"hahaha"`
- **Length:** `len("hello")` = `5`
- **Indexing:** `"hello"[0]` = `"h"` (first), `"hello"[-1]` = `"o"` (last)
- **Slicing:** `"hello"[1:4]` = `"ell"` (start inclusive, stop exclusive)
- **Step in slicing:** `"hello"[::2]` = `"hlo"` (every 2nd character)

### Common String Methods
- `.upper()` - uppercase
- `.lower()` - lowercase
- `.title()` - capitalize each word
- `.strip()` - remove leading/trailing whitespace
- `.replace(old, new)` - replace substring
- `.find(sub)` - index of substring (-1 if not found)
- `.count(sub)` - count occurrences
- `.split()` - split into list of words
- `.startswith(pre)` - True if starts with prefix
- `.endswith(suf)` - True if ends with suffix

### Type Conversion Functions
- `int(x)` - convert to integer
- `float(x)` - convert to float
- `str(x)` - convert to string
- `bool(x)` - convert to Boolean
- `type(x)` - return the type of x

### Math Module (import math)
- `math.sqrt(x)` - square root
- `math.pow(x, y)` - x to the power of y
- `math.pi` - constant π ≈ 3.14159
- `math.e` - constant e ≈ 2.71828
- `math.ceil(x)` - round up
- `math.floor(x)` - round down
- `math.abs(x)` - absolute value (also `abs()` without import)

### F-Strings
```python
name = "Alice"
age = 25
# Basic interpolation
print(f"Name: {name}, Age: {age}")

# Formatting numbers
price = 9.5
print(f"${price:.2f}")  # $9.50

# Expressions in f-strings
print(f"Next year: {age + 1}")
```

### Naming Conventions
- **Variables:** `snake_case` (lowercase with underscores): `first_name`, `total_score`
- **Constants:** `UPPER_CASE` (all caps): `PI = 3.14159`, `MAX_ATTEMPTS = 5`
- **Meaningful names:** Use `age` not `a`, `temperature` not `t`

### Common Functions
- `print()` - display output
- `input()` - read user input (returns string)
- `len()` - length of string
- `abs()` - absolute value
- `round(x, n)` - round to n decimal places
- `max()`, `min()` - maximum and minimum
- `sum()` - sum of values
- `int()`, `float()`, `str()`, `bool()` - type conversion

---

## Days 21-45: Daily Content

See individual Daily Notes files (Day21.md through Day45.md) for detailed lessons, guided practice, and problem sets.

### Week 5 Overview (Days 21-25): Deep Dive into Data Types
- Day 21: Review of variables & types; int vs float in depth
- Day 22: String deep dive — indexing, len(), string basics
- Day 23: String slicing — [start:stop:step] notation
- Day 24: String methods — .upper(), .lower(), .replace(), .strip(), .find(), .count()
- Day 25: Practice lab — string manipulation programs

### Week 6 Overview (Days 26-30): Type Conversion & Boolean Logic
- Day 26: Type conversion — int(), float(), str(), bool(); when and why
- Day 27: Boolean data type — True/False, comparison operators
- Day 28: Compound expressions — combining math and string operations
- Day 29: The math module — import math, math.sqrt(), math.pi, math.ceil/floor
- Day 30: Practice lab — geometry calculator, unit converter

### Week 7 Overview (Days 31-35): Advanced Expressions
- Day 31: Augmented assignment operators (+=, -=, *=, /=)
- Day 32: String formatting — f-strings in depth, alignment, decimal places
- Day 33: Multiple assignment, swapping variables, unpacking
- Day 34: Building multi-step calculations — tax calculators, grade averagers
- Day 35: Practice lab — payroll calculator, BMI calculator

### Week 8 Overview (Days 36-40): Real-World Applications
- Day 36: Constants and naming conventions (UPPER_CASE, snake_case)
- Day 37: Building a complete interactive program with input validation
- Day 38: Working with money — rounding, formatting currency
- Day 39: Mini-project work day — student choice calculator program
- Day 40: Mini-project presentations and peer review

### Week 9 Overview (Days 41-45): Review & Assessment
- Day 41: Comprehensive review — vocabulary and concepts
- Day 42: Review — practice problems and code tracing
- Day 43: Review — common mistakes workshop
- Day 44: Unit 2 Assessment
- Day 45: Assessment review and reflection

---

## Additional Resources

### Reference Guides
- **ReferenceGuide.md:** Quick-lookup tables for operators, methods, and syntax
- **UnitPractice.md:** 25 numbered problems organized by difficulty
- **UnitAssessment.md:** 15 review questions with answer key

### Student Expectations
- Attend all 25 days of instruction (55 min per period)
- Complete daily guided practice and practice problems
- Participate in labs and mini-projects
- Prepare thoroughly for Unit Assessment on Day 44
- Demonstrate mastery of all 11 Learning Targets

---

**End of Unit 2 Hyperbook**
