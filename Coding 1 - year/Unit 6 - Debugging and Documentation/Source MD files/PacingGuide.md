# Unit 6 - Debugging and Documentation: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 25 days / 5 weeks (Days 121–145, 55-minute periods)
- **Core topics covered:** Three error types (syntax, runtime, logic), reading and interpreting tracebacks, debugging strategies (print statements, rubber duck debugging, systematic reasoning), testing and edge cases, try/except exception handling, writing clear comments and docstrings, Python naming conventions, file I/O (reading, writing, appending), processing file data (splitting, parsing CSV), using context managers (with statement), designing complete programs with all best practices
- **Prerequisites students need:** Mastery of Units 1–5 (all language features); understanding of program structure; experience building moderately complex programs

---

## Week-by-Week Pacing

### Week 25 (Days 121–125): Error Types & Reading Tracebacks
**Topics:** Three error types (syntax, runtime, logic), tracebacks and how to read them, common syntax errors, common runtime errors (ZeroDivisionError, TypeError, NameError, IndexError), debugging mindset

#### Essential days (cannot skip):
- **Day 121:** Three error types — foundational classification
- **Day 122:** Reading tracebacks and locating errors — essential debugging skill
- **Day 123:** Common syntax errors and how to fix them
- **Day 124:** Common runtime errors and how to fix them
- **Day 125:** Practice lab identifying and fixing all error types

#### Flexible days (can compress or cut if pressed for time):
- None. Understanding errors is foundational for all debugging.

#### If ahead of pace:
- Have them create a "traceback decoder" guide for peers
- Challenge: analyze complex tracebacks with multiple function calls
- Introduce exception types beyond the common ones

#### If behind pace:
- Combine Days 123–124 into one day (common errors)
- Extend Day 125 with additional error-identification exercises
- Provide error templates (show the error, show the fix)
- **Minimum viable coverage:** Days 121–124 (error types, tracebacks, common errors)

---

### Week 26 (Days 126–130): Debugging Strategies
**Topics:** Print debugging, rubber duck debugging, systematic debugging process, debugging loops and functions, common debugging mistakes, when to ask for help

#### Essential days (cannot skip):
- **Day 126:** Print debugging — adding print statements to trace execution
- **Day 127:** Rubber duck debugging — explaining code to find bugs
- **Day 129:** Debugging functions — tracing parameters and return values
- **Day 130:** Practice lab with challenging debugging scenarios

#### Flexible days (can compress or cut if pressed for time):
- **Day 128 (Debugging Loops):** Can be folded into Day 126 (print debugging) or combined with Day 130

#### If ahead of pace:
- Introduce debugging tools (debugger, breakpoints in IDE)
- Have them debug intentionally complex code
- Challenge: optimize debugging strategy (find bug in fewest steps)

#### If behind pace:
- Focus on print debugging only; defer rubber duck until later
- Provide debugging templates (where to add print statements)
- Combine Days 126–127 into one day
- **Minimum viable coverage:** Days 126, 129 (print debugging, function debugging)

---

### Week 27 (Days 131–135): Testing & Edge Cases
**Topics:** Testing mindset, identifying edge cases, writing test cases, manual testing strategies, try/except basics, handling errors gracefully

#### Essential days (cannot skip):
- **Day 131:** What is testing and why it matters
- **Day 132:** Identifying edge cases (boundary values, empty inputs, large values)
- **Day 133:** Writing test cases (expected vs. actual output)
- **Day 134:** try/except blocks — handling errors without crashing
- **Day 135:** Practice lab with comprehensive testing

#### Flexible days (can compress or cut if pressed for time):
- None. Testing and error handling are essential practices.

#### If ahead of pace:
- Introduce more exception types (ValueError, AttributeError, etc.)
- Have them write comprehensive test cases for complex programs
- Challenge: write a program that gracefully handles all possible errors

#### If behind pace:
- Focus on identifying edge cases and basic try/except
- Simplify testing to single test cases per program
- Provide test case templates
- **Minimum viable coverage:** Days 132–134 (edge cases, try/except)

---

### Week 28 (Days 136–140): Documentation & File I/O
**Topics:** Comments (explaining why, not what), docstrings (function documentation), Python naming conventions (snake_case, CONSTANT_NAMES), file I/O (reading, writing, appending), processing file data (splitting, parsing), context managers (with statement)

