# Unit 6 - Debugging & Documentation: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 6 days (compressed for STEM semester)
- **Core topics covered:** Error types (syntax/runtime/logic), debugging strategies, file I/O (reading and writing), exception handling (try/except/finally), docstrings, code comments and documentation
- **Prerequisites students need:** Mastery of Units 1-5; ability to recognize when code isn't working; understanding of program flow

---

## Week-by-Week Pacing (compressed into 1.5 weeks)

### Week 1 (Days 1–3): Errors & Debugging

#### Day 1: Types of Errors & Debugging Strategies
- **Essential days:** YES—recognizing and fixing bugs
- **Key learning:** Syntax errors (won't run), runtime errors (crash), logic errors (wrong answer), exception types, debugging strategies
- **What to teach:** Reading error messages; where errors appear in output; common exception types with causes; systematic debugging approach
- **If ahead of pace:** Advanced debugging with IDE tools; profiling and optimization
- **If behind pace:** Focus on syntax and runtime errors; skip logic error complexity

#### Day 2: File Input & Output
- **Essential days:** YES—reading and writing files essential for STEM
- **Key learning:** open(), reading files (readlines, readline, read), writing files, close() or with statement, file modes
- **What to teach:** File paths; text vs. binary; with statement for safe file handling; basic file operations
- **If ahead of pace:** CSV parsing, JSON, working with complex files
- **If behind pace:** Simple read and write only; skip file modes; provide templates

#### Day 3: Exception Handling (try/except)
- **Essential days:** YES—handling errors gracefully
- **Key learning:** try/except blocks, catching specific exceptions, finally block, avoiding silent failures
- **What to teach:** What happens when exception occurs; how try/except prevents crash; multiple except blocks for different errors
- **If ahead of pace:** Complex exception hierarchies; custom exceptions; exception best practices
- **If behind pace:** Basic try/except; catch all exceptions; simple error messages

---

### Week 2 (Days 4–6): Documentation & Integration

#### Day 4: Docstrings & Code Comments
- **Essential days:** YES—documentation enables code understanding
- **Key learning:** Docstrings for functions (what, parameters, returns), inline comments for logic, documentation standards, writing for others
- **What to teach:** Docstring format; what to comment (why, not what); making code self-documenting; professional documentation
- **If ahead of pace:** Markdown docstrings; API documentation generation
- **If behind pace:** Simple docstrings; basic comments; focus on clarity

#### Day 5: Review & Integration
- **Essential days:** YES—putting all skills together
- **Key learning:** Applying all prior units' concepts with debugging and documentation emphasis
- **What to teach:** Debugging workflow; when to use which debugging strategy; complete programs with documentation
- **If ahead of pace:** Code review and refactoring; documentation review
- **If behind pace:** Guided walkthroughs of debugging; templates for documentation

#### Day 6: Unit 6 Project
- **Essential days:** FLEXIBLE (but recommended)—complete program with all skills
- **Key learning:** Building working, documented, debugged program from scratch
- **What to teach:** Project requirements and expectations; debugging workflow; documentation standard
- **If ahead of pace:** Complex programs with file I/O and multiple functions
- **If behind pace:** Simpler requirements; provided structure and comments template

---

## Differentiation Strategies

### For Struggling Students

**Scaffolding tips for this unit:**
- Provide error reference sheet with common exceptions and causes
- Use visual debugging flow (Is it syntax? Runtime? Logic?)
- Provide file I/O templates for common operations
- Use checklists for documentation (docstring items, comment placement)
- Practice reading error messages in small examples first

**Which practice problems to assign first (easiest wins):**
- Identify error type before fixing (syntax, runtime, or logic)
- Read simple files before writing
- Write simple files before complex I/O
- Try/except with single exception type before multiple
- Copy-paste docstring template before writing from scratch

**Suggested pacing adjustments:**
- Focus on syntax and runtime errors; defer complex logic errors
- Skip exception handling complexity; basic try/except only
- Focus on file reading, skip writing initially
- Provide docstring templates to fill in
- Combine Days 1-2 into "error handling" and Days 3-4 into "documentation"
- Shorten Day 5 and use Day 6 for guided project work

**What prerequisite gaps to look for:**
- Cannot read error messages or identify the problem
- Doesn't understand what exceptions are
- Never used file operations before
- Weak understanding of function parameters (documentation becomes confusing)
- Limited experience with long programs (documentation seems unnecessary)

---

### For On-Track Students

**Standard path through the unit:**
- Follow 6-day schedule as written
- Assign problems covering all error types
- Implement file I/O in practice
- Complete project on Day 6 with all requirements

**Which practice problems to assign:**
- Days 1-3: Mix of error identification, file I/O, exception handling
- Days 4-5: Documentation and integration practice
- Day 6: Full project

---

### For Advanced Students

**Extension activities specific to this unit's topics:**
- Automated testing and test-driven development (TDD)
- Logging systems for debugging complex programs
- Working with structured data formats (JSON, CSV)
- Custom exception classes
- Code coverage and test effectiveness

**Challenge problems to assign:**
- Build robust programs with comprehensive error handling
- Parse complex file formats
- Implement custom exception types
- Write logging systems
- Test and debug others' code
- Build data processing pipelines with file I/O

**Ways to deepen understanding beyond the curriculum:**
- Ask: "How would this code fail if given unexpected input?" (robustness thinking)
- Challenge: "Debug this complex multi-function program" (tracing through code)
- Explore: Unit tests and automated testing (preview)
- Build: Data processing pipeline reading, processing, and writing files
- Investigate: How professional code handles errors and documents itself

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Day 1:** Before file I/O (debugging workflow established)
- **End of Day 3:** Before documentation (error handling functional)
- **End of Day 5:** Before project (all skills reviewed)

### Topics students most commonly struggle with:
- **Reading error messages:** Not finding the actual problem in the message
- **Logic errors:** Hardest to identify (program runs but is wrong)
- **File paths:** Relative vs. absolute; file not found errors
- **Exception handling:** Over-catching exceptions (catching everything); silent failures
- **Documentation quality:** Writing obvious comments ("x = 5 # set x to 5"); missing important context
- **File I/O modes:** Overwriting files accidentally; trying to read non-existent files

### Topics students typically move through quickly:
- **Syntax errors:** Clear error message identifies problem
- **Basic try/except:** Simple concept once explained
- **Reading files:** Straightforward operation
- **Docstring format:** Copy template and fill in
- **Identifying error type:** With practice, pattern recognition helps

---

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**After Day 1:**
- Can they classify errors into categories?
- Can they read and interpret error messages?
- Checkpoint: "Here's an error message—what type is it and where's the problem?"

**After Day 2:**
- Can they read and write files?
- Checkpoint: "Write program that reads file, prints lines with a word count"

**After Day 3:**
- Can they use try/except?
- Checkpoint: "Write try/except that handles ValueError from int(input())"

**After Day 4:**
- Can they write clear docstrings?
- Checkpoint: "Write docstring for a function that takes a list and returns average"

**After Day 5:**
- Can they debug a multi-part program?
- Checkpoint: "Given broken program, identify and fix all errors"

---

## STEM-Specific Pacing Notes

Unit 6 is a **professional skills unit** that bridges to capstone projects. Error handling and documentation are essential for scientific code that others must understand and extend. Unit 6 is compressed from 7-8 days in full-year courses to 6 days for STEM semester.

**Key implications:**
- File I/O is critical for STEM (reading experimental data, writing results)
- Error handling prevents silent failures in scientific programs (critical!)
- Documentation is essential for scientific reproducibility
- Time is short—prioritize essentials (errors, files, basic exceptions)
- Can defer advanced topics to Unit 7 or project work

**Recommended daily structure (if 50-min class periods):**
- 5 min: Hook with debugging a provided program
- 10 min: Concept explanation and common error examples
- 20 min: Guided practice (debug together, write files, etc.)
- 10 min: Assign practice; work on one together
- 5 min: Checkpoint: Can they identify the issue/explain the concept?

**Critical mastery targets:**
By end of Unit 6, students MUST be able to:
1. Classify errors as syntax, runtime, or logic
2. Read error messages and identify the problem
3. Read from and write to files
4. Use try/except to handle errors gracefully
5. Write clear docstrings and helpful comments
6. Systematically debug a broken program

---

## Assessment & Mastery Validation

Quick verification questions:

1. **Day 1:** Given error message, can they identify type and fix?
2. **Day 2:** Can they read data from file and process it?
3. **Day 3:** Can they use try/except to handle specific exceptions?
4. **Day 4:** Does docstring clearly describe function's purpose/parameters/return?
5. **Day 5:** Can they debug a multi-function program with mixed error types?
6. **Project:** Complete working, documented program that handles errors gracefully

---

## Special STEM Considerations

**File I/O in STEM Context:**
- Reading experimental data (CSV, plain text)
- Writing analysis results to files
- Handling large datasets efficiently
- Maintaining data integrity through processing

**Error Handling in STEM Context:**
- Invalid data in experiments (out of range, missing values)
- Computational errors (division by zero, sqrt of negative)
- Silent failures masking bad results
- Need for robust error messages for debugging

**Documentation in STEM Context:**
- Reproducibility requires clear code and methods
- Others must understand your algorithms
- Comments should explain "why," not "what"
- Scientific accuracy depends on clear implementation

