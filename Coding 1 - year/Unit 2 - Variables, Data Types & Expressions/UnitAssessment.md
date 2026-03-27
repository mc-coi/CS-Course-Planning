# Unit 2 Assessment Review Questions (15 Q&As)

## Part 1: Conceptual Questions (Short Answer, 2-3 sentences)

**Q1: Explain the difference between `=` and `==`. Give an example of when you'd use each.**

A: `=` is the assignment operator that gives a variable a value; `==` is the comparison operator that checks if two values are equal and returns True or False. Example: `age = 25` assigns 25 to the variable age; `if age == 25:` checks if age equals 25.

---

**Q2: Why does `10 / 2` return `5.0` instead of `5` in Python 3? What operator would you use if you wanted an integer result?**

A: In Python 3, the `/` operator always performs floating-point division, which returns a float type. To get an integer result without decimals, use the `//` operator for floor division: `10 // 2` returns `5`.

---

**Q3: What is string indexing, and why is it important that indexing starts at 0?**

A: String indexing accesses individual characters within a string using bracket notation (e.g., `word[0]`). Indexing starting at 0 is a computer science convention that affects how we extract characters—the first character is at index 0, not 1. This requires careful calculation when manipulating strings.

---

**Q4: Describe string slicing [start:stop:step] and explain what each component means.**

A: String slicing extracts a portion of a string using [start:stop:step]. Start is the beginning index (inclusive), stop is the ending index (exclusive, not included), and step is how many positions to skip. For example, `"Python"[1:4]` gives "yth" (indices 1, 2, 3).

---

**Q5: Name three string methods and explain what each does.**

A: `.upper()` converts all letters to uppercase; `.lower()` converts to lowercase; `.strip()` removes leading and trailing whitespace; `.replace(old, new)` replaces all occurrences of a substring; `.find(sub)` returns the index where a substring first appears.

---

**Q6: What is type conversion and why is it necessary in programming?**

A: Type conversion changes a value from one data type to another using functions like `int()`, `float()`, `str()`. It's necessary because operations often require matching types—for example, you can't concatenate a string with a number, so you must convert: `"Score: " + str(100)`.

---

**Q7: What does an f-string do, and how would you use it to display a price with exactly 2 decimal places?**

A: An f-string (formatted string literal) allows you to embed variables and expressions directly in strings using `f"..."` syntax. To display a price with 2 decimals: `price = 9.5; print(f"${price:.2f}")` outputs `"$9.50"`.

---

**Q8: Explain why this is wrong: `s[0] = "x"`. How would you correctly modify the first character of a string?**

A: Strings are immutable (unchangeable) in Python, so you cannot modify a character at an index—trying this causes an error. Instead, reassign the variable to a new string: `s = "x" + s[1:]` or use string methods like `s.replace(s[0], "x")`.

---

**Q9: What does operator precedence mean, and what is the correct order (give the acronym)?**

A: Operator precedence determines which operations are evaluated first in an expression. The order is PEMDAS: Parentheses, Exponents, Multiplication/Division (left-to-right), Addition/Subtraction (left-to-right). For example, `2 + 3 * 4` equals 14 because multiplication happens before addition.

---

**Q10: What are the three values that can go in a slice [start:stop:step], and what does each default to if omitted?**

A: Start defaults to 0 (beginning of string), stop defaults to the length of the string (end), and step defaults to 1 (consecutive characters). For example, `word[:]` returns the whole word, and `word[::2]` returns every 2nd character starting from index 0.

---

## Part 2: Code Tracing (Predict Output)

**Q11: What does this code print?**
```python
word = "Python"
print(word[0])
print(word[-1])
print(word[1:4])
print(word[::-1])
```

A:
```
P
n
yth
nohtyP
```

---

**Q12: What does this code print?**
```python
x = 10
y = 3
x = x + y
y = x - y
x = x - y
print(x, y)
```

A: `3 10` (This swaps the values: x becomes 3, y becomes 10)

---

**Q13: What does this code print?**
```python
text = "  HELLO WORLD  "
print(text.strip().lower())
print(text.count("L"))
print(text.find("WORLD"))
```

A:
```
hello world
2
9
```

---

**Q14: What does this code print?**
```python
a = 5
b = 2
result = a + b * 2 - (8 / 2)
print(result)
```

A: `5.0` (Calculation: 5 + 4 - 4.0 = 5.0; note division returns float)

---

**Q15: What does this code print?**
```python
import math
radius = 2
area = math.pi * radius ** 2
print(f"Area: {area:.1f}")
```

A: `Area: 12.6` (π × 2² ≈ 12.566... rounded to 1 decimal place)

---

## Study Guide Summary

### Key Concepts You Should Know:
1. ✓ Data types: int, float, str, bool
2. ✓ Variables: declaration, reassignment, multiple assignment
3. ✓ Operators: arithmetic, comparison, assignment, compound assignment
4. ✓ Strings: concatenation, repetition, indexing, slicing, methods
5. ✓ Type conversion: when and how to use int(), float(), str(), bool()
6. ✓ F-strings: formatting with decimals, alignment, currency
7. ✓ Math module: sqrt(), pi, ceil(), floor()
8. ✓ Operator precedence: PEMDAS
9. ✓ Input validation: checking user input before using it
10. ✓ Building complete programs: combining concepts

### Common Pitfalls to Avoid:
- [ ] Using `=` instead of `==`
- [ ] Forgetting that `/` returns float
- [ ] Starting indices at 1 instead of 0
- [ ] Including the stop index in slices
- [ ] Trying to modify strings with indexing
- [ ] Concatenating strings with numbers
- [ ] Forgetting `.strip()` on input()
- [ ] Confusing negative indices

### If You Get Questions Wrong on the Assessment:

1. **Multiple choice you got wrong:** Review that vocabulary term in the Unit 2 hyperbook
2. **Code tracing you got wrong:** Practice more tracing problems; work step-by-step
3. **Short answer you got wrong:** Write out the explanation in your own words; explain aloud to someone
4. **Code writing you got wrong:** Rewrite the program; test it with different inputs; trace through it

### When You're Ready:

✓ Review all 15 Q&As in this document
✓ Complete Practice Problems (problems 1-25)
✓ Trace code from Day 42
✓ Do a final review using the Reference Guide
✓ Get a good night's sleep before the assessment
✓ Trust your preparation and do your best!

---

## Assessment Tips

- **Read questions carefully.** Take time to understand what's being asked.
- **Work through problems step-by-step.** Don't rush; show your work.
- **Double-check your syntax.** Python is picky about capitalization, quotes, colons.
- **Test your logic.** Does the answer make sense?
- **Manage your time.** Don't spend too long on one question; come back to it.
- **Answer all questions.** Even if you're unsure, make your best attempt.

---

**You've got this! Unit 2 is comprehensive, but you've covered all the material. Go show what you know!**
