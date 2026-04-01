# Unit 1 - Data Structures: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 6 days / 2 weeks
- **Core topics covered:** Lists (creation, indexing, slicing, methods), list comprehensions, nested/2D lists, tuples (immutable sequences, packing/unpacking), dictionaries (key-value pairs), sets (unique collections), choosing appropriate data structures
- **Prerequisites students need:** Basic Python syntax (variables, loops, conditionals); foundational understanding of functions

## Week-by-Week Pacing

### Week 1 (Days 1–3): Lists, Tuples & Foundations
- **Essential days** (must teach):
  - Day 1: Lists—indexing, slicing, basic methods (append, remove, pop, sort)
  - Day 2: List comprehensions and nested/2D lists
  - Day 3: Tuples and immutability concept

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Cut advanced slicing patterns (e.g., step values beyond `[::2]`); have students use `.sort()` rather than explore sorting algorithms in detail

- **If ahead of pace:**
  - Extend Day 2: Have students create and manipulate 3D lists or explore complex slicing patterns
  - Have advanced students write code to swap matrix rows/columns using slicing
  - Introduce list comprehension with nested conditions

- **If behind pace:**
  - Combine Days 1–2: Teach lists and list comprehensions in single day; cut some slicing edge cases
  - Move tuple unpacking examples to Day 3 only; skip tuple() constructor variations
  - Consider assigning nested lists as homework rather than class activity

### Week 2 (Days 4–6): Dictionaries, Sets & Application
- **Essential days** (must teach):
  - Day 4: Dictionaries—creation, access, adding/updating, iteration with `.items()`
  - Day 5: Sets and choosing appropriate data structures (comparison table in unit)
  - Day 6: Project (Student Gradebook)—consolidation of all concepts

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Cut frozensets; focus dictionaries on basic operations only
  - Cut set operations (union, intersection) if time is tight—teach just `.add()`, `.remove()`, and membership testing
  - Project day can be shortened: Provide more starter code; reduce features (e.g., skip class average calculation)

- **If ahead of pace:**
  - Extend Day 4: Have students build nested dictionaries (school with departments and teachers)
  - Extend Day 5: Introduce frozensets and use them as dictionary keys; explore more complex set operations
  - Project enhancement: Add sorting by grade/GPA, search functionality, or file I/O (preview Unit 4)

- **If behind pace:**
  - Combine Days 4–5: Teach dictionaries and sets in single day; cover only essential operations
  - Use worksheet with pre-written dictionary/set code for modification rather than creation from scratch
  - Simplify project: Use provided data structure; focus on iteration and access, not building from scratch

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Provide visual representations: Show that lists are like numbered boxes, dictionaries like name tags on boxes
- Use concrete examples: Shopping lists (lists), phonebook (dictionaries), unique colors in a painting (sets)
- Start with built-in data before teaching creation: Show `[1, 2, 3]` works before teaching `list()` constructor
- Provide code templates and fill-in-the-blank exercises

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–5: Create and access basic lists and tuples (Days 1–3)
- Unit Practice #8: Basic dictionary iteration (Day 4)
- Emphasize: Unit Practice #3 (loop through list), #5 (unpack tuple), #1 (set creation)

**Suggested pacing adjustments:**
- Spend extra time on indexing (especially negative indices) with lots of examples
- Delay list comprehensions by 1–2 days; teach loops first, then comprehensions as shortcuts
- Use printed index cards to physically demonstrate indexing and slicing
- Pair-program dictionaries; have one student write keys, other writes values

**What prerequisite gaps to look for:**
- Confusion with 0-based indexing: Many students expect `list[1]` to be second item; they understand it is
- Loop syntax mistakes when iterating dictionaries: Reinforce `for key in dict:` vs. `for item in list:`
- Confusion between `.append()` vs. `+=`: Show both modify the list but differently

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–6 as designed
- Assign Unit Practice problems #1–10 (mix of beginner and intermediate)
- Complete Student Gradebook project as written
- Daily formative checks: Quick quiz at end of each day (3–5 True/False or short-answer questions)

**Which practice problems to assign:**
- Problems #1–4: Lists and indexing
- Problems #5–7: Tuples and list comprehensions
- Problems #8–9: Dictionaries and sets
- Problems #10: Functions returning tuples
- Project: Full Student Gradebook with all features

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 2:** Explore NumPy arrays and compare performance vs. nested lists; benchmark list comprehension vs. loops
- **Day 5:** Create a custom class that mimics dictionary behavior (implement `__getitem__`, `__setitem__`)
- **Project:** Extend Student Gradebook: Add plotting grades with matplotlib; export to CSV; implement weighted GPA calculation

