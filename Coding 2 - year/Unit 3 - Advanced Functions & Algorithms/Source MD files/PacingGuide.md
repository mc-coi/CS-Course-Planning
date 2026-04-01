# Unit 3 - Advanced Functions & Algorithms: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 27 days (~5.5 weeks)
- **Core topics covered:**
  - Lambda functions and anonymous functions
  - Higher-order functions (map, filter, zip, enumerate)
  - List, dictionary, set, and generator comprehensions
  - Recursion: base case, recursive case, call stack, memoization
  - Big O notation and algorithm complexity analysis
  - Decorators and closures
  - Generators with yield and lazy evaluation
  - Functional programming patterns
  - Algorithm optimization and performance analysis
- **Prerequisites students need:**
  - Unit 1: Data structures (lists, dicts, sets)
  - Unit 2: Classes and methods
  - Functions: definition, calls, return values, scope
  - Solid understanding of loops and conditionals

---

## Week-by-Week Pacing

### Week 1 (Days 1–5): Functional Programming Fundamentals

#### Day 1: Lambda Functions
- **Essential days** (must teach): YES
  - Lambda functions are used throughout this unit and are Pythonic
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Complex lambda expressions, lambda with multiple lines (use regular functions)
- **If behind pace**: Start with very simple lambdas: lambda x: x * 2; show only key examples

#### Days 2–4: map(), filter(), zip()
- **Essential days** (must teach): YES
  - These are core functional programming tools used throughout Python
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Function composition, chaining operations, lazy evaluation details
- **If behind pace**: One day per function; start with concrete examples

#### Day 5: Functional Programming Lab
- **Essential days** (must teach): YES
  - Integration of lambda, map, filter, zip in real problems
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 2–4
- **If ahead of pace**: Complex data pipelines, performance analysis of functional vs loop approaches
- **If behind pace**: Provide templates; focus on understanding how to use functions together

### Week 2 (Days 6–10): Comprehensions

#### Days 6–7: List & Nested Comprehensions
- **Essential days** (must teach): YES
  - Comprehensions are essential Pythonic syntax
- **Flexible days** (can compress or cut if pressed for time): Nested comprehensions can be simplified
- **If ahead of pace**: Triple-nested comprehensions, complex conditions, performance analysis
- **If behind pace**: Start with simple comprehensions [x*2 for x in range(5)], add conditions slowly

#### Days 8–9: Dict/Set Comprehensions & Generator Expressions
- **Essential days** (must teach): YES for dict comprehensions; PARTIAL for generators
- **Flexible days** (can compress or cut if pressed for time): Generators can be deferred
- **If ahead of pace**: Generator functions with yield, memory efficiency analysis
- **If behind pace**: Focus on dict comprehensions; skip generators initially

#### Day 10: Comprehension Lab
- **Essential days** (must teach): YES
  - Choosing the right comprehension type is essential
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 8–9
- **If ahead of pace**: Comprehension optimization, comparing comprehensions vs loops vs map/filter
- **If behind pace**: Provide examples; focus on when to use each type

### Week 3 (Days 11–16): Recursion

#### Days 11–12: Recursion Fundamentals & Classic Problems
- **Essential days** (must teach): YES
  - Recursion is a core algorithm design technique
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Complex recursive problems, memoization optimization, tail recursion
- **If behind pace**: Simple recursion only (factorial, fibonacci); trace calls on paper

#### Days 13–14: Complex Recursion & Tower of Hanoi
- **Essential days** (must teach): YES
  - Complex recursion shows power of decomposition
- **Flexible days** (can compress or cut if pressed for time): Tower of Hanoi can be simplified
- **If ahead of pace**: Backtracking algorithms, permutations/combinations, advanced decomposition
- **If behind pace**: Stick to factorial and fibonacci; skip complex problems

#### Days 15–16: Recursion vs Iteration & Lab
- **Essential days** (must teach): YES
  - Understanding trade-offs is important for algorithm design
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 13–14
- **If ahead of pace**: Performance analysis, when recursion is superior, tail call optimization
- **If behind pace**: Simple examples showing both approaches

### Week 4 (Days 17–21): Algorithms & Complexity

