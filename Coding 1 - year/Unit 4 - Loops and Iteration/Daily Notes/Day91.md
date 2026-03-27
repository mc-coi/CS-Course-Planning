# Day 91: Review — While Loops and For Loops

**Learning Target:** I can review and reinforce my understanding of while and for loops, choosing the right loop for the task.

### Key Concepts Review

**While Loops:** Repeat while a condition is true.
```python
counter = 0
while counter < 5:
    print(counter)
    counter += 1
```

**Patterns:**
- Counter: increment/decrement to control iterations
- Sentinel: special value signals exit
- Accumulator: collect/combine values
- Validation: ensure valid input

**For Loops:** Repeat a known number of times, or iterate over a sequence.
```python
for i in range(5):           # 0-4
    print(i)

for name in names:           # Each element
    print(name)
```

**Choosing the right loop:**
- For loop: known iterations, iterating over sequences
- While loop: user input, sentinel, changing conditions

---

### Practice Problems

**Problem 1 — Beginner:** Write a while loop that asks for numbers until the user enters 0, then prints the sum.

**Problem 2 — Intermediate:** Write a for loop that asks the user for a number N, then prints all multiples of N up to 100.

**Problem 3 — Challenge:** Write a program that uses both while and for loops:
- While loop: ask for names until "done"
- For loop: print each name with a number

<details>
<summary>✅ Solutions</summary>

```python
# Problem 1
total = 0
while True:
    num = int(input("Number (0 to stop): "))
    if num == 0:
        break
    total += num
print(f"Sum: {total}")

# Problem 2
n = int(input("Number: "))
for multiple in range(n, 101, n):
    print(multiple)

# Problem 3
names = []
while True:
    name = input("Name ('done' to stop): ")
    if name == "done":
        break
    names.append(name)

for i in range(len(names)):
    print(f"{i+1}: {names[i]}")
```

</details>

---

### Self-Assessment

Check your understanding:
- [ ] Can you write a while loop with a counter?
- [ ] Can you write a sentinel loop (until special value)?
- [ ] Can you use the accumulator pattern (sum, count)?
- [ ] Can you validate input with a loop?
- [ ] Can you write a for loop with range()?
- [ ] Can you iterate over a list with for-each?
- [ ] Can you choose between for and while appropriately?

---

### Common Mistakes to Avoid

1. **Infinite loop:** Make sure condition eventually becomes false or break is reached
2. **Off-by-one error:** Remember range(5) is 0-4, not 1-5
3. **Forgetting loop body indentation:** Indentation matters in Python
4. **Not updating condition:** Counter must change to exit loop
5. **Wrong comparison:** Use `<` not `<=` (or vice versa) deliberately

---
