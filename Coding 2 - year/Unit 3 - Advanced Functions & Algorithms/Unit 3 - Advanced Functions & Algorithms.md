# Unit 3: Advanced Functions & Algorithms

## Unit Overview

**Duration:** 27 days (5.5 weeks), 55-minute periods
**Credit Standard:** TN 9-12.CCI.3 - Computational Thinking & Programming

This unit builds on foundational Python skills to explore advanced function patterns, recursion, and algorithm design. Students master lambda functions, higher-order functions (map, filter, zip), comprehensions, recursion with base and recursive cases, Big O notation, decorators, closures, generators, and iterators. Through hands-on practice and real-world applications, students develop problem-solving skills essential for computer science.

**Key Learning Outcomes:**
- Write and use lambda functions and higher-order functions
- Master comprehensions (list, dict, set, generator)
- Understand and implement recursive solutions
- Analyze algorithms using Big O notation
- Create decorators and closures
- Build custom iterators and generators
- Apply functional programming patterns

---

## Daily Breakdown (Days 1-27)

### Week 1: Functional Programming Fundamentals

**Day 1: Lambda Functions — Syntax, Uses, Limitations**
- Learning Target: Create and use lambda functions for simple operations
- Key Topics: Anonymous functions, single expressions, limitations
- Practice: Write lambdas for transformation and filtering

**Day 2: map() — Transforming Collections**
- Learning Target: Use map() to transform every element in a collection
- Key Topics: Higher-order functions, lazy evaluation, chaining
- Practice: Apply transformations with map() and lambda

**Day 3: filter() — Selecting Elements**
- Learning Target: Use filter() to select elements based on conditions
- Key Topics: Predicate functions, filtering logic, None as filter
- Practice: Filter data by multiple criteria

**Day 4: zip() & enumerate()**
- Learning Target: Combine and index iterables with zip() and enumerate()
- Key Topics: Pairing data, lazy iteration, unpacking
- Practice: Parallel iteration, creating lookups

**Day 5: Functional Programming Lab**
- Learning Target: Combine lambda, map, filter, and zip in real applications
- Key Topics: Function composition, data pipelines
- Practice: Real-world data processing problems

### Week 2: Comprehensions & Generators

**Day 6: Advanced List Comprehensions (Nested, Conditional)**
- Learning Target: Write nested and conditional list comprehensions
- Key Topics: Nested loops, multiple conditions, performance
- Practice: Complex transformations with comprehensions

**Day 7: Dictionary & Set Comprehensions**
- Learning Target: Create dictionaries and sets using comprehension syntax
- Key Topics: Key-value mapping, uniqueness, transformation
- Practice: Build lookup tables and unique collections

**Day 8: Generator Expressions & yield**
- Learning Target: Create generators for memory-efficient data processing
- Key Topics: yield keyword, lazy evaluation, infinite sequences
- Practice: Generator functions and expressions

**Day 9: Comprehension Lab**
- Learning Target: Choose and implement the right comprehension type
- Key Topics: Trade-offs between types, readability vs. terseness
- Practice: Multi-type comprehension challenges

### Week 3: Recursion

**Day 10: Introduction to Recursion — Base Case & Recursive Case**
- Learning Target: Explain recursion and identify base and recursive cases
- Key Topics: Call stack, base case necessity, recursion depth
- Practice: Trace recursive calls on paper

**Day 11: Recursion — Factorial, Fibonacci**
- Learning Target: Solve classic recursive problems with optimization
- Key Topics: Memoization, efficiency, mathematical sequences
- Practice: Optimize recursive solutions

**Day 12: Recursion — Towers of Hanoi, Flattening Nested Lists**
- Learning Target: Solve complex recursive problems and work with nested structures
- Key Topics: Multi-step decomposition, nested data handling
- Practice: Real algorithm implementations

**Day 13: Recursion vs Iteration — When to Use Which**
- Learning Target: Compare recursive and iterative solutions
- Key Topics: Performance, readability, memory, problem fit
- Practice: Implement both approaches and evaluate

