# Unit 3 - Conditionals: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 25 days / 5 weeks (Days 46–70, 55-minute periods)
- **Core topics covered:** Boolean expressions (review), comparison operators, logical operators (and, or, not), if/else/elif statements, nested conditionals, input validation with conditionals, debugging logic errors, real-world applications (games, menus, eligibility systems)
- **Prerequisites students need:** Mastery of Unit 2 (Boolean expressions, comparison operators, type conversion); ability to write Python programs with input and output

---

## Week-by-Week Pacing

### Week 10 (Days 46–50): Boolean Logic & Comparisons
**Topics:** Boolean expressions, comparison operators (==, !=, <, >, <=, >=), truth tables, logical operators (and, or, not), compound conditions, Boolean variables as flags

#### Essential days (cannot skip):
- **Day 46:** Boolean expressions and comparison operators — everything in conditionals depends on evaluating these correctly
- **Day 47:** Logical operators (and, or, not) with truth tables — essential for compound conditions
- **Day 50:** Practice lab reinforcing Days 46–47 — students must be able to evaluate complex Boolean expressions

#### Flexible days (can compress or cut if pressed for time):
- **Day 48 (Chained Comparisons):** Can be abbreviated to 10-minute demonstration with examples; students often learn through practice
- **Day 49 (Boolean Variables as Flags):** Can be shortened or folded into Day 50 practice

#### If ahead of pace:
- Introduce De Morgan's Laws: not (A and B) == (not A) or (not B)
- Have them evaluate complex nested Boolean expressions
- Challenge: write code that determines if three numbers form a valid triangle
- Explore short-circuit evaluation: what happens with `False and x` (x is not evaluated)

#### If behind pace:
- Spend 2 days on comparison operators (Days 46–47) before moving to logical operators
- Simplify logical operators; focus only on and/or first, defer not
- Extend Day 50 with additional practice problems
- **Minimum viable coverage:** Days 46–47 (comparisons and basic logical operators)

---

### Week 11 (Days 51–55): if/else Statements
**Topics:** if statement syntax and indentation, if/else two-path decisions, if/elif/else multi-way branching, nested if statements, common if/else patterns (even/odd, grade classification, range checking)

#### Essential days (cannot skip):
- **Day 51:** if statement syntax and structure — indentation and colon are critical
- **Day 52:** if/else for two-path decisions — the fundamental control structure
- **Day 53:** if/elif/else for multi-way branching — grade calculators, menus, classifications
- **Day 55:** Practice lab combining all three days — essential synthesis

#### Flexible days (can compress or cut if pressed for time):
- **Day 54 (Grade Calculators & Menus):** Can be folded into Day 53 or Day 55 if time is tight

#### If ahead of pace:
- Introduce nested if statements early (combined with Week 12 content)
- Have them write menu systems with multiple elif branches
- Challenge: write a program that determines leap years or zodiac signs based on date input
- Explore edge cases: what happens at boundary values (score == 90 for an A)?

#### If behind pace:
- Spend 2 days on if/else syntax (Days 51–52)
- Defer if/elif/else to extra time; focus on if/else first
- Combine Days 53 and 55 into one extended day
- **Minimum viable coverage:** Days 51–52 (if and if/else)

---

### Week 12 (Days 56–60): Nested Conditionals & Complex Logic
**Topics:** Nested if statements, complex conditions with and/or in if statements, short-circuit evaluation, truthy/falsy values in conditionals, input validation with conditionals

#### Essential days (cannot skip):
- **Day 56:** Nested if statements — students need comfort with indentation and logic layering
- **Day 57:** Complex conditions combining and/or with comparisons — powerful decision-making
- **Day 59:** Input validation with conditionals — essential for robust programs
- **Day 60:** Practice lab with login systems and eligibility checkers — real-world application

#### Flexible days (can compress or cut if pressed for time):
- **Day 58 (Short-circuit Evaluation & Truthy/Falsy):** Can be a 15-minute demo rather than a full lesson; emphasize practical usage

#### If ahead of pace:
- Introduce Boolean variables that store condition results: `is_adult = age >= 18; if is_adult:`
- Have them write complex eligibility checkers (multiple AND/OR conditions)
- Challenge: write a login system that validates username, password, and account status
- Explore De Morgan's Laws: simplifying complex Boolean expressions

#### If behind pace:
- Spend extra time on nested indentation; visual aids help (indentation guide on screen)
- Focus on simple nested if, not complex nested-nested combinations
- Simplify input validation to single-condition checks first
- **Minimum viable coverage:** Days 56–57 (nested if, complex conditions)

---

### Week 13 (Days 61–65): Real-World Applications
**Topics:** Text-based menu systems, Rock-Paper-Scissors game, number guessing game, mini-projects combining all conditional concepts

