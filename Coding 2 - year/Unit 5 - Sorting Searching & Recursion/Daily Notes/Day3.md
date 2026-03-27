# Day 3: Linear Search Algorithm

**Learning Target:** I can implement linear search and analyze its time complexity.

---

## Key Concepts

**Linear Search**: Checking each element in a list one by one until you find the target or reach the end. Also called **sequential search**.

**Time Complexity**:
- **Best case:** O(1) — target is the first element
- **Average case:** O(n) — target is somewhere in the middle
- **Worst case:** O(n) — target is at the end or not in the list

**When to use:** Small lists, unsorted data, or when you only search once.

**When NOT to use:** Large lists that don't change (use binary search instead).

---

## Code Examples

```python
# Iterative Linear Search
def linear_search(arr, target):
    """
    Search for target in arr using linear search.
    Returns the index if found, -1 if not found.
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Found it!
    return -1  # Never found it

# Test
scores = [45, 78, 23, 89, 56, 92, 34]
print(linear_search(scores, 89))    # Output: 3
print(linear_search(scores, 50))    # Output: -1

# With counting comparisons (to understand efficiency)
def linear_search_with_count(arr, target):
    comparisons = 0
    for i in range(len(arr)):
        comparisons += 1
        if arr[i] == target:
            return i, comparisons
    return -1, comparisons

# Test
index, comps = linear_search_with_count(scores, 92)
print(f"Found at index {index} after {comps} comparisons")  # Output: Found at index 5 after 6 comparisons
```

---

## Guided Practice

**Step 1:** Given the list `[10, 15, 23, 31, 47, 52, 64]`, manually trace `linear_search(arr, 31)`.
- Which element do we check first? Second? When do we find it?

**Step 2:** Now trace `linear_search(arr, 50)`. How many elements do we check before returning -1?

**Step 3:** For the same list, what is the best-case scenario? Worst case? Average case (in terms of comparisons)?

**Step 4:** Create your own list of 10 numbers. Use linear search to find three different targets: one at the beginning, one in the middle, and one not in the list. Count comparisons for each.

---

## Practice Problems

**Beginner:** Write a function `linear_search_string` that finds a string in a list of strings. Return the index or -1.

**Intermediate:** Write a function that returns ALL indices where a value appears in a list (not just the first occurrence).

**Challenge:** Write a function `linear_search_custom` that takes a list, a target, and a **comparison function** as a parameter. Use it to search a list of dictionaries by a specific key.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Very similar to the numeric version; just compare strings instead of numbers.
- **Intermediate:** Instead of returning when you find a match, append the index to a results list and keep searching.
- **Challenge:** A comparison function might look like `lambda item: item['name'] == target`. Use it inside your loop to compare.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def linear_search_string(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# Intermediate
def find_all_indices(arr, target):
    indices = []
    for i in range(len(arr)):
        if arr[i] == target:
            indices.append(i)
    return indices

print(find_all_indices([1, 2, 3, 2, 4, 2], 2))  # Output: [1, 3, 5]

# Challenge
def linear_search_custom(arr, target, compare_func):
    for i in range(len(arr)):
        if compare_func(arr[i], target):
            return i
    return -1

# Usage
people = [
    {'name': 'Alice', 'age': 20},
    {'name': 'Bob', 'age': 22},
    {'name': 'Charlie', 'age': 21}
]

result = linear_search_custom(people, 'Bob', lambda p, t: p['name'] == t)
print(result)  # Output: 1
```
</details>
