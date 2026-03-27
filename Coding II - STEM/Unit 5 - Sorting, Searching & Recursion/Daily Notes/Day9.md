# Day 9: Project Day — Sort & Search Visualizer
**Learning Target:** I can create an interactive program visualizing sorting/searching algorithms.

### Project Overview
Build a visualizer showing:
- Different sorting algorithms in action
- Search algorithm steps
- Comparison and analysis
- Interactive controls

### Requirements
- Visualize algorithm steps (print state after each comparison/swap)
- Show statistics (comparisons, swaps, time)
- Support multiple algorithms
- Display results clearly

### Scaffold & Starter Code
```python
class SortVisualizer:
    def __init__(self, data):
        self.data = data
        self.comparisons = 0
        self.swaps = 0

    def display(self):
        print(self.data)

    def bubble_sort_visual(self):
        n = len(self.data)
        for i in range(n):
            for j in range(n - i - 1):
                self.comparisons += 1
                if self.data[j] > self.data[j + 1]:
                    self.data[j], self.data[j + 1] = self.data[j + 1], self.data[j]
                    self.swaps += 1
                self.display()
        return self.data

    def report(self):
        print(f"Comparisons: {self.comparisons}")
        print(f"Swaps: {self.swaps}")

# Usage
data = [5, 2, 8, 1, 9]
visualizer = SortVisualizer(data)
visualizer.bubble_sort_visual()
visualizer.report()
```

### Enhancement Ideas
- Color-coded visualization (showing comparisons, swaps)
- Step-by-step control (next/back buttons)
- Algorithm comparison side-by-side
- Custom data input
- Real-time statistics

---

# Unit Practice Bank

1. **Beginner:** Implement linear search.
2. **Beginner:** Implement binary search.
3. **Beginner:** Implement bubble sort.
4. **Intermediate:** Implement selection sort.
5. **Intermediate:** Implement insertion sort.
6. **Intermediate:** Implement merge sort.
7. **Intermediate:** Use sorted() with key parameter.
8. **Challenge:** Compare sorting algorithms on large data.
9. **Challenge:** Implement recursive binary search.
10. **Challenge:** Create sorting visualizer.
11. **Challenge:** Benchmark and analyze algorithms.
12. **Challenge:** Implement quicksort or heapsort.
13. **Challenge:** Create multi-level sorting.
14. **Challenge:** Optimize search in specific data structure.
15. **Challenge:** Build comprehensive algorithm analyzer.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Using binary search on unsorted list | Returns wrong result | Sort data first |
| Off-by-one errors in loops | Misses last element or crashes | Double-check indices |
| Not resetting comparisons counter | Wrong statistics | Initialize before each sort |
| Comparing very different algorithm sizes | Unfair benchmark | Use same data size |

---

# Unit Assessment Prep

**Review Questions:**

1. What's the complexity of linear search?
2. What's required for binary search?
3. Compare bubble and selection sort.
4. What makes merge sort fast?
5. When is insertion sort efficient?
6. How does Python's sorted() work?
7. Compare best and worst cases.
8. When would you use each algorithm?
9. How do you benchmark algorithms?
10. What is the `key` parameter in sorted()?

**Answers:**

1. O(n) — checks each element
2. Data must be sorted
3. Both O(n²), but selection has fewer swaps
4. Divide-and-conquer, O(n log n) complexity
5. For small or nearly-sorted data
6. Uses Timsort hybrid algorithm
7. Best: O(n) on sorted data; Worst: O(n log n)
8. Choose based on data size, pre-sortedness, memory
9. Time actual execution on various data sizes
10. Function returning comparison key for sorting

---

# Vocabulary & Quick Reference

**Key Terms:**
- **Linear search:** Sequential checking, O(n)
- **Binary search:** Divide-and-conquer search, O(log n)
- **Bubble sort:** Compare and swap adjacent, O(n²)
- **Merge sort:** Divide-and-conquer sort, O(n log n)
- **Comparison:** Two items checked against each other
- **Swap:** Exchange two elements' positions
- **In-place:** Sorting without extra memory

**Big O Complexity:**
- O(1): Constant
- O(log n): Logarithmic (binary search)
- O(n): Linear (linear search)
- O(n log n): Fast sorting (merge sort)
- O(n²): Slow sorting (bubble, selection, insertion)

---