**Day 14: Recursion Lab**
- Learning Target: Apply recursion to diverse real-world problems
- Key Topics: Problem decomposition, edge cases, testing
- Practice: Permutations, combinations, algorithm design

### Week 4: Algorithms & Complexity

**Day 15: Algorithm Design & Pseudocode**
- Learning Target: Write pseudocode and design algorithms systematically
- Key Topics: Top-down design, control flow, algorithm templates
- Practice: Pseudocode for classic algorithms

**Day 16: Big O Notation — Time Complexity Basics**
- Learning Target: Analyze and classify algorithms by time complexity
- Key Topics: Common complexities O(1) through O(n!), practical implications
- Practice: Analyze code for complexity class

**Day 17: Big O — Space Complexity & Common Patterns**
- Learning Target: Analyze space complexity and understand time/space tradeoffs
- Key Topics: Call stack, auxiliary space, memory efficiency
- Practice: Optimize for space or time

### Week 5: Advanced Functions

**Day 18: Closures — Functions Remembering State**
- Learning Target: Use closures to create functions that remember state
- Key Topics: Enclosing scope, LEGB rule, nonlocal keyword
- Practice: State management with closures

**Day 19: Decorators — Wrapping Functions**
- Learning Target: Write decorators to modify function behavior
- Key Topics: Function wrapping, @decorator syntax, metadata preservation
- Practice: Simple decorator implementations

**Day 20: Practical Decorators (Timing, Logging, Memoization)**
- Learning Target: Implement real-world decorators
- Key Topics: functools.wraps, common patterns, performance
- Practice: Timing, logging, and caching decorators

**Day 21: Decorator Lab**
- Learning Target: Apply decorators to complex problems
- Key Topics: Decorator composition, parameterized decorators
- Practice: Multi-decorator solutions

**Day 22: Iterators & Iterables**
- Learning Target: Understand and implement iterator protocol
- Key Topics: __iter__, __next__, StopIteration, iteration protocol
- Practice: Custom iterators

**Day 23: Custom Iterators with __iter__ and __next__**
- Learning Target: Create custom iterator classes
- Key Topics: Iterator pattern, state management, protocol implementation
- Practice: Complex iterator implementations

**Day 24: Generators Deep Dive**
- Learning Target: Master generator syntax and advanced patterns
- Key Topics: Generator chaining, send(), memory efficiency
- Practice: Advanced generator techniques

### Week 6: Review & Assessment

**Day 25: Review Day — Advanced Functions**
- Learning Target: Connect and review all unit concepts
- Key Topics: Comparison matrix, common mistakes, best practices
- Practice: Integrated challenges

**Day 26: Practice Day — Algorithm Challenges**
- Learning Target: Apply all concepts to challenging problems
- Key Topics: Complex problem-solving, algorithm selection
- Practice: Coding challenges from multiple domains

**Day 27: Unit 3 Assessment**
- Learning Target: Demonstrate mastery of all Unit 3 concepts
- Assessment Types: Multiple choice, short answer, coding problems
- Coverage: All 27 days of content

---

## Common Mistakes & How to Avoid Them

| Mistake | Why It Happens | Solution |
|---------|---|---|
| Using `==` instead of `is` for None | Equals feels like a comparison | Use `if x is None:` always |
| Forgetting parentheses when passing function to map/filter | Lambda has parentheses, function doesn't | `map(int, list)` NOT `map(int(), list)` |
| Recursion without base case | Excited about recursion, forgot to stop | Always write base case first |
| List slicing creates new list in recursion | Each call to lst[1:] copies the list | Use indices instead: `function(lst, start+1)` |
| Mutable default arguments | `def f(x, lst=[]):` captures at definition time | Use `def f(x, lst=None):` instead |
| Loop variable in closure captures reference | `[lambda: i for i in range(3)]` all return 2 | Use default argument: `lambda i=i: i` |
| Not using `@wraps` in decorators | Metadata lost, debugging harder | Always: `from functools import wraps` |
| Confusing `map()` return type | Returns iterator, not list | Convert: `list(map(...))` |
| Generator exhaustion | Generators can only be iterated once | Create new generator for second iteration |
| Analyzing wrong complexity | Confusing best/average/worst cases | Specify which case you're analyzing |

