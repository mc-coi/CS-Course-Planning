# Unit 5 - Functions & Modularity: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days (compressed for STEM semester)
- **Core topics covered:** Function definition, parameters, return values, variable scope (local vs. global), default parameters, keyword arguments, multiple returns with tuples, modular program design
- **Prerequisites students need:** Mastery of Units 1-4 (variables, conditionals, loops); ability to think about abstraction and code reuse

---

## Week-by-Week Pacing

### Week 1 (Days 1–3): Function Basics

#### Day 1: Defining & Calling Functions
- **Essential days:** YES—foundational concept
- **Key learning:** def keyword, function definition, calling functions, no parameters yet, functions without returns
- **What to teach:** Why functions matter (reuse, organization); def/call distinction; running code in function body
- **If ahead of pace:** Introduce parameters and returns early; function documentation
- **If behind pace:** Very simple functions (print only); no complex logic inside functions yet

#### Day 2: Parameters & Arguments
- **Essential days:** YES—passing data to functions
- **Key learning:** Parameters in function definition, arguments in function calls, matching number of arguments, parameter ordering
- **What to teach:** Parameters as placeholders; arguments as actual values; how data flows in; multiple parameters
- **If ahead of pace:** Named arguments/keyword arguments; default parameters; *args
- **If behind pace:** Single parameter examples; visual diagrams of argument passing; repeat with 2-3 examples

#### Day 3: Return Values
- **Essential days:** YES—getting results from functions
- **Key learning:** return keyword, returning values, using returned values in expressions, None return
- **What to teach:** return vs. print distinction; functions that compute vs. output; storing return values
- **If ahead of pace:** Multiple returns; returning different types; early return patterns
- **If behind pace:** Simple return examples; print result to verify; skip multiple returns

---

### Week 2 (Days 4–6): Scope & Advanced Concepts

#### Day 4: Variable Scope (Local vs. Global)
- **Essential days:** YES—avoiding mysterious bugs and variable conflicts
- **Key learning:** Local variables exist only in function, global variables accessible everywhere, shadowing, scope rules
- **What to teach:** Why scope matters; local-first principle; when global is necessary (rarely); namespace concepts
- **If ahead of pace:** Explore global keyword; scope gotchas; closures introduction
- **If behind pace:** Emphasize local variables; skip global entirely; use simple naming patterns

#### Day 5: Default Parameters & Keyword Arguments
- **Essential days:** FLEXIBLE—useful but not critical
- **Key learning:** Default values in function definition, optional parameters, keyword arguments, improving function flexibility
- **What to teach:** When defaults make sense; how they're used; keyword arguments for clarity
- **If ahead of pace:** Complex default patterns; *args and **kwargs preview
- **If behind pace:** Skip this entirely; stick to required parameters

#### Day 6: Putting It Together - Modular Program Design
- **Essential days:** YES—applying functions to real programs
- **Key learning:** Breaking problems into functions, each function does one thing, composing functions, top-down design
- **What to teach:** How to identify what should be a function; naming functions clearly; designing before coding
- **If ahead of pace:** Complex multi-function programs; organizing functions logically
- **If behind pace:** Provide function outlines; template structures

---

### Week 3 (Days 7–9): Lists & Functions Project

#### Day 7: Functions with Lists
- **Essential days:** YES—essential for STEM data processing
- **Key learning:** Passing lists to functions, modifying lists in functions, returning lists, processing collections
- **What to teach:** Lists as mutable; modifying lists inside functions affects original; list processing patterns
- **If ahead of pace:** List comprehensions with functions; higher-order functions
- **If behind pace:** Simple list iteration in functions; avoid side effects initially

#### Day 8: Review & Refactoring
- **Essential days:** YES—strengthening understanding through application
- **Key learning:** Reviewing concepts, recognizing when to use functions, refactoring existing code
- **What to teach:** Code review process; improving organization; making code more modular
- **If ahead of pace:** Complex refactoring; optimization
- **If behind pace:** Provide functions to refactor; guided practice

#### Day 9: Unit 5 Project
- **Essential days:** FLEXIBLE (but strongly recommended)—integrates all unit concepts
- **Key learning:** Complete program using multiple functions, parameters, returns, and modular design
- **What to teach:** Planning function structure; implementing and testing functions; integration
- **If ahead of pace:** Complex project with nested function calls; optimization
- **If behind pace:** Provide structure; simpler function requirements

---

## Differentiation Strategies

### For Struggling Students

**Scaffolding tips for this unit:**
- Use visual diagrams showing how arguments pass to parameters
- Provide function templates with def/return structure pre-filled
- Start with functions that only print (no returns)
- Use consistent parameter naming conventions
- Trace function execution step by step on paper first
- Focus on one function at a time

**Which practice problems to assign first (easiest wins):**
- Simple print-only functions before functions with returns
- Single parameter before multiple parameters
- Functions returning simple values before complex logic
- Built-in functions (len, sum, max) for reference models
- Avoid scope/global concepts initially

