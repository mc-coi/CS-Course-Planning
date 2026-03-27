# Unit 4: File I/O & Data Processing

> Learn to read, write, and process data from files. Master CSV, JSON, exception handling, and regular expressions for real-world data tasks.

## Unit Overview

- **Duration:** 26 days / ~5 weeks
- **Course Days:** 80–105 (traditional schedule)
- **TN Standard:** 9-12.CCI.4 — Use external data sources and appropriate tools to collect, organize, process, and interpret data
- **Prerequisite:** Coding II Units 1-3 (variables, functions, data structures)

---

## Essential Question

*How can we efficiently read, validate, and process data from external files to solve real-world problems?*

---

## Learning Outcomes

By the end of Unit 4, students will be able to:

✓ Open, read, and write text files using proper file handling patterns
✓ Parse and process CSV and JSON data formats
✓ Validate and clean data before processing
✓ Handle errors gracefully with exception handling
✓ Search text patterns using regular expressions
✓ Analyze data by computing statistics and generating reports
✓ Build complete data processing pipelines from file I/O to output

---

## Unit Schedule

### Days 1-3: File Reading & Writing Basics
- File opening modes and the `with` statement
- Reading entire files and line-by-line processing
- Writing data to files
- Understanding when and why files must be closed

### Days 4-8: CSV File Processing
- Using `csv.reader()` for list-based data
- Using `csv.DictReader()` and `csv.DictWriter()` for dictionary-based data
- Reading, filtering, and transforming CSV files
- Lab: Building a student records system

### Days 9-11: JSON File Processing
- Parsing JSON with `json.loads()` and `json.dumps()`
- Reading and writing JSON files
- Working with nested JSON structures
- Lab: Processing API-like data

### Days 12-16: Exception Handling
- Try/except/else/finally patterns
- Handling specific and multiple exception types
- Raising custom exceptions
- Creating exception hierarchies
- Practical error handling in file operations

### Days 17-20: Data Validation & Regex
- Validating input data (types, ranges, formats)
- Using regular expressions for pattern matching
- Email and phone number validation
- Text pattern extraction and substitution

### Days 21-22: Data Analysis & Reporting
- Computing statistics (mean, median, min, max)
- Grouping and aggregating data
- Writing formatted reports to files
- Exporting results as JSON and CSV

### Days 23-24: Integration & Review
- Combining all unit concepts into complete pipelines
- Code review and debugging techniques
- Real-world problem-solving scenarios
- Consolidation of key concepts

### Days 25-26: Capstone & Assessment
- Planning comprehensive data processing projects
- Unit assessment with multiple choice, short answer, and coding challenges

---

## Key Topics by Category

### File I/O
- File modes (`'r'`, `'w'`, `'a'`, `'x'`)
- Context managers (`with` statement)
- Reading methods (`.read()`, `.readline()`, `.readlines()`)
- Writing methods (`.write()`, `.writelines()`)
- File object properties and methods

### CSV Processing
- `csv.reader()` — iterate rows as lists
- `csv.DictReader()` — access columns by name
- `csv.writer()` — write rows as lists
- `csv.DictWriter()` — write rows as dicts
- Handling special characters and delimiters

### JSON Processing
- `json.loads()` / `json.load()` — parse JSON
- `json.dumps()` / `json.dump()` — convert to JSON
- Nested data structures
- Pretty-printing with indentation

### Exception Handling
- `try/except/else/finally` pattern
- Multiple exception handlers
- Raising exceptions with meaningful messages
- Custom exception classes

### Data Validation
- Type checking with `isinstance()`
- Range validation
- Format validation (regex patterns)
- Required field checking
- Data cleaning and normalization

### Regular Expressions
- Common patterns (email, phone, date, URL)
- `re.search()`, `re.match()`, `re.findall()`
- `re.sub()` for replacement
- Character classes and quantifiers

### Data Analysis
- Computing statistics (mean, median, mode, min, max)
- Grouping and aggregating data
- Percentiles and distributions
- Trend analysis

---

## Daily Notes & Resources

All daily lessons (Day 1-26) include:
- **Learning Target** — specific, measurable skill for the day
- **Key Concepts** — vocabulary and big ideas
- **Code Examples** — 5-10 annotated examples
- **Guided Practice** — step-by-step activity with teacher
- **Practice Problems** — 3 levels (Beginner, Intermediate, Challenge)
- **Solutions** — complete working code for all problems

