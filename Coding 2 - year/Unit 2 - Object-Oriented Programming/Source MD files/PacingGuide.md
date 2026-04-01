# Unit 2 - Object-Oriented Programming: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 30 days (~6 weeks)
- **Core topics covered:**
  - Classes and objects: design, instantiation, attributes, methods
  - Special methods (__init__, __str__, __repr__, __eq__, __lt__, __add__, etc.)
  - Inheritance: single and multi-level, super(), method overriding
  - Encapsulation: public/private attributes, properties, getters/setters
  - Polymorphism: method overriding, duck typing, design patterns
  - Class variables vs instance variables
  - Class methods (@classmethod) and static methods (@staticmethod)
  - Abstract classes and interfaces (ABC module)
  - Composition and aggregation
  - Design patterns: Singleton, Factory, Builder
- **Prerequisites students need:**
  - All Unit 1 data structures (lists, dicts, sets)
  - Functions (parameters, return values, scope)
  - Loops and conditionals
  - Understanding of when to use different data structures

---

## Week-by-Week Pacing

### Week 1 (Days 1–5): Object-Oriented Fundamentals

#### Day 1: Classes, Objects & Instance Variables
- **Essential days** (must teach): YES
  - Foundation for everything in this unit
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Multiple attributes, constructor validation, defensive copying
- **If behind pace**: Use one or two simple attributes; focus on the concept of objects as bundles of data

#### Day 2: Methods & The __init__ Constructor
- **Essential days** (must teach): YES
  - Must understand how methods work and how __init__ initializes objects
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Method chaining, fluent interfaces, builder patterns
- **If behind pace**: Use simple methods with one or two parameters; emphasize self

#### Day 3: __str__ & __repr__ Special Methods
- **Essential days** (must teach): YES
  - String representation is essential for debugging and display
- **Flexible days** (can compress or cut if pressed for time): __repr__ can be deferred; focus on __str__
- **If ahead of pace**: __repr__ for debugging, __format__ for custom formatting
- **If behind pace**: Focus only on __str__; keep format strings simple

#### Day 4: Properties & Encapsulation
- **Essential days** (must teach): YES
  - Encapsulation (hiding internal state) is a core OOP principle
- **Flexible days** (can compress or cut if pressed for time): Can simplify to getters/setters without @property initially
- **If ahead of pace**: Computed properties, property validation with complex logic
- **If behind pace**: Start with simple getters/setters; introduce @property syntax later

#### Day 5: Class Variables & Instance Variables
- **Essential days** (must teach): YES
  - Understanding the difference is critical for design
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Class method examples, class state across instances
- **If behind pace**: Use clear visual examples (e.g., all circles have math.pi; each circle has its own radius)

### Week 2 (Days 6–11): Inheritance & Relationships

#### Day 6: Introduction to Inheritance
- **Essential days** (must teach): YES
  - Inheritance is a core OOP concept
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Multi-level inheritance, method overriding patterns
- **If behind pace**: Simple parent-child relationships; use animal examples (Dog is-a Animal)

#### Day 7: Method Overriding & Polymorphism
- **Essential days** (must teach): YES
  - Understanding that children can override parent methods is essential
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Method resolution order (MRO), multiple inheritance considerations
- **If behind pace**: Use simple overrides; avoid complex scenarios

#### Day 8: super() & Calling Parent Methods
- **Essential days** (must teach): YES
  - super() is essential for proper inheritance design
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: super() with multiple inheritance, coordinating parent constructors
- **If behind pace**: Focus on super().__init__() pattern; keep examples simple

#### Day 9: @classmethod and @staticmethod
- **Essential days** (must teach): PARTIAL
  - Static methods are useful; class methods are less common at this level
- **Flexible days** (can compress or cut if pressed for time): YES — static methods can be optional
- **If ahead of pace**: Class methods for alternative constructors, factory patterns
- **If behind pace**: Focus on @staticmethod as "utility functions in a class"; class methods optional

#### Day 10: Special Methods for Comparison & Operators
- **Essential days** (must teach): YES
  - Students need to understand __eq__, __lt__, __add__, etc.