#### Essential days (cannot skip):
- **Day 61-62:** Building interactive applications (menu system, game) — students apply all unit concepts
- **Days 63-64:** Mini-project work days — student choice project with conditionals
- **Day 65:** Mini-project presentations and peer review — communication of code

#### Flexible days (can compress or cut if pressed for time):
- None. These are hands-on application days; compress by simplifying project scope instead

#### If ahead of pace:
- Have students add complexity to games (score tracking, multiple rounds, difficulty levels)
- Extend menu systems to have sub-menus
- Challenge: write a program that plays tic-tac-toe or higher/lower guessing game with strategy

#### If behind pace:
- Provide starter code for games (Rock-Paper-Scissors decision structure)
- Reduce project scope (simple number guessing vs complex game)
- Allow pair programming or peer support
- **Minimum viable coverage:** Days 62 (game example), 63–64 (mini-project)

---

### Week 14 (Days 66–70): Review & Assessment
**Topics:** Unit 3 vocabulary, Boolean logic review, code tracing with conditionals, common mistakes workshop, unit assessment, reflection

#### Essential days (cannot skip):
- **Day 66:** Vocabulary and Boolean logic review — targeted re-teaching of misconceptions
- **Day 69:** Unit 3 Assessment — formal evaluation
- **Day 70:** Assessment review and reflection

#### Flexible days (can compress or cut if pressed for time):
- **Day 67-68:** Review practice — can be condensed or extended based on performance

#### If ahead of pace:
- Have students create a "debugging conditionals" guide for their peers
- Challenge them to trace and fix conditionally broken code
- Have them teach a complex concept to a struggling peer

#### If behind pace:
- Spend extra time on Days 66–68 for review and re-teaching
- Offer a retake option for those scoring below mastery
- **Minimum viable coverage:** Days 66 (review), 69 (assessment)

---

## Differentiation Strategies

### For Struggling Students
**Specific scaffolding tips:**
- **Comparison operators:** Explicitly connect to English: a < b means "a is less than b". Use number lines and visual aids.
- **Logical operators:** Teach with Venn diagrams and truth tables. `and` means both must be true; `or` means at least one is true.
- **if/else indentation:** Provide an indentation guide (4 spaces after if/elif/else). Use a ruler or visual marker on screen.
- **Nested if:** Start with shallow nesting (if inside if, not deeper). Use clear comments: `# Outer if` and `# Inner if`.
- **Debugging conditional logic:** Use print() statements to trace which branch is being executed. Print condition values before the if.

**Which practice problems to assign first (easiest wins):**
- From UnitPractice.md, start with Boolean & Comparison Tier problems 1-2 (simple comparisons, alphabetical ordering)
- Then Logical Operators Tier problems 6-7 (and/or with simple conditions)
- Then if/elif/else Tier problems 11-12 (even/odd, voting eligibility)
- Build to Nested & Complex Tier (problems 16+) only after foundational confidence

**Suggested pacing adjustments:**
- Spend 2 days on comparison operators instead of 1
- Spend 2 days on logical operators (and/or separate from not)
- Provide decision trees or flowcharts alongside code
- Use physical examples: "If it's raining AND you want to go out, take an umbrella"

**What prerequisite gaps to look for:**
- **Boolean expressions:** Can they evaluate `5 > 3 and 2 < 4`? If not, go back to Unit 2
- **Code indentation:** Did they struggle with this in earlier units? Revisit now with explicit guidance
- **Logical thinking:** Can they explain why `if score >= 60 and score <= 100:` is different from `if score >= 60 or score <= 100:`?

### For On-Track Students
**Standard path through the unit:**
- Follow the week-by-week breakdown as written
- Complete problems from Boolean & Comparison, Logical Operators, and if/elif/else tiers
- Focus on building one complete application (game or menu system)

**Which practice problems to assign:**
- Boolean & Comparison Tier (problems 1-5) for foundational work
- Logical Operators Tier (problems 6-10) for synthesis
- if/elif/else Tier (problems 11-15) for application
- Nested & Complex Tier (1-2 problems) for stretching
- All 5 weekly labs (Days 50, 55, 60, 65)

