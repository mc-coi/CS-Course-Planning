# Unit 5 - Functions and Modularity: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 25 days / 5 weeks (Days 96–120, 55-minute periods)
- **Core topics covered:** Function definition and calling (def keyword), parameters and arguments, return values, multiple parameters and default parameters, variable scope (local vs. global), the global keyword (and why to avoid it), function composition, docstrings and documentation, functions with lists/loops/conditionals, top-down design, the main() function pattern, modular program design, building complete modular programs
- **Prerequisites students need:** Mastery of Units 1–4 (all language features); ability to write multi-feature programs; understanding of problem decomposition

---

## Week-by-Week Pacing

### Week 20 (Days 96–100): Function Basics
**Topics:** def keyword, function definition, calling functions, parameters and arguments, return values, basic function design

#### Essential days (cannot skip):
- **Day 96:** Function definition and calling — foundational concept
- **Day 97:** Parameters and arguments — enables function flexibility
- **Day 98:** Return values — transforms functions from "do something" to "do something and give me a result"
- **Day 100:** Practice lab with function library — synthesis of Days 96–98

#### Flexible days (can compress or cut if pressed for time):
- **Day 99 (Multiple Parameters & Defaults):** Can be folded into Day 97 or abbreviated; students often learn through practice problems

#### If ahead of pace:
- Introduce *args and **kwargs (variable arguments)
- Have them write functions that return multiple values as tuples
- Challenge: write a function that accepts variable number of arguments (using *args)

#### If behind pace:
- Spend 2 days on function definition and calling (Days 96–97)
- Defer return values; focus on functions that perform actions first
- Provide templates for function definitions (fill-in-the-blank)
- **Minimum viable coverage:** Days 96–98 (definition, parameters, return values)

---

### Week 21 (Days 101–105): Scope & Organization
**Topics:** Variable scope (local vs. global), avoiding global variables, function composition, docstrings and documentation, organizing code

#### Essential days (cannot skip):
- **Day 101:** Variable scope (local vs. global) — critical for debugging and good design
- **Day 102:** Why to avoid global keyword — good design practices
- **Day 103:** Function composition — breaking down problems into smaller functions
- **Day 104:** Docstrings — documentation for functions
- **Day 105:** Practice lab — well-documented function library

#### Flexible days (can compress or cut if pressed for time):
- None. Scope and organization are essential for writing maintainable code.

#### If ahead of pace:
- Introduce scope exercises: what variables are accessible where?
- Have them refactor code to eliminate global variables
- Challenge: write a complete program using only local variables and proper function composition

#### If behind pace:
- Spend 2 days on scope (Days 101–102) before moving to composition
- Simplify docstring requirements initially (just one-line descriptions)
- Provide examples of scope and composition extensively
- **Minimum viable coverage:** Days 101–103 (scope, avoiding global, composition)

---

### Week 22 (Days 106–110): Functions with Data Structures
**Topics:** Functions with lists as parameters, functions that return lists, loops inside functions, conditionals inside functions, combining language features in functions

#### Essential days (cannot skip):
- **Day 106:** Functions with lists (passing lists as arguments) — lists are passed by reference
- **Day 107:** Functions that return lists — building data structures
- **Day 108:** Loops in functions — combining iteration with modular code
- **Day 109:** Conditionals in functions — decision-making in modular code
- **Day 110:** Practice lab combining all four days

#### Flexible days (can compress or cut if pressed for time):
- None. These days are essential for practical function use.

#### If ahead of pace:
- Have them write functions that sort, filter, or transform lists
- Introduce list comprehensions in functions: `return [x*2 for x in data]`
- Challenge: write a function that processes complex nested data structures

#### If behind pace:
- Spend extra time on Day 106 (passing lists); this concept is critical
- Provide step-by-step templates for loop/conditional functions
- Combine Days 108–109 into one day if needed
- **Minimum viable coverage:** Days 106–108 (lists, returning lists, loops in functions)

---

### Week 23 (Days 111–115): Modular Design
**Topics:** Top-down design (start big, break into smaller functions), the main() function pattern, building complete modular programs, planning with pseudocode and function signatures, debugging in modular code

