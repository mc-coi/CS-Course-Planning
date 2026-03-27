# Unit 3: Conditionals
> Master decision-making in code by using if/else/elif statements and logical operators.

## Unit Overview
- **Duration:** 25 days / 5 weeks (Days 46–70)
- **Class Period:** 55 minutes
- **Key Concepts:** Boolean expressions, if/else/elif statements, logical operators (and/or/not), nested conditionals, input validation, and debugging logic
- **Big Idea:** Programs make decisions based on conditions—this is what makes them interactive and intelligent

## Learning Targets
- I can evaluate Boolean expressions and understand comparison operators
- I can write if statements that execute code conditionally
- I can use if/else to choose between two paths
- I can use elif for multiple conditions
- I can combine conditions using logical operators (and, or, not)
- I can write nested conditionals for complex decisions
- I can validate user input with conditionals
- I can debug logic errors in conditional statements
- I can build complete interactive programs using conditionals
- I can implement real-world applications like games, menus, and access control systems

---

## Week-by-Week Breakdown

### Week 10 (Days 46–50): Boolean Logic & Comparisons

**Day 46:** Boolean expressions, comparison operators (==, !=, <, >, <=, >=)
**Day 47:** Logical operators (and, or, not) with truth tables
**Day 48:** Combining comparisons — compound conditions
**Day 49:** Boolean variables as flags
**Day 50:** Practice lab — boolean expression evaluator

**Key Idea:** Everything in conditionals starts with True/False. Learn to evaluate Boolean expressions correctly.

---

### Week 11 (Days 51–55): if/else Statements

**Day 51:** if statements — syntax, indentation, single conditions
**Day 52:** if/else — two-path decisions
**Day 53:** if/elif/else — multi-way branching
**Day 54:** Practice with if/elif/else — grade calculators, menus
**Day 55:** Practice lab — decision-based programs

**Key Idea:** Control program flow by making yes/no and multiple-choice decisions.

---

### Week 12 (Days 56–60): Nested Conditionals & Complex Logic

**Day 56:** Nested if statements — decisions inside decisions
**Day 57:** Complex conditions with and/or in if statements
**Day 58:** Short-circuit evaluation and truthy/falsy values
**Day 59:** Input validation with conditionals
**Day 60:** Practice lab — login system, eligibility checker

**Key Idea:** Build sophisticated decision-making by combining nesting and logical operators.

---

### Week 13 (Days 61–65): Real-World Applications

**Day 61:** Building a text-based menu system
**Day 62:** Rock-Paper-Scissors game
**Day 63:** Number guessing game (single guess version)
**Day 64:** Mini-project work day — student choice conditional program
**Day 65:** Mini-project presentations and peer review

**Key Idea:** Apply conditionals to real programs that solve actual problems.

---

### Week 14 (Days 66–70): Review & Assessment

**Day 66:** Review — vocabulary and boolean logic
**Day 67:** Review — code tracing with conditionals
**Day 68:** Review — common mistakes workshop
**Day 69:** Unit 3 Assessment
**Day 70:** Assessment review and reflection

**Key Idea:** Master the concepts through deep review and targeted practice.

---

## Daily Note Structure

Each daily note includes:
- **Learning Target:** 1-sentence goal
- **Key Concepts:** Core ideas (2-5 bullet points)
- **Code Examples:** Runnable Python code (3-5 examples)
- **Guided Practice:** In-class activity (10-15 minutes)
- **Practice Problems:** 3-tier (Beginner/Intermediate/Challenge)
- **Hints:** Guidance for each tier
- **Sample Answers:** Code solutions

---

## Practice Problems (Unit Bank)

### Boolean & Comparison Tier

1. **Beginner:** Write 5 comparison expressions with numbers and strings, predict output
2. **Beginner:** Compare three strings alphabetically; identify smallest and largest
3. **Intermediate:** Evaluate compound expressions like `5 > 3 == True`
4. **Intermediate:** Predict truth value of string comparisons
5. **Challenge:** Analyze lexicographic ordering across multiple strings

### Logical Operators Tier

