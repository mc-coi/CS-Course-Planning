# Day 5: break & continue
**Learning Target:** I can use break and continue to control loop flow.

### Key Concepts
- **break:** Exits the loop immediately
- **continue:** Skips the rest of the current iteration, goes to next iteration
- **for/else:** Else block runs if loop completes without break

### Code Examples
```python
# break — exit when found
for i in range(1, 101):
    if i % 7 == 0 and i % 11 == 0:
        print(f"Found: {i}")
        break  # Exit loop

# continue — skip multiples of 3
for i in range(1, 11):
    if i % 3 == 0:
        continue  # Skip to next iteration
    print(i)  # Prints 1,2,4,5,7,8,10

# for/else — runs if no break
for i in range(2, 20):
    if 20 % i == 0:
        print(f"{i} divides 20")
        break
else:
    print("20 is prime")  # Only if no break occurred
```

### Guided Practice
Write a program that finds the first number divisible by both 3 and 5 starting from 1.

### Practice Problems
**Problem 1 — Beginner:** Print numbers 1-20, skip multiples of 5 using continue.

**Problem 2 — Intermediate:** Find the first number greater than 100 that's prime, exit with break.

**Problem 3 — Challenge:** Search for a user's name in a list; break when found, print "Found" or "Not found".

<details>
<summary>💡 Hints</summary>

- Problem 1: Use `if i % 5 == 0: continue`
- Problem 2: Check if any number < i divides it
- Problem 3: Use break when name matches, with for/else for "not found"
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
for i in range(1, 21):
    if i % 5 == 0:
        continue
    print(i)

# Problem 3
names = ["Alice", "Bob", "Charlie"]
search = input("Search for: ")
for name in names:
    if name == search:
        print("Found!")
        break
else:
    print("Not found")
```
</details>

---