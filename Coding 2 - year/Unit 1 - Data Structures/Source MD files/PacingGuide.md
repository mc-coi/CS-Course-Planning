# Unit 1 - Data Structures: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 22 days (~4.5 weeks)
- **Core topics covered:**
  - Lists: creation, indexing, slicing, methods, comprehensions, 2D lists
  - Tuples: immutability, unpacking, named tuples, use cases
  - Dictionaries: creation, access, methods, nested structures, comprehensions
  - Sets: operations, frozensets, membership testing, real-world applications
  - Choosing appropriate data structures for different problems
- **Prerequisites students need:**
  - Basic Python syntax (variables, operators, if/else, loops)
  - Understanding of function calls and method syntax
  - Familiarity with indexing from Coding 1

---

## Week-by-Week Pacing

### Week 1 (Days 1–6): Lists & Fundamentals

#### Day 1: List Creation & Indexing
- **Essential days** (must teach): YES
  - This is the foundation for all subsequent list work. Students must understand creation syntax and 0-based indexing.
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Introduce advanced list constructor patterns (list(), list comprehensions preview)
- **If behind pace**: Spend extra time on indexing with visual aids; use short, repeated examples

#### Days 2–3: Indexing, Slicing & List Methods
- **Essential days** (must teach): YES
  - Slicing is fundamental to working with data. Methods like append, remove, pop are essential
- **Flexible days** (can compress or cut if pressed for time): Negative indexing can be touched briefly and revisited later if needed
- **If ahead of pace**: Explore advanced slicing patterns (step parameter), introduce slice assignment
- **If behind pace**: Focus on positive indexing first, then slicing with [start:stop] before introducing step. Use list.append() and list.remove() as the core methods

#### Days 4–5: List Comprehensions
- **Essential days** (must teach): YES
  - List comprehensions are core Pythonic syntax; they appear throughout the course
- **Flexible days** (can compress or cut if pressed for time): Complex nested comprehensions can be deferred if time is tight
- **If ahead of pace**: Nested comprehensions with multiple conditions, generator expressions preview
- **If behind pace**: Start with very simple comprehensions: [x*2 for x in range(5)], then add conditions slowly

#### Day 6: 2D Lists & Nested Structures
- **Essential days** (must teach): YES
  - Students need to work with matrices and nested data structures throughout the unit
- **Flexible days** (can compress or cut if pressed for time): Complex deep nesting (3D+ lists) can wait or be optional
- **If ahead of pace**: Flattening algorithms, jagged arrays, multi-level access patterns
- **If behind pace**: Stick to simple 3x3 matrices and [row][col] access patterns

### Week 2 (Days 7–11): Tuples & Dictionaries Intro

#### Day 7: Tuples & Immutability
- **Essential days** (must teach): YES
  - Understanding immutability is critical for later work (e.g., dictionary keys)
- **Flexible days** (can compress or cut if pressed for time): Named tuples can be skipped if time is tight
- **If ahead of pace**: Named tuples as a bridge to OOP, tuple unpacking with *, advanced packing/unpacking
- **If behind pace**: Focus on tuple creation, indexing (similar to lists), and the concept of "unchangeable"

#### Day 8: Tuples in Real Use
- **Essential days** (must teach): YES for returning multiple values from functions
- **Flexible days** (can compress or cut if pressed for time): Named tuples, frozensets as dictionary keys can be deferred
- **If ahead of pace**: Named tuples, advanced unpacking, using tuples as function return values in complex scenarios
- **If behind pace**: Focus on simple function return patterns and tuple unpacking with a, b = (1, 2)

#### Day 9: Dictionaries — Creation & Access
- **Essential days** (must teach): YES
  - Dictionaries are essential for key-value lookups and appear throughout the rest of the course
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Dict() constructor with keyword arguments, dictionary comprehensions preview
- **If behind pace**: Simple dictionary creation and bracket access; .get() method is important for safe access

#### Day 10: Dictionary Methods & Iteration
- **Essential days** (must teach): YES
  - .items(), .keys(), .values() and iteration patterns are essential
- **Flexible days** (can compress or cut if pressed for time): .setdefault() and .update() can be optional if time is tight
- **If ahead of pace**: defaultdict from collections, OrderedDict, advanced iteration patterns
- **If behind pace**: Focus on .items() iteration first; .pop() and .get() as safe access patterns

#### Day 11: Nested Dictionaries
- **Essential days** (must teach): YES
  - Students will work with nested data structures throughout the unit and in later units
- **Flexible days** (can compress or cut if pressed for time): Deep nesting (3+ levels) is optional
- **If ahead of pace**: Chaining .get() calls for deep safety, recursive traversal
- **If behind pace**: Simple 2-level nesting with clear examples (e.g., school → classes → teacher)

### Week 3 (Days 12–17): Sets & Data Structure Selection

#### Day 12: Sets & Set Operations
- **Essential days** (must teach): YES
  - Sets are essential for unique elements and fast membership testing
