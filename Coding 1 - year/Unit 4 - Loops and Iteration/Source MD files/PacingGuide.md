# Unit 4 - Loops and Iteration: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 25 days / 5 weeks (Days 71–95, 55-minute periods)
- **Core topics covered:** while loops (condition, counter pattern, sentinel pattern, accumulator pattern, input validation loops), for loops with range() (start, stop, step), loop control (break, continue), nested loops, iterating over strings, lists (creating, indexing, methods like .append(), .remove(), .sort(), .reverse()), list comprehensions (preview), common loop patterns (min/max, search, flag patterns)
- **Prerequisites students need:** Mastery of Unit 3 (conditionals); understanding of Boolean expressions; ability to write multi-line programs with indentation

---

## Week-by-Week Pacing

### Week 15 (Days 71–75): While Loops
**Topics:** while loop syntax and condition, counter pattern, sentinel loops (user-controlled exit), accumulator pattern (running totals), common errors (infinite loops, off-by-one), practice labs

#### Essential days (cannot skip):
- **Day 71:** while loop syntax and condition evaluation — foundational control structure
- **Day 73:** Accumulator pattern (running totals, counting) — one of the most important patterns in programming
- **Day 74:** Input validation loops — essential for robust programs
- **Day 75:** Practice lab combining all three days

#### Flexible days (can compress or cut if pressed for time):
- **Day 72 (Sentinel Loops):** Can be abbreviated to a 10-minute demo with one example; students often understand this concept quickly once they see counter loops

#### If ahead of pace:
- Introduce while True with break patterns (common in real code)
- Have them write more complex loops: calculating Fibonacci, filtering data, finding factors
- Challenge: write a loop that detects and prevents infinite loops (timeout mechanism, iteration limit)

#### If behind pace:
- Spend 2 days on while loop syntax (Days 71–72) before introducing patterns
- Focus only on counter and accumulator patterns first; defer sentinel loops
- Provide flowcharts alongside code to make loop logic visual
- **Minimum viable coverage:** Days 71–73 (while syntax, counter pattern, accumulator pattern)

---

### Week 16 (Days 76–80): For Loops & Range
**Topics:** for loop with range(), range parameters (start, stop, step), iterating over strings character-by-character, for vs while (choosing the right tool), nested for loops preview, pattern printing

#### Essential days (cannot skip):
- **Day 76:** for loop with range() — cleaner alternative to while for counted loops
- **Day 77:** range() parameters (start, stop, step) — critical flexibility
- **Day 78:** Iterating over strings and lists — foundation for list processing
- **Day 80:** Practice lab combining all three days

#### Flexible days (can compress or cut if pressed for time):
- **Day 79 (for vs while):** Can be a 10-minute discussion rather than a full lesson; guide students to choose the right tool through practice

#### If ahead of pace:
- Introduce negative step and reverse iteration: `range(10, 0, -1)`, `for char in word[::-1]`
- Have them use range() with step to print multiples or patterns
- Challenge: write a program that prints ASCII art or patterns using nested loops

#### If behind pace:
- Simplify range() coverage; focus on range(n) and range(a, b) only; defer step parameter
- Spend extra time iterating over strings; this is a fundamental concept
- Combine Days 78 and 79 into one day
- **Minimum viable coverage:** Days 76–77 (for loops, basic range())

---

### Week 17 (Days 81–85): Loop Control & Nested Loops
**Topics:** break statement (exit loop early), continue statement (skip iteration), nested loops (loops inside loops), nested loop applications (multiplication tables, patterns), common loop patterns (min/max finding, search, flag patterns)

#### Essential days (cannot skip):
- **Day 81:** break and continue — critical control mechanisms
- **Day 82:** Nested loops — enables complex iteration tasks
- **Day 84:** Common loop patterns (min/max, search, flag patterns) — real-world patterns students will use repeatedly
- **Day 85:** Practice lab combining all three days

#### Flexible days (can compress or cut if pressed for time):
- **Day 83 (Nested Loop Applications):** Can be absorbed into Day 82 or combined with Day 85 if time is tight

#### If ahead of pace:
- Introduce more complex nested loop scenarios: nested loop with conditionals, break from nested loops
- Have them write programs that find patterns in data (prime numbers, palindromes within ranges)
- Challenge: write a program that uses nested loops with accumulated results (e.g., sum of products)

#### If behind pace:
- Defer nested loops; focus on break/continue with simple loops first
- Simplify nested loop examples (2 levels only, not 3+)
- Provide flowcharts for nested loop logic
- **Minimum viable coverage:** Days 81–82 (break/continue, basic nested loops)

---

### Week 18 (Days 86–90): Lists & Loop Applications
**Topics:** Lists (creating, indexing, len()), looping through lists (for item in list), list methods (.append(), .remove(), .sort(), .reverse(), .index()), list modification, mini-projects combining loops and lists

