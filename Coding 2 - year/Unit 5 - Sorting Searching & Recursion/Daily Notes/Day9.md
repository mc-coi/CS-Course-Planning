# Day 9: Bubble Sort Code & O(n²) Deep Dive

**Learning Target:** I can trace bubble sort step-by-step and understand why it's slow for large lists.

---

## Key Concepts

**Why O(n²) is Slow:**
```
n = 10       → ~50 comparisons (acceptable)
n = 100      → ~5,000 comparisons
n = 1,000    → ~500,000 comparisons (slow!)
n = 10,000   → ~50,000,000 comparisons (very slow)
n = 1,000,000 → ~500,000,000,000 comparisons (not feasible)
```

**Visual Comparison:**
- O(n): 1,000,000 operations
- O(n log n): ~20,000,000 operations
- O(n²): 1,000,000,000,000 operations

**When Bubble Sort is Acceptable:**
- Small arrays (< 100 elements)
- Nearly sorted data (with optimization)
- Educational purposes
- NOT for real-world production code

---

## Code Examples

```python
# Full bubble sort example with performance test
import time

def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# Test with timing
def test_bubble_sort_performance():
    # Small list
    small = [5, 2, 8, 1, 9, 3, 7]
    start = time.time()
    bubble_sort(small.copy())
    elapsed = time.time() - start
    print(f"7 elements: {elapsed:.6f} seconds")

    # Medium list (100 elements)
    medium = list(range(100, 0, -1))  # Worst case: reverse sorted
    start = time.time()
    bubble_sort(medium.copy())
    elapsed = time.time() - start
    print(f"100 elements (reverse sorted): {elapsed:.6f} seconds")

    # Larger list (1000 elements)
    large = list(range(1000, 0, -1))
    start = time.time()
    bubble_sort(large.copy())
    elapsed = time.time() - start
    print(f"1000 elements (reverse sorted): {elapsed:.6f} seconds")

# test_bubble_sort_performance()

# Detailed trace example
def bubble_sort_with_trace(arr, show_every=1):
    """Trace bubble sort with optional filtering for large arrays."""
    n = len(arr)
    print(f"Sorting: {arr}")

    for i in range(n):
        if i % show_every == 0:
            print(f"Pass {i + 1}:")

        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

                if i % show_every == 0:
                    print(f"  {arr}")

    print(f"Sorted: {arr}\n")
    return arr

# Example traces
print("Example 1: Small array")
bubble_sort_with_trace([5, 2, 8, 1, 9])

print("Example 2: Nearly sorted array (best case for optimization)")
bubble_sort_with_trace([1, 2, 3, 5, 4, 6, 7])

# Comparison with other approaches
def sorted_builtin(arr):
    """Python's built-in sorted is much faster."""
    return sorted(arr)

def test_comparison():
    test_list = list(range(1000, 0, -1))

    # Bubble sort
    start = time.time()
    bubble_sort(test_list.copy())
    bubble_time = time.time() - start

    # Built-in sort
    start = time.time()
    sorted_builtin(test_list)
    builtin_time = time.time() - start

    print(f"Bubble sort: {bubble_time:.4f}s")
    print(f"Built-in sort: {builtin_time:.6f}s")
    print(f"Builtin is {bubble_time / builtin_time:.0f}x faster!")

# test_comparison()
```

---

## Guided Practice

**Activity 1: Complexity Analysis**

For array size n, bubble sort makes n(n-1)/2 comparisons:
- n = 5: 5 * 4 / 2 = 10 comparisons
- n = 10: 10 * 9 / 2 = 45 comparisons
- n = 20: 20 * 19 / 2 = 190 comparisons

Calculate for n = 50, n = 100. Notice the pattern: it grows quadratically!

**Activity 2: Best Case vs. Worst Case**

Sort two lists:
1. Already sorted: `[1, 2, 3, 4, 5]`
2. Reverse sorted: `[5, 4, 3, 2, 1]`

For list 1, how many passes does the optimized version take? For list 2?

**Activity 3: Why Not Use Bubble Sort?**

Imagine sorting 10,000 student records. Bubble sort would do ~50,000,000 comparisons. If each comparison takes 1 microsecond, that's 50 seconds! Meanwhile, a faster algorithm (O(n log n)) would take ~200,000 comparisons (0.2 seconds).

---

## Practice Problems

**Beginner:** Implement bubble sort from scratch without looking at the code. Test it on `[3, 7, 2, 8, 1]`.

**Intermediate:** Modify the bubble sort to also return the NUMBER OF SWAPS made. Which input causes the most swaps: already sorted, random order, or reverse sorted?

**Challenge:** Implement a "cocktail sort" (bubble sort that goes both directions). Does it help? Why or why not?

<details>
<summary>💡 Hints</summary>
- **Beginner:** Two nested loops. Outer loop: i from 0 to n. Inner loop: j from 0 to n-i-1. Swap if arr[j] > arr[j+1].
- **Intermediate:** Add a `swaps` counter. Increment it every time you swap.
- **Challenge:** Cocktail sort alternates: forward pass (left to right), backward pass (right to left). It's still O(n²) but sometimes slightly faster on partially sorted data.
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# Intermediate
def bubble_sort_count_swaps(arr):
    n = len(arr)
    swaps = 0

    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swaps += 1

    return arr, swaps

print(bubble_sort_count_swaps([1, 2, 3, 4, 5]))  # Already sorted: 0 swaps
print(bubble_sort_count_swaps([5, 4, 3, 2, 1]))  # Reverse sorted: 10 swaps (most swaps)

# Challenge - Cocktail Sort
def cocktail_sort(arr):
    n = len(arr)
    start = 0
    end = n - 1

    while start <= end:
        # Forward pass (left to right)
        for i in range(start, end):
            if arr[i] > arr[i + 1]:
                arr[i], arr[i + 1] = arr[i + 1], arr[i]
        end -= 1

        # Backward pass (right to left)
        for i in range(end, start, -1):
            if arr[i - 1] > arr[i]:
                arr[i - 1], arr[i] = arr[i], arr[i - 1]
        start += 1

    return arr

# Still O(n²) but sometimes faster in practice (rarely used).
```
</details>
