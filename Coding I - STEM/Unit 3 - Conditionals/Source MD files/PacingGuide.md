# Unit 3 - Conditionals: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days (compressed for STEM semester)
- **Core topics covered:** Boolean expressions, comparison operators, if/else/elif statements, logical operators (and/or/not), nested conditionals, input validation, logic error debugging
- **Prerequisites students need:** Solid Unit 1-2 mastery (variables, data types, type conversion); understanding of True/False; ability to think through decision logic

---

## Week-by-Week Pacing

### Week 1 (Days 1–3): Boolean Logic & Basic Conditionals

#### Day 1: Boolean Expressions
- **Essential days:** YES—foundation for all conditionals
- **Key learning:** Comparison operators (==, !=, <, >, <=, >=), Boolean results, string comparison, type() returns bool
- **What to teach:** Each operator's meaning; why 5 == "5" is False; alphabetical ordering for strings
- **If ahead of pace:** Introduce chained comparisons; explore truthiness values; compare different types
- **If behind pace:** Focus on ==, !=, <, > only; use number examples; skip string comparisons

#### Day 2: if Statements
- **Essential days:** YES—core conditional structure
- **Key learning:** if syntax, indentation significance, when code runs/skips, code blocks
- **What to teach:** Precise indentation (4 spaces); how if controls execution flow; multiple statements in block
- **If ahead of pace:** Build more complex if blocks; introduce multiple if statements sequentially
- **If behind pace:** Use very simple conditions; provide templates with blanks for indentation guide

#### Day 3: if/else Statements
- **Essential days:** YES—choosing between two paths
- **Key learning:** else block concept, mutually exclusive paths, only one block executes
- **What to teach:** Why else is useful; that if/else covers all cases; relationship between conditions
- **If ahead of pace:** Chain simple if/else statements; introduce nested structures
- **If behind pace:** Use binary true/false scenarios; skip until Day 2 fully understood

---

### Week 2 (Days 4–6): Multiple Conditions & Operators

#### Day 4: elif Statements
- **Essential days:** YES—handling multiple distinct cases
- **Key learning:** elif as "else if", order matters, stops at first True, all elif checked top-to-bottom
- **What to teach:** Grading/categorization patterns; why order matters; all conditions are mutually exclusive
- **If ahead of pace:** Practice complex multi-level elif chains; discuss efficiency; introduce ternary operator (preview)
- **If behind pace:** Use 2-3 elif maximum; provide clear ranges; emphasize order with examples

#### Day 5: Logical Operators (and/or/not)
- **Essential days:** YES—combining conditions
- **Key learning:** and (both True), or (at least one True), not (reverses), short-circuit evaluation
- **What to teach:** Truth tables; real-world examples (AND: meeting requirements; OR: alternative paths); De Morgan's laws (intro)
- **If ahead of pace:** Explore precedence and short-circuit evaluation; use complex logical expressions; introduce bitwise operators (preview)
- **If behind pace:** Focus on and/or; skip not operator; use simple two-condition examples

#### Day 6: Nested Conditionals
- **Essential days:** FLEXIBLE—useful but and/or often cleaner
- **Key learning:** if inside if, indentation levels, dependent decisions, when to use vs. logical operators
- **What to teach:** Deeper indentation levels; cases where nesting is necessary; when to use logical operators instead
- **If ahead of pace:** Compare nested vs. flat with logical operators; deeply nested structures (3+ levels)
- **If behind pace:** Keep nesting to 1 level deep; emphasize that and/or usually cleaner

---

### Week 3 (Days 7–9): Validation & Debugging

#### Day 7: Input Validation & Chained Comparisons
- **Essential days:** YES—professional coding skill
- **Key learning:** Validating user input, range checking, chained comparisons (1 <= x <= 10), error prevention
- **What to teach:** Common validation patterns; why validation matters; chained comparison syntax and semantics
- **If ahead of pace:** Complex validation (multiple fields, conditional validation); introduce try/except preview
- **If behind pace:** Simple range validation only; skip chained comparisons initially

#### Day 8: Review & Debugging Logic Errors
- **Essential days:** YES—catching and fixing common mistakes
- **Key learning:** Common logic errors (= vs ==, off-by-one, wrong operator), debugging strategies, tracing execution
- **What to teach:** Error types; how to identify and fix each type; print-based debugging; hand-tracing
- **If ahead of pace:** Complex multi-level bugs; code walkthroughs of sophisticated logic
- **If behind pace:** Focus on most common errors; provide bugs pre-marked with hints

#### Day 9: Unit 3 Project
- **Essential days:** FLEXIBLE (but strongly recommended)—brings together all unit concepts
- **Key learning:** Complete program with user interaction, decisions, and validation
- **What to teach:** Project requirements; scaffolding and support for implementation
- **If ahead of pace:** Complex scenario with nested logic; multiple validation layers
- **If behind pace:** Provide structure and starter code; simpler requirements

---

## Differentiation Strategies

### For Struggling Students

**Scaffolding tips for this unit:**
- Use visual flowcharts for every conditional structure
- Provide comparison operator quick reference card
- Create decision trees before writing code
- Use concrete scenarios (age, score ranges) before abstract logic
- Color-code indentation levels or use visual brackets

**Which practice problems to assign first (easiest wins):**
- Practice Bank items 1-3 first (basic Boolean, simple if, if/else)
- Focus on numeric comparisons before string comparisons
- == and != before <, >, <=, >=
- Simple two-option if/else before multi-way if/elif/else
- And operator before or operator