- **Flexible days** (can compress or cut if pressed for time): Frozensets can be optional
- **If ahead of pace**: Frozensets as dictionary keys, set comprehensions, bitwise operations on sets
- **If behind pace**: Focus on creating sets and the membership test (in operator), basic union/intersection

#### Day 13: Frozensets & Real-World Uses
- **Essential days** (must teach): PARTIAL
  - Set use cases are important; frozensets are less critical
- **Flexible days** (can compress or cut if pressed for time): YES — frozensets can be deferred
- **If ahead of pace**: Frozensets for immutable collections, permissions/role-based access patterns
- **If behind pace**: Focus on set operations for removing duplicates and finding common elements

#### Day 14: Choosing the Right Data Structure
- **Essential days** (must teach): YES
  - This conceptual day ties together all structures; essential for problem-solving
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Trade-off analysis for different scenarios, performance comparisons with timing
- **If behind pace**: Provide a clear decision tree table; use concrete examples repeatedly

#### Day 15: Dictionary & Set Comprehensions
- **Essential days** (must teach): YES
  - Comprehensions for all types are essential Pythonic syntax
- **Flexible days** (can compress or cut if pressed for time): Can be combined with Day 14 if compressed
- **If ahead of pace**: Complex comprehensions with nested conditions, set comprehensions with transformations
- **If behind pace**: Start with simple comprehensions: {x: x**2 for x in range(5)} and {1, 2, 3}

### Week 4 (Days 16–22): Integration & Assessment

#### Day 16–17: Mini-Projects (Gradebook, Inventory)
- **Essential days** (must teach): YES
  - Application of all concepts; students must see integration before assessment
- **Flexible days** (can compress or cut if pressed for time): Can be condensed to 1 day if behind
- **If ahead of pace**: Students can extend projects with features (sorting, filtering, analytics)
- **If behind pace**: Provide template code; focus on putting existing concepts together rather than creating from scratch

#### Day 18: Code Review & Debugging Workshop
- **Essential days** (must teach): YES
  - Students learn common mistakes and debugging strategies
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 19 if needed
- **If ahead of pace**: Peer code review, refactoring for readability
- **If behind pace**: Teacher-led code review with live debugging examples

#### Day 19: Unit Review & Assessment Prep
- **Essential days** (must teach): YES
  - Essential for consolidating learning before the assessment
- **Flexible days** (can compress or cut if pressed for time): Can be combined with Day 18
- **If ahead of pace**: Students create their own practice problems; teach study strategies
- **If behind pace**: Provide a comprehensive study guide with categorized problems by difficulty

#### Day 20–22: Assessment (Days 20–21), Flex/Reteach (Day 22)
- **Essential days** (must teach): YES
  - Assessment is required; Day 22 provides time for reteaching
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early assessors can start Unit 2; others get enrichment
- **If behind pace**: Use Day 22 for targeted reteaching based on assessment results

---

## Differentiation Strategies

### For Struggling Students

**Common gaps from Coding 1:**
- May not fully understand indexing or loops from Unit 1
- Confusion between list and dictionary access patterns
- Difficulty with nested structures

**Specific scaffolding for this unit:**
- Use visual representations: draw index positions, show [row][col] on a grid
- Start with concrete examples: student names (list), student-to-GPA (dictionary)
- Provide a **"Data Structure Cheat Sheet"** with examples for each type
- Focus on practical methods first: list.append(), dict.get(), set.add()

**Which practice problems to assign first:**
- Problem 1.1 (list indexing and slicing)
- Problem 1.2 (dictionary creation and access)
- Problem 1.5 (basic set operations)
- Then move to 2.1 (list comprehension for basic transformation)

**Suggested pacing adjustments:**
- Spend 2 days on Days 1–2 (list indexing) instead of 1 day
- Skip frozensets entirely
- Use templates for nested structures (provide the structure, have them fill in data)
- Reduce the depth of nested structures (e.g., only 2 levels)

**Prerequisite gaps to watch for:**
- If students struggle with loops, review for loops before Day 6 (comprehensions)
- If students are unsure about method syntax (e.g., list.append(x)), do extra practice

**Reteaching strategies:**
- Use the same examples repeatedly (e.g., a student roster with names and grades)
- Have students physically map out how indexing works
- Pair students for peer tutoring on Day 16–17 mini-projects

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Complete all beginner and intermediate practice problems
- Do the two mini-projects (Gradebook and Inventory)
- Pass the unit assessment

**Which practice problems to assign:**
- Problem 1.1 through 2.5 (Beginner and Intermediate levels)
- Assign as practice homework or in-class work
- Focus on understanding, not just correctness

**Pacing tips:**
- Days 1–7 should feel manageable
- Days 9–15 pick up in complexity; this is where differentiation happens
- Days 16–17 are critical for consolidation

### For Advanced Students