- **Flexible days** (can compress or cut if pressed for time): Can focus on __eq__ and __lt__ only
- **If ahead of pace**: Implement all comparison methods, operator overloading for custom types
- **If behind pace**: Focus on __eq__ (__str__ and __init__ review first)

#### Day 11: Composition & Aggregation
- **Essential days** (must teach): YES
  - Understanding "has-a" vs "is-a" relationships is essential design skill
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Complex composition patterns, dependency injection
- **If behind pace**: Simple composition examples (Library has Books, Team has Players)

### Week 3 (Days 12–17): Advanced OOP & Design

#### Day 12: Iterator Protocol (__iter__ & __next__)
- **Essential days** (must teach): YES
  - Custom iterators are powerful; students should see how iteration works under the hood
- **Flexible days** (can compress or cut if pressed for time): Can defer to optional topic
- **If ahead of pace**: Generator functions with yield, custom iterables
- **If behind pace**: Show the pattern without deep understanding of StopIteration

#### Day 13: Magic Methods (__len__, __getitem__, __setitem__)
- **Essential days** (must teach): PARTIAL
  - __len__ is common; __getitem__ and __setitem__ are less critical
- **Flexible days** (can compress or cut if pressed for time): YES — can be simplified or optional
- **If ahead of pace**: Implement full sequence protocol, slicing support
- **If behind pace**: Focus on __len__ and __str__; others are optional

#### Day 14: Abstract Classes & Interfaces
- **Essential days** (must teach): YES
  - Abstract base classes enforce contracts; important for design
- **Flexible days** (can compress or cut if pressed for time): Can simplify to "class without @abstractmethod" pattern
- **If ahead of pace**: Multiple abstract methods, abstract properties, interface design
- **If behind pace**: Keep abstract classes simple; use 1-2 abstract methods max

#### Day 15: Design Patterns — Singleton & Factory
- **Essential days** (must teach): PARTIAL
  - Design patterns are important but not essential for all students
- **Flexible days** (can compress or cut if pressed for time): YES — can be moved to advanced topics
- **If ahead of pace**: Builder pattern, Strategy pattern, Observer pattern
- **If behind pace**: Skip patterns; focus on core OOP concepts

#### Day 16–17: Mini-Project Lab (Library Management System)
- **Essential days** (must teach): YES
  - Application of all OOP concepts is essential before assessment
- **Flexible days** (can compress or cut if pressed for time): Can be condensed to 1 day if behind
- **If ahead of pace**: Students extend with additional features (search, sorting, reporting)
- **If behind pace**: Provide partial template code; focus on putting concepts together

### Week 4 (Days 18–23): Integration & Review

#### Day 18: Code Review & Debugging Workshop
- **Essential days** (must teach): YES
  - Students learn common OOP mistakes and debugging strategies
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 19
- **If ahead of pace**: Peer code review, design critique, refactoring exercises
- **If behind pace**: Teacher-led code review with live examples

#### Day 19: Inheritance Hierarchy Workshop
- **Essential days** (must teach): YES
  - Deep practice with inheritance before assessment
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 18
- **If ahead of pace**: Multi-level hierarchies, complex inheritance scenarios
- **If behind pace**: Simple parent-child relationships; visual inheritance trees

#### Day 20: Special Methods & Polymorphism Review
- **Essential days** (must teach): YES
  - Review of complex topics before assessment
- **Flexible days** (can compress or cut if pressed for time): Can combine with Days 18–19
- **If ahead of pace**: Students create test cases showing polymorphism in action
- **If behind pace**: Provide review worksheets; focus on __str__, __init__, method overriding

#### Day 21: Design Patterns & Architecture Review
- **Essential days** (must teach): PARTIAL
  - Good practice but not required for basic mastery
- **Flexible days** (can compress or cut if pressed for time): YES — can be optional
- **If ahead of pace**: Deep dive into patterns, refactoring for design
- **If behind pace**: Quick review of when to use inheritance vs composition

#### Day 22: Unit Review & Assessment Prep
- **Essential days** (must teach): YES
  - Essential consolidation before assessment
- **Flexible days** (can compress or cut if pressed for time): Can compress with study guides
- **If ahead of pace**: Students teach concepts to peers; create practice problems
- **If behind pace**: Provide comprehensive study guide; focus on core concepts only

