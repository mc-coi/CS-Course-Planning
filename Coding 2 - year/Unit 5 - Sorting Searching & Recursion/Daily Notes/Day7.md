# Day 7: Binary Search Applications & Edge Cases

**Learning Target:** I can apply binary search to real-world problems and handle edge cases correctly.

---

## Key Concepts

**Edge Cases** in Binary Search:
- Empty list
- Single element
- Target not in list
- Duplicate values (what should we return?)
- Partially sorted data (breaks algorithm)

**Real-World Applications:**
- Dictionary lookup (find a word)
- Debugging (binary search for the breaking change)
- Range queries (find all values in a range)
- Game state search (chess engines)

**Variant: Finding Boundaries**
- Find FIRST occurrence of a value (useful if there are duplicates)
- Find LAST occurrence of a value
- Find smallest value >= target
- Find largest value <= target

---

## Code Examples

```python
# Robust binary search with edge case handling
def binary_search_safe(arr, target):
    """Handle empty lists and None values."""
    if not arr:  # Empty list
        return -1

    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1

# Find FIRST occurrence (leftmost index)
def binary_search_first(arr, target):
    """Find the leftmost index of target."""
    if not arr:
        return -1

    left = 0
    right = len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid  # Remember this, but keep searching left
            right = mid - 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result

# Find LAST occurrence (rightmost index)
def binary_search_last(arr, target):
    """Find the rightmost index of target."""
    if not arr:
        return -1

    left = 0
    right = len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid  # Remember this, but keep searching right
            left = mid + 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result

# Test duplicates
numbers = [1, 2, 2, 2, 3, 4, 5]
print(binary_search_first(numbers, 2))  # Output: 1 (first occurrence)
print(binary_search_last(numbers, 2))   # Output: 3 (last occurrence)

# Practical: searching a sorted student list by ID
class Student:
    def __init__(self, id, name):
        self.id = id
        self.name = name

def binary_search_students(students, target_id):
    """Binary search on sorted list of students by ID."""
    left = 0
    right = len(students) - 1

    while left <= right:
        mid = (left + right) // 2
        if students[mid].id == target_id:
            return students[mid]
        elif students[mid].id < target_id:
            left = mid + 1
        else:
            right = mid - 1

    return None

# Test
roster = [
    Student(101, "Alice"),
    Student(102, "Bob"),
    Student(103, "Charlie"),
    Student(105, "Diana")
]

found = binary_search_students(roster, 103)
if found:
    print(f"Found: {found.name} (ID: {found.id})")
```

---

## Guided Practice

**Step 1:** Test `binary_search_safe` with:
- An empty list: `[]`
- A single element: `[5]`
- A list where target is not found: `[1, 2, 3, 4, 5]` searching for 6

**Step 2:** Use `binary_search_first` and `binary_search_last` on `[10, 20, 20, 20, 30, 40]` searching for 20. What's the difference in results?

**Step 3:** Explain: What would happen if you used regular binary search on data with duplicates? Would it always find the first occurrence? Try it!

**Step 4:** Design a test suite for binary search. What are the minimum number of test cases needed to verify correctness?

---

## Practice Problems

**Beginner:** Write a function that checks if a value exists in a sorted list using binary search. Return True/False instead of an index.

**Intermediate:** Given a sorted list with some duplicate values, write a function that returns the COUNT of how many times a target value appears. Use binary search to find the first and last occurrence.

**Challenge:** Implement a "ceiling" function: `binary_search_ceiling(arr, target)` returns the index of the smallest value >= target. For example, in `[1, 3, 5, 7]` searching for 4 should return index 2 (value 5).

<details>
<summary>💡 Hints</summary>
- **Beginner:** Just return the result of binary search > -1 (or == -1 for True/False).
- **Intermediate:** Once you have first and last indices, count = last - first + 1.
- **Challenge:** If you find the target, return its index. If not found, `right` will be at the position just before where the target would be, so `left` is where it should be.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def exists(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return False

# Intermediate
def count_occurrences(arr, target):
    first = binary_search_first(arr, target)
    if first == -1:
        return 0
    last = binary_search_last(arr, target)
    return last - first + 1

print(count_occurrences([1, 2, 2, 2, 3], 2))  # Output: 3

# Challenge
def binary_search_ceiling(arr, target):
    """Find smallest value >= target."""
    left = 0
    right = len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] >= target:
            result = mid
            right = mid - 1  # Try to find even smaller value
        else:
            left = mid + 1

    return result

# Test
print(binary_search_ceiling([1, 3, 5, 7], 4))  # Output: 2 (value 5)
print(binary_search_ceiling([1, 3, 5, 7], 1))  # Output: 0 (value 1)
```
</details>
