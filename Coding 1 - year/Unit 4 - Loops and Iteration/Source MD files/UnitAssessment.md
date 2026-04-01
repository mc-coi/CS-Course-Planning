# Unit 4 Assessment Preparation — 15 Essential Questions & Answers

## Part 1: Concept & Vocabulary Questions

**Question 1: What is the difference between a while loop and a for loop? When would you use each?**

**Answer:**

A **while loop** repeats while a condition is true. You use it when you don't know exactly how many iterations—for example, when waiting for user input to signal exit, validating input repeatedly, or processing data until a condition changes.

A **for loop** repeats a specific number of times, especially useful when iterating over a sequence (like a list or range). You use it when you know exactly how many iterations or when you're iterating over a collection.

**Example:**
```python
# While loop (condition-based)
while age < 18:
    print("Not yet an adult")
    age += 1

# For loop (count-based)
for year in range(1, 19):
    print(f"Age {year}")
```

**Key differences:**
- For loop: "repeat 5 times"
- While loop: "repeat until condition is false"

---

**Question 2: Explain the accumulator pattern and give a code example.**

**Answer:**

The **accumulator pattern** uses a variable that collects or combines values as a loop iterates. The accumulator starts with an initial value (often 0 for sum, 1 for product, "" for strings), and each iteration updates it.

**Structure:**
```python
accumulator = initial_value
for item in items:
    accumulator = accumulator operator item
```

**Common accumulators:**
- **Sum:** Start with 0, use `+=`
- **Product:** Start with 1, use `*=`
- **Count:** Start with 0, use `+= 1`
- **String:** Start with "", use `+=`

**Example (sum):**
```python
total = 0  # Accumulator
for num in [5, 3, 8, 2]:
    total += num
print(total)  # 18
```

**Why it works:** The variable retains its value after each iteration, growing with each new value.

---

**Question 3: What does the `break` statement do? How is it different from `continue`?**

**Answer:**

**`break`:** Immediately exits the loop completely. No more iterations occur.
```python
for i in range(10):
    if i == 5:
        break  # Loop stops immediately
    print(i)  # Prints 0, 1, 2, 3, 4
```

**`continue`:** Skips the current iteration and jumps to the next one (without executing remaining code in the body).
```python
for i in range(5):
    if i == 2:
        continue  # Skips when i is 2
    print(i)  # Prints 0, 1, 3, 4
```

**Key difference:**
- `break` stops the entire loop
- `continue` skips just the current iteration

**Use cases:**
- `break`: Found what you're looking for (exit early)
- `continue`: Skip unwanted items but keep looping

---

**Question 4: How do you iterate over a list in Python? Show two different methods.**

**Answer:**

**Method 1: For-each loop (simplest, recommended)**
```python
names = ["Alice", "Bob", "Charlie"]
for name in names:
    print(name)
```
Use when you just need the values, not positions.

**Method 2: Index-based loop**
```python
for i in range(len(names)):
    print(f"{i}: {names[i]}")
```
Use when you need the index/position (e.g., to modify the list or track location).

**Method 3 (bonus): Using enumerate()**
```python
for i, name in enumerate(names):
    print(f"{i}: {name}")
```
Gets both index and value in one loop.

**Key insight:** For-each is cleaner when you only need values. Use index-based when you need positions.

---

**Question 5: What is a sentinel loop? How does it work?**

**Answer:**

A **sentinel loop** uses a special value (the sentinel) to signal when the loop should stop. Instead of a counter or known number of iterations, the loop depends on user input.

**Structure:**
```python
while True:
    value = input("Enter value (or 'quit'): ")
    if value == "quit":  # Sentinel
        break
    # Process value
```

**How it works:**
1. Loop runs indefinitely (`while True`)
2. Gets user input
3. Checks if the sentinel value was entered
4. If yes, exits with `break`
5. If no, processes the input and continues

**Common sentinels:**
- `"quit"`, `"done"`, `"exit"` (for strings)
- `-1`, `0` (for numbers, when negative/zero is invalid)
- `"no"` (for yes/no)

**Why useful:**
- User controls when to stop (flexible)
- Don't know in advance how much data to collect
- Real-world programs often work this way

**Example:**
```python
total = 0
while True:
    num = int(input("Number (0 to stop): "))
    if num == 0:
        break
    total += num
print(f"Sum: {total}")
```

---

## Part 2: Code Analysis & Problem-Solving

**Question 6: What will this code print? Trace through it.**

```python
for i in range(1, 4):
    for j in range(2):
        print(i * j, end=" ")
    print()
```

**Answer:**

Tracing:
- i=1: j=0 (1*0=0), j=1 (1*1=1) → prints "0 1 " then newline
- i=2: j=0 (2*0=0), j=1 (2*1=2) → prints "0 2 " then newline
- i=3: j=0 (3*0=0), j=1 (3*1=3) → prints "0 3 " then newline

**Output:**
```
0 1
0 2
0 3
```

---

**Question 7: Find the bug in this code:**

```python
count = 0
while count < 5:
    print(count)
    count += 2
```

**Answer:**

**The code runs, but it doesn't print 0, 1, 2, 3, 4.**

The code increments by 2 each time, so it prints:
```
0
2
4
```

It stops at 4 because the next iteration would be 6, which is >= 5, so the condition becomes false.

**If the goal was to print 0-4:**
```python
count = 0
while count < 5:
    print(count)
    count += 1  # Increment by 1
```

**Note:** There's not a technical "bug" if incrementing by 2 was intentional. But it's a common source of confusion.

---

**Question 8: What is the output of this code?**

