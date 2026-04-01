# Unit 4 - File I/O & Data Processing: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days / 3 weeks
- **Core topics covered:** File I/O (reading, writing, appending), text processing, CSV files, JSON files, exception handling, custom exceptions, data validation, and basic data analysis
- **Prerequisites students need:** Strong Python syntax (loops, conditionals, functions); comfortable with strings and lists; preferably Unit 1 (Data Structures) for dict/JSON understanding; error handling concepts

## Week-by-Week Pacing

### Week 1 (Days 1–3): File I/O & Text Processing
- **Essential days** (must teach):
  - Day 1: File reading/writing with `open()` and `with` statement
  - Day 2: Reading/writing files line-by-line; text processing
  - Day 3: File modes (read, write, append) and practical applications

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip line-by-line processing; focus on `read()` and `write()` only
  - Combine Days 1–2 into single day if necessary
  - Skip seek/tell operations; keep to basic file operations

- **If ahead of pace:**
  - Extend Day 2: String processing with regex (preview advanced topic)
  - Extend Day 3: Build file manipulation utilities (copy, merge, search)
  - Explore pathlib module for cross-platform file handling

- **If behind pace:**
  - Provide pre-written code; students run and modify rather than write from scratch
  - Use template for file operations; just change filenames/modes
  - Delay text processing; focus on basic read/write

### Week 2 (Days 4–6): CSV, JSON & Data Handling
- **Essential days** (must teach):
  - Day 4: CSV file operations using `csv` module
  - Day 5: JSON file operations; parsing and creating JSON
  - Day 6: Data validation and cleaning

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip JSON; use CSV only
  - Cut data validation; focus on reading/writing
  - Provide CSV/JSON reading code; students focus on analysis

- **If ahead of pace:**
  - Extend Day 4: CSV with DictReader; complex data transformations
  - Extend Day 5: Working with nested JSON; large JSON files
  - Extend Day 6: Data cleaning pipelines; handling missing values

- **If behind pace:**
  - Combine Days 4–5: Single day on CSV and JSON
  - Skip DictReader; use regular reader with manual index access
  - Use `json.load()` and `json.dump()` examples only

### Week 3 (Days 7–9): Exception Handling & Data Analysis
- **Essential days** (must teach):
  - Day 7: Exception handling—try/except, handling common file errors
  - Day 8: Custom exceptions; creating robust programs
  - Day 9: Data analysis project (combine all concepts)

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip custom exceptions; focus on built-in try/except
  - Cut advanced exception chains; teach basic error handling
  - Project: Provide heavy scaffolding and starter code

- **If ahead of pace:**
  - Extend Day 7: Multiple exception types, exception hierarchy
  - Extend Day 8: Building exception handling framework
  - Project: Add visualization with matplotlib; multi-file processing

- **If behind pace:**
  - Combine Days 7–8: Basic exception handling focus; skip custom exceptions
  - Project: Use provided exception code; students focus on data operations
  - Reduce project scope; use single data file

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Explain file I/O as "talking to files on your computer"; demystify it
- Use visual representation: File path like "address" of where file lives
- Emphasize `with` statement for safety: "Python closes file automatically"
- CSV/JSON: Show before/after: "This is how data looks in text, how Python sees it"
- Exception handling: Show "try do this, if it fails, do that instead"

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–3: Open file, read file, write file
- Unit Practice #4–5: Read CSV, write CSV (provide template)
- Unit Practice #6: Handle FileNotFoundError
- Unit Practice #7: Parse JSON file
- Emphasize: Getting any program to run successfully before optimization

**Suggested pacing adjustments:**
- Spend extra time on file paths; many students struggle with relative vs. absolute paths
- Use actual files on disk; let students see file creation in system
- Provide CSV/JSON template files for reading; don't require creation first
- Delay JSON parsing; start with simple JSON reading
- Use error messages as teaching tool; show what they mean

**What prerequisite gaps to look for:**
- String formatting and processing: If weak at string operations, file processing is harder
- Loop syntax with complex data: CSV and JSON require nested loops sometimes
- Dictionary understanding: JSON is nested dicts; if Unit 1 weak, JSON is very hard
- Error reading: If students can't read error messages, exception handling is mysterious

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–9 as designed
- Assign Unit Practice problems #1–10 (progression from basic I/O to error handling)
- Complete data analysis project with file reading, CSV/JSON, basic analysis
- Checkpoints: File operations quiz, exception handling scenarios

**Which practice problems to assign:**
- Problems #1–3: File I/O (read, write)
- Problems #4–7: CSV and JSON operations
- Problems #8–10: Data cleaning, statistics, full pipeline
- Project: Read data file, process/filter/analyze, generate report

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 5:** Explore nested JSON; work with real APIs (integrate Unit 6)
- **Day 6:** Build data cleaning pipeline; handle edge cases
- **Day 8:** Design exception handling framework for large application
- **Project:** Build data analysis tool with multiple file formats