#### Days 17–19: Big O Notation & Algorithm Analysis
- **Essential days** (must teach): YES
  - Understanding algorithm efficiency is critical
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Amortized analysis, practical Big O analysis of real code
- **If behind pace**: Simple Big O: O(1), O(n), O(n²), O(log n) with examples

#### Days 20–21: Decorators, Closures & Review
- **Essential days** (must teach): PARTIAL
  - Decorators are useful; closures are important but abstract
- **Flexible days** (can compress or cut if pressed for time): YES — can be optional or brief
- **If ahead of pace**: Complex decorators with arguments, decorator stacking, closures with state
- **If behind pace**: Skip decorators; brief intro to closures only

### Week 5 (Days 22–27): Integration & Assessment

#### Days 22–23: Integration Lab
- **Essential days** (must teach): YES
  - Application of all unit concepts
- **Flexible days** (can compress or cut if pressed for time): Can be 1 day if behind
- **If ahead of pace**: Multi-concept problems, optimization challenges
- **If behind pace**: Provide templates; focus on putting concepts together

#### Days 24–25: Code Review & Algorithm Design Workshop
- **Essential days** (must teach): YES
  - Learning from mistakes and practicing algorithm design
- **Flexible days** (can compress or cut if pressed for time): Can combine into 1 day
- **If ahead of pace**: Peer code review, refactoring for performance
- **If behind pace**: Teacher-led examples, focus on core concepts

#### Day 26: Unit Review & Assessment Prep
- **Essential days** (must teach): YES
  - Consolidation before assessment
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 25
- **If ahead of pace**: Students create practice problems, teach peers
- **If behind pace**: Provide comprehensive study guide

#### Day 27: Unit Assessment
- **Essential days** (must teach): YES
  - Assessment required
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early completers start Unit 4 or get enrichment
- **If behind pace**: Extended time if needed

---

## Differentiation Strategies

### For Struggling Students

**Common gaps:**
- Difficulty understanding abstract function programming concepts
- Weak recursion intuition
- Confusion with lambda syntax

**Specific scaffolding:**
- Provide **"Recursion Trace Templates"** to help visualize call stack
- Use **concrete examples repeatedly** (factorial, fibonacci, searching lists)
- Create a **"Big O Cheat Sheet"** with common operations and their complexity
- Show **step-by-step transformations** with map/filter using manual loops first

**Which practice problems to assign first:**
- Start with simple lambdas and map/filter
- Basic list comprehensions only
- Factorial and fibonacci recursion
- Simple Big O analysis

**Suggested pacing adjustments:**
- Skip generators, decorators, closures
- Skip complex recursion (Tower of Hanoi, permutations)
- Reduce Big O to essentials: O(1), O(n), O(n²)
- Provide loop-based alternatives to comprehensions
- Use templates for complex comprehensions

**Prerequisite gaps to watch for:**
- If weak on functions, review function definition and calls before Day 1
- If weak on loops, they'll struggle with comprehensions; review for loops
- If weak on data structures, review lists/dicts before Day 6

**Reteaching strategies:**
- Use the same examples repeatedly
- Physical tracing of recursion on paper
- Side-by-side comparison: lambda vs regular function, comprehension vs loop
- Pair with stronger students for lab days

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Complete practice problems covering all concepts
- Participate in labs
- Pass the unit assessment

**Which practice problems to assign:**
- Core beginner and intermediate problems
- Focus on functional programming (Days 1–10)
- Basic recursion (Days 11–16)
- Basic Big O analysis (Days 17–19)

**Pacing tips:**
- Days 1–10 should feel manageable
- Days 11–16 (recursion) requires careful pacing; watch for confusion
- Days 17–19 introduce abstract concept (Big O); monitor closely

### For Advanced Students

**Extension activities:**
- Implement recursive solutions to complex problems
- Analyze real code for Big O complexity
- Implement memoization for recursive functions
- Study dynamic programming as advanced recursion technique
- Build decorator-based frameworks
- Implement generator-based data pipelines

**Challenge problems to assign:**
- Complex recursion (Tower of Hanoi, permutations, combinations)
- Nested comprehensions with multiple conditions
- Generator functions for memory-efficient processing
- Algorithm optimization challenges
- Performance benchmarking and analysis