```python
numbers = [3, 1, 4, 1, 5]
for num in numbers:
    if num == 1:
        continue
    print(num, end=" ")
```

**Answer:**

The `continue` statement skips the print when num is 1.

**Output:** `3 4 5`

---

**Question 9: Find the error(s) in this code:**

```python
names = ["Alice", "Bob", "Charlie"]
for name in names
    print(name)
```

**Error:** Missing colon (`:`) after `names`

**Fixed:**
```python
for name in names:
    print(name)
```

Python requires a colon after loop and conditional statements.

---

**Question 10: What does this code do? Describe in words.**

```python
text = input("Word: ")
count = 0
for char in text.lower():
    if char in "aeiou":
        count += 1
print(f"Vowels: {count}")
```

**Answer:**

This program:
1. Asks the user for a word
2. Converts it to lowercase
3. Loops through each character
4. Counts how many are vowels (a, e, i, o, u)
5. Prints the count

**Example:** If user enters "Hello", output is "Vowels: 2" (e and o)

---

## Part 3: Code Writing Questions

**Question 11: Write a while loop that asks the user for positive numbers until they enter 0. Calculate and print the sum.**

**Answer:**

```python
total = 0
while True:
    num = int(input("Number (0 to stop): "))
    if num == 0:
        break
    total += num
print(f"Sum: {total}")
```

**Alternative (without break):**
```python
num = int(input("Number (0 to stop): "))
total = 0
while num != 0:
    total += num
    num = int(input("Number (0 to stop): "))
print(f"Sum: {total}")
```

---

**Question 12: Write a for loop using range() that prints all multiples of 5 from 5 to 50.**

**Answer:**

```python
for num in range(5, 51, 5):
    print(num)
```

**Output:**
```
5
10
15
20
25
30
35
40
45
50
```

**Explanation:**
- `range(5, 51, 5)` starts at 5, goes up to 50 (51 exclusive), step of 5
- Prints: 5, 10, 15, ..., 50

---

**Question 13: Write nested loops that print a 4×4 grid like this:**
```
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
```

**Answer:**

```python
counter = 1
for row in range(4):
    for col in range(4):
        print(counter, end=" ")
        counter += 1
    print()  # Newline after each row
```

**Alternative (more compact):**
```python
for row in range(4):
    for col in range(4):
        num = row * 4 + col + 1
        print(num, end=" ")
    print()
```

---

**Question 14: Create a list, ask the user for 5 names, then print them in reverse order.**

**Answer:**

```python
names = []
for i in range(5):
    name = input(f"Name {i+1}: ")
    names.append(name)

print("Names in reverse:")
for name in reversed(names):
    print(name)
```

**Alternative (using indexing):**
```python
names = []
for i in range(5):
    name = input(f"Name {i+1}: ")
    names.append(name)

print("Names in reverse:")
for i in range(len(names)-1, -1, -1):
    print(names[i])
```

---

**Question 15: Write a program that asks the user for numbers until "done". Find and print the highest number, lowest number, and average.**

**Answer:**

```python
numbers = []
while True:
    user_input = input("Number ('done' to stop): ")
    if user_input == "done":
        break
    numbers.append(float(user_input))

if len(numbers) > 0:
    print(f"Highest: {max(numbers)}")
    print(f"Lowest: {min(numbers)}")
    print(f"Average: {sum(numbers) / len(numbers):.2f}")
else:
    print("No numbers entered.")
```

**Explanation:**
- Collects numbers in a list (sentinel pattern)
- Uses `max()`, `min()`, and `sum()` built-in functions
- Calculates average by dividing sum by count
- Checks that list isn't empty before processing

---

## Assessment Tips

**For Concept Questions:**
- Use your own words
- Give examples when asked
- Be specific about terminology
- Show understanding, not just memorization

**For Code Analysis:**
- Trace step-by-step
- Write down variable values
- Predict before running
- Look for off-by-one errors

**For Code Writing:**
- Read requirements carefully
- Include comments if logic is complex
- Test mentally or on paper first
- Check indentation and colons
- Verify variable initialization

---

## Common Mistakes to Avoid

1. **Infinite loops:** Make sure condition changes or break is reached
2. **Off-by-one errors:** `range(5)` is 0-4, not 1-4
3. **Missing colons:** Always `:` after loops, if, else
4. **Wrong indentation:** Loop body must be indented consistently
5. **Forgetting to initialize:** Variables must exist before use
6. **Type errors:** Can't mix strings and numbers in operations
7. **List index out of range:** Check bounds before accessing
8. **Confusing `break` and `continue`:** `break` exits; `continue` skips

---

## Study Checklist

Before taking the assessment:

- [ ] Can you write a while loop with a counter?
- [ ] Can you write a sentinel loop?
- [ ] Do you understand the accumulator pattern?
- [ ] Can you validate input with a loop?
- [ ] Can you write a for loop with range()?
- [ ] Do you understand range(start, stop, step)?
- [ ] Can you iterate over lists and strings?
- [ ] Do you know when to use break and continue?
- [ ] Can you write and trace nested loops?
- [ ] Can you find min/max in a list?
- [ ] Can you search for a value in a list?
- [ ] Do you know list methods (.append, .remove, .sort)?
- [ ] Can you trace code and predict output?
- [ ] Can you identify common bugs?
- [ ] Can you write complete programs combining multiple concepts?

---

## Good Luck!

You've worked hard on Unit 4. Remember:
- Read questions carefully
- Show your work
- Trace code before running it
- Test with multiple inputs
- Ask for help if stuck

**You've got this!**

---