**Challenge problems to assign:**
- Unit Practice #11–15: CSV filtering, custom exceptions, data cleaning, statistical analysis, data visualization
- Advanced: Build interactive data analyzer (read file, filter by user input, generate report)
- Challenge: Merge multiple CSV files; remove duplicates; generate summary
- Challenge: Create data validation system that checks data before processing
- Challenge: Build data transformation tool (CSV to JSON, JSON to CSV)

**Ways to deepen understanding beyond the curriculum:**
- Explore pandas library for data analysis (powerful alternative to manual file processing)
- Discuss data quality issues: missing values, inconsistent formatting, outliers
- Build real data project: Download actual CSV (e.g., Kaggle), analyze, visualize
- Explore XML and other data formats
- Challenge: Optimize code for processing very large files (memory efficiency)

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 3:** Before CSV/JSON, ensure file I/O is solid—students need confidence
- **After Day 6:** Before exceptions, ensure data handling is clear
- **After Day 8:** Before project, review file operations and error handling together

### Topics students most commonly struggle with:
1. **File paths:** Absolute vs. relative paths confuse many; path separators on different systems
2. **File modes:** Forgetting what 'w' vs. 'a' does; overwriting files accidentally
3. **`with` statement purpose:** Not understanding why it's important; trying to manually close
4. **CSV parsing:** Understanding data in list form; accessing rows and columns correctly
5. **JSON structure:** Forgetting JSON is nested dictionaries/lists; confusion on access patterns
6. **Exception syntax:** `except Exception as e:` syntax; forgetting indentation in except block
7. **Error messages:** Not reading error messages; not understanding what they mean

### Topics students typically move through quickly:
1. **Basic file reading:** `with open(...) as f: content = f.read()` is intuitive
2. **Writing files:** `f.write()` makes sense quickly
3. **CSV reading with csv module:** Once shown, pattern is clear
4. **JSON dumps/loads:** Conceptually straightforward
5. **Try/except basics:** Basic error catching feels natural

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Write code to open and read a file"
- "Why should we use `with` statement?"
- Check: Correct `with` syntax, understanding of automatic closing

**Day 2 Check (5 min):**
- "Read a file line-by-line and print each"
- "What method do you use?"
- Check: `.readlines()` or loop with `.readline()`, understanding of line processing

**Day 3 Check (5 min):**
- "What does mode 'a' do? Mode 'w'?"
- "How would you add to a file without overwriting?"
- Check: File mode understanding, practical application

**Day 4 Check (5 min):**
- "Read a CSV file and print the first row"
- "How do you access specific columns?"
- Check: csv module usage, row/column understanding

**Day 5 Check (5 min):**
- "Load a JSON file and print a nested value"
- "How does JSON structure relate to dictionaries?"
- Check: json.load() syntax, nested access

**Day 6 Check (5 min):**
- "Validate that a number is between 1 and 100; if not, print error"
- "What makes good validation?"
- Check: Validation logic, error messaging

**Day 7 Check (5 min):**
- "Write try/except to handle FileNotFoundError"
- "What should happen in each block?"
- Check: Try/except syntax, appropriate error handling

**Day 8 Check (5 min):**
- "Create a custom exception class"
- "When would you raise it?"
- Check: Custom exception syntax, understanding of when to use

**Day 9 Check (Project submission):**
- Data analysis project demonstrates: file I/O, CSV/JSON, exception handling, data processing
- Rubric: Correct file operations, proper error handling, accurate analysis, clean code

## STEM-Specific Pacing Notes

**Important:** File I/O is practical foundation for real-world programming. Tighter STEM timeline requires focus on essentials.

- **Essential vs. Optional:**
  - Essential: Basic file I/O, CSV reading/writing, try/except error handling (Days 1–7)
  - Optional: JSON in depth, custom exceptions, advanced data cleaning (Days 8–9)
  - Cut if behind: JSON parsing, custom exceptions, data validation complexity

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: loops, string operations, accessing nested data
  - File processing amplifies these gaps—consider review before Unit 4
  - Error messages can be intimidating; normalize them as "helpful feedback"

- **When to cut:**
  - If behind after Day 3, skip JSON entirely; focus on CSV and text files
  - Skip custom exceptions; teach only built-in exception handling
  - Skip data validation complexity; keep to basic checks
  - Reduce project: Single file, single operation (read/write or analyze)

- **When to accelerate:**
  - Fast students can jump to pandas library for data operations
  - Use excess time for integration with Unit 6 (APIs produce JSON)
  - Have advanced students build data pipeline tools

**Project scope by level:**
- Minimum: Read text file or CSV; print processed data; handle 1 exception type
- Standard: Read CSV/JSON; filter/analyze; generate report; handle multiple exceptions
- Extended: Multiple file formats; data cleaning; visualization; interactive analysis

**Connection to other units:**
- **Unit 1:** Data structures essential for understanding CSV rows and JSON nesting
- **Unit 2:** Classes can wrap file operations (e.g., DataFile class with methods)
- **Unit 5:** Sorting/searching CSV data is practical application
- **Unit 6:** APIs produce JSON; file I/O stores the results