#### Day 23: Unit Assessment
- **Essential days** (must teach): YES
  - Assessment is required
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early completers start Unit 3 or get enrichment
- **If behind pace**: Extended time if needed; focused feedback for reteaching

#### Day 24–30: Reteaching, Projects, or Unit 3 Start
- Based on assessment results, use remaining days for targeted reteaching or moving forward

---

## Differentiation Strategies

### For Struggling Students

**Common gaps from Unit 1:**
- Weak understanding of methods and syntax
- Confusion about how objects store data
- Difficulty with nested structures (which appear in composition)

**Specific scaffolding for this unit:**
- Use **concrete examples repeatedly:** Pet class, Student class, BankAccount
- Provide **class templates** with blanks to fill in
- Use **visual object diagrams** showing state and methods
- Create a **"Class Design Cheat Sheet"** with __init__, method, and __str__ templates
- Emphasize the **rule:** "Every method needs self as its first parameter"

**Which practice problems to assign first:**
- Problem 1 (Circle class) — simple attributes and methods
- Problem 2 (Student class) — introduces class variables
- Problem 3 (Rectangle with properties)
- Problem 4 (Simple inheritance — Animal/Dog)
- Then move to inheritance patterns (Problems 5–7)

**Suggested pacing adjustments:**
- Spend 2 days on Days 1–3 (class fundamentals) instead of 1 day each
- Skip abstract classes (@abstractmethod), design patterns, magic methods beyond __str__ and __init__
- Provide full templates for inheritance examples
- Reduce inheritance depth (just 1 level: parent → child)
- Skip static/class methods (@staticmethod, @classmethod)

**Prerequisite gaps to watch for:**
- If students are weak on method syntax from Unit 1, do extra practice with object.method(args)
- If students struggle with data structures, review dictionaries and lists before Day 11
- If students can't understand "self," use lots of concrete examples and diagrams

**Reteaching strategies:**
- Use consistent, repeating examples (e.g., Student class throughout)
- Physical objects help: "This student object has a name attribute and a grade() method"
- Pair students with stronger partners for Days 16–17 project
- Have students trace through code line-by-line to understand object creation

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Complete beginner and intermediate practice problems (1–15)
- Do the Library Management System mini-project
- Pass the unit assessment

**Which practice problems to assign:**
- Problems 1–15 (Beginner through Intermediate)
- Assign as homework or in-class work
- Focus on understanding, not just correctness
- Encourage students to test their code

**Pacing tips:**
- Days 1–11 cover essential OOP; pace should be solid
- Days 12–15 get more abstract; monitor for confusion
- Days 16–17 are consolidation; should feel manageable with practice

### For Advanced Students

**Extension activities:**
- **Problem 3 (Rectangle):** Add diagonal, rotation, transformation operations
- **Problem 4 (Inheritance):** Build a full animal hierarchy with Mammal, Reptile, Bird subclasses
- **Problem 10 (Polymorphism):** Add more vehicle types, create a traffic simulation
- **Problem 14 (Abstract classes):** Design a complete animal behavior system with multiple abstract methods
- **Problem 17 (Singleton):** Implement database connection pool with multiple connections
- **Problem 18 (Factory):** Extend to support configuration files, JSON-based factory
- **Problem 20 (Complete system):** Add GUI, advanced search, analytics

**Challenge problems to assign:**
- All Challenge level problems (16–20)
- Extend with additional features (notifications, advanced reporting, integration with external systems)

**Ways to deepen understanding:**
- Implement design patterns not covered (Strategy, Observer, Adapter, Decorator)
- Refactor non-OOP code into OOP design
- Explore Python's MRO (Method Resolution Order) with multiple inheritance
- Implement metaclasses for advanced object creation
- Study real-world frameworks (Django models, Flask views) to see OOP in practice
- Have them design their own abstract class hierarchy for a domain they're interested in

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 5:** Good checkpoint for class fundamentals before inheritance
- **After Day 11:** Good checkpoint for basic OOP before advanced topics
- **After Day 17:** Final practice point before assessment

