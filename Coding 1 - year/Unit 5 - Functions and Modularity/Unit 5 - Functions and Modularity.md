# Unit 5: Functions and Modularity

## Unit Overview

**Duration:** 25 days (5 weeks) | **Days 96–120** | **Coding I**

Functions are the building blocks of Python programs. Rather than writing the same code over and over, functions allow you to package a sequence of instructions into a reusable block with a name. This unit covers everything from the basics of function definition and calling to advanced topics like scope, composition, and modular design.

By the end of Unit 5, you will:
- Write and call functions with parameters and return values
- Understand variable scope (local vs. global)
- Design modular programs using top-down design
- Write well-documented code with docstrings
- Build complete, maintainable programs using functions as the primary organizational tool

---

## Week 20: Function Basics (Days 96–100)

### Day 96: What Are Functions? Why Use Them?
Functions allow you to bundle code into reusable, named blocks. Instead of repeating code, you call the function by name. Learn the `def` keyword, how to define a function, and how to call it.

**Topics:** Function definition, calling functions, why functions matter
**[→ Day 96 Notes](Daily%20Notes/Day96.md)**

### Day 97: Parameters and Arguments
Functions become powerful when they accept **parameters**—variables that receive data when the function is called. Learn how to define parameters and pass arguments when calling.

**Topics:** Parameters, arguments, passing data into functions
**[→ Day 97 Notes](Daily%20Notes/Day97.md)**

### Day 98: Return Values
Functions can send data back to the caller using the `return` keyword. This transforms functions from "do something" into "do something and give me a result."

**Topics:** Return values, the return keyword, returning data
**[→ Day 98 Notes](Daily%20Notes/Day98.md)**

### Day 99: Multiple Parameters and Defaults
Learn how to define functions with multiple parameters and assign default values so callers don't always have to provide all arguments.

**Topics:** Multiple parameters, default parameter values, function flexibility
**[→ Day 99 Notes](Daily%20Notes/Day99.md)**

### Day 100: Practice Lab
Build your own function library: write a set of 5–8 related functions (e.g., math helpers, string utilities, or game functions) and test them together.

**Topics:** Function design, testing, practice
**[→ Day 100 Notes](Daily%20Notes/Day100.md)**

---

## Week 21: Scope & Organization (Days 101–105)

### Day 101: Variable Scope — Local vs. Global
Every variable exists in a **scope**. Variables defined inside a function are **local** (exist only in that function). Variables defined at the top level are **global** (exist everywhere). Understanding scope prevents bugs.

**Topics:** Local scope, global scope, scope rules
**[→ Day 101 Notes](Daily%20Notes/Day101.md)**

### Day 102: The Global Keyword and Why to Avoid It
You *can* modify global variables inside functions using the `global` keyword, but this is usually a bad practice. Learn why and how to design functions that avoid needing it.

**Topics:** The global keyword, side effects, good design
**[→ Day 102 Notes](Daily%20Notes/Day102.md)**

### Day 103: Functions Calling Functions — Composition
Functions can call other functions. This **composition** is key to breaking large problems into smaller, manageable pieces.

**Topics:** Function composition, abstraction, breaking down problems
**[→ Day 103 Notes](Daily%20Notes/Day103.md)**

### Day 104: Docstrings and Function Documentation
Write **docstrings**—documentation inside your function definition—to explain what the function does, what parameters it expects, and what it returns. Good documentation is essential for maintainable code.

**Topics:** Docstrings, documentation, code readability
**[→ Day 104 Notes](Daily%20Notes/Day104.md)**

### Day 105: Practice Lab
Write a set of well-documented functions and a main program that uses them to solve a real problem (e.g., a student grade calculator, inventory system, or simple game).

**Topics:** Documentation, organization, complete programs
**[→ Day 105 Notes](Daily%20Notes/Day105.md)**

---

## Week 22: Functions with Data Structures (Days 106–110)

### Day 106: Functions with Lists — Passing Lists as Arguments
Lists are often passed to functions for processing. Learn how lists are passed (by reference), what that means, and how to write functions that work with list data.

**Topics:** Lists as parameters, passing by reference, list processing
**[→ Day 106 Notes](Daily%20Notes/Day106.md)**

### Day 107: Functions That Return Lists
Functions can build and return new lists. Learn techniques for accumulating data and returning it as a result.

**Topics:** Building lists in functions, returning collections, data transformation
**[→ Day 107 Notes](Daily%20Notes/Day107.md)**

### Day 108: Functions with Loops
Combine loops inside functions to process data repeatedly. Learn patterns for iterating through lists and accumulating results.

**Topics:** Loops in functions, iteration, processing sequences
**[→ Day 108 Notes](Daily%20Notes/Day108.md)**