**Suggested pacing adjustments:**
- Spread Unit 3 to 10-11 days instead of 9
- Dedicate full day to indentation and if syntax alone
- Split Day 4 (elif) into two days—one for 2-way, one for 3+ way
- Combine Days 5-6 (logical operators and nesting) selectively
- Skip nesting; use logical operators instead
- Provide template programs with structure pre-made

**What prerequisite gaps to look for:**
- Confusion between = and ==
- Weak understanding of True/False (from Unit 1)
- Indentation not solid (from Unit 1 review)
- Type confusion (comparing int with string)
- Unable to think sequentially through decision logic

---

### For On-Track Students

**Standard path through the unit:**
- Follow 9-day schedule as written
- Assign Beginner + Intermediate problems daily
- Use logical operators alongside conditionals
- Complete project on Day 9 with all standard requirements

**Which practice problems to assign:**
- Days 1-3: Beginner + Intermediate problems
- Days 4-6: Intermediate + one Challenge per day
- Days 7-8: Mixed Intermediate and Challenge
- Day 9: Full project

---

### For Advanced Students

**Extension activities specific to this unit's topics:**
- Implement complex decision logic in games or simulations
- Explore De Morgan's Laws and logical equivalences
- Refactor nested conditions to use logical operators (and vice versa)
- Build input validation libraries for reuse
- Introduce state machines (if time permits)

**Challenge problems to assign:**
- Unit 3 Practice Bank items 9-15 (all Challenge tier)
- Day 5: Implement complex logic with 3+ operators
- Day 6: Refactor nested code to use logical operators
- Day 7: Build robust validation with multiple input fields
- Day 8: Debug complex multi-level conditional code
- Extra: Simple game with sophisticated decision logic

**Ways to deepen understanding beyond the curriculum:**
- Ask: "What's the opposite condition?" (De Morgan's Laws intro)
- Challenge: "Write this two different ways (nested vs. logical operators)"
- Explore: Short-circuit evaluation impacts in complex conditions
- Build: Input validation system for a realistic scenario
- Design: State diagram for a complex decision process

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Day 2:** Before else (foundation: if works correctly)
- **End of Day 4:** Before logical operators (foundation: if/elif/else solid)
- **End of Day 6:** Before validation (foundation: all conditional structures understood)

### Topics students most commonly struggle with:
- **= vs ==:** Assignment vs. comparison; syntax errors from using =
- **Indentation:** Off-by-one indent levels; code accidentally outside if block
- **Off-by-one errors:** >= vs >, <= vs <; should 90 count as passing (>=)?
- **Operator precedence:** and/or evaluated in unexpected order
- **else execution:** Thinking else runs when condition True (opposite of reality)
- **Logic reversal:** Conditional tests for success but code handles failure case

### Topics students typically move through quickly:
- **Boolean concept:** Most understand True/False quickly
- **== operator:** Familiar from math
- **Simple if:** Basic concept gets picked up immediately
- **and operator:** Intuitive from English
- **Comparison of numbers:** Students with math comfort move fast

---

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**After Day 1:**
- Can students evaluate comparison expressions?
- Do they understand each operator?
- Checkpoint: "Evaluate: 5 > 3, 'a' < 'b', 10 == 10, 'hello' != 'hello'"

**After Day 2:**
- Can they write basic if statements?
- Is indentation correct?
- Checkpoint: "Write if statement that checks if age >= 18 and prints 'Adult'"

**After Day 3:**
- Can they choose between two paths?
- Does else execute correctly?
- Checkpoint: "Write if/else that checks even/odd and prints appropriate message"

**After Day 4:**
- Can they handle 3+ cases with elif?
- Does order matter?
- Checkpoint: "Grade checker: A (90+), B (80-89), C (70-79), F (<70)"

**After Day 5:**
- Can they combine conditions with and/or?
- Do they understand operator meanings?
- Checkpoint: "Write condition: age between 13-19 AND password length >= 8"

**After Day 7:**
- Can they validate input?
- Do they understand range checking?
- Checkpoint: "Ask for number 1-10, keep asking until valid"

---

## STEM-Specific Pacing Notes

Unit 3 is **critical gatekeeper unit** for STEM courses. Everything after depends on understanding conditionals. Unit 3 is compressed from 10 days in full-year courses to 9 days for STEM semester.

**Key implications:**
- Must ensure solid mastery of if/else/elif before moving to loops
- Students falling behind here will struggle in all units after
- Logical operators (and/or) can be taught implicitly if time is tight
- Nested conditionals can be skipped if logical operators are solid
- **Cannot afford to move to Unit 4 without mastery**

**Recommended daily structure (if 50-min class periods):**
- 5 min: Review previous concept (quick examples)
- 10 min: New concept with multiple real-world examples
- 20 min: Guided practice (live code with class deciding logic)
- 10 min: Assign practice problems; code along
- 5 min: Checkpoint question on concept understanding

**Critical mastery targets:**
By end of Unit 3, students MUST be able to:
1. Write if/else/elif statements with correct syntax and indentation
2. Evaluate Boolean expressions and comparison operators
3. Use and/or to combine conditions correctly
4. Design conditional logic for a given scenario
5. Identify and fix logic errors in conditional code
6. Validate user input with appropriate conditions

---

## Assessment & Mastery Validation

Use these questions to verify mastery:

1. **Day 1:** Can students predict output of comparisons? Understand ==/!=, <, >, <=, >=?
2. **Day 2:** Can students write if with correct indentation?
3. **Day 3:** Do they understand else only runs if condition is False?
4. **Day 4:** Can they decide between if/elif/else vs. nested if?
5. **Day 5:** Do they understand and/or semantics and operator precedence?
6. **Day 7:** Can they validate input ranges correctly?
7. **Project:** Complete working program with multiple decision paths