6. **Beginner:** Use `and` to check if number is in range (1-10)
7. **Beginner:** Use `or` to check multiple values
8. **Intermediate:** Combine `and`, `or`, `not` in one expression
9. **Intermediate:** Write conditions for real scenarios (college eligibility, discounts)
10. **Challenge:** Evaluate short-circuit evaluation behavior

### if/elif/else Tier

11. **Beginner:** Write simple if statement checking even/odd
12. **Beginner:** Write if/else for positive/negative/zero
13. **Intermediate:** Grade classifier with if/elif/else
14. **Intermediate:** Season finder based on month number
15. **Challenge:** Multi-branch menu system with 4+ options

### Nested & Complex Tier

16. **Beginner:** Nested if to check positive and even
17. **Intermediate:** Login system with nested password check
18. **Intermediate:** Eligibility checker (age AND status AND requirements)
19. **Challenge:** Complex game logic with dependencies
20. **Challenge:** Advanced access control system

### Real-World Applications Tier

21. **Beginner:** Leap year checker
22. **Intermediate:** BMI calculator with classification
23. **Intermediate:** Simple rock-paper-scissors outcome checker
24. **Intermediate:** Input validation wrapper
25. **Challenge:** Multi-feature program combining all concepts

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using `=` instead of `==`: `if x = 5:` | SyntaxError | Use `==` for comparison: `if x == 5:` |
| Forgetting colon: `if x > 5` | SyntaxError: expected ':' | Add colon after condition: `if x > 5:` |
| Wrong indentation (tabs vs spaces) | IndentationError or logic error | Use exactly 4 spaces after `if`, `elif`, `else` |
| Using `and` instead of `or`: `if day == "Sat" and day == "Sun":` | Condition never True | Use `or`: one variable can't be two values simultaneously |
| Forgetting `elif` stops checking | Multiple branches execute | Use `elif` to make conditions mutually exclusive |
| Off-by-one error: `if score > 90:` but should include 90 | Score of 90 doesn't qualify when it should | Use `>=` instead of `>`, or `<` vs `<=` |
| Testing conditions in wrong order | Earlier specific True condition catches later general cases | Put most specific conditions first in elif chain |
| Not validating input | Crashes on invalid input (letters when expecting numbers) | Use try/except or if statements to validate input types |
| Condition never True (impossible logic) | Code path never executes | Review operator choice (and vs or) |
| Nested indentation confusion | Code in wrong scope (inside/outside conditional) | Use visual indentation guides; count spaces carefully |
| Forgetting `not` reverses Boolean | Using `not` incorrectly | Remember: `not True` = False, `not False` = True |
| Using string "True"/"False" instead of Boolean | Condition always True (non-empty string) | Use Boolean literals: `True`, `False` (capitalized, no quotes) |
| Chained comparisons syntax error | SyntaxError | Correct syntax: `1 <= x <= 10` (not `1 <= x and x <= 10`, though that works) |

---

## Unit Assessment Prep

### Review Questions with Answers

**1. What is the difference between `=` and `==`?**
- `=` is the assignment operator; it assigns a value to a variable
- `==` is the comparison operator; it checks if two values are equal and returns True or False

**2. When should you use `if` vs `elif` vs `else`?**
- `if` tests the initial condition
- `elif` (else if) tests another condition only if the previous `if` was False
- `else` catches all remaining cases (no condition needed)

**3. Explain `and`, `or`, and `not` operators.**
- `and`: Both conditions must be True for the result to be True
- `or`: At least one condition must be True for the result to be True
- `not`: Reverses a Boolean value (True becomes False, False becomes True)

**4. What does a nested conditional look like?**
- An if statement inside another if statement. Example:
```python
if condition1:
    if condition2:
        # code runs if both conditions are True
```

**5. Why is indentation important in Python?**
- Python uses indentation to define code blocks. Incorrect indentation causes IndentationError or changes program logic unintentionally.

**6. Write an if statement with 3+ branches (if/elif/elif/else).**
```python
score = 85
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```

