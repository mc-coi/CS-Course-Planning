# Unit 5 - Sorting, Searching & Recursion: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 28 days (~5.5 weeks)
- **Core topics covered:**
  - Linear search and binary search algorithms
  - Bubble sort, selection sort, insertion sort
  - Merge sort and quick sort (divide-and-conquer)
  - Python's built-in sort with custom key functions
  - Big O notation and algorithm analysis
  - Recursion review and optimization
  - Algorithm benchmarking and performance measurement
  - Practical applications of sorting and searching
- **Prerequisites students need:**
  - Unit 1: Data structures (lists)
  - Unit 3: Recursion, Big O notation
  - Unit 4: File I/O (for large data sets)
  - Strong understanding of loops and conditionals
  - Basic comprehension of algorithm efficiency

---

## Week-by-Week Pacing

### Week 1 (Days 1–6): Searching Algorithms

#### Day 1: Recursion Review
- **Essential days** (must teach): YES
  - Foundation for rest of unit; many algorithms are recursive
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Memoization review, tail recursion optimization
- **If behind pace**: Keep review brief; focus on factorial and fibonacci only

#### Days 2–3: Linear Search
- **Essential days** (must teach): YES
  - Foundation for understanding search efficiency
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Searching with custom predicates, searching multiple data types
- **If behind pace**: Simple linear search through lists; focus on concept

#### Days 4–6: Binary Search & Search Algorithms Lab
- **Essential days** (must teach): YES
  - Binary search shows power of efficient algorithms
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Variations of binary search (first occurrence, last occurrence), interpolation search
- **If behind pace**: Simple binary search only; may need to trace through multiple times

### Week 2 (Days 7–13): Simple Sorting Algorithms

#### Days 7–8: Bubble Sort & Selection Sort
- **Essential days** (must teach): YES
  - Foundational understanding of how sorting works
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Optimizations (early exit in bubble sort), analyzing exact operation counts
- **If behind pace**: Trace through manually multiple times; use visual aids

#### Days 9–10: Insertion Sort & Sorting Lab
- **Essential days** (must teach): YES
  - Insertion sort shows practical sorting algorithm
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Performance comparison with bubble sort, hybrid sorting strategies
- **If behind pace**: Simple examples only; focus on concept not optimization

#### Days 11–12: Comparing Sort Algorithms
- **Essential days** (must teach): YES
  - Understanding Big O and performance differences is critical
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Detailed Big O analysis, real-world performance measurement
- **If behind pace**: Simple Big O comparison (O(n²) vs O(n log n)); visual patterns

#### Day 13: Simple Sorting Lab & Practice
- **Essential days** (must teach): YES
  - Integration of sorting concepts
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 11–12
- **If ahead of pace**: Implementing and benchmarking sorts, optimizations
- **If behind pace**: Provide templates; focus on understanding existing sorts

### Week 3 (Days 14–19): Advanced Sorting Algorithms

#### Days 14–15: Merge Sort & Divide-and-Conquer
- **Essential days** (must teach): YES
  - Merge sort demonstrates divide-and-conquer strategy
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Analysis of merge sort complexity, space-time trade-offs
- **If behind pace**: Understand concept; may not implement from scratch

#### Days 16–17: Quick Sort
- **Essential days** (must teach): YES
  - Quick sort is most commonly used sorting algorithm
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Pivot selection strategies, worst-case scenarios, randomized quick sort
- **If behind pace**: Understand concept; provide implementation

#### Days 18–19: Advanced Sorting Lab
- **Essential days** (must teach): YES
  - Application of merge sort and quick sort
- **Flexible days** (can compress or cut if pressed for time): Can be 1 day if behind
- **If ahead of pace**: Comparing implementations, performance on different data patterns
- **If behind pace**: Provide templates; focus on understanding how algorithms work

### Week 4 (Days 20–26): Python's Built-In Sort & Applications

#### Days 20–21: Python's sort() and sorted() with Custom Keys
- **Essential days** (must teach): YES
  - Using built-in sort with custom key functions is most practical
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Complex key functions, multi-level sorting, reverse sorting strategies
- **If behind pace**: Simple key functions (by attribute, by calculated value)