#### Essential days (cannot skip):
- **Day 111:** Top-down design — essential software engineering practice
- **Day 112:** The main() function pattern — industry standard code organization
- **Day 113-114:** Building a complete modular program (multi-part project) — application of all unit concepts
- **Day 115:** Mini-project work day — student choice project

#### Flexible days (can compress or cut if pressed for time):
- None. These are hands-on application days.

#### If ahead of pace:
- Have them build more complex programs (multiple features, user menus)
- Introduce refactoring: improving code structure without changing functionality
- Challenge: write a program with 10+ helper functions organized around a main() function

#### If behind pace:
- Provide a top-down design template (start with pseudocode for main())
- Provide partial code for Days 113–114; students complete/extend
- Allow pair programming or peer support
- **Minimum viable coverage:** Days 112–114 (main pattern, modular program)

---

### Week 24 (Days 116–120): Review & Assessment
**Topics:** Function design review, scope review, modular design review, code tracing, common mistakes, unit assessment, reflection

#### Essential days (cannot skip):
- **Day 116:** Function design review — write functions effectively
- **Day 119:** Unit 5 Assessment — formal evaluation
- **Day 120:** Assessment review and reflection

#### Flexible days (can compress or cut if pressed for time):
- **Days 117-118:** Review practice — can be condensed or extended based on performance

#### If ahead of pace:
- Have students refactor previous projects to use functions
- Challenge them to debug modular code and identify scope issues
- Have them create a "function design guide" for peers

#### If behind pace:
- Spend extra time on Days 116–118 for review and re-teaching
- Offer a retake option
- **Minimum viable coverage:** Days 116 (review), 119 (assessment)

---

## Differentiation Strategies

### For Struggling Students
**Specific scaffolding tips:**
- **Function definition:** Use a template consistently: `def function_name(parameter): [body] return result`. Fill in the blanks first.
- **Parameters vs arguments:** Explain the distinction clearly: parameters are in the definition; arguments are in the call. Use consistent language.
- **Return values:** Show the distinction between functions that return values (`x = func()`) vs. functions that print (`func()` without assignment).
- **Scope:** Use variable visualization (memory model). Show which variables exist in which scopes with clear boxes/arrows.
- **Top-down design:** Start with simple functions (single task). Show how to build larger programs by calling multiple functions.

**Which practice problems to assign first (easiest wins):**
- Simple functions with no parameters: `def greet(): print("Hello")`
- Functions with one parameter: `def add_five(x): return x + 5`
- Functions with one loop or conditional
- Build to complex functions (multiple parameters, multiple statements) gradually

**Suggested pacing adjustments:**
- Spend 2 days on function basics (Days 96–97)
- Provide function templates for practice problems
- Have them write functions with just one task first
- Delay functions with data structures (lists) until confident with basic functions

**What prerequisite gaps to look for:**
- **Indentation:** If indentation is still shaky, function indentation will be harder. Reinforce explicit spacing.
- **Return vs print:** Do they understand the difference? Show examples where return enables composition.
- **Variable names:** Are they using meaningful names? Emphasize: parameter names should be clear (`calculate_tax(amount, rate)` not `calc(a, b)`)

### For On-Track Students
**Standard path through the unit:**
- Follow the week-by-week breakdown as written
- Complete practice problems from all five weeks
- Focus on building two complete modular programs (one from curriculum, one choice)

**Which practice problems to assign:**
- Week 20: Functions with 0–2 parameters, simple return values
- Week 21: Scope analysis, refactoring to eliminate globals, basic documentation
- Week 22: Functions with lists, loops, conditionals
- Week 23: Modular design, top-down thinking
- All 5 weekly labs (Days 100, 105, 110, 115)

**Expectations:**
- Functions should have single, clear responsibility
- Parameters and return values should be used properly
- Docstrings should explain function purpose, parameters, and return value
- Code should follow the main() pattern for large programs
- Variable names should be meaningful throughout

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Advanced function features:** Introduce *args, **kwargs, lambda functions, decorators (preview)
- **Design patterns:** Have them implement common patterns (factory functions, callback functions)
- **Refactoring:** Take a procedural program and refactor it into a modular design with many functions
- **Testing:** Introduce unit testing for functions (write test cases before code — TDD preview)