**7. Explain short-circuit evaluation in `and`/`or`.**
- With `and`: if the first condition is False, the second is not evaluated (it's already False)
- With `or`: if the first condition is True, the second is not evaluated (it's already True)
- This can save time and prevent errors if the second condition would cause a crash

**8. What does `1 <= x <= 10` do?**
- Checks if x is greater than or equal to 1 AND less than or equal to 10 (chained comparison)
- Equivalent to: `x >= 1 and x <= 10`

**9. Write a chained comparison.**
```python
if 80 <= score <= 100:
    print("In the 80-100 range")
```

**10. Describe input validation.**
- Checking that user input meets requirements (correct type, within range, etc.) before using it
- Example: ensure age is a number between 0-150 before processing

---

## Vocabulary & Quick Reference

### Key Terms
- **Boolean:** Data type with only two values: True or False
- **Condition:** Expression that evaluates to True or False
- **Comparison operator:** ==, !=, <, >, <=, >=
- **Logical operator:** and, or, not
- **Compound condition:** Multiple conditions combined with and/or
- **Nested:** One structure inside another (if inside if)
- **Indentation:** Spacing that defines code blocks in Python (4 spaces standard)
- **Mutually exclusive:** Only one path can execute (if/elif/else pattern)
- **Short-circuit evaluation:** Stopping evaluation early when result is already determined
- **Truthy/Falsy:** Non-Boolean values that evaluate as True or False in conditionals
- **Input validation:** Checking user input before using it
- **Flag variable:** Boolean variable used to track state

### Key Syntax

```python
# Basic if
if condition:
    # code runs if True

# if/else
if condition:
    # runs if True
else:
    # runs if False

# if/elif/else
if condition1:
    # if True
elif condition2:
    # else if condition2 True
elif condition3:
    # else if condition3 True
else:
    # catch all remaining

# Logical operators
condition1 and condition2    # both True
condition1 or condition2     # at least one True
not condition               # reverse

# Chained comparison
1 <= x <= 100              # x is between 1 and 100

# Common patterns
if value in [1, 2, 3]:     # check if in list
if "substring" in "text":  # check if substring exists
if not is_valid:           # check if False
```

### Boolean Truth Tables

**and operator:**
| and | T | F |
|-----|---|---|
| T   | T | F |
| F   | F | F |

**or operator:**
| or | T | F |
|----|---|---|
| T  | T | T |
| F  | T | F |

**not operator:**
| Value | not Value |
|-------|-----------|
| T     | F         |
| F     | T         |

### Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| == | equal to | `5 == 5` → True |
| != | not equal to | `5 != 3` → True |
| < | less than | `3 < 5` → True |
| > | greater than | `5 > 3` → True |
| <= | less than or equal | `5 <= 5` → True |
| >= | greater than or equal | `5 >= 5` → True |

---

## Assessment Rubric

### Code Functionality (40%)
- Conditionals work correctly for all test cases
- Logic is sound and free of off-by-one errors
- Input validation functions properly

### Code Quality (30%)
- Indentation is consistent and correct
- Variable names are descriptive
- Code is organized and readable

### Completeness (20%)
- All required components included
- Meets all problem requirements
- Handles edge cases

### Comments & Documentation (10%)
- Code includes helpful comments
- Logic is explained where non-obvious
- Variable purposes are clear

---

## Resources & Extensions

### For Students Ahead of Schedule
- Explore truthy/falsy values with non-Boolean types
- Research the `switch`/`match` statement (Python 3.10+)
- Build more complex games: tic-tac-toe, Hangman
- Explore input validation with try/except blocks

### For Students Needing Support
- Use truth tables as reference materials
- Practice with visual flowcharts before coding
- Work through provided examples line-by-line
- Use print() statements to debug and trace execution

### Key Takeaways
1. Boolean expressions are the foundation of all decisions in programs
2. Correct indentation and operator choice are critical in Python
3. Combining `and`, `or`, `not` enables sophisticated logic
4. Nested conditionals allow complex, hierarchical decisions
5. Input validation makes programs robust and user-friendly
6. Real-world programming always involves conditional logic

---

## How to Use This Unit

1. **Daily:** Complete the daily learning target and guided practice (55-minute period)
2. **Problems:** Solve 1-2 practice problems each day (homework if needed)
3. **Week 13:** Apply learning to real-world projects (games, menus)
4. **Week 14:** Intensive review and assessment
5. **Throughout:** Reference the Quick Reference section as needed

---

*Unit 3 Conditionals is the bridge between simple scripts and intelligent, interactive programs. Master these concepts and you'll build powerful, responsive software.*
