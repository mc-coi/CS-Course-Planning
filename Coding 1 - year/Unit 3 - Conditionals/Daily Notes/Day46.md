# Day 46: Boolean Expressions & Comparison Operators

**Learning Target:** I can evaluate Boolean expressions and understand comparison operators (==, !=, <, >, <=, >=).

---

## Key Concepts

A **Boolean expression** is any expression that evaluates to either `True` or `False`. These are the foundation of all decision-making in programs.

**Comparison operators** create Boolean results:
- `==` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

**Important:** In Python, `=` is assignment, but `==` is comparison. They are NOT the same!

Strings are compared **alphabetically** (lexicographically): `"apple" < "banana"` is True because "a" comes before "b" in the alphabet.

---

## Code Examples

```python
# Numeric comparisons
print(5 > 3)           # True
print(5 < 3)           # False
print(5 == 5)          # True
print(5 != 3)          # True
print(10 >= 10)        # True
print(10 <= 9)         # False

# String comparisons (alphabetical)
print("apple" < "banana")   # True (a comes before b)
print("zebra" > "apple")    # True (z comes after a)
print("hello" == "hello")   # True (exact match)
print("cat" != "dog")       # True (different)

# Variable comparisons
age = 17
print(age >= 16)       # True

score = 85
print(score > 90)      # False (not an A)

# Type of comparison — result is a Boolean
is_student = (age < 18)
print(type(is_student))    # <class 'bool'>

# Chaining comparisons (Pythonic!)
x = 50
print(1 <= x <= 100)   # True (equivalent to: x >= 1 and x <= 100)
```

---

## Guided Practice (15 minutes)

**Activity:** Prediction Game

1. Write these expressions and predict their output BEFORE running:
   ```python
   print(7 > 5)
   print(10 == 10)
   print("dog" > "cat")
   print(100 != 100)
   print(3.5 <= 3.5)
   ```

2. Compare strings: `"apple"`, `"banana"`, `"apricot"`. Which is largest alphabetically? Which is smallest?

3. Write expressions to check:
   - Is 100 greater than or equal to 50?
   - Is "python" equal to "Python"? (Hint: case matters!)
   - Is your age greater than 17?

**Discussion:** Why is "python" != "Python"? What does case sensitivity mean?

---

## Practice Problems

### Problem 1 — Beginner
Write 5 comparison expressions using numbers and strings. Predict the output before running, then verify.

```python
# Starter code
print()
print()
print()
print()
print()
```

**Requirement:** Mix numeric and string comparisons. Include at least one inequality (!=).

---

### Problem 2 — Intermediate
Compare the three strings: "apple", "banana", "apricot". Write print statements to:
1. Determine which is smallest alphabetically
2. Determine which is largest alphabetically
3. Check if "apricot" is between "apple" and "banana"

**Hint:** Use comparison operators and remember alphabetical ordering.

---

### Problem 3 — Challenge
Predict the output of each expression. Explain your reasoning:

```python
print(5 > 3 == True)
print("5" > "3")
print(len("hi") > 1)
print((10 > 5) == True)
print("abc" < "abd")
```

**Challenge:** Why does `"5" > "3"` give a different result than `5 > 3`?

---

## Hints

- **Problem 1:** Try mixing numbers, strings, and comparisons. What happens when you compare a number to a string?
- **Problem 2:** Remember alphabetical (lexicographic) order: "a" < "b" < "c", etc.
- **Problem 3:** Think about string comparison character-by-character. What about when comparing integers to Booleans?

---

## Sample Answers

### Problem 1 Example
```python
print(10 > 5)              # True
print("cat" < "dog")       # True
print(3.5 <= 3.5)          # True
print(100 != 99)           # True
print("hello" == "hello")  # True
```

### Problem 2 Example
```python
# Smallest: "apple"
print("apple" < "apricot" and "apple" < "banana")  # True

# Largest: "banana"
print("banana" > "apple" and "banana" > "apricot")  # True

# "apricot" between "apple" and "banana"?
print("apple" < "apricot" and "apricot" < "banana")  # True
```

### Problem 3 Example
```python
print(5 > 3 == True)    # True (5>3 is True, True==True is True)
print("5" > "3")        # True (string comparison: "5" comes after "3" in ASCII)
print(len("hi") > 1)    # True (length is 2, 2>1 is True)
print((10 > 5) == True) # True (10>5 is True, True==True is True)
print("abc" < "abd")    # True (both start with "ab", but "c"<"d")
```

---

## Key Takeaway

Boolean expressions are True or False. Comparison operators let you compare values and create Boolean expressions. These are the building blocks for conditional statements coming next!