**Extension activities:**
- **Problem 3.1 (Transpose):** Have students implement matrix rotation (90°, 180°, 270°)
- **Problem 3.2 (Grade Analysis):** Add weighted grades, GPA calculation by course, trend analysis
- **Problem 3.3 (Anagrams):** Find anagrams from a real dictionary file; suggest word corrections
- **Problem 3.4 (Vending Machine):** Add currency handling, sales reports, inventory tracking
- **Problem 3.5 (Word Association):** Make it bidirectional; add confidence scores to associations

**Challenge problems to assign:**
- All Challenge level problems (3.1–3.5)
- Extend with the "Challenge Extensions" listed in the UnitPractice.md

**Ways to deepen understanding:**
- Analyze performance: which data structure is fastest for a given task?
- Implement a custom data structure (e.g., a simple cache using dictionaries)
- Write their own "performance comparison" by timing different approaches
- Teach them about hash tables and why dictionary lookups are O(1)
- Have them explore collections module (defaultdict, Counter, deque)

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 6:** Good checkpoint for list mastery before moving to new structures
- **After Day 11:** Good checkpoint before sets (which require different mindset)
- **After Day 15:** Final practice point before application

### Topics students typically struggle with:
1. **Nested structures** (Days 7–8, 11, 13): Requires mental model of "structure within structure"
   - *Fix:* Use visual diagrams, build one level at a time
2. **Immutability of tuples** (Day 7): Abstract concept
   - *Fix:* Show what happens when you try to modify; contrast with lists
3. **Dictionary iteration** (Day 10): Multiple ways to iterate can be confusing
   - *Fix:* Emphasize .items() first; others are optional
4. **Sets vs. Lists** (Day 12–14): When to use which?
   - *Fix:* Provide decision criteria: ordered? indexed? unique?

### Topics students typically move through quickly:
1. **Basic list operations** (Days 1–3): Most intuitive
2. **Dictionary creation and access** (Days 9–10): Syntax is clear
3. **Set membership testing** (Day 12): Just like list membership
4. **Comprehensions** (once they "get" the syntax): Fast once the pattern clicks

### Coding 1 gaps that surface here:
- **Loops:** If students didn't master for loops, they'll struggle with iteration and comprehensions
  - *Monitor:* Days 4–5, 10, 15
  - *Fix:* Quick review of for loops before Day 4
- **Function calls/methods:** If students don't know method syntax well, Days 4, 10, 12 will be slow
  - *Monitor:* First day of each new structure
  - *Fix:* Brief review of object.method(args) syntax

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 5:** Can students create lists, index them, slice them, and use basic comprehensions?
   - Quick quiz: 5 questions (creation, indexing, slicing, methods, comprehension)
2. **After Day 11:** Can students work with dictionaries and nested structures?
   - Quick quiz: 5 questions (creation, access, iteration, nesting, safe access)
3. **After Day 15:** Can students choose appropriate structures?
   - Mini task: "For this scenario, which structure would you use and why?"

### Summative checks (end-of-unit):
1. **Day 20–21 Assessment:**
   - Part A: Multiple choice (data structure properties, syntax)
   - Part B: Short answer (explain a concept, trace code)
   - Part C: Coding (problems like the practice bank, increasing difficulty)

### Code review checkpoints (Days 16–18):
- Day 16–17: Students submit mini-project code; you/peers review for:
  - Correct data structures chosen
  - Proper syntax
  - Working output
- Day 18: Live debugging workshop highlights common mistakes

---

## Notes on Coding 1 Prerequisites

This unit assumes students have solid Coding 1 foundations. Watch for these gaps:

- **Loops:** If students struggle with for loops, they'll struggle with comprehensions and iteration
- **Functions:** If students aren't comfortable calling methods, Days 4, 10, 12 will be slow
- **Conditional logic:** If students don't understand if/else well, the filtering in comprehensions will be hard
- **Indexing basics:** Some students may not have strong indexing from Coding 1 — Day 1 is essential for review

If you notice gaps, do a brief review of the Coding 1 concept before moving forward. Don't let weak foundations slow down the whole class; use small group review or extended practice during Days 16–18.

---

## Time Management Tips

- **If 5 days ahead:** Use the time for deeper projects, extensions, or early Unit 2 start
- **If 3 days behind:** Combine Days 16–17 mini-projects into 1 day; skip frozensets; provide more templates
- **If 1 week behind:** Focus only on Lists (Days 1–6), Dicts (Days 9–11), and Sets (Days 12–13); defer comprehensions; simplify projects
- **If 2 weeks behind:** Teach only the essential data structures (lists, dicts, sets); minimal nesting; provide templates for projects

---

## Key Assessment Targets

By the end of Unit 1, all students should demonstrate:
1. Creating, indexing, and modifying lists
2. Using list comprehensions for simple transformations
3. Creating and accessing dictionaries safely
4. Iterating through dictionaries with .items()
5. Understanding when to use sets (unique elements, membership)
6. Choosing appropriate data structures for given problems
7. Working with nested structures (at least 2 levels)

Students working at advanced level should additionally demonstrate:
- Writing nested comprehensions
- Designing efficient solutions using appropriate structures
- Analyzing performance trade-offs
- Extending projects with custom features
