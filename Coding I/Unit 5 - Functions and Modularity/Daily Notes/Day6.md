# Day 6: Functions with Lists

### Key Concepts
- Lists can be passed as arguments just like numbers and strings
- Functions can process, filter, transform, and analyze list data
- Returning a new list is cleaner than modifying the original (in most cases)
- You can build list-processing functions that work for any list

### Code Examples

```python
# ── Pass a list to a function ──────────────────────────────
def print_all(items):
    for item in items:
        print(f"  - {item}")

fruits = ["apple", "banana", "cherry"]
print_all(fruits)

# ── Calculate stats on a list ──────────────────────────────
def list_sum(numbers):
    total = 0
    for n in numbers:
        total += n
    return total

def list_average(numbers):
    if len(numbers) == 0:
        return 0
    return list_sum(numbers) / len(numbers)

def list_max(numbers):
    biggest = numbers[0]
    for n in numbers:
        if n > biggest:
            biggest = n
    return biggest

def list_min(numbers):
    smallest = numbers[0]
    for n in numbers:
        if n < smallest:
            smallest = n
    return smallest

scores = [85, 92, 78, 95, 88, 73, 90]
print(f"Sum:     {list_sum(scores)}")
print(f"Average: {list_average(scores):.1f}")
print(f"Max:     {list_max(scores)}")
print(f"Min:     {list_min(scores)}")

# ── Return a new filtered list ─────────────────────────────
def passing_scores(scores, threshold=70):
    passing = []
    for s in scores:
        if s >= threshold:
            passing.append(s)
    return passing

grades = [55, 82, 70, 91, 44, 78, 65]
print(passing_scores(grades))        # [82, 70, 91, 78]
print(passing_scores(grades, 80))    # [82, 91]

# ── Modify a list in-place ─────────────────────────────────
def double_all(numbers):
    for i in range(len(numbers)):
        numbers[i] *= 2   # modifies the original list!

data = [1, 2, 3, 4, 5]
double_all(data)
print(data)    # [2, 4, 6, 8, 10]

# ── Return a transformed version (no mutation) ─────────────
def doubled_copy(numbers):
    return [n * 2 for n in numbers]

original = [1, 2, 3, 4, 5]
new_list = doubled_copy(original)
print(original)   # [1, 2, 3, 4, 5]  (unchanged)
print(new_list)   # [2, 4, 6, 8, 10]
```

### Practice Problems — Day 6

**Beginner:**
1. Write `count_evens(numbers)` that returns how many even numbers are in the list.
2. Write `all_caps(words)` that returns a new list with every string converted to uppercase.

**Intermediate:**

3. Write `remove_negatives(numbers)` that returns a new list with all negative numbers removed.
4. Write `grade_stats(scores)` that prints the average, highest, lowest, and number of passing scores (≥70) for a list of grades.

**Challenge:**

5. Write `normalize(numbers)` that returns a new list where every number is scaled to a 0–100 range: `normalized = (value - min) / (max - min) * 100`. Handle the case where all numbers are the same.

<details>
<summary>✅ Answer for #5</summary>

```python
def normalize(numbers):
    mn = min(numbers)
    mx = max(numbers)
    if mx == mn:
        return [50.0] * len(numbers)  # all same, use midpoint
    return [(n - mn) / (mx - mn) * 100 for n in numbers]

print(normalize([10, 20, 30, 40, 50]))
# [0.0, 25.0, 50.0, 75.0, 100.0]
```
</details>

---