### Day 109: Functions with Conditionals
Use `if`, `elif`, and `else` inside functions to make functions that make decisions based on their input.

**Topics:** Conditionals in functions, decision-making functions, control flow
**[→ Day 109 Notes](Daily%20Notes/Day109.md)**

### Day 110: Practice Lab
Write a set of data-processing functions that use lists, loops, and conditionals together to solve real problems (e.g., filtering data, calculating statistics, transforming lists).

**Topics:** Data processing, combining language features, practice
**[→ Day 110 Notes](Daily%20Notes/Day110.md)**

---

## Week 23: Modular Design (Days 111–115)

### Day 111: Top-Down Design
Learn **top-down design**: start with the big picture, then break it into smaller functions. This prevents "spaghetti code" and makes programs easier to understand and maintain.

**Topics:** Top-down design, problem decomposition, design patterns
**[→ Day 111 Notes](Daily%20Notes/Day111.md)**

### Day 112: The main() Function Pattern
A common pattern: write a `main()` function that orchestrates everything, and call `main()` at the bottom. This makes code clean and readable.

**Topics:** The main() pattern, program structure, entry points
**[→ Day 112 Notes](Daily%20Notes/Day112.md)**

### Day 113: Building a Complete Modular Program (Part 1)
Start building a moderately complex program (e.g., a quiz game, grade tracker, or text processor) using top-down design.

**Topics:** Modular design, planning, implementation
**[→ Day 113 Notes](Daily%20Notes/Day113.md)**

### Day 114: Building a Complete Modular Program (Part 2)
Continue building, refining, and testing your modular program.

**Topics:** Debugging, testing, refinement
**[→ Day 114 Notes](Daily%20Notes/Day114.md)**

### Day 115: Mini-Project Work Day
Choose a project of your own (or from a suggested list) and build a complete, modular program from start to finish.

**Topics:** Independent work, project management, creativity
**[→ Day 115 Notes](Daily%20Notes/Day115.md)**

---

## Week 24: Review & Assessment (Days 116–120)

### Day 116: Mini-Project Presentations and Peer Code Review
Present your mini-project to the class and review others' code. Learn to read and evaluate code written by your peers.

**Topics:** Communication, code review, feedback
**[→ Day 116 Notes](Daily%20Notes/Day116.md)**

### Day 117: Review — Function Syntax, Parameters, Return Values
Review the fundamentals: How do you define a function? How do you use parameters? How do return values work?

**Topics:** Function fundamentals, syntax, review
**[→ Day 117 Notes](Daily%20Notes/Day117.md)**

### Day 118: Review — Scope, Composition, Modular Design
Review advanced concepts: How does scope work? How do functions call each other? How do you design modular programs?

**Topics:** Scope, composition, design patterns, review
**[→ Day 118 Notes](Daily%20Notes/Day118.md)**

### Day 119: Unit 5 Assessment
A formal assessment covering all topics: function definitions, parameters, return values, scope, composition, and modular design.

**Topics:** Assessment, evaluation
**[→ Assessment](UnitAssessment.md)**

### Day 120: Assessment Review and Mid-Year Reflection
Review the assessment, discuss key takeaways, and reflect on your progress halfway through the course.

**Topics:** Reflection, metacognition, celebration
**[→ Day 120 Notes](Daily%20Notes/Day120.md)**

---

## Quick Reference Links

- **[Reference Guide](ReferenceGuide.md)** — Syntax, common patterns, troubleshooting
- **[Unit Practice](UnitPractice.md)** — 25 additional practice problems with answers
- **[Unit Assessment](UnitAssessment.md)** — 15 assessment questions with answers

---

## Key Learning Outcomes

By the end of Unit 5, you should be able to:

1. **Write functions** with proper syntax, including parameters and return values
2. **Understand scope** and correctly identify where variables are accessible
3. **Compose functions** that call other functions to solve larger problems
4. **Design modular programs** using top-down design and the main() pattern
5. **Write clear documentation** with docstrings and comments
6. **Work with lists and loops** inside functions for data processing
7. **Use functions with conditionals** to write decision-making functions
8. **Evaluate and review code** written by yourself and others

---

## Course Context

This unit is **Unit 5** of a year-long Coding I course (traditional schedule, 180 days).

- **Unit 4:** Variables and Data Types
- **Unit 5:** Functions and Modularity ← *You are here*
- **Unit 6:** Working with Files and Strings
- **Unit 7:** Dictionaries and Complex Data Structures
- **Unit 8:** Object-Oriented Programming (Intro)

Functions are fundamental to programming and provide the foundation for everything that follows. Master these concepts now, and the rest of the course will feel natural.

---

*Last updated: 2026-03-25*
