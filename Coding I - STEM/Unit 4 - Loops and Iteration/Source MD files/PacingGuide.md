# Unit 4 - Loops & Iteration: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days (compressed for STEM semester)
- **Core topics covered:** while loops with loop control, for loops with range(), loop control flow (break/continue), nested loops, accumulator pattern, iterating over strings, choosing appropriate loop type
- **Prerequisites students need:** Solid Unit 3 mastery (conditionals, Boolean logic); ability to think about repetition and pattern recognition

---

## Week-by-Week Pacing

### Week 1 (Days 1–3): while Loops & Loop Control

#### Day 1: while Loops
- **Essential days:** YES—fundamental iteration structure
- **Key learning:** Loop initialization, condition testing, loop update, avoiding infinite loops, sentinel values
- **What to teach:** Structure of while loop; importance of updating loop variable; countdown patterns; accumulator variable
- **If ahead of pace:** Explore various loop patterns; nested while loops; introduce loop control variables
- **If behind pace:** Simple countdown examples only; use visual trace of loop execution; skip accumulator for now

#### Day 2: Loop Control - break and continue
- **Essential days:** YES—precise control of iterations
- **Key learning:** break (exit loop immediately), continue (skip to next iteration), when to use each, avoiding common pitfalls
- **What to teach:** When break is useful; when continue is useful; difference between them; exiting vs. skipping
- **If ahead of pace:** Complex patterns with nested loops; combining break/continue
- **If behind pace:** Focus on break; skip continue initially; use simple examples

#### Day 3: Accumulator Pattern
- **Essential days:** YES—critical pattern for sum, average, counting
- **Key learning:** Accumulator variable, initializing to 0 (or 1 for product), updating each iteration, final result
- **What to teach:** Sum pattern (total += value); product pattern; count pattern; why initialization matters
- **If ahead of pace:** Variations like min/max tracking; nested accumulators
- **If behind pace:** Sum pattern only; use clear variable names; print at each step to trace

---

### Week 2 (Days 4–6): for Loops & Range

#### Day 4: for Loops with range()
- **Essential days:** YES—for loops more convenient than while for counted iterations
- **Key learning:** for loop structure, range(n), range(start, stop, step), no manual counter needed, when to use for vs. while
- **What to teach:** range() syntax; stop value is exclusive; three-parameter form; how for simplifies while patterns
- **If ahead of pace:** Negative step for countdown; combining range with other operations
- **If behind pace:** range(n) and range(start, stop) only; skip step parameter; use simple counting examples

#### Day 5: Strings and Looping
- **Essential days:** YES—iterating over data is fundamental skill
- **Key learning:** for loop over strings character by character, len() with loops, index-based iteration, accumulating string results
- **What to teach:** Each iteration gets next character; index tracking; building new strings in loops
- **If ahead of pace:** Nested loops with strings; complex string building; comprehensions preview
- **If behind pace:** Iterate character by character; skip index-based loops initially; use simple examples

#### Day 6: Choosing Loop Type & Complex Patterns
- **Essential days:** FLEXIBLE—applying knowledge to scenarios
- **Key learning:** When to use while vs. for, nested loops, combining patterns, real-world applications
- **What to teach:** Decision rubric (counted vs. unknown repetitions); practical nested loop examples (multiplication table, patterns)
- **If ahead of pace:** Complex nested patterns; optimizing with appropriate loop choice
- **If behind pace:** Simple decision trees; provide templates for common patterns

---

### Week 3 (Days 7–9): Applications & Debugging

#### Day 7: Input Validation with Loops
- **Essential days:** YES—professional error handling
- **Key learning:** Using loops to re-ask until valid, combining loops with conditionals, graceful input handling
- **What to teach:** Pattern: "while invalid: ask, validate"; distinguishing sentinel values from errors
- **If ahead of pace:** Sophisticated validation; multiple conditions; try/except introduction preview
- **If behind pace:** Simple single-field validation; use template pattern

#### Day 8: Debugging Loop Logic
- **Essential days:** YES—finding and fixing loop bugs
- **Key learning:** Common loop errors (off-by-one, infinite loops, missing update, wrong initialization), tracing execution, print debugging in loops
- **What to teach:** How to identify infinite loops; off-by-one error patterns; initialization effects; print statements to trace
- **If ahead of pace:** Complex multi-level debugging; optimizing loop logic
- **If behind pace:** Provide loops with hints; trace one iteration by hand first

#### Day 9: Unit 4 Project
- **Essential days:** FLEXIBLE (but recommended)—integrates all unit concepts
- **Key learning:** Complete program with loops for repetition, conditionals for decisions, input for data, output for results
- **What to teach:** Combining all concepts; building programs with multiple loops and conditionals
- **If ahead of pace:** Complex nested structures; multiple patterns in one program
- **If behind pace:** Provide structure; simpler requirements

---

## Differentiation Strategies

### For Struggling Students

**Scaffolding tips for this unit:**
- Use visual loop traces on paper/whiteboard
- Provide loop templates with blanks for key parts
- Start with countdown (simplest while pattern)
- Color-code loop variable updates
- Use small loop examples (3-5 iterations max)
- Trace execution by hand before coding

**Which practice problems to assign first (easiest wins):**
- Practice Bank items 1-3 first (simple while, for with range)
- Countdown loops before accumulator patterns
- range(n) before range(start, stop)
- Avoid nested loops initially
- String iteration only with for loops over characters