**Suggested pacing adjustments:**
- Spread Unit 5 to 10-11 days instead of 9
- Dedicate full day to parameters only
- Dedicate full day to return values only
- Skip default parameters entirely
- Skip scope/global concepts
- Use simpler projects with 3-4 simple functions

**What prerequisite gaps to look for:**
- Cannot identify what should go in function vs. outside
- Confusion about parameter vs. variable
- Return vs. print still unclear
- Scope issues from not mastering variable shadowing
- Difficulty with indentation (from earlier units)

---

### For On-Track Students

**Standard path through the unit:**
- Follow 9-day schedule as written
- Assign Beginner + Intermediate problems daily
- Build programs with 5-7 functions
- Complete project on Day 9 with standard requirements

**Which practice problems to assign:**
- Days 1-3: Beginner + Intermediate parameter/return problems
- Days 4-6: Intermediate + one Challenge per day
- Days 7-8: Mixed Intermediate and Challenge
- Day 9: Full multi-function project

---

### For Advanced Students

**Extension activities specific to this unit's topics:**
- Recursive functions (factorial, Fibonacci)
- Higher-order functions (functions taking functions as parameters)
- Lambda functions and map/filter/reduce
- Decorators introduction (preview)
- Design patterns in function organization

**Challenge problems to assign:**
- Build functions with sophisticated logic (sorting, searching)
- Recursive problem solving
- List comprehensions with functions
- Higher-order function usage
- Refactoring complex code into modular functions
- Multi-function game or simulation

**Ways to deepen understanding beyond the curriculum:**
- Ask: "What would go wrong if this function modified global variables?"
- Challenge: "Write this algorithm as one big function vs. modular functions" (compare)
- Explore: How standard library functions are organized (modules/packages intro)
- Build: Function library for common operations (stats, text processing)
- Investigate: Stack trace following when functions call functions

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Day 1:** Before parameters (functions work without them)
- **End of Day 3:** Before scope (functions with returns working)
- **End of Day 6:** Before lists with functions (basic functions solid)

### Topics students most commonly struggle with:
- **Parameters vs. arguments:** Confusing which is definition vs. call
- **Return vs. print:** Returning None by accident instead of printing
- **Local variables in functions:** Thinking they persist outside function
- **Modifying lists in functions:** Unexpected behavior with mutable objects
- **Function naming:** Unclear names making purpose ambiguous
- **When to use functions:** Creating functions for single-use code
- **Scope with global:** Using global when not needed; confusing namespace

### Topics students typically move through quickly:
- **Basic function definition:** Creating and calling simple functions
- **Single parameter:** Passing one value in
- **Simple return:** Returning a computed value
- **Naming functions clearly:** Obvious from context
- **Testing functions:** Quick to verify with print

---

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**After Day 1:**
- Can students define and call a simple function?
- Checkpoint: "Create function called greet() that prints 'Hello!', call it 3 times"

**After Day 2:**
- Can they use parameters correctly?
- Checkpoint: "Create function that takes name parameter, prints 'Hello [name]!'"

**After Day 3:**
- Can they return values and use them?
- Checkpoint: "Function that takes two numbers, returns their sum, use result in print"

**After Day 4:**
- Do they understand local variables?
- Checkpoint: "What happens to variable created inside a function after function ends?"

**After Day 6:**
- Can they design a program with multiple functions?
- Checkpoint: "List 3 functions that would help solve [scenario]"

**After Day 7:**
- Can they process lists with functions?
- Checkpoint: "Write function that takes list of numbers, returns their average"

---

## STEM-Specific Pacing Notes

Unit 5 is a **critical organizational unit** for STEM. Modular design enables scientific programs to be understandable and extensible. Unit 5 is compressed from 10-11 days in full-year courses to 9 days for STEM semester.

**Key implications:**
- Functions are non-negotiable for STEM programs
- Modularity enables code reuse across experiments/simulations
- Must understand parameter passing and returns before Unit 6
- List processing with functions appears in many STEM contexts
- Scope issues can cause mysterious bugs in long STEM programs

**Recommended daily structure (if 50-min class periods):**
- 5 min: Hook with code organization problem (why functions matter)
- 10 min: Concept with multiple examples showing parameter flow
- 20 min: Guided practice (define and call functions together, trace execution)
- 10 min: Assign practice problems; write one together
- 5 min: Checkpoint: Can they explain parameter passing?

**Critical mastery targets:**
By end of Unit 5, students MUST be able to:
1. Define functions with parameters and return values
2. Call functions with correct arguments
3. Understand and use local variables
4. Design programs as collections of functions
5. Pass lists to functions and process them
6. Trace function execution with parameters and returns
7. Write functions that take a list and return a computed value

---

## Assessment & Mastery Validation

Quick verification questions:

1. **Day 1:** Can students explain why functions are useful?
2. **Day 2:** Do they understand parameter vs. argument distinction?
3. **Day 3:** Can they write function that returns computed value?
4. **Day 4:** Do they understand where variables exist/don't exist?
5. **Day 6:** Can they design function structure for a problem?
6. **Day 7:** Can they write function to process a list (sum, average, etc.)?
7. **Project:** Complete working program with 5+ functions, each with clear purpose

