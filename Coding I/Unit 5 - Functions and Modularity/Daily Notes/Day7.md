# Day 7: Default Parameters & Multiple Returns

### Key Concepts
- **Default parameter:** A parameter with a pre-set value if no argument is given
- **Multiple return values:** A function can return multiple values as a tuple
- You can unpack returned tuples directly into separate variables

### Code Examples

```python
# ── Default parameters ─────────────────────────────────────
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")              # Hello, Alice!  (uses default)
greet("Bob", "Good morning")  # Good morning, Bob!  (overrides default)
greet("Carlos", "Hola")    # Hola, Carlos!

# ── Multiple defaults ──────────────────────────────────────
def create_profile(name, grade=9, sport="none", gpa=0.0):
    print(f"Name: {name}, Grade: {grade}, Sport: {sport}, GPA: {gpa}")

create_profile("Destiny")
create_profile("Marcus", grade=11)
create_profile("Priya", 10, "soccer", 3.9)
create_profile("Jordan", sport="basketball", gpa=3.5)

# Default params must come AFTER required params
# def bad(default=5, required):  ← SyntaxError!

# ── Returning multiple values ──────────────────────────────
def min_max(numbers):
    return min(numbers), max(numbers)    # returns a tuple

result = min_max([3, 1, 7, 2, 8])
print(result)           # (1, 8)
print(type(result))     # <class 'tuple'>

# ── Unpacking the tuple ────────────────────────────────────
low, high = min_max([3, 1, 7, 2, 8])
print(f"Min: {low}, Max: {high}")   # Min: 1, Max: 8

# ── Real-world example ─────────────────────────────────────
def analyze_scores(scores):
    total = sum(scores)
    average = total / len(scores)
    highest = max(scores)
    lowest = min(scores)
    passing = sum(1 for s in scores if s >= 70)
    return average, highest, lowest, passing

grades = [85, 92, 78, 55, 90, 67, 88]
avg, hi, lo, passed = analyze_scores(grades)
print(f"Average: {avg:.1f}")
print(f"Highest: {hi}, Lowest: {lo}")
print(f"Passing: {passed}/{len(grades)}")

# ── Divmod: built-in multiple return ──────────────────────
quotient, remainder = divmod(17, 5)
print(f"17 ÷ 5 = {quotient} remainder {remainder}")   # 3 remainder 2
```

### Practice Problems — Day 7

**Beginner:**
1. Write `power(base, exponent=2)` that returns `base ** exponent`. Test with both one and two arguments.
2. Write `get_range(numbers)` that returns both the minimum and maximum of a list as a tuple.

**Intermediate:**

3. Write `split_list(items, split_point=None)` where if `split_point` is `None`, it splits at the midpoint. Return two lists.
4. Write `stats(numbers)` that returns a tuple of (mean, median, mode). Use a helper function for each.

**Challenge:**

5. Write `parse_name(full_name)` that returns `(first, middle, last)` handling names with 2 words (no middle name — return `""` for middle) and 3+ words. Test with `"John Doe"`, `"Mary Jane Watson"`, and `"Cher"`.

---