**Ways to deepen understanding:**
- Study multiple recursion solutions and compare efficiency
- Implement decorators for timing, caching, validation
- Analyze real-world algorithms (binary search, merge sort preview)
- Explore generator patterns in data processing
- Study Python's functional programming capabilities (functools module)

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 5:** Checkpoint for functional programming fundamentals
- **After Day 10:** Checkpoint for comprehensions before moving to recursion
- **After Day 16:** Checkpoint for recursion before Big O
- **After Day 21:** Final checkpoint before assessment

### Topics students typically struggle with:
1. **Lambda syntax** (Days 1–5): Unusual syntax
   - *Fix:* Start with regular functions, introduce lambdas as shorthand
2. **Recursion** (Days 11–16): Abstract concept, difficult to visualize
   - *Fix:* Trace calls on paper, use print statements to show execution
3. **Big O notation** (Days 17–19): Abstract analysis
   - *Fix:* Concrete examples, counting operations, visual patterns
4. **Nested comprehensions** (Days 6–7): Multiple levels of logic
   - *Fix:* Build from simple comprehensions, add nesting gradually
5. **Generators** (Days 8–9): Lazy evaluation is non-obvious
   - *Fix:* Compare to lists, explain memory efficiency

### Topics students typically move through quickly:
1. **map() and filter()** (Days 2–3): Once they see examples
2. **Simple comprehensions** (Days 6–7): Pattern is straightforward
3. **Factorial recursion** (Day 11): Clear base case and recursion
4. **Basic Big O** (Days 17–18): Simple O(n) and O(n²) analysis
5. **zip()** (Day 4): Intuitive once shown

### Coding 1 gaps that surface here:
- **Functions:** If weak, they'll struggle with lambda and higher-order functions
- **Loops:** If weak, comprehensions won't make sense
- **Scope:** If weak, closures and decorators will be confusing

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 5:** Can students use lambda, map, filter?
   - Quick task: "Filter numbers > 5 using filter()"
2. **After Day 10:** Can students write comprehensions?
   - Quick task: "Write a list comprehension to square all numbers"
3. **After Day 16:** Can students write and analyze recursion?
   - Quick task: "Write factorial() and trace the call stack"
4. **After Day 21:** Can students analyze Big O?
   - Quick task: "What's the Big O of searching a list?"

### Summative checks (end-of-unit):
1. **Day 27 Assessment:**
   - Part A: Multiple choice (syntax, concepts, Big O)
   - Part B: Short answer (explain recursion, algorithm analysis)
   - Part C: Coding (write functions, analyze complexity)

### Lab checkpoints (Days 5, 10, 16, 21, 22–23):
- Demonstrate functional programming, recursion, and algorithm design in practice

---

## Notes on Unit 2 Prerequisites

This unit builds on Unit 2 (classes) and assumes strong Unit 1 (data structures) knowledge. Watch for:

- **Data structures:** If weak on lists/dicts, comprehensions won't make sense
- **Functions:** If weak on function definition/calls, lambda and higher-order functions will be hard
- **Scope:** If weak on variable scope, closures will be confusing
- **Loops:** If weak on for loops, comprehensions won't click

---

## Time Management Tips

- **If 5 days ahead:** Use time for advanced recursion, decorators, dynamic programming, or early Unit 4 start
- **If 3 days behind:** Skip decorators/closures, simplify recursion, provide templates for comprehensions
- **If 1 week behind:** Focus only on functional programming (Days 1–10) and basic recursion; skip Big O and advanced topics
- **If 2 weeks behind:** Teach only functional programming basics; skip recursion and Big O

---

## Key Assessment Targets

By the end of Unit 3, all students should demonstrate:
1. Using lambda functions for simple transformations
2. Applying map() and filter() to collections
3. Writing list comprehensions with conditions
4. Writing dictionary and set comprehensions
5. Implementing and analyzing recursion (base case, recursive case, call stack)
6. Understanding Big O notation for basic complexities (O(1), O(n), O(n²), O(log n))
7. Analyzing algorithm efficiency

Students working at advanced level should additionally demonstrate:
- Complex recursion with optimization (memoization)
- Generator functions and lazy evaluation
- Decorators and closures
- Advanced Big O analysis
- Algorithm design and optimization