#### Days 22–23: Real-World Sorting Applications
- **Essential days** (must teach): YES
  - Practical applications of sorting and searching
- **Flexible days** (can compress or cut if pressed for time): Can combine if behind
- **If ahead of pace**: Complex sorting scenarios, optimization for real data
- **If behind pace**: Simplified applications; provide templates

#### Days 24–25: Benchmarking & Performance Analysis
- **Essential days** (must teach): YES
  - Measuring performance validates Big O analysis
- **Flexible days** (can compress or cut if pressed for time): Can be brief
- **If ahead of pace**: Detailed benchmarking, comparing on different data sizes
- **If behind pace**: Simple timing comparisons, visual performance graphs

#### Day 26: Code Review & Optimization Workshop
- **Essential days** (must teach): YES
  - Learning from mistakes
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 25
- **If ahead of pace**: Peer code review, refactoring for performance
- **If behind pace**: Teacher-led examples only

### Week 5 (Days 27–28): Assessment

#### Day 27–28: Unit Assessment & Reteaching/Enrichment
- **Essential days** (must teach): YES
  - Assessment required
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early completers work on extensions or start Unit 6
- **If behind pace**: Day 28 for reteaching and support

---

## Differentiation Strategies

### For Struggling Students

**Common gaps:**
- Difficulty visualizing algorithm execution
- Weak Big O understanding
- Confusion with recursion in sorting algorithms
- Trouble comparing algorithms conceptually

**Specific scaffolding:**
- Use **visual animations** of sorting algorithms (many available online)
- Provide **traced examples** of each algorithm step-by-step
- Create a **Big O comparison chart** with visual patterns
- Use **concrete data sets** (same list throughout unit)
- Provide **templates** for all algorithm implementations
- Focus on **understanding over implementation**

**Which practice problems to assign first:**
- Linear search
- Simple bubble sort
- Comparing two algorithms on same data
- Basic Big O identification (O(n²), O(n log n))
- Using Python's sort() with simple key functions

**Suggested pacing adjustments:**
- Skip quick sort or provide full implementation
- Skip merge sort details; may use built-in sort instead
- Simplify Big O to O(n²) and O(n log n) only
- Provide implementation templates for all algorithms
- Reduce number of algorithms to learn (bubble, insertion, Python sort)
- Skip benchmarking complexity; focus on understanding

**Prerequisite gaps to watch for:**
- If weak on recursion, divide-and-conquer (merge sort, quick sort) will be hard; review recursion first
- If weak on Big O, algorithm analysis will be slow; provide concrete operation counts
- If weak on loops, understanding algorithm details will be hard; review nested loops

**Reteaching strategies:**
- Use the same data set throughout
- Manual tracing on paper with step-by-step guidance
- Pair with stronger students for lab days
- Provide working code; focus on understanding how it works
- Visual demonstrations with physical objects (cards, numbers on board)

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Implement basic algorithms (linear search, bubble sort, insertion sort)
- Understand merge sort and quick sort conceptually
- Use Python's built-in sort effectively
- Analyze algorithm performance

**Which practice problems to assign:**
- All searching problems (linear, binary)
- Simple sorting algorithms (bubble, selection, insertion)
- Python sort with custom keys
- Big O analysis of various algorithms
- Performance comparisons

**Pacing tips:**
- Days 1–13 focus on fundamentals; should feel solid
- Days 14–19 introduce advanced algorithms; monitor for confusion
- Days 20–26 focus on practical application; should feel manageable

### For Advanced Students

**Extension activities:**
- Implement and optimize all sorting algorithms
- Study advanced sorting (heap sort, radix sort, bucket sort)
- Implement custom data structure operations with sorting
- Perform detailed algorithm benchmarking and analysis
- Study algorithm optimizations and trade-offs
- Explore real-world sorting (database indexes, cache efficiency)

**Challenge problems to assign:**
- Implementing merge sort and quick sort from scratch
- Analyzing algorithm complexity on paper (not just Big O)
- Benchmarking and comparing algorithms empirically
- Sorting complex data structures
- Optimizing algorithms for specific data patterns
- Studying hybrid sorting strategies

