# Unit 3 - Advanced Functions & Algorithms: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days / 3 weeks
- **Core topics covered:** Lambda functions, higher-order functions (map, filter, zip), list and dictionary comprehensions, recursion, pseudocode, Big O notation, decorators, closures, and functional programming patterns
- **Prerequisites students need:** Strong function skills from Coding 1; comfortable with loops and conditionals; Unit 1 (Data Structures) mastery; preferably Unit 2 (OOP) for decorator understanding

## Week-by-Week Pacing

### Week 1 (Days 1–3): Lambda & Higher-Order Functions
- **Essential days** (must teach):
  - Day 1: Lambda functions—syntax, when to use, basic examples
  - Day 2: Higher-order functions (map, filter, zip)—concepts and applications
  - Day 3: List and dictionary comprehensions

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip complex lambda conditions (`a if a > b else b`); use only simple lambdas
  - Cut dictionary comprehensions; focus on list comprehensions only
  - Cut zip until later; it can wait

- **If ahead of pace:**
  - Extend Day 1: Explore lambda with multiple arguments, nested lambdas
  - Extend Day 2: Use map/filter/zip on complex data (nested lists, objects)
  - Extend Day 3: Three-level comprehensions, comprehensions with nested conditions

- **If behind pace:**
  - Combine Days 1–2: Teach lambdas and map/filter in one day
  - Skip zip entirely if time is critical
  - Delay comprehensions to Day 5; use loops instead
  - Use visual representations (before/after code comparisons)

### Week 2 (Days 4–6): Recursion & Algorithm Basics
- **Essential days** (must teach):
  - Day 4: Recursion fundamentals—base case, recursive case, call stack
  - Day 5: Big O notation—understanding algorithm complexity at high level
  - Day 6: Analyzing and comparing algorithms

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Teach only simple recursion (factorial, fibonacci); skip advanced topics
  - Big O notation can be simplified: Focus on O(1), O(n), O(n²), O(log n) only
  - Cut algorithm comparison benchmarking; show examples instead

- **If ahead of pace:**
  - Extend Day 4: Explore tail recursion, mutual recursion, complex recursion problems
  - Extend Day 5: Detailed Big O analysis; amortized complexity
  - Extend Day 6: Implement optimization techniques (memoization, dynamic programming)

- **If behind pace:**
  - Combine Days 4–5: Teach recursion with emphasis; Big O overview only
  - Provide recursion templates (factorial, list sum, binary search)
  - Skip algorithm comparison details

### Week 3 (Days 7–9): Advanced Patterns & Projects
- **Essential days** (must teach):
  - Day 7: Decorators and closures (or alternate: More recursion practice)
  - Day 8–9: Integrated project demonstrating comprehensions, lambda, recursion

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip decorators entirely; focus on practical recursion and comprehensions
  - Cut closures; explain decorators as black boxes only
  - Project: Provide significant starter code

- **If ahead of pace:**
  - Extend Day 7: Build custom decorators, use functools library
  - Project: Add complexity (multiple algorithms, performance comparison, visualization)
  - Explore functools module (reduce, partial)

- **If behind pace:**
  - Combine Days 8–9 into extended guided project
  - Skip decorators; focus on recursion and comprehensions
  - Project: Simplify; provide 60% of code; students fill in logic

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Use visual representations: Draw call stacks for recursion; show recursion "tree" of calls
- Start with loops, then show comprehensions as shorthand: `[x*2 for x in list]` vs. loop version side-by-side
- Lambda: Show `lambda x: x+1` as "a tiny function" before diving into syntax
- Recursion: Provide recursive tree diagrams and trace through by hand first
- Use concrete examples: Factorial of 5, fibonacci sequence, searching a list

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–2: Write lambda, use map to double numbers
- Unit Practice #3: Use filter for even numbers
- Unit Practice #4: Simple list comprehension
- Unit Practice #5: Factorial recursion
- Emphasize: Understanding before optimization

**Suggested pacing adjustments:**
- Spend 2 days on lambdas/comprehensions if students struggling; don't rush
- Provide comprehension templates with blanks to fill
- Introduce recursion with visual tracing (flowchart style)
- Delay Big O notation; teach it conceptually before formal notation
- Use pair programming on recursion problems

**What prerequisite gaps to look for:**
- Function parameter confusion: Will struggle with `map(lambda x: x*2, list)` if unsure about function syntax
- Loop syntax issues: Comprehensions are shorthand; weak loopers won't understand
- Call stack confusion: Recursion requires understanding how functions call each other
- Nested data structure trouble: Comprehensions and recursion on nested structures are hard

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–9 as designed
- Assign Unit Practice problems #1–10 (progression from basic to intermediate-advanced)
- Complete algorithm analysis project
- Weekly quizzes: Big O notation identification, predict output of lambdas/comprehensions

**Which practice problems to assign:**
- Problems #1–3: Lambda and higher-order functions
- Problems #4–6: Comprehensions and recursion basics
- Problems #7–10: Dictionary comprehensions, memoized fibonacci, binary search
- Project: Implement multiple algorithms; analyze complexity; compare performance

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 2:** Explore `itertools` module (combinations, permutations); lazy evaluation with generators
- **Day 4:** Implement advanced recursion (backtracking, graph traversal)
- **Day 7:** Design custom decorators; explore decorator patterns (logging, timing, validation)
- **Project:** Build optimization project: Take O(n²) solution, optimize to O(n log n)

