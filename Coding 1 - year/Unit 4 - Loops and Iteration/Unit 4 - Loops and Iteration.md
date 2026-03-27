# Unit 4: Loops and Iteration
## 25-Day Unit for Traditional-Schedule Coding I (Days 71–95)

---

## Unit Overview

**Unit Goal:** Master iteration through loops, control flow statements, and foundational data structures.

**Essential Questions:**
- How do loops automate repetitive tasks?
- When should you use a while loop vs. a for loop?
- How can break and continue control loop execution?
- What patterns do loops follow in real applications?
- How do lists extend the power of loops?

**Learning Outcomes:**
By the end of this unit, students will:
1. Write while loops with proper condition and counter patterns
2. Implement sentinel loops and input validation patterns
3. Use the accumulator pattern for running totals and counting
4. Write for loops using range() with flexible parameters
5. Iterate over strings and lists character-by-character
6. Use break and continue statements effectively
7. Write and debug nested loops
8. Apply common loop patterns (min/max, search, flag patterns)
9. Create lists and manipulate them with methods
10. Write complete programs combining loops and lists

---

## Unit Structure (5 Weeks)

### Week 15: While Loops (Days 71–75)
Focus on the while loop as the primary iteration tool, condition evaluation, and three fundamental patterns.

- **Day 71:** While loop basics — syntax, condition, body
- **Day 72:** Sentinel loops — user-controlled exit
- **Day 73:** Accumulator pattern — running totals and counting
- **Day 74:** Input validation loops — defensive programming
- **Day 75:** Practice lab — while loop programs

### Week 16: For Loops & Range (Days 76–80)
Introduce the for loop and range() as tools for counted iteration.

- **Day 76:** for loop with range() — counting loops
- **Day 77:** range(start, stop, step) — flexible parameters
- **Day 78:** Iterating over strings — character-by-character
- **Day 79:** for vs while — choosing the right tool
- **Day 80:** Practice lab — pattern printing and string analysis

### Week 17: Loop Control & Nested Loops (Days 81–85)
Master control flow within loops and the power of nested loops.

- **Day 81:** break and continue — altering loop flow
- **Day 82:** Nested loops — loops inside loops
- **Day 83:** Nested loop applications — patterns and tables
- **Day 84:** Common loop patterns — min/max, search, flag
- **Day 85:** Practice lab — advanced loop challenges

### Week 18: Lists & Loop Applications (Days 86–90)
Introduce lists as data structures and combine with loops.

- **Day 86:** Lists intro — creating, indexing, len()
- **Day 87:** Looping through lists — for item in list
- **Day 88:** List methods — .append(), .remove(), .sort(), .reverse()
- **Day 89:** Mini-project — number analyzer or quiz game
- **Day 90:** Mini-project work day and peer testing

### Week 19: Review & Assessment (Days 91–95)
Consolidate learning and assess mastery.

- **Day 91:** Review — while loops and for loops
- **Day 92:** Review — nested loops and list basics
- **Day 93:** Review — code tracing and debugging loops
- **Day 94:** Unit 4 Assessment
- **Day 95:** Assessment review, reflection, semester check-in

---

## Key Concepts & Vocabulary

### Loop Structures

**while Loop:** A loop that continues executing while a condition is true.
```python
counter = 0
while counter < 5:
    print(counter)
    counter += 1  # Must change condition or loop runs forever
```

**for Loop:** A loop that iterates a specific number of times or over a sequence.
```python
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4
```

**range():** A function that generates a sequence of numbers.
```python
range(5)           # 0, 1, 2, 3, 4
range(2, 8)        # 2, 3, 4, 5, 6, 7
range(1, 10, 2)    # 1, 3, 5, 7, 9
```

### Loop Patterns

**Counter Pattern:** A variable incremented/decremented to control loop iterations.
```python
count = 0
while count < 10:
    count += 1
```

**Sentinel Pattern:** A loop controlled by a special value (sentinel) that triggers exit.
```python
while True:
    value = input("Enter (quit to exit): ")
    if value == "quit":
        break
```