**Suggested pacing adjustments:**
- Spread Unit 4 to 10-11 days instead of 9
- Dedicate full day to loop mechanics and structure
- Separate while loops (2 days) from for loops (2 days)
- Skip break/continue initially; focus on while condition
- Skip nested loops; combine with Unit 5
- Avoid complex range() forms

**What prerequisite gaps to look for:**
- Weak understanding of Boolean conditions (Unit 3)
- Cannot identify loop variable and its updates
- Confusion about range() behavior
- Off-by-one thinking errors
- Indentation not mastered from Units 1-3

---

### For On-Track Students

**Standard path through the unit:**
- Follow 9-day schedule as written
- Assign Beginner + Intermediate problems daily
- Practice both while and for loops
- Complete project on Day 9 with standard requirements

**Which practice problems to assign:**
- Days 1-3: Beginner + Intermediate while loop problems
- Days 4-6: Intermediate + one Challenge per day
- Days 7-8: Mixed Intermediate and Challenge
- Day 9: Full project

---

### For Advanced Students

**Extension activities specific to this unit's topics:**
- List comprehensions (preview of Unit 5)
- Complex nested loops (multiple independence variables)
- Optimizing loops for efficiency
- Pattern generation (art, sequences, fractals)
- Algorithms like bubble sort or linear search

**Challenge problems to assign:**
- Unit 4 Practice Bank items 8-15 (all Challenge tier)
- Day 2: FizzBuzz and pattern printing challenges
- Day 4: Complex range() forms and generation patterns
- Day 5: String manipulation with nested loops
- Day 6: Game with sophisticated loop logic
- Extra: ASCII art generator, number pattern builder

**Ways to deepen understanding beyond the curriculum:**
- Ask: "How would you do this without loops?" (emphasize loops' power)
- Challenge: "Write this with a while loop, then with for loop" (compare approaches)
- Explore: Big O notation introduction (loop efficiency)
- Build: Program analyzing text (word frequency, patterns)
- Investigate: How loops enable processing large datasets

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Day 1:** Before break/continue (while loops fully understood)
- **End of Day 3:** Before for loops (loop concept established)
- **End of Day 4:** Before nested loops (basic for loops solid)

### Topics students most commonly struggle with:
- **Infinite loops:** Missing or incorrect loop variable update; misunderstood condition
- **Off-by-one errors:** range(10) giving 0-9 not 1-10; one iteration too few/many
- **Loop variable scope:** Thinking variable only exists in loop body
- **Initializing accumulators:** Starting total at wrong value; starting at wrong data point
- **String indexing in loops:** Confusing character with index; 0-based indexing still
- **Nested loops:** Controlling multiple variables; tracking which variable does what

### Topics students typically move through quickly:
- **Countdown pattern:** Simple and intuitive
- **range(n) basic form:** Easy to understand once explained
- **Printing in loops:** Immediate visual feedback reinforces concept
- **for loop over list:** More intuitive than while for beginners
- **break statement:** Logical when explained with clear examples

---

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**After Day 1:**
- Can students write a while loop that counts to 10?
- Do they understand loop variable updates?
- Checkpoint: "Write while loop that prints 5, 4, 3, 2, 1, Blast off!"

**After Day 2:**
- Can they use break to exit a loop?
- Checkpoint: "Loop asking for positive number, break when valid"

**After Day 3:**
- Can they accumulate (sum) values in a loop?
- Checkpoint: "Ask for 5 numbers, print their sum"

**After Day 4:**
- Can they write for loops with range()?
- Checkpoint: "Print multiplication table for 7 (7×1 through 7×10)"

**After Day 5:**
- Can they iterate over strings?
- Checkpoint: "Count vowels in a word"

**After Day 7:**
- Can they validate input with loops?
- Checkpoint: "Ask for number 1-100, re-ask until valid"

---

## STEM-Specific Pacing Notes

Unit 4 is the **first unit using loops extensively**. Loops are essential for all scientific/data processing programs. This unit is compressed from 10-11 days in full-year courses to 9 days for STEM semester.

**Key implications:**
- while and for loop proficiency are non-negotiable for STEM success
- Many STEM applications require nested loops and accumulator patterns
- Students must be comfortable with loops before Unit 5 (functions)
- Loop-based algorithms (searching, summing, counting) appear in later units

**Recommended daily structure (if 50-min class periods):**
- 5 min: Hook with a repetitive problem (why loops matter)
- 10 min: New concept with visual traces
- 20 min: Guided practice (live coding loops, students predict output)
- 10 min: Assign practice problems; code one together
- 5 min: Checkpoint: predict loop output or identify bug

**Critical mastery targets:**
By end of Unit 4, students MUST be able to:
1. Write while loops with proper initialization, condition, and update
2. Use for loops with range() in multiple forms
3. Apply accumulator pattern (sum, count, product)
4. Iterate over strings character by character
5. Combine loops with conditionals (if inside while/for)
6. Trace loop execution step by step
7. Identify and fix common loop errors

---

## Assessment & Mastery Validation

Quick verification questions:

1. **Day 1:** What happens if loop variable never updates? Can students trace while execution?
2. **Day 2:** What's the difference between break and continue?
3. **Day 3:** Can students sum numbers in a loop and compute average?
4. **Day 4:** Do students understand range(10) vs. range(1,11) vs. range(10,0,-1)?
5. **Day 5:** Can they count occurrences of a character in a string?
6. **Day 7:** Can they validate input and re-ask on error?
7. **Project:** Complete working program with loops performing meaningful computation

