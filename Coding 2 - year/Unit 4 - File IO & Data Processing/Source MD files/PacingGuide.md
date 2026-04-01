# Unit 4 - File I/O & Data Processing: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 26 days (~5 weeks)
- **Core topics covered:**
  - File I/O fundamentals: reading, writing, file modes
  - The with statement and context managers
  - CSV file processing: csv.reader(), csv.DictReader()
  - JSON file processing: json.loads(), json.dumps()
  - Exception handling: try/except/else/finally
  - Data validation and type checking
  - Regular expressions: pattern matching, substitution
  - Data analysis: statistics, grouping, aggregation
  - Building data processing pipelines
  - Real-world file operations and error handling
- **Prerequisites students need:**
  - Unit 1: Data structures (lists, dicts)
  - Unit 2: OOP concepts
  - Unit 3: Functional programming (map, filter, comprehensions)
  - String manipulation basics
  - Strong loop and conditional knowledge

---

## Week-by-Week Pacing

### Week 1 (Days 1–5): File I/O Fundamentals

#### Days 1–3: File Reading & Writing Basics
- **Essential days** (must teach): YES
  - Foundation for everything in this unit
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: File modes (r, w, a, x), binary vs text files, large file processing
- **If behind pace**: Focus on read() and write() with simple files; skip readline() details

#### Days 4–5: File I/O Lab & Practice
- **Essential days** (must teach): YES
  - Integration of file operations with data processing
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 1–3
- **If ahead of pace**: Efficient file reading strategies, working with large files
- **If behind pace**: Provide templates; focus on basic read/write patterns

### Week 2 (Days 6–11): CSV & JSON Processing

#### Days 6–8: CSV File Processing
- **Essential days** (must teach): YES
  - CSV is the most common data format in practice
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Advanced CSV features (dialects, escaping), handling malformed CSV
- **If behind pace**: Focus on csv.reader() and csv.DictReader(); skip writing initially

#### Days 9–11: JSON File Processing
- **Essential days** (must teach): YES
  - JSON is essential for APIs and data interchange
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Complex nested JSON, streaming JSON processing
- **If behind pace**: Focus on json.loads() and json.dumps(); simple nested structures

### Week 3 (Days 12–17): Exception Handling

#### Days 12–16: Exception Handling Patterns
- **Essential days** (must teach): YES
  - Robust error handling is critical for production code
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Custom exceptions, exception hierarchies, logging
- **If behind pace**: Focus on basic try/except; skip else and finally initially

#### Day 17: Exception Handling Lab
- **Essential days** (must teach): YES
  - Practice with real file operations
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 12–16
- **If ahead of pace**: Complex error handling scenarios, recovery strategies
- **If behind pace**: Provide templates; focus on FileNotFoundError and ValueError

### Week 4 (Days 18–22): Data Validation & Regex

#### Days 18–19: Data Validation
- **Essential days** (must teach): YES
  - Validating data before processing prevents bugs
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Schema validation, complex validation rules
- **If behind pace**: Focus on type checking and range validation

#### Days 20–21: Regular Expressions
- **Essential days** (must teach): PARTIAL
  - Regex is useful but optional; focus on common patterns
- **Flexible days** (can compress or cut if pressed for time): YES — can be simplified
- **If ahead of pace**: Complex regex patterns, lookahead/lookbehind, regex optimization
- **If behind pace**: Simple patterns only (email, phone, basic search)

#### Day 22: Data Analysis & Reporting
- **Essential days** (must teach): YES
  - Computing statistics and generating reports is practical
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 20–21
- **If ahead of pace**: Statistical analysis, grouping operations
- **If behind pace**: Focus on mean, median, min, max; skip advanced aggregation

### Week 5 (Days 23–26): Integration & Assessment

#### Days 23–24: Integration Lab & Mini-Project
- **Essential days** (must teach): YES
  - Application of all concepts
- **Flexible days** (can compress or cut if pressed for time): Can be 1 day if behind
- **If ahead of pace**: Complex data pipelines, multiple file processing
- **If behind pace**: Provide templates; focus on putting concepts together

#### Day 25: Code Review & Best Practices
- **Essential days** (must teach): YES
  - Learning from mistakes
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 24
- **If ahead of pace**: Performance optimization, real-world best practices
- **If behind pace**: Teacher-led examples only

#### Day 26: Unit Assessment
- **Essential days** (must teach): YES
  - Assessment required
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early completers start Unit 5 or get enrichment
- **If behind pace**: Extended time if needed

---

## Differentiation Strategies

### For Struggling Students

**Common gaps:**
- Weak on exception handling concepts
- Confusion with file mode syntax
- Difficulty with data structure complexity in CSV/JSON

**Specific scaffolding:**
- Provide **"File I/O Cheat Sheet"** with mode explanations
- Use **concrete data sets** (student records, weather data) consistently
- Create **exception handling templates** with try/except structure
- Show **CSV and JSON examples** side-by-side for comparison
- Provide **regex pattern library** for common needs

**Which practice problems to assign first:**
- Basic file reading and writing
- Simple CSV reading with csv.DictReader()
- Simple JSON parsing
- Basic try/except with FileNotFoundError
- Simple data validation (type checking)

**Suggested pacing adjustments:**
- Skip regex or reduce to basic patterns only
- Skip custom exceptions
- Focus on try/except; skip else and finally
- Provide CSV and JSON templates
- Simplify mini-project requirements