**Accumulator Pattern:** A variable that collects values (sum, product, count).
```python
total = 0
for i in range(1, 6):
    total += i  # total accumulates: 1, 3, 6, 10, 15
```

**Input Validation Pattern:** A loop that keeps asking until valid input is received.
```python
while True:
    age = int(input("Age (1-120): "))
    if 1 <= age <= 120:
        break
    print("Invalid. Try again.")
```

### Control Statements

**break:** Immediately exits a loop (breaks out).
```python
for i in range(10):
    if i == 5:
        break  # Stops the loop
    print(i)  # 0, 1, 2, 3, 4
```

**continue:** Skips the current iteration and moves to the next.
```python
for i in range(5):
    if i == 2:
        continue  # Skips when i is 2
    print(i)  # 0, 1, 3, 4
```

### Nested Loops

A loop within another loop. The inner loop completes all iterations for each iteration of the outer loop.
```python
for row in range(3):
    for col in range(3):
        print(f"({row},{col})", end=" ")
    print()  # Newline after each row
```

### Lists

**List:** An ordered collection of items (like variables that hold multiple values).
```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]
mixed = [42, "hello", 3.14, True]

# Indexing (0-based)
print(names[0])  # "Alice"
print(names[-1]) # "Charlie" (last element)

# Length
print(len(names))  # 3
```

**List Methods:**
- `.append(value)` — Add to the end
- `.remove(value)` — Remove first occurrence
- `.pop(index)` — Remove at index (default last)
- `.insert(index, value)` — Insert at position
- `.sort()` — Sort in place (ascending)
- `.reverse()` — Reverse in place
- `.index(value)` — Find index of first occurrence
- `.count(value)` — Count occurrences

```python
numbers = [3, 1, 4, 1, 5]
numbers.append(9)       # [3, 1, 4, 1, 5, 9]
numbers.remove(1)       # [3, 4, 1, 5, 9] (first 1 only)
numbers.sort()          # [1, 3, 4, 5, 9]
print(numbers.count(1)) # 1
```

### Looping Patterns with Lists

**for-each loop:** Iterate directly over items in a list.
```python
names = ["Alice", "Bob", "Charlie"]
for name in names:
    print(f"Hello, {name}!")
```

**Index-based loop:** Iterate over indices to access/modify items.
```python
for i in range(len(names)):
    names[i] = names[i].upper()
```

**Enumerate:** Get both index and value.
```python
for i, name in enumerate(names):
    print(f"{i}: {name}")
```

---

## Common Loop Patterns

### Min/Max Finding
```python
numbers = [5, 2, 9, 1, 7]
max_val = numbers[0]
for num in numbers:
    if num > max_val:
        max_val = num
print(max_val)  # 9
```

### Search Pattern
```python
target = 7
found = False
for num in numbers:
    if num == target:
        found = True
        break
if found:
    print("Found!")
else:
    print("Not found.")
```

### Flag Pattern
```python
is_valid = True
for char in password:
    if not char.isalnum():  # Not alphanumeric
        is_valid = False
        break
```

### Running Total
```python
total = 0
for num in numbers:
    total += num
print(total)  # Sum of all numbers
```

---

## Common Mistakes & How to Fix Them

| Mistake | Error/Result | Fix |
|---------|----------|-----|
| Infinite loop (no counter change) | Program hangs/doesn't stop | Ensure counter/condition changes: `count += 1` |
| Off-by-one error in range | Wrong number of iterations | Remember: `range(5)` goes 0–4, not 1–5 |
| Missing colon after while/for | SyntaxError | Always use `:` after condition: `while x < 5:` |
| Indentation wrong | IndentationError | Loop body must be indented 4 spaces |
| break/continue outside loop | NameError or SyntaxError | These only work inside loops |
| List index out of range | IndexError: list index out of range | Check bounds: `0 <= index < len(list)` |
| Modifying list while looping | Skips elements or crashes | Create copy or loop backward |
| Confusing `range(5)` with `range(1, 6)` | Off-by-one error | `range(n)` starts at 0; use `range(1, n+1)` for 1–n |
| Using `=` in loop condition | Logic error | Use comparison: `while x < 5:` not `while x = 5:` |
| Nested loop logic wrong | Extra iterations or wrong output | Trace nested loops on paper first |
| `.append()` instead of `+` | TypeError | For lists, use `.append()`; for strings, use `+` |

