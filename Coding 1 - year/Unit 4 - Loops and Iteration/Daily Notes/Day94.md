# Day 94: Unit 4 Assessment

**Learning Target:** I can demonstrate mastery of loops, iteration, and related concepts through a comprehensive assessment.

### Assessment Overview

This assessment covers all topics from Unit 4 (Days 71–93):
- While loops and patterns
- For loops and range()
- Nested loops
- Break and continue
- Lists and methods
- Common patterns (min/max, search, flag)
- Code tracing and debugging

**Format:**
- Part A: Concept & Vocabulary (5 questions)
- Part B: Code Writing (5 questions)
- Part C: Code Analysis (5 questions)

**Time:** 55 minutes

---

## PART A: Concept & Vocabulary (5 questions)

Answer in complete sentences.

**Question 1:** What is the difference between a while loop and a for loop? When would you use each?

**Question 2:** Explain the accumulator pattern and give a code example.

**Question 3:** What does the `break` statement do? How is it different from `continue`?

**Question 4:** How do you iterate over a list in Python? Show two different methods.

**Question 5:** What is a sentinel loop? How does it work?

---

## PART B: Code Writing (5 questions)

Write complete, working Python code.

**Question 6:** Write a while loop that asks the user for positive numbers until they enter 0. Calculate and print the sum of all numbers entered (not counting 0).

**Question 7:** Write a for loop using range() that prints all multiples of 5 from 5 to 50.

**Question 8:** Write nested loops that print a 4×4 grid like this:
```
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
```

**Question 9:** Create a list, ask the user for 5 names, then print them in reverse order using a for loop.

**Question 10:** Write a program that asks the user for numbers until "done". Find and print:
- The highest number
- The lowest number
- The average

---

## PART C: Code Analysis (5 questions)

**Question 11:** What will this code print? Trace through it.
```python
for i in range(1, 4):
    for j in range(2):
        print(i * j, end=" ")
    print()
```

**Question 12:** Find the bug in this code and explain what's wrong:
```python
count = 0
while count < 5:
    print(count)
    count += 2
```
(Hint: It might run, but the logic might be wrong for some scenarios.)

**Question 13:** What is the output of this code?
```python
numbers = [3, 1, 4, 1, 5]
for num in numbers:
    if num == 1:
        continue
    print(num, end=" ")
```

**Question 14:** Find the error(s) in this code:
```python
names = ["Alice", "Bob", "Charlie"]
for name in names
    print(name)
```

**Question 15:** What does this code do? Describe in words.
```python
text = input("Word: ")
count = 0
for char in text.lower():
    if char in "aeiou":
        count += 1
print(f"Vowels: {count}")
```

---

## Assessment Rubric

**Concept Questions (5 points each):**
- Complete, accurate answer
- Uses proper terminology
- Shows understanding

**Code Writing (5 points each):**
- Code runs without errors
- Logic is correct
- Output matches expectations
- Code is readable

**Code Analysis (5 points each):**
- Correct answer/explanation
- Shows understanding of code flow
- Explains bugs clearly

---

## Tips for Success

1. **Read carefully.** Make sure you understand what each question asks.
2. **Show your work.** For tracing, write down variables and their values.
3. **Indent correctly.** Python is sensitive to indentation.
4. **Include colons.** Don't forget colons after loops, if statements, etc.
5. **Test your code** (mentally or on paper) before submitting.
6. **Use clear variable names.** Make your code readable.
7. **Comment complex logic.** Explain what your code does.

---

## Study Checklist

Before the assessment, make sure you can:

- [ ] Write a while loop with a counter
- [ ] Write a sentinel loop (until special value)
- [ ] Use the accumulator pattern (sum, count, etc.)
- [ ] Validate input with a loop
- [ ] Write a for loop with range()
- [ ] Use range(start, stop, step)
- [ ] Iterate over a list or string
- [ ] Use break and continue correctly
- [ ] Write nested loops
- [ ] Find min/max in a list
- [ ] Search for a value in a list
- [ ] Use list methods (append, remove, sort)
- [ ] Trace code and predict output
- [ ] Identify and fix common errors
- [ ] Choose between for and while loops

---

**Good luck on your assessment!**

---
