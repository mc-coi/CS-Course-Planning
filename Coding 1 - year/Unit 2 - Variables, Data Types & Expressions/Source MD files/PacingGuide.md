# Unit 2 - Variables, Data Types & Expressions: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 25 days / 5 weeks (Days 21–45, 55-minute periods)
- **Core topics covered:** Compound assignment operators, numeric operations (int/float distinction, //, %), strings (indexing, slicing, methods like .upper(), .lower(), .strip(), .replace(), .find(), .count()), Boolean expressions and comparison operators, type conversion, math module, f-string formatting with precision, variable naming conventions, building complete interactive programs with input validation
- **Prerequisites students need:** Mastery of Unit 1 (variables, basic data types, input/output, arithmetic operators); understanding of PEMDAS; ability to write simple Python programs

---

## Week-by-Week Pacing

### Week 5 (Days 21–25): Deep Dive into Data Types
**Topics:** Review of int/float/str/bool; compound assignment operators (+=, -=, *=, /=, //=, %=); string operations (indexing, slicing, concatenation, length); introduction to string methods

#### Essential days (cannot skip):
- **Day 21:** Compound assignment operators and numeric review — students will use += constantly in future units
- **Day 23:** String indexing and slicing — foundational for string manipulation
- **Day 24:** String methods (.upper(), .lower(), .strip(), .replace(), .find(), .count()) — most-used string operations
- **Day 25:** Practice lab combining all four days — essential skill-building

#### Flexible days (can compress or cut if pressed for time):
- **Day 22 (Numeric Operations Review):** If students mastered Unit 1 thoroughly, this can be a 15-minute review with quick examples

#### If ahead of pace:
- Introduce string method chaining: "HELLO".lower().replace("o", "0")
- Have students explore string slicing with negative indices and step: "Python"[-2:], "Python"[::-1]
- Introduce the `in` operator for substring checking (preview of Unit 3 concepts)
- Challenge: write a program that analyzes a word (counts vowels, checks for palindrome, etc.)

#### If behind pace:
- Spend 2 days on string indexing/slicing (Days 23–24 focus on just these concepts)
- Reduce the number of string methods taught; focus on the top 3: .upper(), .lower(), .strip()
- Combine Days 24 and 25 into one extended lab day
- **Minimum viable coverage:** Days 21–24 (compound assignment, string basics)

---

### Week 6 (Days 26–30): Type Conversion & Boolean Logic
**Topics:** Review of type conversion (int(), float(), str(), bool()); Boolean expressions; comparison operators (==, !=, <, >, <=, >=); truthy/falsy values; input validation

#### Essential days (cannot skip):
- **Day 26:** Type conversion review with practical examples — students must be confident converting between types
- **Day 27:** Comparison operators and Boolean expressions — foundation for Unit 3 conditionals
- **Day 28:** Truthy/falsy values and boolean evaluation — deeper understanding of how Python evaluates conditions
- **Day 30:** Practice lab with input validation — essential skill

#### Flexible days (can compress or cut if pressed for time):
- **Day 29 (Introduction to try/except basics):** If time is short, this can be abbreviated or moved to Unit 6. Focus on type conversion without exception handling first.

#### If ahead of pace:
- Introduce the `in` operator for checking substring membership
- Have them write validation loops that check for multiple conditions: `if 0 <= age <= 120 and isinstance(age, int):`
- Challenge: write a program that validates multiple inputs (name, age, GPA) and reports all validation errors
- Explore edge cases: What happens with very large numbers? Empty strings?

#### If behind pace:
- Spend 2 days on type conversion (Days 26–27)
- Skip Day 29 (try/except) entirely; focus on type conversion and validation through practice
- Combine Days 28 and 30 into one day
- **Minimum viable coverage:** Days 26–28 (type conversion, comparisons, Boolean logic)

---

### Week 7 (Days 31–35): Advanced Expressions
**Topics:** Complex expressions combining arithmetic, strings, and type operations; operator precedence with mixed operators; math module (import math, math.sqrt(), math.pi, math.ceil(), math.floor()); f-string formatting with alignment and decimal precision; multiple assignment (a, b = b, a)

#### Essential days (cannot skip):
- **Day 31:** Complex expressions and mixed operators — students need confidence combining concepts
- **Day 32:** Math module introduction (math.sqrt(), math.pi, math.floor(), math.ceil()) — enables real-world calculations
- **Day 33:** F-string advanced formatting (decimal precision, alignment, padding) — professional output formatting
- **Day 35:** Practice lab with complex programs — synthesis of all three days

#### Flexible days (can compress or cut if pressed for time):
- **Day 34 (Multiple Assignment):** If time is tight, this can be a 10-minute demo. It's clever but not essential for most programs. Can be revisited in Unit 4.

#### If ahead of pace:
- Introduce more math module functions: math.pow(), math.abs(), math.sin(), math.cos()
- Have them create financial calculators with precise decimal formatting
- Challenge: write a program that calculates complex formulas (physics, compound interest, etc.)
- Explore f-string edge cases (negative numbers, scientific notation)

#### If behind pace:
- Simplify math module coverage to just math.sqrt()
- Reduce f-string precision requirements; focus on basic decimal formatting (:.2f)
- Combine Days 31–32 into one day of "working with numbers"
- **Minimum viable coverage:** Days 31–33 (expressions, math module, f-strings)

---

### Week 8 (Days 36–40): Real-World Applications
**Topics:** Building complete interactive programs; input validation patterns; money handling with precise formatting; multi-step programs (payroll calculators, currency converters, tip calculators); working with user input robustly

#### Essential days (cannot skip):
- **Day 36:** Input validation pattern with feedback — essential for robust programs
- **Day 37-38:** Work days building complete programs (projects chosen by students or assigned)
- **Day 39:** Code review and debugging session — peer feedback and improvement
- **Day 40:** Code polish and wrap-up

#### Flexible days (can compress or cut if pressed for time):
- None. These are work days; compress by reducing scope of projects rather than skipping days

#### If ahead of pace:
- Have students build more complex programs: tip calculator with party splitting, currency converter with multiple currencies
- Introduce file I/O preview: save calculations to a file
- Challenge: build a program that stores multiple calculations in a list and displays a summary

#### If behind pace:
- Reduce project complexity; focus on simple payroll (gross, tax, net) rather than multi-feature programs
- Allow students to work in pairs for support
- Extend work days if needed
- **Minimum viable coverage:** Days 36, 38–40 (validation, work days, polish)

---

### Week 9 (Days 41–45): Review & Assessment
**Topics:** Unit 2 vocabulary review, misconception workshop, code tracing, common mistakes, formal assessment

#### Essential days (cannot skip):
- **Day 41:** Review of common mistakes and misconceptions — targeted re-teaching
- **Day 44:** Unit 2 Assessment — formal evaluation
- **Day 45:** Assessment review and reflection

#### Flexible days (can compress or cut if pressed for time):
- **Day 42:** Code tracing practice — can be incorporated into Day 41 review
- **Day 43:** Additional practice — can be shortened or extended based on class performance

#### If ahead of pace:
- Have students create a "cheat sheet" or blog post explaining string methods
- Challenge them to trace and debug more complex code
- Have them teach a peer about a concept they struggled with

#### If behind pace:
- Spend extra time on Days 41–43 for review and re-teaching
- Offer a retake option for those who score below mastery on Day 44
- **Minimum viable coverage:** Days 41 (review), 44 (assessment)

---

## Differentiation Strategies

### For Struggling Students
**Specific scaffolding tips:**
- **String indexing:** Teach with visual aids (number each character: "hello" → h(0) e(1) l(2) l(3) o(4)). Have them practice only positive indices first.
- **String slicing:** Start with [start:stop] only; introduce step parameter later. Use concrete examples like "Python"[0:3] = "Pyt"
- **Type conversion:** Always show the error when you forget conversion, then show the fix. Use error-driven learning.
- **Boolean expressions:** Provide truth tables. Have them evaluate expressions on paper before coding.
- **F-strings:** Start with basic {variable}, then introduce :.2f. Too many format options is overwhelming.

**Which practice problems to assign first (easiest wins):**
- From UnitPractice.md, Tier 1 (Beginner) problems 1-10 (variable basics, simple string operations, type conversion)
- Then Tier 2 (Intermediate) problems 11-15 (string methods, simple calculations)
- Build to Tier 2 problems 16-20 (more complex scenarios) only after confidence is built

**Suggested pacing adjustments:**
- Spend 2 days on string indexing/slicing instead of 1
- Spend 2 days on type conversion instead of 1
- Provide worked examples for every category of problems before independent practice
- Use print() debugging liberally; have them predict output before running code

**What prerequisite gaps to look for:**
- **String concept:** Can they distinguish between the string "5" and the integer 5? If not, unit will struggle.
- **Order of operations:** Do they understand PEMDAS? Test with 2 + 3 * 4. If confused, go back to Unit 1.
- **Variable reassignment:** Can they trace a variable changing value? Use visual diagrams (memory model).

### For On-Track Students
**Standard path through the unit:**
- Follow the week-by-week breakdown as written
- Complete Tier 1 and Tier 2 practice problems
- Focus on building real interactive programs (payroll, currency, grade calculators)

**Which practice problems to assign:**
- Tier 1 (Beginner) problems 1-10 for foundational skill-building
- Tier 2 (Intermediate) problems 11-20 for synthesis
- 1-2 Tier 3 (Challenge) problems for stretching
- All 5 weekly lab days (Days 25, 30, 35, 40)

**Expectations:**
- Code should be readable with meaningful variable names (not a, b, c)
- Programs should validate user input and handle errors gracefully
- F-string formatting should be professional (prices with $, 2 decimal places; coordinates with alignment)

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **String manipulation:** Teach regular expressions (regex) overview; show power of pattern matching
- **Math module:** Explore trigonometric functions (math.sin(), math.cos(), math.tan()); create geometry calculator
- **Data validation:** Have them implement complex validation (checking for duplicate entries, ensuring age is reasonable range)
- **Type system:** Explore edge cases (float precision, integer overflow in other languages, duck typing)

**Challenge problems to assign:**
- Tier 3 (Challenge) problems 21-25 (compound interest, string analysis, statistics calculations)
- Have them create their own problem and solve it (e.g., "Write a program that calculates your age in days")
- Ask them to refactor a messy program for readability
- Challenge: write a program that validates complex multi-part input and calculates results with precise formatting

**Ways to deepen understanding beyond the curriculum:**
- Explore string encoding and Unicode (why can Python handle "café" and emoji?)
- Investigate float precision issues: `0.1 + 0.2 == 0.3` → False. Why? (floating-point representation)
- Create a "string method cheat sheet" with examples
- Write a program that analyzes text (counts words, finds longest word, calculates average word length)

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Week 5:** Before introducing type conversion, ensure string indexing/slicing is solid
- **End of Week 6:** Before moving to math module, ensure type conversion and Boolean logic are strong
- **After Day 35:** Before Week 8 projects, checkpoint on f-string formatting and math module usage

### Topics students most commonly struggle with (and expected time):
1. **String slicing:** 1-2 extra days. Off-by-one errors are common; [start:stop] not including stop confuses many.
2. **Type conversion complexity:** 1 extra day. Why is str(42) necessary before concatenation? Needs repeated examples.
3. **F-string formatting:** 1 day. The syntax f"${price:.2f}" feels foreign at first.
4. **Math module import:** 30 minutes. Students forget to `import math` or write math.sqrt instead of math.sqrt().
5. **Boolean expressions:** 1 day. Understanding when to use and vs or; chained comparisons.

### Topics students typically move through quickly:
- **Compound assignment operators:** Once they see `x += 1`, they grasp it in 5 minutes
- **String methods:** Most methods (.upper(), .lower()) are intuitive once they understand the method call syntax
- **Comparison operators:** If they understand math, `<` and `>` are obvious
- **Multiple assignment:** Clever but optional; many students skip this and do it the long way

---

## Suggested Checkpoints

Use these quick formative checks mid-unit (not full assessments):

### After Day 25 (end of Week 5):
- **Quick Check:** "What is 'Python'[2]?" (Answer: 't')
- **Code Check:** Write a program that takes a word as input and prints it in uppercase

### After Day 30 (end of Week 6):
- **Quick Check:** "Is 0.5 < 0.05 true or false?" (Answer: False) and "What does bool(0) return?" (Answer: False)
- **Code Check:** Write a program that validates a user's age (must be 1-120) and re-asks if invalid

### After Day 35 (end of Week 7):
- **Quick Check:** "What is the area of a circle with radius 5?" (Expect: math.pi * 5**2 ≈ 78.54)
- **Code Check:** Write a program that calculates and formats the result as "$78.54"

### Before Day 40 (mid-Week 8):
- **Code Check:** Students' projects in progress. Scan: Does input validation work? Are calculations correct? Is formatting professional?

---

## Common Misconceptions to Watch For

1. **"String slicing includes the stop index"** — "Hello"[0:3] gives "Hel", not "Hell". The stop is exclusive.
2. **"Negative indices start at 1"** — "Hello"[-1] is 'o', not 'l'. -1 is the last character, -2 is second-to-last.
3. **"Methods modify the original string"** — "hello".upper() doesn't change the original; it returns a new string. Strings are immutable.
4. **"You need to import print()"** — print() is built-in; you don't import it. Only import math, not common functions.
5. **"F-strings are the same as concatenation"** — f"Score: {score}" is better than "Score: " + str(score). Show both; explain readability.
6. **"Type conversion is optional"** — str() is necessary before concatenating; int() is necessary before arithmetic on user input.
7. **"All floats have the same precision"** — Floating-point precision issues exist; 0.1 + 0.2 ≠ 0.3 in binary representation.

---

## Notes on Unit 2 Assessment

- **Assessment (Day 44):** Should include short-answer (What does string slicing do?), code tracing (What does this print?), and a coding task (write a complete program with input validation and formatting).
- **Common assessment mistakes to watch for:** Students forgetting str() when concatenating, using = instead of == in Boolean expressions (syntax error, caught early), using [start:stop] incorrectly
- **Retakes:** Offer retakes focused on weakest areas (e.g., string manipulation, type conversion, or formatting).