---

## Assessment Prep: Review Questions

### Concept Questions

1. **What is the difference between a while loop and a for loop?**
2. **Explain the accumulator pattern and give an example.**
3. **What does the sentinel pattern do? Write a simple example.**
4. **How do break and continue differ?**
5. **What is the purpose of range()? Give three different examples.**

### Code Writing

6. **Write a program that asks the user for numbers until they enter 0, then prints the sum of all numbers entered.**
7. **Write a program that prints a 3×3 multiplication table using nested loops.**
8. **Write a program that takes a string and counts how many vowels it contains.**
9. **Create a list, then use a loop to print each element with its index.**
10. **Write input validation: repeatedly ask for an age until 0–120 is entered.**

### Code Analysis

11. **Trace this code and state what it prints:**
    ```python
    for i in range(1, 4):
        for j in range(2):
            print(i, j, end=" ")
    ```

12. **Find the error in this code:**
    ```python
    numbers = [1, 2, 3]
    for i in range(5):
        print(numbers[i])
    ```

13. **What does this accumulator loop calculate?**
    ```python
    total = 1
    for i in range(1, 6):
        total *= i
    ```

14. **Write a loop that finds the largest number in a list without using max().**

15. **Write a program that filters a list (keeps only numbers > 5) and prints the result.**

---

## Practice Bank: 25 Problems by Difficulty

### Beginner (Straightforward while/for loops)

**Problem 1:** Write a while loop that prints 1 through 10.

**Problem 2:** Write a for loop using range() that prints every other number from 0 to 10.

**Problem 3:** Write a loop that asks the user for a number and prints it 5 times.

**Problem 4:** Write a loop that calculates and prints the sum of numbers 1 through 20.

**Problem 5:** Write a loop that asks the user to enter names until they type "done", then prints how many names were entered.

### Beginner-Intermediate (Patterns & simple nesting)

**Problem 6:** Write a loop that asks for test scores until the user enters -1, then prints the average.

**Problem 7:** Write nested loops to print a 4×4 grid of asterisks.

**Problem 8:** Write a loop that iterates over the string "HELLO" and prints each character.

**Problem 9:** Write a loop that counts how many times the letter 'a' appears in the string "banana".

**Problem 10:** Write a loop that asks the user for a number, then prints the multiplication table for that number (1–10).

### Intermediate (Patterns, lists, multiple concepts)

**Problem 11:** Create a list of numbers, then use a loop to find the minimum value without using min().

**Problem 12:** Write a program that asks for 5 numbers, stores them in a list, then prints them in reverse order.

**Problem 13:** Write a loop that validates input: keep asking for a password until it's at least 8 characters long.

**Problem 14:** Write nested loops that print a right triangle of asterisks (first row 1 star, second row 2 stars, etc., up to 5 rows).

**Problem 15:** Write a loop that asks the user for numbers, stores them in a list, then prints how many are even.

### Intermediate-Advanced (Complex patterns & list operations)

**Problem 16:** Write a program that asks the user for a number n, then prints the first n Fibonacci numbers using a loop.

**Problem 17:** Create a list, use a loop to modify each element (multiply by 2), and print the result.

**Problem 18:** Write a loop using break and continue: ask for test scores, skip negative scores, stop at 0, then print the valid average.

**Problem 19:** Write nested loops that print a diamond pattern of asterisks.

**Problem 20:** Write a program that asks the user for a word, then checks if it's a palindrome using a loop (no slicing).