---

## Assessment Rubric

### Beginner Level (Days 1-9)
- Use lambdas and map/filter appropriately
- Write working list comprehensions
- Understand basic functional patterns
- Success Rate: 70%+ on beginner problems

### Intermediate Level (Days 10-17)
- Implement recursive solutions with correct base/recursive cases
- Analyze time and space complexity
- Design algorithms with pseudocode
- Success Rate: 70%+ on intermediate problems

### Advanced Level (Days 18-27)
- Create and use closures and decorators
- Build custom iterators and generators
- Optimize algorithms for performance
- Apply multiple concepts together
- Success Rate: 70%+ on challenge problems

---

## Unit 3 Practice Bank

### Functional Programming (5+ problems)
- Lambda and higher-order function challenges
- Comprehension complexity challenges
- Data transformation pipelines

### Recursion (5+ problems)
- Factorial and Fibonacci variants
- Nested structure processing
- Algorithm implementation

### Algorithms (5+ problems)
- Sorting and searching implementations
- Complexity analysis challenges
- Algorithm optimization

### Advanced Functions (5+ problems)
- Decorator creation and application
- Iterator and generator implementation
- Closure-based state management

---

## Vocabulary & Quick Reference

**Lambda:** Anonymous function defined with `lambda args: expression`
**Higher-Order Function:** Function that takes or returns functions (map, filter, zip)
**Comprehension:** Concise syntax for creating lists, dicts, sets: `[expr for item in iterable]`
**Recursion:** Function calling itself with smaller problem until base case
**Base Case:** Condition that stops recursion
**Recursive Case:** Code path where function calls itself
**Big O Notation:** Describes how algorithm scales (O(1), O(n), O(n²), etc.)
**Time Complexity:** How runtime grows with input size
**Space Complexity:** How memory grows with input size
**Closure:** Function that remembers variables from enclosing scope
**Decorator:** Function that modifies another function's behavior
**Iterator:** Object with `__iter__` and `__next__` methods
**Generator:** Function using `yield` for lazy evaluation
**Memoization:** Caching function results to avoid recomputation

---

## Unit Success Criteria

Students successfully complete Unit 3 when they can:

1. **Write and use lambda functions** in appropriate contexts
2. **Apply map, filter, and zip** to transform and combine data
3. **Create comprehensions** (list, dict, set, generator) for various tasks
4. **Implement recursive solutions** with correct base and recursive cases
5. **Analyze algorithms** using Big O notation for time and space
6. **Write decorators** to modify function behavior
7. **Create closures** that manage state
8. **Build custom iterators and generators** for efficient data processing
9. **Choose appropriate tools** for different programming problems
10. **Optimize code** for readability and performance

---

## Prerequisites for Unit 4

- Solid understanding of functions and parameters
- Comfortable with loops and conditionals
- Experience with lists, dictionaries, and sets
- Understanding of algorithm basics
- Ability to write and test Python programs

Students not meeting these prerequisites should review Unit 2 before proceeding.

---

## Additional Resources

**Online Documentation:**
- Python functools module
- Iterator and Generator docs
- Recursion tutorials

**Practice Platforms:**
- LeetCode (algorithm challenges)
- HackerRank (recursion problems)
- Project Euler (algorithm problems)

**Recommended Reading:**
- "Fluent Python" by Luciano Ramalho (Ch. 5-7)
- "Algorithms" by Sedgewick & Wayne

---

## Unit 3 Complete!

Congratulations on completing Unit 3: Advanced Functions & Algorithms. You now have mastered essential computer science concepts including functional programming, recursion, algorithm analysis, and advanced Python features. These skills form the foundation for Object-Oriented Programming (Unit 4) and advanced computer science courses.

**Next Steps:**
- Proceed to Unit 4: Object-Oriented Programming
- Practice these concepts in personal projects
- Explore specialized libraries (functools, itertools, etc.)
- Study classic algorithms in depth

---

**Created:** 2026
**Grade Level:** 9-12
**Subject:** Computer Science / AP Computer Science Principles
**Standards:** TN 9-12.CCI.3