**Prerequisite gaps to watch for:**
- If weak on data structures, CSV/JSON parsing will be hard; review dicts/lists
- If weak on loops, processing file lines will be slow; review for loops
- If weak on conditionals, exception handling logic won't click; review if/else

**Reteaching strategies:**
- Use the same data sets repeatedly
- Show file operations visually (print before/after states)
- Physical demonstrations of exception flow
- Pair with stronger students for Days 23–24 project

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Complete practice problems covering all concepts
- Do the integration lab and mini-project
- Pass the unit assessment

**Which practice problems to assign:**
- All basic to intermediate CSV and JSON problems
- Exception handling with multiple try/except patterns
- Basic regex for common patterns
- Data analysis and reporting

**Pacing tips:**
- Days 1–11 should feel manageable
- Days 12–17 (exception handling) monitor for confusion
- Days 18–22 get more abstract (regex); monitor closely

### For Advanced Students

**Extension activities:**
- Build complete data processing pipelines
- Implement custom validation schemas
- Advanced regex patterns with lookahead/lookbehind
- Performance optimization for large files
- Error recovery and data repair strategies
- Building data cleaning tools

**Challenge problems to assign:**
- Complex CSV/JSON with nested structures
- Multiple file processing and merging
- Advanced regex with complex patterns
- Statistical analysis and reporting
- Performance benchmarking
- Error handling and recovery strategies

**Ways to deepen understanding:**
- Study streaming file processing for memory efficiency
- Implement custom exception hierarchies
- Build data cleaning utilities
- Explore pandas for advanced data processing
- Study real-world data processing pipelines
- Learn about data formats beyond CSV/JSON

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 5:** Checkpoint for file I/O before moving to CSV/JSON
- **After Day 11:** Checkpoint for data format processing before exception handling
- **After Day 17:** Checkpoint for exception handling before validation/regex
- **After Day 22:** Final checkpoint before assessment

### Topics students typically struggle with:
1. **File modes** (Days 1–3): r, w, a, x syntax
   - *Fix:* Visual chart, repetition, show what happens with each
2. **Exception handling** (Days 12–16): Flow control is non-obvious
   - *Fix:* Trace through examples, show what catches what
3. **Regular expressions** (Days 20–21): Pattern syntax is cryptic
   - *Fix:* Provide pattern library, start with simple patterns
4. **CSV/JSON parsing** (Days 6–11): Structure complexity
   - *Fix:* Visual examples, step-by-step extraction
5. **Data validation** (Days 18–19): What to validate?
   - *Fix:* Provide validation templates, concrete examples

### Topics students typically move through quickly:
1. **Reading files** (Days 1–2): Straightforward with templates
2. **Basic exception handling** (Days 12–13): try/except pattern is simple
3. **Simple JSON parsing** (Days 9–10): json.loads() is straightforward
4. **Data analysis** (Day 22): Computing mean, median is familiar math

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 5:** Can students read and write files?
   - Quick task: "Read a file, process lines, write results"
2. **After Day 11:** Can students parse CSV and JSON?
   - Quick task: "Extract data from CSV and JSON, compare"
3. **After Day 17:** Can students handle exceptions?
   - Quick task: "Write try/except for file not found"
4. **After Day 22:** Can students validate and analyze data?
   - Quick task: "Validate numbers in range, compute statistics"

### Summative checks (end-of-unit):
1. **Day 26 Assessment:**
   - Part A: Multiple choice (file modes, concepts)
   - Part B: Short answer (exception handling, validation)
   - Part C: Coding (read file, parse data, process, handle errors)

### Lab checkpoints (Days 5, 11, 17, 22, 23–24):
- Demonstrate file operations, data processing, and error handling in practice

---

## Notes on Unit 3 Prerequisites

This unit builds on Unit 3 (functions, comprehensions, recursion). Watch for:

- **Data structures:** If weak on dicts/lists, JSON and CSV parsing will be hard
- **Comprehensions:** If weak, data processing will be slow; review comprehensions
- **Exception handling:** First time seeing this; no prerequisite but explain carefully
- **File operations:** File I/O is new; start from basics

---

## Time Management Tips

- **If 5 days ahead:** Use time for advanced regex, streaming, performance optimization, or early Unit 5 start
- **If 3 days behind:** Simplify regex to basics, provide CSV/JSON templates, provide exception templates
- **If 1 week behind:** Focus only on file I/O (Days 1–5) and CSV/JSON (Days 6–11); skip regex and advanced topics
- **If 2 weeks behind:** Teach only basic file I/O and CSV; skip JSON, regex, validation

---

## Key Assessment Targets

By the end of Unit 4, all students should demonstrate:
1. Reading and writing text files with proper file handling
2. Parsing CSV files with csv.DictReader()
3. Parsing JSON files with json.loads()
4. Handling exceptions with try/except patterns
5. Validating input data (type, range, format)
6. Using regular expressions for simple pattern matching
7. Computing basic statistics (mean, median, min, max)
8. Building a complete data processing pipeline

Students working at advanced level should additionally demonstrate:
- Complex JSON and CSV with nested structures
- Custom exception handling and recovery
- Advanced regex patterns
- Statistical analysis and aggregation
- Performance optimization
- Error handling in production code