### Advanced (Synthesis, complex logic, mini-programs)

**Problem 21:** Write a program that asks the user to guess a random number (use a sentinel loop with attempts counter).

**Problem 22:** Create a program that builds a frequency table: ask for words until "done", count each word's occurrences, print results.

**Problem 23:** Write a program that simulates a quiz: store questions and answers in lists, loop through asking questions, count correct answers.

**Problem 24:** Write a program that finds all prime numbers between 1 and 50 using a nested loop (check each number).

**Problem 25:** Create a number-guessing game: computer picks random 1–100, user guesses with "higher/lower" feedback, count attempts.

---

## Scaffolding & Differentiation

### For Struggling Learners
- Provide loop structure templates (fill-in-the-blank)
- Use Python Tutor (pythontutor.com) to visualize loop execution
- Start with small, concrete examples (loop 3 times before 10)
- Break nested loops into separate single-loop examples first
- Use debugging as teaching: "Why doesn't this loop stop?"

### For Advanced Learners
- Introduce list comprehensions (optional extension)
- Explore while loops with complex conditions
- Challenge: write loops without using range() helpers
- Mini-projects: number analyzer, word game, data processor
- Investigate time complexity (why some loops are slow)

### Accessibility Considerations
- Provide code in larger fonts for visually impaired students
- Use syntax highlighting consistently (both on board and materials)
- Offer both visual tracing (flowcharts) and textual explanations
- Kinesthetic: act out loop iterations (walk through, repeat actions)
- Provide digital copies for screen readers

---

## Assessment Strategy

### Formative Assessment
- Daily guided practice (on board, watched together)
- 3-tier practice problems (self-checking with provided answers)
- Weekly code reviews (peer or self)
- Tracing exercises (what does this loop do?)

### Summative Assessment
- **Unit 4 Assessment (Day 94):** 15 questions (concept, code writing, code analysis)
- **Mini-projects (Days 89–90):** Interactive programs using loops and lists
- **Practice labs (Days 75, 80, 85):** Culminating practice for each phase

### Assessment Rubric Elements
- **Correctness:** Does the code run and produce correct output?
- **Logic:** Does the student understand when to use while vs. for?
- **Efficiency:** Are patterns (accumulator, sentinel) applied correctly?
- **Code Quality:** Is the code readable and commented?
- **Debugging:** Can the student trace and fix loop errors?

---

## Standards Alignment

**CSTA K-12 Computer Science Framework:**
- **Algorithm & Programming:** Iteration, control flow, data representation
- **Level 1C:** Understand iteration, decomposition, abstraction
- **Level 2A:** Implement algorithms with loops and conditional logic

**AP Computer Science Principles:**
- Iteration and loop structures
- Control flow (break, continue)
- Data representation (lists, arrays)

---

## Materials & Resources

### Daily Lesson Components
- Daily Note (with learning target, key concepts, examples, practice)
- Code examples for live demonstration
- Guided practice (do together)
- 3-tier practice problems (self-paced)
- Quick reference (vocabulary, syntax)

### Supporting Documents
- `ReferenceGuide.md` — Loop syntax, patterns, common mistakes table
- `UnitPractice.md` — 25 practice problems with solutions
- `UnitAssessment.md` — 15 review questions with answers

### External Tools
- Python IDE (Thonny, IDLE, Replit, Trinket)
- Python Tutor (pythontutor.com) for visualization
- Interactive visualizations (loopsandconditions.com, if available)
- Whiteboard/flowchart tools (draw.io, Lucidchart)

---

## Daily Lesson Plan Summary

