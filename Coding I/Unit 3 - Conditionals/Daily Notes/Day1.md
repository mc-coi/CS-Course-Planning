# Day 1: Boolean Expressions
**Learning Target:** I can evaluate Boolean expressions and understand comparison operators.

### Key Concepts
A **Boolean expression** is any expression that evaluates to True or False. Comparison operators create Boolean results:
- `==` equal to
- `!=` not equal to
- `>` greater than
- `<` less than
- `>=` greater than or equal to
- `<=` less than or equal to

Strings are compared **alphabetically** (lexicographically): "apple" < "banana" is True because "a" comes before "b".

### Code Examples
```python
# Numeric comparisons
print(5 > 3)        # True
print(5 < 3)        # False
print(5 == 5)       # True
print(5 != 3)       # True
print(10 >= 10)     # True
print(10 <= 9)      # False

# String comparisons
print("apple" < "banana")   # True (alphabetical)
print("zebra" > "apple")    # True
print("hello" == "hello")   # True

# Variable comparisons
age = 17
print(age >= 16)    # True (can vote)

score = 85
print(score > 90)   # False (not an A)

# Type of comparison
is_student = (age < 18)  # True
print(type(is_student))  # <class 'bool'>
```

### Guided Practice
Write expressions that check:
1. Is 100 greater than 50?
2. Is "python" equal to "Python"?
3. Is 3.14 less than or equal to 3.14?
4. Is a given age greater than or equal to 18?

### Practice Problems
**Problem 1 — Beginner:** Write 5 comparison expressions and predict their output before running.

```python
# Starter code
print()
print()
print()
print()
print()
```

**Problem 2 — Intermediate:** Compare strings: "apple", "banana", "apricot". Which is largest? Which is smallest?

**Problem 3 — Challenge:** Predict the output of each: `5 > 3 == True`, `"5" > "3"`, `len("hi") > 1`

<details>
<summary>💡 Hints</summary>

- Problem 1: Mix numbers and strings
- Problem 2: Remember alphabetical comparison
- Problem 3: String "5" and "3" compare alphabetically, not numerically
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
print(10 > 5)              # True
print("cat" < "dog")       # True
print(3.5 <= 3.5)          # True
print(100 != 99)           # True
print("hello" == "hello")  # True
```
</details>

---