**Access Daily Notes:** See `Daily Notes/` folder for Day1.md through Day26.md

---

## Supporting Resources

### ReferenceGuide.md
Quick reference for syntax and patterns:
- File operations cheat sheet
- CSV/JSON quick syntax
- Exception handling patterns
- Common error messages and solutions
- Best practices checklist

### UnitPractice.md
**20 practice problems** with full solutions:
- File I/O Basics (3 problems)
- CSV Processing (5 problems)
- JSON Processing (3 problems)
- Exception Handling (3 problems)
- Data Validation & Regex (6 problems)

### UnitAssessment.md
**Formal unit assessment:**
- 10 multiple choice questions
- 5 short answer questions
- 3 coding challenges
- Answer key and grading rubric

---

## Common Mistakes to Avoid

| Mistake | Impact | Solution |
|---------|--------|----------|
| Forgetting to close files | Resource leak, file locks | Always use `with` statement |
| No error handling | Program crashes | Use try/except for file operations |
| Assuming file format | Crashes on unexpected data | Validate and clean data first |
| Hard-coding file paths | Won't work on other computers | Use relative paths or `pathlib` |
| Reading huge files at once | Memory overflow | Read line-by-line for large files |
| Invalid JSON syntax | Parsing fails | Check quotes, commas, braces |
| No data validation | Bad data processed as good | Validate types and ranges |
| Greedy regex patterns | Unexpected matches | Test regex carefully |

---

## Vocabulary Reference

**Essential Terms:**

- **API** — Application Programming Interface; often returns JSON data
- **CSV** — Comma-Separated Values; tabular text file format
- **Exception** — Error that occurs during program execution
- **JSON** — JavaScript Object Notation; lightweight data format
- **Parsing** — Converting text into usable data structures
- **Regex** — Regular expression; pattern for matching text
- **Validation** — Checking data meets expected requirements
- **with statement** — Context manager ensuring file closure

---

## Assessment Levels

### Level 1: Foundational (Can do with assistance)
- Open and read files with `with` statement
- Use basic CSV reading with `csv.reader()`
- Parse simple JSON strings
- Write try/except blocks
- Validate basic data types

### Level 2: Proficient (Can do independently)
- Process CSV files with filtering and transformation
- Work with nested JSON structures
- Handle multiple exception types
- Use regex for pattern matching
- Compute basic statistics

### Level 3: Mastery (Can teach others)
- Design complete data pipelines
- Build custom validation systems
- Process complex nested data
- Create robust error handling
- Generate formatted reports

---

## Real-World Applications

**Where File I/O & Data Processing is Used:**

- **Data Science** — Reading datasets, processing, analyzing
- **Web Development** — Handling CSV uploads, processing form data
- **System Administration** — Log file analysis, data migration
- **Business** — ETL pipelines, data validation, reporting
- **Scientific Computing** — Processing experimental data
- **Machine Learning** — Data preparation and cleaning

---

## Tools & Resources

**Built-in Python Modules:**
- `csv` — CSV file reading/writing
- `json` — JSON parsing
- `re` — Regular expressions
- `os` — File system operations
- `pathlib` — Modern path handling

**Note for Online IDEs:**
Students using Kira Learning or similar platforms should be aware that file paths may behave differently. Relative paths like `'./data.txt'` work best.

---

## Success Tips

1. **Always use `with` statements** — Guarantees file closure
2. **Test with small data first** — Before processing large files
3. **Print intermediate results** — Debug by seeing what data looks like
4. **Validate early** — Check data quality before processing
5. **Use meaningful variable names** — Makes code easier to understand
6. **Handle errors explicitly** — Don't let exceptions crash silently
7. **Comment complex logic** — Explain why, not just what
8. **Reuse code** — Write functions for repeated operations

---

## Getting Help

**If you're stuck:**
1. Check the ReferenceGuide for syntax examples
2. Review the corresponding day's lesson
3. Look at worked examples in UnitPractice
4. Work through the Guided Practice section
5. Ask for help with error messages

---

## Final Project (Days 23-26)

Students will complete a **Capstone Data Processing Project** that:
- Reads data from CSV or JSON
- Validates and cleans the data
- Performs meaningful analysis
- Generates a report
- Includes comprehensive error handling

This project demonstrates mastery of all Unit 4 concepts.

---

**Good luck! File I/O and data processing are essential skills for any programmer. You're building the foundation for data science, web development, and many other fields.**