| Day | Topic | Key Learning | Assessment |
|-----|-------|--------------|------------|
| 71 | while loops | Syntax, condition, body, counter pattern | Guided practice |
| 72 | Sentinel loops | User-controlled exit, break | 3-tier problems |
| 73 | Accumulator pattern | Running totals, counting | Guided practice |
| 74 | Input validation | Defensive loops, bounds checking | 3-tier problems |
| 75 | **Lab (Week 1)** | while loop programs | Peer review |
| 76 | for + range() | Counting loops, range behavior | Guided practice |
| 77 | range() parameters | start, stop, step | 3-tier problems |
| 78 | String iteration | Character-by-character loops | Guided practice |
| 79 | for vs while | Choosing the right loop | 3-tier problems |
| 80 | **Lab (Week 2)** | Pattern printing, string analysis | Code review |
| 81 | break & continue | Loop control flow | Guided practice |
| 82 | Nested loops | Loops inside loops | 3-tier problems |
| 83 | Nested applications | Multiplication tables, patterns | Guided practice |
| 84 | Loop patterns | min/max, search, flag | 3-tier problems |
| 85 | **Lab (Week 3)** | Advanced challenges | Peer testing |
| 86 | Lists intro | Creating, indexing, len() | Guided practice |
| 87 | Loop through lists | for-each iteration | 3-tier problems |
| 88 | List methods | append, remove, sort, reverse | Guided practice |
| 89 | **Mini-project start** | Number analyzer or quiz game | Project work |
| 90 | **Mini-project finish** | Integration & testing | Peer demo |
| 91 | Review (while/for) | Consolidation | Practice quiz |
| 92 | Review (nested/lists) | Consolidation | Practice quiz |
| 93 | Review (debugging) | Error tracing, fixing | Code analysis |
| 94 | **Unit Assessment** | 15-question exam | Formal assessment |
| 95 | Reflection & closure | Semester check-in | Self-assessment |

---

## Notes for Instruction

### Pacing Guidance
- **Week 15 (while loops):** 2 days per concept, 1 lab day. Build confidence before moving to for loops.
- **Week 16 (for loops):** Explicitly compare to while loops. Show that for loops are "while loops made easy."
- **Week 17 (nested):** This is where students struggle. Use visual tracing (grid drawings, colored arrows). One nested loop per day.
- **Week 18 (lists):** Lists are game-changing. Mini-projects keep motivation high.
- **Week 19 (review):** Allow time for questions. Some students need more practice.

### Classroom Strategies
- **Live coding:** Type alongside students; make mistakes intentionally and fix them together.
- **Pair programming:** Have students work in pairs during practice labs.
- **Python Tutor:** Use it to visualize every nested loop example.
- **Tracing on paper:** Have students trace code by hand before running it.
- **Backwards design:** Show a program's output; ask students to write the loop.

### Potential Challenges
1. **Infinite loops:** Emphasize counter updates. Have a "stop the madness" key (Ctrl+C) ready.
2. **Off-by-one errors:** Use range(3) and ask "which numbers?" (0, 1, 2). Repeat often.
3. **Nested loop confusion:** Start with 2×2, then 3×3. Always have students print the loop variables.
4. **Lists vs. strings:** Clarify: both are sequences, both are indexable, but lists are mutable.
5. **Performance:** Some nested loop patterns are slow. Show time cost visually (outer × inner iterations).

### Motivation & Engagement
- Show real-world loop use: bank transactions, game loops, data processing.
- Use culturally relevant examples: text analysis, playlist management, voting.
- Celebrate incremental progress: "Yesterday, you couldn't do nested loops. Today, you can!"
- Connect to Unit 5 (functions): "Loops + functions = powerful tools."

---

## Reflection & Semester Context

By the end of Unit 4, students have learned **procedural programming** with:
- Sequence (execute in order)
- Selection (if/else, conditionals)
- Iteration (while/for, loops)

These are the **three fundamental control structures**. With Unit 4 complete, students are ready for **Unit 5: Functions and Modularity**, which teaches code organization and reuse.

---

**Prepared for:** Coding I (Year-Long, Traditional Schedule)
**Unit:** 4 of 7
**Total Days:** 25 (Days 71–95)
**Duration:** 5 weeks at 55 minutes per period
**Prerequisite:** Units 1–3 (print, input, variables, data types, conditionals)

---
