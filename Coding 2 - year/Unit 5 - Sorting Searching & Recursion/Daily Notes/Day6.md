# Day 6: Recursive Binary Search

**Learning Target:** I can implement binary search recursively and compare it to the iterative version.

---

## Key Concepts

**Recursive Binary Search**: Uses the same divide-and-conquer logic but calls itself on smaller subarrays instead of using a loop.

**Advantage:** More elegant and easier to understand the "divide and conquer" concept.

**Disadvantage:** Uses more memory (call stack) than iterative. For very deep recursion, iterative is better.

**Base Cases** in Recursive Binary Search:
1. Target found: `arr[mid] == target` → return index
2. Search space exhausted: `left > right` → return -1

---

## Code Examples

```python
# Recursive Binary Search
def binary_search_recursive(arr, target, left, right):
    """
    Recursive implementation of binary search.
    left and right are the current search boundaries.
    """
    # Base case 1: search space exhausted
    if left > right:
        return -1

    mid = (left + right) // 2

    # Base case 2: target found
    if arr[mid] == target:
        return mid
    # Recursive case 1: target is in the right half
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    # Recursive case 2: target is in the left half
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# Wrapper function (easier to call)
def binary_search(arr, target):
    return binary_search_recursive(arr, target, 0, len(arr) - 1)

# Test
numbers = [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
print(binary_search(numbers, 35))   # Output: 6
print(binary_search(numbers, 15))   # Output: 2
print(binary_search(numbers, 100))  # Output: -1

# Recursive with visualization
def binary_search_recursive_verbose(arr, target, left, right, depth=0):
    indent = "  " * depth
    print(f"{indent}Search [{left}..{right}] for {target}")

    if left > right:
        print(f"{indent}→ Not found")
        return -1

    mid = (left + right) // 2
    print(f"{indent}→ Check index {mid} (value: {arr[mid]})")

    if arr[mid] == target:
        print(f"{indent}→ Found!")
        return mid
    elif arr[mid] < target:
        print(f"{indent}→ {arr[mid]} < {target}, recurse right")
        return binary_search_recursive_verbose(arr, target, mid + 1, right, depth + 1)
    else:
        print(f"{indent}→ {arr[mid]} > {target}, recurse left")
        return binary_search_recursive_verbose(arr, target, left, mid - 1, depth + 1)

# Test with visualization
print("\nSearching for 35:")
binary_search_recursive_verbose(numbers, 35, 0, len(numbers) - 1)
```

---

## Guided Practice

**Step 1:** Trace `binary_search([10, 20, 30, 40, 50], 30)` recursively.
- First call: What are left, right, mid?
- Second call: What are the new left and right?
- Which base case stops the recursion?

**Step 2:** Now trace searching for a value NOT in the list, like 25.
- How many recursive calls happen before `left > right`?

**Step 3:** Compare iterative vs. recursive:
- Iterative uses a `while` loop to adjust `left` and `right`.
- Recursive calls itself with new left/right values.
- Which do you find easier to understand? Why?

**Step 4:** Call stack visualization: Draw the stack of function calls for searching a 16-element list. How deep does the stack go?

---

## Practice Problems

**Beginner:** Rewrite the recursive binary search without the wrapper function. Can you call it more easily?

**Intermediate:** Modify the recursive binary search to count how many recursive calls were made. (Hint: Add a counter parameter or use a global variable.)

**Challenge:** What's the maximum recursion depth (call stack depth) for a list of 1,000,000 items? Calculate log₂(1,000,000). How does this compare to iterative binary search?

<details>
<summary>💡 Hints</summary>
- **Beginner:** You can pass default arguments: `def binary_search_recursive(arr, target, left=0, right=None):` and set `right = len(arr) - 1` if it's None.
- **Intermediate:** Add `calls=0` parameter and increment it before each recursive call.
- **Challenge:** log₂(1,000,000) ≈ 20. So max depth is about 20 function calls. Still small!
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# Intermediate
def binary_search_count_calls(arr, target, left, right, calls=0):
    calls += 1
    print(f"Call {calls}")

    if left > right:
        return -1, calls

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid, calls
    elif arr[mid] < target:
        return binary_search_count_calls(arr, target, mid + 1, right, calls)
    else:
        return binary_search_count_calls(arr, target, left, mid - 1, calls)

# Challenge
import math
max_depth = math.ceil(math.log2(1000000))
print(f"Max recursion depth: {max_depth}")  # Output: 20

# For iterative: the while loop just adjusts pointers, no stack growth.
# For recursive: each call uses stack space, so max depth is log n.
# Both are efficient, but iterative uses slightly less memory.
```
</details>
