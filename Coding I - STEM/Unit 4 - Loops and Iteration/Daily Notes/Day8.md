# Day 8: FizzBuzz & Review
**Learning Target:** I can trace loop execution and solve classic loop problems.

### Key Concepts
**FizzBuzz** is a classic programming problem: print 1-100, but:
- Multiples of 3: print "Fizz"
- Multiples of 5: print "Buzz"
- Multiples of both: print "FizzBuzz"
- Otherwise: print the number

### Code Examples
```python
# FizzBuzz
for i in range(1, 101):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)

# Number pyramid
for i in range(1, 6):
    print(str(i) * i)  # 1, 22, 333, 4444, 55555

# Print numbers in order (review for/while choice)
for i in range(10):
    print(i, end=" ")  # for loop — fixed count
```

### Practice Problems
**Problem 1 — Beginner:** Implement basic FizzBuzz (multiples of 3 only).

**Problem 2 — Intermediate:** Implement full FizzBuzz as described.

**Problem 3 — Challenge:** Extend FizzBuzz: add "Bazz" for multiples of 7.

---