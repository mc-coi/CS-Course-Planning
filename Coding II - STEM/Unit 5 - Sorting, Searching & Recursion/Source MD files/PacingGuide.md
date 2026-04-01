# Unit 5 - Sorting, Searching & Recursion: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days / 3 weeks
- **Core topics covered:** Linear and binary search, bubble/selection/insertion/merge sort, Python's built-in sorting, algorithm complexity analysis, algorithm benchmarking, choosing appropriate algorithms
- **Prerequisites students need:** Strong understanding of Big O notation (Unit 3); comfortable with recursion (Unit 3); solid understanding of lists and loops (Unit 1); analytical thinking

## Week-by-Week Pacing

### Week 1 (Days 1–3): Search Algorithms
- **Essential days** (must teach):
  - Day 1: Linear search—implementation, understanding, complexity O(n)
  - Day 2: Binary search—implementation, requirements (sorted data), complexity O(log n)
  - Day 3: Comparing search algorithms; practical application

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip binary search implementation; show concept only
  - Use built-in `in` operator or `index()` for linear search demonstration
  - Focus on understanding, not memorization of code

- **If ahead of pace:**
  - Extend Day 2: Implement binary search recursively (connects to Unit 3)
  - Extend Day 3: Explore search in specific data structures (BST preview)
  - Implement interpolation search or other advanced search

- **If behind pace:**
  - Combine Days 1–2: Single day on search algorithms
  - Provide linear and binary search code; students trace and analyze
  - Skip implementation; focus on understanding complexity difference

### Week 2 (Days 4–6): Basic Sorting Algorithms
- **Essential days** (must teach):
  - Day 4: Bubble sort and selection sort—implementations and complexity
  - Day 5: Insertion sort and Python's built-in `sorted()` and `.sort()`
  - Day 6: Comparing sorting algorithms; choosing appropriate sorts

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Implement only bubble sort and selection sort; skip insertion sort
  - Use `sorted()` for practical sorting; teach algorithm implementations for understanding
  - Reduce code writing; focus on tracing existing code

- **If ahead of pace:**
  - Extend Day 4: Optimize bubble sort (early termination)
  - Extend Day 5: Custom sorting with key parameter; sorted() on complex data
  - Extend Day 6: Implement quicksort or heapsort for additional practice

- **If behind pace:**
  - Combine Days 4–5: Single day on sorting algorithms
  - Provide sorting implementations; students trace and analyze
  - Skip most implementations; use sorted() for practical work

### Week 3 (Days 7–9): Merge Sort & Complex Analysis
- **Essential days** (must teach):
  - Day 7: Merge sort—divide-and-conquer, recursion, complexity O(n log n)
  - Day 8: Algorithm benchmarking; comparing performance on real data
  - Day 9: Capstone—integrate searching/sorting in complete project

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Provide merge sort code; students trace and analyze rather than implement
  - Skip benchmarking code; show results instead
  - Project: Heavy scaffolding and starter code

- **If ahead of pace:**
  - Extend Day 7: Discuss why merge sort is divide-and-conquer; explore variations
  - Extend Day 8: Real benchmarking project comparing all algorithms
  - Extend Day 9: Optimize sorting for specific data patterns

- **If behind pace:**
  - Combine Days 7–8: Overview of merge sort and analysis
  - Skip benchmarking; focus on algorithm selection
  - Project: Simplified; use built-in sorting

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Use visual representations: Show sorting algorithms with colored cards or numbers
- Animate sorting: Trace through bubble sort by hand step-by-step
- Explain Big O with real examples: "Linear search like reading book page-by-page; binary search like looking in phonebook middle first"
- Start with searching (intuitive) before diving into sorting (complex)
- Emphasize practical application: Why do we care? (Sorted data searches faster)

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–3: Linear search, binary search, bubble sort (implementation or tracing)
- Unit Practice #4–5: Selection sort, insertion sort
- Emphasize: Understanding what code does before memorizing syntax

**Suggested pacing adjustments:**
- Spend extra time on linear search; it's intuitive
- Trace binary search by hand many times before coding
- Animate sorting algorithms; use visual tools (draw on board)
- Focus on understanding O(n) vs O(n log n) before deep analysis
- Use pair programming for sorting implementations

**What prerequisite gaps to look for:**
- Big O confusion: If Unit 3 weak, algorithm analysis will be very hard
- Recursion issues: Binary search and merge sort require recursion; if Unit 3 weak, these are very hard
- Loop syntax: Sorting implementations need nested loops
- List manipulation: Need comfortable with slicing for merge sort

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–9 as designed
- Assign Unit Practice problems #1–10 (progression from implementation to analysis)
- Complete sorting/searching project with multiple algorithms
- Weekly quizzes: Algorithm complexity, comparing implementations, practical selection

**Which practice problems to assign:**
- Problems #1–3: Linear and binary search
- Problems #4–6: Bubble, selection, insertion sort
- Problems #7–10: Merge sort, sorted() with key, algorithm comparison, benchmarking
- Project: Implement multiple algorithms; benchmark; write analysis

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 4:** Optimize bubble sort with early termination; explore other sort variations
- **Day 6:** Implement quicksort; analyze why it's faster in practice than theory
- **Day 8:** Create sorting visualizer (animated visualization of algorithm execution)
- **Project:** Performance analysis project; benchmark with large datasets