### Topics students typically struggle with:
1. **The "self" parameter** (Days 1–2): Most confusing concept
   - *Fix:* Repetition, visual examples, "self refers to this specific object"
2. **Method overriding** (Day 7): Students sometimes call parent method accidentally
   - *Fix:* Trace through method calls, show call order
3. **Inheritance hierarchies** (Days 6–8): When to use inheritance vs composition
   - *Fix:* Decision tree, lots of examples, emphasize "is-a" vs "has-a"
4. **Special methods** (Days 10, 12–13): Syntax is unusual
   - *Fix:* Provide templates, show when they're called
5. **Abstract classes** (Day 14): Abstract concept of enforcing structure
   - *Fix:* Show what happens when you try to instantiate without implementing abstract methods

### Topics students typically move through quickly:
1. **Basic class creation** (Day 1): Most understand object bundles quickly
2. **Method creation** (Day 2): Once they understand self, adding methods is straightforward
3. **__str__ implementation** (Day 3): Simple pattern to follow
4. **Inheritance basics** (Day 6): Many intuitively understand parent-child
5. **Method overriding** (Day 7): Once they see an example, they can do it

### Coding 1 gaps that surface here:
- **Functions:** If students don't understand function definition/calling, they'll struggle with methods
  - *Monitor:* Days 1–2
  - *Fix:* Quick review of function syntax; emphasize methods are functions with self
- **Data structures:** If students don't know lists/dicts well, composition (Day 11) will be hard
  - *Monitor:* Day 11
  - *Fix:* Review how to use lists in attributes (self.items = [])

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 5:** Can students create a class, write __init__, and use instance variables?
   - Quick task: "Write a Temperature class with celsius attribute and fahrenheit method"
2. **After Day 11:** Can students understand inheritance and composition?
   - Quick task: "Design a Creature class and Animal class; decide which is parent"
3. **After Day 15:** Can students apply special methods and design patterns?
   - Code review: "Does this special method implementation make sense?"

### Summative checks (end-of-unit):
1. **Day 23 Assessment:**
   - Part A: Multiple choice (OOP concepts, syntax)
   - Part B: Short answer (inheritance, polymorphism, design)
   - Part C: Coding (design classes, use inheritance, implement special methods)

### Code review checkpoints (Days 16–20):
- Day 16–17: Mini-project code review for:
  - Correct class design
  - Proper use of inheritance or composition
  - Working implementation
- Day 18: Live debugging workshop highlights common OOP mistakes

---

## Notes on Unit 1 Prerequisites

This unit builds heavily on Unit 1. Watch for these gaps:

- **Data structures:** If students don't understand lists/dicts, they'll struggle with storing objects
- **Methods:** If students don't know method syntax, they'll struggle with class methods
- **Variable scope:** If students don't understand variable scope, self will confuse them
- **Conditionals & loops:** If students are weak here, they'll struggle with complex methods

If you notice gaps, do a brief review of the Unit 1 concept. Use small group review during Days 16–20 if needed.

---

## Time Management Tips

- **If 5 days ahead:** Use time for design patterns, multiple inheritance, metaclasses, or early Unit 3 start
- **If 3 days behind:** Combine Days 16–17 into 1 project day; skip design patterns; provide templates
- **If 1 week behind:** Focus only on Days 1–11 (classes and basic inheritance); skip advanced topics
- **If 2 weeks behind:** Teach only class basics (Days 1–5) and simple inheritance (Days 6–8); skip everything else

---

## Key Assessment Targets

By the end of Unit 2, all students should demonstrate:
1. Creating a class with __init__, instance variables, and methods
2. Writing __str__ for readable output
3. Using properties or getters/setters for encapsulation
4. Implementing single-level inheritance and method overriding
5. Using super() to call parent constructors
6. Understanding the difference between class and instance variables
7. Choosing between inheritance and composition appropriately
8. Applying OOP design to solve a complete problem

Students working at advanced level should additionally demonstrate:
- Multi-level inheritance hierarchies
- Special methods (__eq__, __lt__, __add__, __getitem__, __len__)
- Abstract base classes with enforced contracts
- Design patterns (Singleton, Factory)
- Iterator protocol implementation
- Complex polymorphic systems
