# Day 42: Review — Practice Problems and Code Tracing

**Learning Target:** I can solve Unit 2 practice problems and trace code to predict output.

### Practice Problem Set

**Tier 1: Beginner (10 problems)**

1. **Variable Basics:** Create a variable `score = 100`, reassign it to `150`, and print it.

2. **Arithmetic:** Calculate `(10 + 5) * 2 - 8`. Show the order of operations.

3. **String Creation:** Concatenate `"Hello" + ", " + "World"`.

4. **Indexing:** Given `word = "Python"`, print `word[0]`, `word[-1]`, and `word[2]`.

5. **Length:** What is `len("Programming")`?

6. **Slicing:** What does `"Hello"[1:3]` return?

7. **Type Conversion:** Convert `"42"` to an integer and add 8.

8. **String Methods:** What does `"HELLO".lower()` return?

9. **Comparison:** Is `5 < 10` True or False?

10. **F-string:** Format `9.5` as currency: `f"${9.5:.2f}"`.

**Tier 2: Intermediate (10 problems)**

11. **Compound Assignment:** Start with `x = 20`. Show the result of `x += 5`, `x -= 3`, `x *= 2`.

12. **Slicing with Step:** What does `"Python"[::2]` return?

13. **String Methods Chain:** What does `"  HELLO  ".strip().lower()` return?

14. **Multiple Assignment:** After `a, b = 10, 20` and `a, b = b, a`, what are the values?

15. **Operator Precedence:** What is `2 + 3 * 4 - 5`?

16. **Type Conversion:** Convert `3.7` to an integer using `int()`. What is the result?

17. **Math Calculations:** Calculate the area of a circle with radius 5 (use π ≈ 3.14159).

18. **String Finding:** What is the result of `"banana".find("an")`?

19. **Boolean Comparison:** What does `"apple" < "banana"` return?

20. **F-string with Alignment:** Right-align `"Python"` in 10 characters: `f"{'Python':>10}"`.

**Tier 3: Challenge (5 problems)**

21. **Code Trace:** Predict the output:
    ```python
    text = "CodeIsArt"
    print(text[4:7])
    print(text[-3:])
    print(text[::3])
    ```

22. **Complex Expression:** Calculate `result = 10 + 5 * 2 ** 2 - (8 / 2)`. Show your work.

23. **String Manipulation:** If `name = "alice"`, what is `name.title() + name[1:]`?

24. **Type Conversion Error:** Why would `int("3.5")` cause an error? How would you fix it?

25. **Program Logic:** Write code that asks for a price, calculates 8% tax, and displays formatted total.

### Code Tracing Exercises

**Exercise 1: Simple Trace**
```python
x = 10
y = 3
print(x + y)     # ?
print(x * y)     # ?
print(x / y)     # ?
print(x // y)    # ?
print(x % y)     # ?
```

**Exercise 2: String Trace**
```python
word = "Computer"
print(word[0])       # ?
print(word[-2])      # ?
print(word[1:4])     # ?
print(word[::-1])    # ?
print(len(word))     # ?
```

**Exercise 3: Method Trace**
```python
text = "  PYTHON IS FUN  "
print(text.strip())           # ?
print(text.strip().lower())   # ?
print(text.count("P"))        # ?
print(text.find("IS"))        # ?
```

**Exercise 4: Conversion Trace**
```python
price = "19.99"
quantity = "5"
price_float = float(price)
quantity_int = int(quantity)
total = price_float * quantity_int
print(f"${total:.2f}")        # ?
```

**Exercise 5: Complex Trace**
```python
a = 5
b = 2
c = a + b * 2
d = (a + b) * 2
print(f"c = {c}")  # ?
print(f"d = {d}")  # ?
print(c == d)      # ?
```

### Answer Key

**Tier 1:**
1. `150`
2. `(10+5)*2 - 8 = 15*2 - 8 = 30 - 8 = 22`
3. `"Hello, World"`
4. `"P"`, `"n"`, `"t"`
5. `11`
6. `"el"`
7. `42 + 8 = 50`
8. `"hello"`
9. `True`
10. `"$9.50"`

**Tier 2:**
11. `x += 5` → `25`; `x -= 3` → `22`; `x *= 2` → `44`
12. `"Pto"` (indices 0, 2, 4)
13. `"hello"`
14. `a = 20`, `b = 10`
15. `2 + 12 - 5 = 9`
16. `3` (truncates, doesn't round)
17. `3.14159 * 25 ≈ 78.54`
18. `1` (index where "an" starts)
19. `True` (alphabetically)
20. `"    Python"`

**Tier 3:**
21. `"Is"`, `"Art"`, `"Caart"` (wait, let me recalculate: `text[::3]` is indices 0, 3, 6, 9 → `"C"`, `"e"`, `"A"`, `"t"` → `"CeAt"`)
22. `10 + 5*4 - 4 = 10 + 20 - 4 = 26`
23. `"Alice" + "lice" = "Alicelice"`
24. Can't convert string with decimal directly; use `float("3.5")` first, then `int()` if needed
25. (See solution below)

<details>
<summary>✅ Solution for Problem 25</summary>

```python
price = float(input("Price: $"))
tax = price * 0.08
total = price + tax
total = round(total, 2)
print(f"Price: ${price:.2f}")
print(f"Tax: ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

</details>

### Self-Assessment

Rate yourself on each topic (1-5, where 5 = mastery):

- [ ] Variable assignment and reassignment (___/5)
- [ ] Data types: int, float, string, bool (___/5)
- [ ] Arithmetic operators and precedence (___/5)
- [ ] String indexing and slicing (___/5)
- [ ] String methods (___/5)
- [ ] Type conversion (___/5)
- [ ] Comparison operators and Boolean (___/5)
- [ ] F-string formatting (___/5)
- [ ] Math module (___/5)
- [ ] Building multi-step programs (___/5)

**If you scored 4-5 on all topics, you're ready for the assessment!**

**If you scored 1-3 on any topic, review that section before Day 44.**