#### Essential days (cannot skip):
- **Day 136:** Comments and docstrings — documentation best practices
- **Day 137:** Python naming conventions — readability
- **Day 138:** Reading and writing files
- **Day 139:** Processing file data and parsing
- **Day 140:** Practice lab with file I/O programs

#### Flexible days (can compress or cut if pressed for time):
- Days 136–137 can be combined into one day if time is tight

#### If ahead of pace:
- Introduce JSON and CSV libraries
- Have them build file processing programs (data analysis, report generation)
- Challenge: write a program that reads multiple files and produces a summary report

#### If behind pace:
- Focus on reading and writing simple text files first
- Defer advanced parsing (CSV, JSON) to later
- Provide file I/O templates
- **Minimum viable coverage:** Days 138–139 (reading/writing files, basic parsing)

---

### Week 29 (Days 141–145): Review & Assessment
**Topics:** Comprehensive review of all debugging and documentation concepts, mini-projects combining all unit skills, formal assessment, reflection, preparation for Unit 7

#### Essential days (cannot skip):
- **Day 141:** Mini-project 1 — student writes a program with debugging, testing, documentation
- **Day 142:** Mini-project 2 — student writes a file I/O program with error handling
- **Day 144:** Unit 6 Assessment — formal evaluation
- **Day 145:** Assessment review, reflection, preparation for project unit

#### Flexible days (can compress or cut if pressed for time):
- **Day 143:** Review and practice — can be extended or condensed

#### If ahead of pace:
- Have students optimize for edge cases and error handling
- Challenge them to refactor earlier projects with proper debugging/documentation

#### If behind pace:
- Extend mini-project work days (141–142)
- Simplify project scope
- Offer retake option
- **Minimum viable coverage:** Days 141, 144 (mini-projects, assessment)

---

## Differentiation Strategies

### For Struggling Students
**Specific scaffolding tips:**
- **Reading tracebacks:** Highlight the key information: the error type, the line number, the error message. Trace back through the code to find the bug.
- **Print debugging:** Start with simple `print("Here 1")`, `print("Here 2")` to trace execution flow. Then add variable values: `print(f"x = {x}")`.
- **Rubber duck:** Provide a literal debugging duck (toy) or image. Have them verbally explain code line-by-line.
- **Edge cases:** Provide a checklist: empty input? zero? negative? very large? special characters?
- **try/except:** Show the template: `try: [risky code] except [error type]: [handle error]`. Fill in the blanks.

**Which practice problems to assign first (easiest wins):**
- Identify error type in simple code snippets (syntax, runtime, or logic?)
- Read simple tracebacks and locate the error
- Write try/except for division (ZeroDivisionError)
- Read and write simple text files
- Test simple programs with basic edge cases

**Suggested pacing adjustments:**
- Spend 2 days on reading tracebacks (Days 121–122) before moving to fix errors
- Provide error templates and solutions
- Use pair debugging (two students debug together)
- Extend practice labs with guided debugging exercises

**What prerequisite gaps to look for:**
- **Code reading comprehension:** Can they trace through code? If not, help with that skill first.
- **Problem-solving mindset:** Do they approach bugs systematically or randomly guess? Teach a process.
- **File knowledge:** Can they navigate file systems? Test this before file I/O.

### For On-Track Students
**Standard path through the unit:**
- Follow the week-by-week breakdown as written
- Complete practice problems from all five weeks
- Build two mini-projects: one debugging-focused, one file I/O-focused

**Which practice problems to assign:**
- Week 25: Identify error types, read tracebacks, fix syntax/runtime errors
- Week 26: Debug programs using print statements and rubber duck
- Week 27: Identify edge cases, write test cases, use try/except
- Week 28: Add documentation to programs, use file I/O
- All 5 weekly labs (Days 125, 130, 135, 140)

**Expectations:**
- Programs should have comprehensive comments explaining key sections
- Functions should have docstrings
- Code should use snake_case for variables and functions, CONSTANT_CASE for constants
- Programs should handle errors gracefully with try/except where appropriate
- All I/O operations should use context managers (with statement)

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Advanced debugging:** Use IDE debugger, set breakpoints, step through code
- **Automated testing:** Write unit tests using pytest or unittest framework
- **Advanced exception handling:** Catch multiple exception types, use else and finally clauses
- **File processing:** Parse JSON, CSV, or other structured data; build data processing pipelines
- **Code quality tools:** Introduce linters (flake8, pylint) to check code style