**Expectations:**
- Code should be readable with meaningful variable names
- Programs should handle edge cases (boundary values for ranges)
- Indentation should be consistent and correct
- Comments should explain complex conditions

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Boolean algebra:** Teach simplification using Boolean laws (De Morgan's, absorption, etc.)
- **Complex logic:** Have them write eligibility systems with 4+ conditions (age, GPA, attendance, behavioral record)
- **Game strategy:** Have them implement AI for games (Rock-Paper-Scissors bot with strategy, number guessing with binary search)
- **State machines:** Introduce the concept of programs with states (menu state, game state, results state)

**Challenge problems to assign:**
- Nested & Complex Tier (problems 16-20) — login systems, game logic, eligibility checkers
- Real-World Applications Tier (problems 21-25) — leap year calculator, BMI classifier, complex validation
- Have them write a program with 3+ nested if statements and complex and/or combinations
- Challenge: write a simple text adventure with conditional branching (choices lead to different outcomes)

**Ways to deepen understanding beyond the curriculum:**
- Explore Boolean circuit logic (AND/OR gates in electronics)
- Write a program that simulates a decision tree (medical diagnosis, troubleshooting guide)
- Create a "ternary operator" explanation (conditional expression in one line: `x if condition else y`)
- Build a more complex menu system with input validation and error handling

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Week 10:** Before moving to if/else, ensure students can evaluate complex Boolean expressions with and/or
- **End of Week 11:** Before moving to nested if, ensure if/elif/else indentation and logic are solid
- **After Day 60:** Before real-world applications, checkpoint that students can write error-free if/elif/else blocks

### Topics students most commonly struggle with (and expected time):
1. **Logical operators (and vs or):** 1-2 extra days. Many students intuitively use "and" for conditions that need "or". Use English phrase test: "age < 5 AND age > 65" means the same person can't be both → should be OR
2. **Indentation:** 1 extra day if students struggle with it in earlier units. Provide visual guides; be explicit: "exactly 4 spaces, not tabs"
3. **Nested if indentation:** 1 extra day. Double indentation (8 spaces) looks odd; practice with simple nested examples
4. **Boundary conditions:** 1 day. Does >= include 60 or not? Many off-by-one errors here
5. **Complex elif chains:** 1 day. Grade classification (if/elif/elif/elif/else) requires careful structuring

### Topics students typically move through quickly:
- **if statement syntax:** Once they see the colon and indentation, they grasp it in 5 minutes
- **Comparison operators:** If they mastered Unit 2, <, >, ==, != feel obvious
- **Simple if/else:** Binary decisions (even/odd, pass/fail) are intuitive
- **Boolean variables:** Once shown an example, most students grasp the concept

---

## Suggested Checkpoints

Use these quick formative checks mid-unit:

### After Day 50 (end of Week 10):
- **Quick Check:** Evaluate `5 > 3 and 2 < 1` (Answer: False) and `5 > 3 or 2 < 1` (Answer: True)
- **Code Check:** Write a condition that checks if a number is between 1 and 100 (inclusive)

### After Day 55 (end of Week 11):
- **Quick Check:** "Write an if/elif/else to classify scores: A (90+), B (80-89), C (70-79), else F"
- **Code Check:** Write a program that asks for an age and prints "Child", "Teen", or "Adult" based on thresholds

### After Day 60 (end of Week 12):
- **Quick Check:** "Write nested if to check if a number is positive AND even"
- **Code Check:** Write a login system that validates both username and password with error messages

### Before Day 65 (mid-Week 13):
- **Code Check:** Students' mini-projects in progress. Scan: Does the game logic work? Are all paths tested?

---

## Common Misconceptions to Watch For

1. **"and means 'or' in English"** — "I need apples and oranges" (both). But in conditionals, `age < 5 and age > 65` can't be true simultaneously; use `or`.
2. **"= is the same as =="** — `if x = 5:` is a syntax error. Use == for comparison, = for assignment.
3. **"The colon is optional"** — `if x > 5` without a colon is a syntax error. Python requires it.
4. **"indentation doesn't matter"** — Indentation determines what's inside the if block. Wrong indentation = wrong logic.
5. **"else if is spelled 'else if'"** — Python uses `elif`, not `else if`.
6. **"Multiple elif means you need multiple ifs"** — `if/elif/elif/elif/else` is cleaner than nested if statements for multi-way branching
7. **"< > checks if a number is in a range"** — `score < 90 and score > 80` is correct; `score > 80 and score < 90` is equivalent
8. **"not reverses everything"** — `not (x > 5)` is equivalent to `x <= 5`. Teach using English: "not greater than" = "less than or equal to"

---

## Notes on Unit 3 Assessment

- **Assessment (Day 69):** Should include Boolean expression evaluation (multiple choice or short answer), code tracing with if/elif/else, and a coding task (write a complete program with multi-branch logic, e.g., grade classifier or game outcome checker)
- **Common assessment mistakes:** Using = instead of ==, forgetting colons, incorrect indentation, using "and" when "or" is needed
- **Retakes:** Offer retakes focused on weakest areas (Boolean operators, if/elif/else logic, nested conditionals)

