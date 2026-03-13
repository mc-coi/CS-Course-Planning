# Day 8: Data Analysis Basics
**Learning Target:** I can calculate statistics from file data.

### Key Concepts
Basic statistics: mean, median, mode, standard deviation, min, max, sorting.

### Code Examples
```python
def analyze_numbers(numbers):
    # Mean
    mean = sum(numbers) / len(numbers)

    # Median (middle value)
    sorted_nums = sorted(numbers)
    n = len(sorted_nums)
    median = sorted_nums[n // 2] if n % 2 else (sorted_nums[n//2 - 1] + sorted_nums[n//2]) / 2

    # Mode (most frequent)
    from collections import Counter
    mode = Counter(numbers).most_common(1)[0][0]

    # Min/Max
    min_val = min(numbers)
    max_val = max(numbers)

    # Range
    range_val = max_val - min_val

    return {"mean": mean, "median": median, "mode": mode, "min": min_val, "max": max_val, "range": range_val}

# Using with files
import csv
grades = []
with open("grades.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        grades.append(float(row["Grade"]))

stats = analyze_numbers(grades)
print(f"Average: {stats['mean']:.2f}")
print(f"Median: {stats['median']:.2f}")
```

### Guided Practice
Read CSV of student grades, calculate statistics.

### Practice Problems
**Problem 1 — Beginner:** Calculate mean of a list.

**Problem 2 — Intermediate:** Calculate mean, median, mode.

**Problem 3 — Challenge:** Create comprehensive statistics report from file data.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
numbers = [1, 2, 3, 4, 5]
mean = sum(numbers) / len(numbers)

# Problem 2 (shown above)
```
</details>

---

---