**Challenge problems to assign:**
- Write a program that processes a CSV file with error handling and generates a report
- Debug complex code with multiple functions and nested loops
- Write comprehensive test cases for a complex program
- Build a data analyzer that reads files, processes data, and writes results
- Refactor a previous project to include proper error handling and documentation

**Ways to deepen understanding beyond the curriculum:**
- Explore exception hierarchy and custom exceptions
- Study debugging best practices from software engineering
- Introduce continuous integration and automated testing
- Learn about logging (using the logging module instead of print())
- Build a project with comprehensive documentation and user guide

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Week 25:** Before moving to debugging strategies, ensure students can read tracebacks
- **End of Week 26:** Before moving to testing, ensure debugging strategies are comfortable
- **After Day 135:** Before file I/O, ensure try/except is solid

### Topics students most commonly struggle with (and expected time):
1. **Reading tracebacks:** 1-2 extra days. The format is unfamiliar; students focus on the error message but miss the line number.
2. **Edge cases:** 1 extra day. Students don't think about boundaries (empty, zero, negative). Use a checklist approach.
3. **try/except syntax:** 1 day. The block structure is new; students forget the exception type or the except clause.
4. **File paths:** 30 minutes to 1 day. Relative vs. absolute paths confuse some students; use explicit paths first.
5. **CSV parsing:** 1 day. Understanding how to split lines and access fields takes practice.

### Topics students typically move through quickly:
- **Print debugging:** Most students grasp adding print statements quickly
- **Common errors (TypeError, NameError):** Once they see examples, they recognize patterns
- **Naming conventions:** Snake_case vs CamelCase is easy to adopt with examples
- **Basic file reading:** Opening and reading lines from a file is straightforward
- **try/except for basic exceptions:** Simple `try/except ZeroDivisionError:` is intuitive

---

## Suggested Checkpoints

Use these quick formative checks mid-unit:

### After Day 125 (end of Week 25):
- **Quick Check:** Identify error type: `print(10 / 0)` (runtime), `if x > 5 print("yes")` (syntax), `sum = 5 + "5"` (runtime)
- **Code Check:** Read a traceback and identify where the error occurred

### After Day 130 (end of Week 26):
- **Quick Check:** "Add print statements to debug this function" (provide buggy function)
- **Code Check:** Debug a simple program using print debugging

### After Day 135 (end of Week 27):
- **Quick Check:** "Identify edge cases for a program that calculates age" (negative age? future date? zero?)
- **Code Check:** Write a try/except block that handles invalid user input

### Before Day 140 (mid-Week 28):
- **Code Check:** Students' file I/O programs in progress. Scan: Do files open/close properly? Is data parsed correctly?

---

## Common Misconceptions to Watch For

1. **"All bugs crash the program"** — Logic errors don't crash; they produce wrong answers.
2. **"Print debugging is unprofessional"** — Print debugging is a standard technique even in industry.
3. **"Tracebacks don't help"** — Tracebacks tell you exactly where the error occurred; students just need to learn to read them.
4. **"You must handle all errors"** — Some errors are worth letting the program crash on; focus on user input errors.
5. **"Comments should explain every line"** — Comments should explain WHY, not WHAT. Code is clear; comments explain intent.
6. **"Files are always available"** — File I/O can fail (missing file, permission denied, disk full). Always use try/except.
7. **"Edge cases don't matter"** — Edge cases (empty, zero, boundary values) are where bugs hide.
8. **"Testing is optional"** — Testing is essential; even professionals test before shipping code.

---

## Notes on Unit 6 Assessment

- **Assessment (Day 144):** Should include error identification (what type? fix it?), debugging challenge (find and fix bugs), edge case identification, and a coding task (write a program with file I/O, error handling, and documentation)
- **Common assessment mistakes:** Missing edge case testing, insufficient error handling, poor documentation, not reading tracebacks carefully
- **Retakes:** Offer retakes focused on weakest areas (debugging, testing, documentation)

---

## Performance Benchmarks

By the end of Unit 6, students should be able to:
- Identify and classify syntax, runtime, and logic errors
- Read and interpret tracebacks to locate bugs
- Use debugging strategies (print, rubber duck) to find and fix bugs
- Identify edge cases and write test cases
- Use try/except blocks to handle errors gracefully
- Write clear comments, docstrings, and follow naming conventions
- Read from and write to files using proper file I/O
- Process and parse file data
- Design and implement complete programs with quality, reliability, and documentation