#### Essential days (cannot skip):
- **Day 86:** Lists intro (creating, indexing, len()) — data structure foundation
- **Day 87:** Looping through lists (for item in list) — critical list processing technique
- **Day 88:** List methods (.append(), .remove(), .sort()) — practical list manipulation
- **Days 89-90:** Mini-projects — students apply loops and lists together

#### Flexible days (can compress or cut if pressed for time):
- None. Lists are essential for any programming beyond trivial tasks.

#### If ahead of pace:
- Introduce list slicing: `my_list[1:3]`, negative indices
- Teach list comprehensions (preview): `[x*2 for x in range(5)]`
- Have them build more complex data structures (list of lists) and iterate through them
- Challenge: write a quiz game that stores questions and scores in lists

#### If behind pace:
- Spend 2 days on list basics (Days 86–87) before introducing methods
- Focus on only .append() and .sort() first; defer other methods
- Extend mini-project work days (Days 89–90) with extra support
- **Minimum viable coverage:** Days 86–88 (lists, iteration, basic methods)

---

### Week 19 (Days 91–95): Review & Assessment
**Topics:** Comparing while and for loops, nested loop review, list review, code tracing, common mistakes, final practice, unit assessment, reflection

#### Essential days (cannot skip):
- **Day 91:** while and for loop review — tracing execution, choosing the right tool
- **Day 92:** Nested loops and list review — common mistakes workshop
- **Day 94:** Unit 4 Assessment — formal evaluation
- **Day 95:** Assessment review, reflection, semester check-in

#### Flexible days (can compress or cut if pressed for time):
- **Day 93:** Additional practice — can be shortened or extended based on performance

#### If ahead of pace:
- Have students debug intentionally broken loop code
- Challenge them to optimize loop solutions (e.g., minimize iterations)
- Have them create a "loops and lists cheat sheet" for peers

#### If behind pace:
- Spend extra time on Days 91–93 for review and re-teaching
- Offer a retake option for those scoring below mastery
- **Minimum viable coverage:** Days 91 (review), 94 (assessment)

---

## Differentiation Strategies

### For Struggling Students
**Specific scaffolding tips:**
- **While loops:** Use a visual representation of condition checking (circle diagram: check condition → execute body → back to check). Have them trace loops step-by-step.
- **Loop counters:** Always start with counter = 0, then counter += 1. Show the pattern consistently.
- **for vs while:** Use a decision tree: "Is the number of iterations known? Use for. Is it unknown? Use while."
- **Break/continue:** Show the loop flow with arrows/diagrams. continue jumps back to top; break exits loop entirely.
- **Nested loops:** Draw nested boxes; outer loop wraps inner loop. Trace one full execution of the outer loop carefully.
- **Lists:** Use physical analogies (a list is a labeled container with numbered slots). Show indexing visually.

**Which practice problems to assign first (easiest wins):**
- Start with simple while loops: counter from 1 to 10, sum of numbers, countdown
- Then simple for loops: range(5), range(1, 11), print multiples
- Then basic list operations: create list, print each item, append, remove
- Build to nested loops and complex list operations only after foundational confidence