**Ways to deepen understanding:**
- Study algorithm analysis in detail (counting exact operations)
- Implement sorting variants with different pivot selection
- Explore how real-world systems use sorting (databases, search engines)
- Study cache efficiency and memory patterns
- Learn about stable vs unstable sorting
- Explore probabilistic algorithm analysis

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 6:** Checkpoint for searching before moving to simple sorting
- **After Day 13:** Checkpoint for simple sorting before advanced algorithms
- **After Day 19:** Checkpoint for algorithm implementation before practical applications
- **After Day 25:** Final checkpoint before assessment

### Topics students typically struggle with:
1. **Binary search** (Days 4–6): Non-obvious that list must be sorted
   - *Fix:* Show what happens if list is unsorted, emphasize prerequisite
2. **Merge sort** (Days 14–15): Divide-and-conquer and merging is complex
   - *Fix:* Visual animations, step-by-step manual tracing
3. **Quick sort** (Days 16–17): Pivot selection and partitioning is non-obvious
   - *Fix:* Show partition step carefully, trace through small examples
4. **Big O analysis** (Days 11–12, 22–23): Abstract concept
   - *Fix:* Concrete operation counting, visual patterns, empirical validation
5. **Recursion in sorting** (Days 14–17): Combining recursion with sorting
   - *Fix:* Review recursion first, then explain how sorting uses it

### Topics students typically move through quickly:
1. **Linear search** (Days 2–3): Straightforward concept
2. **Bubble sort** (Days 7–8): Visual pattern is clear
3. **Using Python's sort()** (Days 20–21): Already know the function
4. **Simple Big O** (Days 11–12): O(n²) and O(n) are easy
5. **Insertion sort** (Days 9–10): Intuitive algorithm

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 6:** Can students implement linear and binary search?
   - Quick task: "Implement binary search on a sorted list"
2. **After Day 13:** Can students implement simple sorting algorithms?
   - Quick task: "Implement bubble sort and trace it"
3. **After Day 19:** Can students understand divide-and-conquer?
   - Quick task: "Explain how merge sort divides the problem"
4. **After Day 25:** Can students analyze and compare algorithms?
   - Quick task: "What's the Big O of these sorts? Why?"

### Summative checks (end-of-unit):
1. **Days 27–28 Assessment:**
   - Part A: Multiple choice (algorithm names, Big O, concepts)
   - Part B: Short answer (trace algorithm, analyze complexity)
   - Part C: Coding (implement search, implement sort, analyze performance)

### Lab checkpoints (Days 6, 13, 19, 25):
- Demonstrate search and sorting in practice

---

## Notes on Unit 4 Prerequisites

This unit builds heavily on Unit 3 (recursion, Big O) and Unit 4 (file I/O for data). Watch for:

- **Recursion:** If weak, merge sort and quick sort will be hard; review recursion
- **Big O:** If weak, algorithm analysis will not make sense; review Big O notation
- **Loops:** If weak, understanding algorithm details will be hard; review nested loops
- **Data structures:** Must understand lists thoroughly

---

## Time Management Tips

- **If 5 days ahead:** Use time for advanced sorts, detailed algorithm analysis, or early Unit 6 start
- **If 3 days behind:** Simplify to linear search, bubble sort, insertion sort only; provide templates
- **If 1 week behind:** Focus only on searching (Days 1–6) and simple sorting (Days 7–13); skip advanced sorts
- **If 2 weeks behind:** Teach only linear/binary search and bubble sort; skip merge/quick sorts

---

## Key Assessment Targets

By the end of Unit 5, all students should demonstrate:
1. Implementing and understanding linear search
2. Implementing and understanding binary search
3. Understanding and potentially implementing simple sorting (bubble, selection, insertion)
4. Understanding Big O notation for sorting algorithms
5. Comparing algorithm performance conceptually
6. Using Python's sort() with custom key functions
7. Analyzing algorithm efficiency on real data

Students working at advanced level should additionally demonstrate:
- Implementing merge sort and quick sort
- Detailed Big O analysis (counting operations)
- Empirical performance benchmarking
- Algorithm optimization
- Understanding cache and memory effects
- Sorting complex data structures