**Challenge problems to assign:**
- Unit Practice #11–15: Function composition, memoized fibonacci, binary search, merge sort, algorithm optimization
- Advanced: Write quicksort or heapsort with Big O analysis
- Challenge: Create a decorator that times function execution and logs results
- Challenge: Flatten deeply nested list using recursion
- Challenge: Implement dynamic programming solution to complex problem

**Ways to deepen understanding beyond the curriculum:**
- Explore functional programming paradigm (immutability, pure functions)
- Discuss trade-offs between readability and conciseness in comprehensions
- Build real optimization case study: Show real code improvement from O(n²) to O(n log n)
- Explore generator expressions: `(x*2 for x in list)` vs. list comprehensions
- Challenge: Create their own decorator for data validation or performance monitoring

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 3:** Before recursion, ensure comprehensions are solid—mastery here helps recursion understanding
- **After Day 4:** Before Big O, ensure recursion concept is clear—analysis is easier with examples
- **After Day 6:** Before project, review algorithm analysis with familiar examples (e.g., analyze linear vs. binary search)

### Topics students most commonly struggle with:
1. **Lambda syntax:** The `lambda x: x+1` feels backwards; `x` comes before what to do with it
2. **Comprehension syntax:** `[x*2 for x in list]` reads backwards for beginners
3. **Recursion base case:** Forgetting to define when recursion stops; infinite loops result
4. **Call stack visualization:** Hard to track what happens when functions call themselves
5. **Big O understanding:** Confusing Big O with actual runtime; thinking O(n) is "better" than O(n²) always (varies by n)
6. **Map/filter output type:** Not realizing `map()` returns iterator, not list; must convert

### Topics students typically move through quickly:
1. **Lambda usage in sorted():** `sorted(list, key=lambda x: x[1])` becomes intuitive quickly
2. **Basic list comprehensions:** Creating squared numbers or filtered lists
3. **Simple recursion:** Factorial, counting down are natural once base case clicks
4. **Big O intuition:** Understanding O(n) scales differently than O(n²) makes sense

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Write a lambda that multiplies a number by 3"
- "When would you use a lambda vs. a regular function?"
- Check: Correct syntax, conceptual understanding

**Day 2 Check (5 min):**
- "Use map() to double all numbers in a list"
- "Use filter() to keep only numbers > 5"
- Check: Correct map/filter syntax, understanding of function as argument

**Day 3 Check (5 min):**
- "Write a list comprehension that creates squares of 1–10"
- "Write a list comprehension with a condition (only even numbers)"
- Check: Correct comprehension syntax, conditional logic

**Day 4 Check (5 min):**
- "Write a recursive function that counts down from n to 1"
- "What's the base case and recursive case?"
- Check: Correct recursion structure, understanding of base case

**Day 5 Check (5 min):**
- "What's the Big O of linear search? Binary search?"
- "Why does Big O matter?"
- Check: Big O notation, conceptual understanding

**Day 6 Check (5 min):**
- "Given two sorting algorithms, which would be better for 1 million items?"
- "Explain your reasoning"
- Check: Big O comparison, practical thinking

**Day 7–9 Check (Project submission):**
- Algorithm project demonstrates: comprehensions, lambda, recursion, Big O analysis
- Rubric: Correct implementations, accurate Big O analysis, clean code, documentation

## STEM-Specific Pacing Notes

**Important:** Unit 3 is dense. STEM timeline requires efficiency without sacrificing understanding.

- **Essential vs. Optional:**
  - Essential: Lambda, list comprehensions, basic recursion, Big O concepts (Days 1–5)
  - Optional: Dictionary comprehensions, decorators, advanced functional programming (Day 7)
  - Cut if behind: Decorators, closures, advanced Big O analysis

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: function definition, parameter passing, nested structures
  - Recursion amplifies these gaps—do 1-on-1 review for struggling students
  - Ensure they understand "function as a value" (passed to map/filter)

- **When to cut:**
  - If behind after Day 3, skip comprehensions; use loops instead throughout course
  - Cut dictionary comprehensions and zip entirely if time is tight
  - Skip decorators completely; teach higher-order functions without decorator syntax
  - Simplify Big O: Teach only that algorithms differ in speed; skip notation if necessary

- **When to accelerate:**
  - Fast students can skip Day 7 lecture; work directly on project
  - Use excess time for Unit 5 (Sorting & Searching) where Big O becomes practical
  - Have advanced students optimize given O(n²) code to O(n log n)

**Project scope by level:**
- Minimum: Implement 2 algorithms (e.g., linear search, bubble sort); analyze Big O
- Standard: Implement 3–4 algorithms; analyze complexity; compare performance
- Extended: Implement multiple sorting algorithms; optimize one; create visual comparison

**Connection to Unit 5:**
- Big O notation is essential foundation for Unit 5 (Sorting & Searching)
- If Unit 3 Big O is weak, Unit 5 will require heavy review
- Recursion is used in merge sort and binary search; ensure solid before Unit 5