**Challenge problems to assign:**
- Unit Practice #11–15: Algorithm visualizer, multi-level sorting, search optimization, heapsort, comprehensive analyzer
- Advanced: Implement hybrid sort (e.g., timsort concept)
- Challenge: Optimize merge sort for space efficiency
- Challenge: Create sorting algorithm that adapts based on data characteristics
- Challenge: Benchmark and analyze why quicksort is faster in practice despite O(n²) worst case

**Ways to deepen understanding beyond the curriculum:**
- Explore real-world sorting: How does Python's `sorted()` work internally (timsort)?
- Discuss sorting stability: Why does it matter?
- Analyze space vs. time trade-offs: When does space efficiency matter?
- Build visualization: Animate algorithms executing
- Challenge: Optimize for specific data patterns (nearly sorted, reverse sorted, etc.)

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 3:** Before sorting, ensure search concepts are solid—both build on Big O understanding
- **After Day 6:** Before merge sort, ensure basic sorts are understood
- **After Day 8:** Before project, review Big O analysis and practical algorithm selection

### Topics students most commonly struggle with:
1. **Binary search requirements:** Forgetting data must be sorted first
2. **Big O analysis:** Confusing theory with practice (quicksort is O(n²) worst case but faster than merge sort usually)
3. **Merge sort recursion:** Two recursive calls in merge sort is harder than simple recursion
4. **Space complexity:** Understanding merge sort uses extra space while bubble sort doesn't
5. **Choosing algorithm:** Real-world selection requires considering data size, sortedness, stability
6. **Off-by-one errors:** Sorting implementations have boundary issues

### Topics students typically move through quickly:
1. **Linear search concept:** "Check each one until found" is intuitive
2. **Bubble sort:** "Bigger items float up" is memorable and intuitive
3. **Understanding sorted() works:** Just calling built-in function
4. **Binary search intuition:** "Guess middle and narrow range" makes sense
5. **Comparing two algorithms:** Recognizing O(n log n) is faster than O(n²) is straightforward

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Implement linear search for a target in a list"
- "What's the Big O? Why?"
- Check: Correct implementation, correct Big O, explanation

**Day 2 Check (5 min):**
- "Implement binary search"
- "What's required of the data? Why?"
- Check: Correct implementation, understanding of sorted requirement

**Day 3 Check (5 min):**
- "Compare linear and binary search. When would you use each?"
- "What size data matters?"
- Check: Practical understanding of trade-offs

**Day 4 Check (5 min):**
- "Trace bubble sort through 5 elements [3,1,4,1,5]"
- "How many passes? Why?"
- Check: Correct tracing, understanding of algorithm

**Day 5 Check (5 min):**
- "Implement insertion sort" or "Trace through [3,1,4]"
- "Compare insertion vs. bubble. When is insertion better?"
- Check: Implementation/tracing, understanding of differences

**Day 6 Check (5 min):**
- "Given a large nearly-sorted list, which algorithm? Why?"
- "Given random data, which? Why?"
- Check: Practical algorithm selection reasoning

**Day 7 Check (5 min):**
- "Trace merge sort through [3,1,4,1,5]"
- "Why is it O(n log n)?"
- Check: Understanding divide-and-conquer, correct Big O reasoning

**Day 8 Check (5 min):**
- "Benchmark bubble sort vs. merge sort on 10,000 items"
- "Does theory match practice?"
- Check: Benchmarking capability, understanding of practical performance

**Day 9 Check (Project submission):**
- Algorithm project demonstrates: implementation, analysis, comparison, selection
- Rubric: Correct implementations, accurate Big O analysis, working benchmarks, clear comparison report

## STEM-Specific Pacing Notes

**Important:** Unit 5 is conceptually dense. Algorithm analysis requires strong Unit 3 foundation. Tighter STEM timeline requires strategic choices.

- **Essential vs. Optional:**
  - Essential: Linear/binary search, bubble/insertion sort, understanding Big O in practice (Days 1–5)
  - Optional: Merge sort implementation, advanced analysis, benchmarking tools (Days 7–8)
  - Cut if behind: Merge sort, heapsort, advanced benchmarking

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: loops (sorting requires nested), Big O (Unit 3)
  - Recursion issues amplify with binary search and merge sort
  - Consider 1-on-1 review for Unit 3 weak students before starting Unit 5

- **When to cut:**
  - If behind after Day 3, skip binary search implementation; teach concept/complexity only
  - Skip merge sort implementation; provide code for tracing/analysis
  - Cut benchmarking; focus on theoretical Big O comparison
  - Use built-in `sorted()` for practical work; skip bubble/selection/insertion

- **When to accelerate:**
  - Fast students implement merge sort and quicksort on schedule
  - Use excess time for advanced visualizations or real-world optimization
  - Have students benchmark with large realistic datasets

**Project scope by level:**
- Minimum: Implement linear/binary search; bubble/selection sort; analyze Big O; select appropriate for 3 scenarios
- Standard: Implement multiple sorts; benchmark; write analysis; visualize algorithm execution
- Extended: Implement merge sort; create visualizer; real-world optimization project; explore advanced sorts

**Connection to other units:**
- **Unit 3:** Big O foundation is critical; if weak, Unit 5 is very difficult
- **Unit 6:** Real-world sorting of API data
- **Unit 2:** Sorting objects by attribute (implement custom sorting)

**Timeline note:**
Given STEM constraints, Unit 5 can be 7 days (drop advanced analysis) or 9 days (full treatment). Prioritize understanding over breadth.