**Suggested pacing adjustments:**
- Spend 2 days on while loop syntax (Days 71–72) instead of 1
- Spend 2 days on for loop syntax (Days 76–77) instead of 1
- Provide step-by-step tracing templates (table: iteration #, condition value, body output)
- Use multiple examples for each pattern; don't move on after one demo

**What prerequisite gaps to look for:**
- **Conditionals:** Can they write an if statement correctly? If indentation is shaky, loops will be harder.
- **Boolean expressions:** Can they evaluate `count < 10`? If not, while conditions will confuse them.
- **Variable reassignment:** Do they understand that `count += 1` changes the variable? Use variable visualization.

### For On-Track Students
**Standard path through the unit:**
- Follow the week-by-week breakdown as written
- Complete practice problems from all five weeks
- Focus on building complete programs (number analyzer, quiz game, grade tracker)

**Which practice problems to assign:**
- Week 15: Simple while loops (counter, accumulator, validation)
- Week 16: for loops with range() (basic to multi-parameter)
- Week 17: break/continue, nested loops, common patterns
- Week 18: Lists and list methods
- All 5 weekly labs (Days 75, 80, 85, 90)

**Expectations:**
- Code should use appropriate loop type (for counted, while for conditional)
- Programs should handle edge cases (empty lists, single element, large values)
- Variable names should be meaningful (count, total, student_grades, not c, t, g)
- Comments should explain loop purpose and critical sections

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Algorithm optimization:** Have them think about loop efficiency (how many iterations? can it be reduced?)
- **List comprehensions:** Teach `[x*2 for x in range(10)]` and filtering `[x for x in numbers if x > 5]`
- **Nested data structures:** Introduce list of lists and iterate through them (2D arrays)
- **Searching and sorting:** Have them implement binary search, bubble sort (algorithm design, not built-ins)

**Challenge problems to assign:**
- Write a program that finds all prime numbers up to 1000 (nested loops, efficiency)
- Implement a simple inventory system with lists and loops (add, remove, search, sort by price)
- Write a number guessing game with binary search (hint: divide search space in half each time)
- Create a gradebook program that stores student grades in lists and calculates statistics

**Ways to deepen understanding beyond the curriculum:**
- Explore loop performance: `for i in range(1000000)` vs. while equivalents; which is faster?
- Introduce Big O notation informally (how does program speed scale with data size?)
- Write programs that generate patterns (pyramids, diamonds) using nested loops
- Build a data processing program (read data, filter, sort, summarize using loops and lists)

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Week 15:** Before moving to for loops, ensure while loop syntax and accumulator pattern are solid
- **End of Week 16:** Before moving to break/continue, ensure for loop range() is mastered
- **After Day 85:** Before list focus, ensure nested loops are comfortable

### Topics students most commonly struggle with (and expected time):
1. **Infinite loops:** 1-2 extra days. Students write `while True:` and forget break, or forget counter increment. Debug by adding print statements.
2. **Loop counter patterns:** 1 extra day. Starting count at 0 vs 1, incrementing at right time, loop condition off-by-one errors.
3. **range() parameters:** 1 day. What is range(1, 10)? (1 to 9, not 1 to 10). Why range(5) starts at 0, not 1.
4. **Nested loop indentation:** 1 extra day. Nested loops require careful indentation; visual guides help.
5. **List indexing:** 1 day. Lists start at index 0, not 1. Negative indices confuse some students.

### Topics students typically move through quickly:
- **for loop with range(n):** Most grasp this in 5 minutes
- **Iterating over strings:** Once they see one example, it's intuitive
- **break statement:** Usually obvious once they see it used
- **List creation and append():** Straightforward once they understand list concept
- **Sorted() and reverse():** Many students quickly pick up basic list methods

---

## Suggested Checkpoints

Use these quick formative checks mid-unit:

### After Day 75 (end of Week 15):
- **Quick Check:** "What does this while loop do?" (Trace `count = 0; total = 0; while count < 5: total += count; count += 1`)
- **Code Check:** Write a while loop that asks for numbers and calculates their sum (sentinel value: "done")

### After Day 80 (end of Week 16):
- **Quick Check:** "What does range(2, 10, 2) produce?" (Answer: 2, 4, 6, 8)
- **Code Check:** Write a for loop that prints all odd numbers from 1 to 20

### After Day 85 (end of Week 17):
- **Quick Check:** "What's the difference between break and continue?" (break exits loop; continue skips to next iteration)
- **Code Check:** Write nested loops to print a 3×3 multiplication table

### Before Day 90 (mid-Week 18):
- **Code Check:** Students' mini-projects with lists and loops. Scan: Do loops iterate correctly? Are list methods used properly?

---

## Common Misconceptions to Watch For

1. **"range(n) goes from 1 to n"** — range(5) produces 0, 1, 2, 3, 4 (not 1 to 5). Start is 0 by default, stop is exclusive.
2. **"You must use while loops"** — for loops are often simpler and clearer for counted iteration.
3. **"Incrementing happens automatically"** — In while loops, you must manually increment counter with `counter += 1`, or loop is infinite.
4. **"break exits all nested loops"** — break exits only the innermost loop, not all levels.
5. **"Lists are the same as strings"** — Lists can contain any type (int, str, bool, even lists). Strings are immutable sequences of characters.
6. **"List indexing starts at 1"** — Lists and strings start at index 0, same as range(). Index 0 is the first element.
7. **".sort() returns a sorted list"** — .sort() modifies the list in place and returns None. Use sorted(list) to get a new sorted list.
8. **"You can modify strings with indexing"** — Strings are immutable. `s[0] = "x"` errors. Use string slicing instead: `s = "x" + s[1:]`.

---

## Notes on Unit 4 Assessment

- **Assessment (Day 94):** Should include code tracing (what does this loop output?), choosing between while/for, writing loops (accumulator, nested, with lists), and a coding task (write a complete program with loops and lists, e.g., grade analyzer, inventory system)
- **Common assessment mistakes:** Off-by-one loop errors, infinite loops, incorrect range() parameters, list indexing errors, forgetting counter increment
- **Retakes:** Offer retakes focused on weakest areas (loop syntax, choosing loop type, list operations)

---

## Performance Benchmarks

By the end of Unit 4, students should be able to:
- Write and trace while and for loops without errors
- Use accumulator pattern to calculate sum, count, average
- Use proper loop type (for for counted iteration, while for conditional)
- Write working nested loops (multiplication table, pattern printing)
- Create lists, access elements, use common methods, iterate through
- Build multi-feature programs combining loops and lists

