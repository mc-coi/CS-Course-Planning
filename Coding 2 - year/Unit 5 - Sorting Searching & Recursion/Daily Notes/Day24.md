# Day 24: Sorting Project Implementation (Days 1-2 of Project)

**Learning Target:** I can implement all sorting algorithms correctly and create a comprehensive test suite.

---

## Key Concepts

**Project Scope Reminder:**
- Implement 6 sorting algorithms
- Implement 2 searching algorithms
- Test correctness thoroughly
- Benchmark performance
- Analyze and report results

**This Phase:** Code and test all algorithms

---

## Code Examples

```python
# Complete sorting algorithm implementations

# SORTING ALGORITHMS

def bubble_sort(arr):
    """Bubble sort - O(n²) in all cases."""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def selection_sort(arr):
    """Selection sort - O(n²) in all cases."""
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

def insertion_sort(arr):
    """Insertion sort - O(n) best case, O(n²) worst."""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

def merge_sort(arr):
    """Merge sort - O(n log n) guaranteed."""
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    """Helper for merge sort."""
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

def quick_sort(arr):
    """Quick sort - O(n log n) average, O(n²) worst."""
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

def builtin_sort(arr):
    """Python's built-in sort (Timsort)."""
    return sorted(arr)

# SEARCHING ALGORITHMS

def linear_search(arr, target):
    """Linear search - O(n)."""
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

def binary_search(arr, target):
    """Binary search iterative - O(log n), requires sorted array."""
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1

def binary_search_recursive(arr, target, left=0, right=None):
    """Binary search recursive - O(log n)."""
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

# TEST SUITE

class TestSuite:
    """Comprehensive test suite for all algorithms."""

    def __init__(self):
        self.test_cases = self.generate_test_cases()
        self.sorting_algorithms = [
            ('Bubble Sort', bubble_sort),
            ('Selection Sort', selection_sort),
            ('Insertion Sort', insertion_sort),
            ('Merge Sort', merge_sort),
            ('Quick Sort', quick_sort),
            ('Built-in Sort', builtin_sort),
        ]
        self.searching_algorithms = [
            ('Linear Search', linear_search),
            ('Binary Search', binary_search),
            ('Binary Search Recursive', binary_search_recursive),
        ]

    def generate_test_cases(self):
        """Generate test cases for sorting."""
        return [
            ([], []),  # Empty
            ([5], [5]),  # Single element
            ([1, 2, 3, 4, 5], [1, 2, 3, 4, 5]),  # Already sorted
            ([5, 4, 3, 2, 1], [1, 2, 3, 4, 5]),  # Reverse sorted
            ([3, 1, 4, 1, 5, 9, 2, 6], [1, 1, 2, 3, 4, 5, 6, 9]),  # Random with duplicates
            ([1, 1, 1, 1, 1], [1, 1, 1, 1, 1]),  # All same
            ([1, 2, 1, 2, 1], [1, 1, 1, 2, 2]),  # Alternating
        ]

    def test_sorting(self):
        """Test all sorting algorithms."""
        print("TESTING SORTING ALGORITHMS")
        print("=" * 80)

        all_passed = True

        for name, algo_func in self.sorting_algorithms:
            print(f"\n{name}:")
            passed = 0
            failed = 0

            for i, (input_arr, expected) in enumerate(self.test_cases):
                test_arr = input_arr.copy()
                result = algo_func(test_arr)

                if result == expected:
                    passed += 1
                    print(f"  Test {i + 1}: ✓ PASS")
                else:
                    failed += 1
                    print(f"  Test {i + 1}: ✗ FAIL")
                    print(f"    Input:    {input_arr}")
                    print(f"    Expected: {expected}")
                    print(f"    Got:      {result}")
                    all_passed = False

            print(f"  Summary: {passed} passed, {failed} failed")

        return all_passed

    def test_searching(self):
        """Test all searching algorithms."""
        print("\n\nTESTING SEARCHING ALGORITHMS")
        print("=" * 80)

        # Test data (must be sorted for binary search)
        sorted_arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        test_targets = [
            (1, 0),      # First element
            (10, 9),     # Last element
            (5, 4),      # Middle element
            (6, 5),      # Another element
            (11, -1),    # Not found
            (0, -1),     # Not found (too small)
        ]

        all_passed = True

        # Test linear search (works on unsorted data)
        print("\nLinear Search (unsorted data):")
        unsorted = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3]
        for target, expected_idx in [(5, -1), (1, 1), (6, 7)]:  # Note: linear returns first occurrence
            result = linear_search(unsorted, target)
            if (result >= 0) == (target in unsorted):
                print(f"  Search {target}: ✓ PASS (found={result >= 0})")
            else:
                print(f"  Search {target}: ✗ FAIL")
                all_passed = False

        # Test binary search algorithms (require sorted data)
        for name, algo_func in self.searching_algorithms[1:]:  # Skip linear
            print(f"\n{name} (sorted data):")
            passed = 0
            failed = 0

            for target, expected in test_targets:
                result = algo_func(sorted_arr, target)

                if result == expected:
                    passed += 1
                    print(f"  Search {target}: ✓ PASS")
                else:
                    failed += 1
                    print(f"  Search {target}: ✗ FAIL (expected {expected}, got {result})")
                    all_passed = False

            print(f"  Summary: {passed} passed, {failed} failed")

        return all_passed

    def run_all_tests(self):
        """Run complete test suite."""
        sort_ok = self.test_sorting()
        search_ok = self.test_searching()

        print("\n" + "=" * 80)
        print("OVERALL RESULTS")
        print("=" * 80)

        if sort_ok and search_ok:
            print("✓ ALL TESTS PASSED")
            return True
        else:
            print("✗ SOME TESTS FAILED")
            return False

# Execute tests
if __name__ == "__main__":
    suite = TestSuite()
    suite.run_all_tests()
```

---

## Guided Practice

**Activity 1: Code Review**

Review each sorting implementation:
- Does it modify in-place or return new array?
- Does it handle edge cases (empty, single element)?
- Is the logic correct?

**Activity 2: Manual Trace**

Trace one sorting algorithm by hand on array `[5, 2, 4, 1, 3]`:
- Show state after each iteration
- Verify final result is sorted

**Activity 3: Add More Tests**

Create additional test cases:
- Negative numbers
- Large numbers
- Strings (for comparison-based algorithms)
- Arrays with many duplicates

---

## Practice Problems

**Beginner:** Implement all 6 sorting algorithms and test on the basic test cases provided.

**Intermediate:** Add 5 new test cases to the test suite and verify all algorithms pass.

**Challenge:** Modify the test suite to check for stability (do equal elements maintain relative order?).

<details>
<summary>💡 Hints</summary>
- **Beginner:** Copy the implementations above
- **Intermediate:** Think of edge cases: negative numbers, duplicates, single element, etc.
- **Challenge:** Create test data with comparable elements that have metadata, check if order preserved
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# All implementations provided above
# Test suite provided above
# Run TestSuite().run_all_tests() to verify correctness
```
</details>