**Challenge problems to assign:**
- Unit Practice #11–15: Nested structures, contact books, filtering with sets, 2D sorting
- Advanced: Implement a student records system where each student is a nested dict with multiple grades per subject
- Challenge: Create a "word frequency counter" program (read a sentence, use sets to find unique words, dictionaries to count)

**Ways to deepen understanding beyond the curriculum:**
- Explore alternative data structures: Explain when OrderedDict is useful (older Python versions)
- Introduce the concept of data structure trade-offs explicitly: Time vs. space complexity for lookups
- Have them design a data structure for a real problem (e.g., storing a social network—which structure best?)
- Explore dictionary comprehensions: `{x: x**2 for x in range(5)}`

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 1:** Before moving to comprehensions, ensure students master basic indexing. Spend an extra day if needed.
- **After Day 3:** Before dictionaries, ensure tuple unpacking is solid—this concept transfers to function arguments.
- **After Day 5:** Before project, review structure choices with a few example problems (e.g., "What structure for a phone book?")

### Topics students most commonly struggle with:
1. **Negative indexing:** Concept of `list[-1]` as "last element" is non-intuitive; requires repeated practice
2. **Slicing syntax:** The `[start:stop:step]` with exclusive stop is confusing; provide many visual examples
3. **Mutability confusion:** Students try to modify tuples or think all sequences behave identically
4. **Dictionary key access:** Mixing up `dict[key]` with `list[index]`; they seem similar but semantically different
5. **Nested structure indexing:** `matrix[row][col]` or `dict["name"]["first"]` requires careful explanation

### Topics students typically move through quickly:
1. **Basic list methods:** `.append()`, `.pop()`, `.sort()` are intuitive
2. **Set uniqueness:** Students grasp "no duplicates" concept quickly
3. **Dictionary creation:** Once they see `{"key": value}`, they understand the pattern
4. **List iteration:** `for item in list:` is natural extension of loop concept

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Write code that gets the last element of a list using negative indexing"
- "What does `[1:4]` return from a 10-element list?"
- Answer: Elements at indices 1, 2, 3 (exclusive of 4)

**Day 2 Check (5 min):**
- "Create a list of all even numbers 1–20 using list comprehension"
- "Access element [1][2] in matrix `[[1,2,3], [4,5,6]]`"
- Answer: `[x for x in range(2, 21, 2)]` and `6`

**Day 3 Check (5 min):**
- "Create a tuple with 3 elements and unpack into variables x, y, z"
- "Why can't you do `t[0] = 10` with a tuple?"
- Answer: Tuples are immutable

**Day 4 Check (5 min):**
- "Create a dictionary with 3 key-value pairs and print all values"
- "How do you safely access a key that might not exist?"
- Answer: Use `.get(key, default)`

**Day 5 Check (5 min):**
- "Create a set and add 3 elements"
- "Given two sets, how do you find common elements?"
- Answer: `set1 & set2` (intersection)

**Day 6 Check (Project submission):**
- Student Gradebook demonstrates: list/dict usage, iteration, method calls
- Rubric: Correct data structure choices, working add/view/calculate functions, clean code

## STEM-Specific Pacing Notes

**Important:** Coding 2 STEM is a semester-length course with tighter timelines than regular Coding 2. Be explicit about priorities:

- **Essential vs. Optional:**
  - Essential: Lists, basic dict operations, understanding choosing data structures (Days 1, 4–5)
  - Optional: Advanced slicing patterns, frozensets, complex nested structures

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: loop syntax, function calls, basic variable assignment
  - These gaps will surface when iterating dicts/lists
  - Be prepared with syntax review for loop iteration

- **When to cut:**
  - If behind after Day 3, skip frozensets entirely and reduce set operations to basics
  - Cut 2D list manipulation beyond simple access if timing is tight
  - Project: Provide 50% more starter code if class is under time pressure

- **When to accelerate:**
  - Advanced students can jump to Unit 2 early if they demonstrate mastery by Day 4
  - Use excess time for real-world applications: parsing CSV (preview Unit 4), building menus with dicts
