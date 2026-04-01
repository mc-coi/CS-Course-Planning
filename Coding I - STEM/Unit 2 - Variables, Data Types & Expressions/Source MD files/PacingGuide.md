# Unit 2 - Variables, Data Types & Expressions: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days (compressed for STEM semester)
- **Core topics covered:** Variable assignment and compound operators, numeric types (int/float), string operations (concatenation, indexing, slicing, methods), Boolean expressions, type conversion, f-string formatting, math module
- **Prerequisites students need:** Comfort with Unit 1 concepts (variables, basic data types); ability to use print() and input(); understanding of basic arithmetic

---

## Week-by-Week Pacing

### Week 1 (Days 1–3): Variables & Numeric Types

#### Day 1: Variable Assignment & Compound Operators
- **Essential days:** YES—foundational for all subsequent units
- **Key learning:** Assignment vs. reassignment, compound assignment operators (+=, -=, *=, /=, //=), multiple assignment
- **What to teach:** Difference between = (assignment) and == (comparison); practical examples with counters and scores; swapping variables
- **If ahead of pace:** Introduce tuple unpacking early; explore all compound operators with different data types
- **If behind pace:** Focus on basic assignment and += only; skip other compound operators for now; use visual diagrams

#### Day 2: Numeric Types & Arithmetic Expressions
- **Essential days:** YES—needed for calculators and science programs
- **Key learning:** int vs. float, arithmetic operators (+, -, *, /, //, %, **), order of operations, round() function
- **What to teach:** When to use int vs. float; precision issues with floats; proper use of round() and formatting
- **If ahead of pace:** Explore float precision issues; use math module early; challenge with complex expressions
- **If behind pace:** Stick to +, -, *, / only; use integer examples; skip modulus and exponentiation

#### Day 3: String Basics & Operations
- **Essential days:** YES—strings are fundamental
- **Key learning:** String concatenation, repetition (*), indexing, slicing notation [start:stop:step], len() function
- **What to teach:** Index from 0; negative indices; slice ranges; string immutability concept
- **If ahead of pace:** Introduce slice notation with all three parameters; negative indices extensively; build string puzzles
- **If behind pace:** Focus on concatenation and basic indexing only; skip slicing; use simple 3-4 character strings

---

### Week 2 (Days 4–6): Strings & Boolean Logic

#### Day 4: String Methods
- **Essential days:** FLEXIBLE—can accelerate or compress
- **Key learning:** Common methods (.upper(), .lower(), .replace(), .split(), .find(), .count(), .strip()), method chaining
- **What to teach:** How to look up methods; most frequently used methods for text processing
- **If ahead of pace:** Explore all string methods; introduce .strip(), .startswith(), .endswith(); method chaining
- **If behind pace:** Teach only .upper() and .lower(); demonstrate basic examples; move to next topic

#### Day 5: Type Conversion & Boolean Logic
- **Essential days:** YES—critical for conditionals unit
- **Key learning:** Converting between types (int(), float(), str(), bool()), truthiness of values, comparison operators (==, !=, <, >, <=, >=)
- **What to teach:** Why conversion is needed; common errors in type conversion; Boolean results from comparisons
- **If ahead of pace:** Explore truthiness of different values (empty strings, 0, None); chain comparisons
- **If behind pace:** Focus on int() and str() conversion only; simple equality (==) and inequality (!=) comparisons

#### Day 6: Formatted Output with f-Strings
- **Essential days:** YES—professional output and user-friendly programs
- **Key learning:** f-string syntax, variable interpolation, alignment and padding, decimal precision
- **What to teach:** Basic f-string structure; embedding variables; formatting numbers for currency and decimals
- **If ahead of pace:** Advanced formatting (field width, alignment), nested expressions, percentage formatting
- **If behind pace:** Simple f-strings with variables only; print(f"Hello {name}"); skip advanced formatting

---

### Week 3 (Days 7–9): Complex Expressions & Project

#### Day 7: Math Module & Complex Expressions
- **Essential days:** FLEXIBLE—useful but not required for all programs
- **Key learning:** Importing modules, math.pi, math.sqrt(), math.pow(), order of operations in expressions
- **What to teach:** How to import and use modules; practical applications (area, distance); operator precedence
- **If ahead of pace:** Explore more math functions (sin, cos, log); use in scientific contexts
- **If behind pace:** Skip math module; focus on expressions using basic operators

#### Day 8: Putting It All Together
- **Essential days:** YES—synthesis and practice
- **Key learning:** Combining variables, operators, type conversion, strings, and formatting in complete programs
- **What to teach:** Solving multi-step problems; mixing data types effectively; clean output formatting
- **If ahead of pace:** Challenge with complex calculator programs; statistics calculations
- **If behind pace:** Provide templates; focus on one concept per program

#### Day 9: Unit 2 Project
- **Essential days:** FLEXIBLE (but recommended)—applies all unit concepts
- **Key learning:** Complete program integration; data manipulation; professional output
- **What to teach:** Designing small data processing programs; combining all concepts learned
- **If ahead of pace:** Add advanced features; require all formatting methods
- **If behind pace:** Provide starter code with structure; reduce requirements

---

## Differentiation Strategies

### For Struggling Students

**Scaffolding tips for this unit:**
- Provide visual aids showing variable boxes and string index positions
- Use concrete analogies: strings as sequences of beads, indices as bead positions
- Focus on one data type at a time before mixing
- Provide templates for f-strings and string methods
- Use online tools to visualize string slicing

**Which practice problems to assign first (easiest wins):**
- Practice Bank items 1-2 first (variable assignment basics)
- String concatenation with literal examples before methods
- Simple type conversion (int to str) before all conversions
- Basic f-strings before advanced formatting

**Suggested pacing adjustments:**
- Spread Unit 2 to 10-11 days instead of 9
- Dedicate full day to string indexing alone
- Skip math module entirely
- Combine Days 7-8 into one comprehensive practice day
- Move project to standalone day outside the 9-day count
- Provide "cheat sheet" with all string methods

**What prerequisite gaps to look for:**
- Weak algebra skills affecting expression evaluation
- Confusion about 0-based indexing
- Unable to distinguish between = and ==
- Difficulty with negative numbers and negative indices
- String immutability confusion (thinking strings can be changed)

---

### For On-Track Students

**Standard path through the unit:**
- Follow the 9-day schedule exactly as written
- Assign Beginner + Intermediate problems daily
- Complete project on Day 9 with all standard requirements
- Use f-strings from Day 6 onward in all outputs

**Which practice problems to assign:**
- Days 1-3: Beginner + Intermediate problems
- Days 4-6: Intermediate + one Challenge per day
- Days 7-8: Mixed Intermediate and Challenge problems
- Day 9: Full project

---

### For Advanced Students

**Extension activities specific to this unit's topics:**
- Explore regex (regular expressions) for pattern matching in strings
- Investigate Unicode and character encoding
- Build text analysis programs (word frequency, readability scores)
- Develop string manipulation libraries with custom functions (preview Unit 5)
- Challenge: implement string methods from scratch

**Challenge problems to assign:**
- Unit 2 Practice Bank items 10-15 (all Challenge tier)
- Day 3: Reverse strings using slicing with negative step
- Day 4: Complex string parsing and analysis problems
- Day 5: Truthiness puzzles with non-obvious values
- Day 6: Formatting with alignment and nested expressions
- Extra: Build a text cipher or simple encryption program

**Ways to deepen understanding beyond the curriculum:**
- Ask: "How would you implement upper() without using .upper()?"
- Explore string immutability: why Python makes strings unchangeable
- Build a program that analyzes text (vowel count, character frequency)
- Implement custom string formatting without f-strings
- Challenge: write a program that validates data types and formats properly

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Day 3:** Before string methods (foundation: basic strings work)
- **End of Day 5:** Before formatting (foundation: type conversion solid)
- **End of Day 6:** Before math module (foundation: output is professional)

### Topics students most commonly struggle with:
- **String indexing:** Off-by-one errors, confusion about negative indices
- **Slicing notation:** Understanding [start:stop:step] fully; why stop is exclusive
- **Type conversion:** Forgetting conversion causes errors; confusion when conversion fails
- **f-string syntax:** Forgetting braces, wrong syntax inside braces
- **Compound operators:** Misusing += with strings (it concatenates, not adds)

### Topics students typically move through quickly:
- **Basic assignment:** Most students pick up immediately
- **+ and - operators:** Familiar from math
- **String concatenation:** Intuitive with +
- **upper() and lower():** Simple methods with obvious purpose
- **Print with multiple variables:** Comfortable after Unit 1

---

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**After Day 1:**
- Can students use += and -=?
- Do they understand reassignment?
- Checkpoint: "Start with x=5, do x+=3, x*=2, print x. What is x?"

**After Day 3:**
- Can students index and slice strings correctly?
- Do they understand 0-based indexing?
- Checkpoint: "For s='hello', what is s[1], s[-1], s[1:3]?"

**After Day 5:**
- Can they convert between types?
- Do they understand when conversion is needed?
- Checkpoint: "Convert '25' to int, then add 5, then convert to string"

**After Day 6:**
- Can they format output with f-strings?
- Do they understand variable interpolation?
- Checkpoint: "Use f-string to print: Name: [name], Score: [score]%"

**After Day 8:**
- Can they combine multiple concepts?
- Can they solve a 2-3 step problem?
- Checkpoint: "Create variables for name and score, do a calculation, print nicely formatted"

---

## STEM-Specific Pacing Notes

This unit is **compressed from 10-12 days in full-year courses to 9 days for STEM semester**. Unit 2 is critical foundation for Unit 3 (conditionals) and all subsequent units.

**Key implications:**
- Every topic must stick the first time—limited re-teaching time
- String slicing is optional; indexing is required
- Math module can be skipped if running behind
- f-strings are strongly recommended despite time pressure
- Project can be shortened or moved if necessary

**Recommended daily structure (if 50-min class periods):**
- 5 min: Hook/review previous day
- 10 min: New concept instruction with examples
- 20 min: Guided practice (live coding with students)
- 10 min: Assign homework + code along for safety
- 5 min: Checkpoint question (exit ticket)

**Assessment checkpoints:**
Students must demonstrate mastery of:
1. Using compound assignment operators correctly
2. Converting between data types when needed
3. Indexing and slicing strings (at least indexing)
4. Using f-strings for formatted output
5. Solving a 2-3 step problem combining multiple concepts

---

## Unit 2 Success Criteria

By end of Unit 2, students should:
- Solve multi-step arithmetic problems with proper type handling
- Extract and manipulate data from strings (indexing, methods)
- Format output professionally using f-strings
- Convert between types as needed for calculations
- Combine variables, operators, and formatting in small programs