**Challenge problems to assign:**
- Write a complete program with 15+ functions organized into modules
- Refactor a previous project into a modular design
- Write a recursive function (factorial, Fibonacci)
- Build a program with a menu system that calls different functions based on user choice
- Create a data analyzer with functions for filtering, sorting, calculating statistics

**Ways to deepen understanding beyond the curriculum:**
- Explore first-class functions: functions as arguments, returning functions from functions
- Introduce lambda expressions and when to use them
- Study design patterns in Python (factory, observer, etc.)
- Write programs that use list comprehensions with functions for elegant data processing
- Build a "function library" that could be reused across multiple projects

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **End of Week 20:** Before moving to scope, ensure parameters, arguments, and return values are solid
- **End of Week 21:** Before moving to data structures, ensure scope and composition are mastered
- **After Day 110:** Before modular design projects, ensure all language features work correctly in functions

### Topics students most commonly struggle with (and expected time):
1. **Parameters vs arguments:** 1 extra day. The terminology is confusing; use consistent language and examples.
2. **Return values vs print:** 1 extra day. Students write functions that print instead of return. Show the difference with composition examples.
3. **Scope and variable visibility:** 1-2 extra days. "Why can't this function see that variable?" Visual memory model helps.
4. **Pass by reference (lists):** 1 extra day. Students don't realize modifying a list parameter modifies the original. Show with before/after examples.
5. **Function naming:** 1 day. Function names should be verbs describing the action (`calculate_tax`, not `tax`).

### Topics students typically move through quickly:
- **Function definition syntax:** Once they see def keyword, syntax is straightforward
- **Simple return values:** Returning a single value is intuitive
- **Function calling:** Students quickly grasp `result = my_function(x)`
- **The main() pattern:** Once shown an example, students understand the benefits
- **Docstrings:** Simple docstrings (one-liner) are easy to adopt

---

## Suggested Checkpoints

Use these quick formative checks mid-unit:

### After Day 100 (end of Week 20):
- **Quick Check:** "Write a function that takes a number and returns it doubled"
- **Code Check:** Write a function that asks the user for their name and prints a greeting

### After Day 105 (end of Week 21):
- **Quick Check:** "Is this variable local or global?" (Show function with variable defined inside)
- **Code Check:** Write a function with a docstring explaining its purpose, parameters, and return value

### After Day 110 (end of Week 22):
- **Quick Check:** "Write a function that takes a list and returns the sum of its elements"
- **Code Check:** Write a function that loops through a list and counts items meeting a condition

### Before Day 115 (mid-Week 23):
- **Code Check:** Students' modular programs in progress. Scan: Do functions work independently? Is there a clear main() function?

---

## Common Misconceptions to Watch For

1. **"Parameters and arguments are the same"** — Parameters are names in the definition; arguments are values in the call.
2. **"Functions that don't return are useless"** — Functions that perform actions (print, modify lists) are valuable even without return.
3. **"You must return from every function"** — Functions don't need return statements; some just perform actions.
4. **"Global variables are convenient"** — Avoid globals; pass parameters instead for cleaner code.
5. **"Lists are copied when passed to functions"** — Lists are passed by reference; modifying them inside a function modifies the original.
6. **"You must name parameters to match argument values"** — Parameter names are internal to the function; argument order matters, not names.
7. **"Functions must have a return type specified"** — Python doesn't require type annotations (though they help). Functions can return any type.
8. **"main() is automatically called"** — You must explicitly call main() at the bottom: `if __name__ == "__main__": main()`.

---

## Notes on Unit 5 Assessment

- **Assessment (Day 119):** Should include function design questions (write a function signature for a given task), scope questions (identify scope of variables), code tracing (what does this function return?), and a coding task (write several functions and a main program that uses them)
- **Common assessment mistakes:** Forgetting to return values, not using parameters, scope confusion, poor function design (too many responsibilities)
- **Retakes:** Offer retakes focused on weakest areas (function design, scope, modular thinking)

---

## Performance Benchmarks

By the end of Unit 5, students should be able to:
- Write functions with appropriate parameters and return values
- Understand scope and avoid global variables
- Use function composition to break down complex problems
- Document functions with docstrings
- Combine loops, conditionals, and lists within functions
- Design and implement complete modular programs with a main() function
- Trace function calls and predict results

