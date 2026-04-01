# Unit 2 - Object-Oriented Programming: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 9 days / 3 weeks
- **Core topics covered:** Classes and objects, `__init__` constructor, attributes and methods, encapsulation with private attributes and properties, inheritance and `super()`, method overriding and polymorphism, special methods (`__str__`, `__repr__`, `__len__`, `__eq__`), design patterns and complete OOP programs
- **Prerequisites students need:** Strong understanding of functions from Coding 1; able to read and write function definitions; familiarity with dictionaries (Unit 1)

## Week-by-Week Pacing

### Week 1 (Days 1–3): OOP Fundamentals & Classes
- **Essential days** (must teach):
  - Day 1: Introduction to OOP—class definition, `__init__`, attributes, methods, creating objects
  - Day 2: Constructors and initialization—the `__init__` method, `self` parameter, instance variables
  - Day 3: Class vs. instance variables, method calls, accessing attributes

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip instance vs. class variables distinction; focus on `self.` attributes only
  - Cut complex `__init__` examples; keep to simple attribute assignment

- **If ahead of pace:**
  - Extend Day 1: Have students define multiple methods in one class
  - Introduce `__str__` method early (makes debugging easier)
  - Have students create related classes (e.g., Car and Engine) to see composition concept

- **If behind pace:**
  - Combine Days 1–2: Teach class definition and `__init__` together
  - Use heavy scaffolding; provide class templates
  - Reduce number of methods per class to 1–2
  - Delay class variables until Week 2

### Week 2 (Days 4–6): Inheritance & Advanced OOP
- **Essential days** (must teach):
  - Day 4: Inheritance basics—parent and child classes, `super()`
  - Day 5: Method overriding, polymorphism, special methods (`__str__`, `__len__`, `__eq__`)
  - Day 6: Encapsulation with private attributes, properties with `@property` decorator

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Cut multiple inheritance; skip `@property` decorator, use getter methods instead
  - Skip advanced special methods beyond `__str__` and `__init__`
  - Reduce inheritance hierarchy depth to 2 levels

- **If ahead of pace:**
  - Extend Day 4: Explore multiple inheritance (carefully!)
  - Extend Day 5: Implement many special methods; explore `__repr__`, `__add__`, `__mul__`
  - Extend Day 6: Advanced decorators, class methods, static methods

- **If behind pace:**
  - Combine Days 4–5: Single day on inheritance and method overriding; cut polymorphism depth
  - Simplify: Provide parent class code; students only write child classes
  - Skip private attributes; use naming convention (`_private`) instead of enforcement

### Week 3 (Days 7–9): Design & Projects
- **Essential days** (must teach):
  - Day 7: Design patterns, composition vs. inheritance, when to use classes
  - Day 8–9: Complete OOP project (build a system with multiple related classes)

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Reduce project scope; provide more starter code
  - Skip design patterns deep dive; focus on practical building
  - Project: Provide partial class hierarchy; students only complete methods

- **If ahead of pace:**
  - Extend Day 7: Introduce design patterns formally (Factory, Singleton)
  - Project: Add file I/O (Unit 4) or visualization (Unit 6)
  - Have students refactor project using design patterns

- **If behind pace:**
  - Combine Days 8–9 into guided project with instructor co-coding
  - Reduce project to single class with related helper classes
  - Allow students to work in pairs

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Use real-world analogies: "A class is a blueprint; an object is a house built from it"
- Provide visual class diagrams showing relationships
- Use step-by-step templates for class definition
- Emphasize that `self` refers to "this object" in everyday language
- Model common mistakes explicitly (forgetting `self`, wrong indentation)

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–3: Create simple class, instantiate, call methods
- Start with single-method classes; add methods one at a time
- Emphasize: Printing output to verify class works

**Suggested pacing adjustments:**
- Spend full period on Days 1–2; this is foundational
- Use 2–3 concrete classes (Dog, Car, Student) repeatedly before introducing new topics
- Delay inheritance to Day 5 if students struggling with basic classes
- Write class definitions on board; have students predict output before running code

**What prerequisite gaps to look for:**
- Function definition confusion: If students struggle with `def`, they'll struggle with methods
- `self` concept: Many students forget `self.` prefix on attributes
- Indentation in nested code: Class bodies with method bodies create triple-nesting

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–9 as designed
- Assign Unit Practice problems #1–10 (progression from simple to complex)
- Complete multi-class project (e.g., Library system with Books, Members, Loans)
- Daily formative checks: Code-along exercises, predict-output problems

**Which practice problems to assign:**
- Problems #1–3: Basic class creation and methods
- Problems #4–7: Inheritance, method overriding, properties, `__str__`
- Problems #8–10: Complex hierarchies and complete systems
- Project: Full implementation with 3+ related classes

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 5:** Explore operator overloading (`__add__`, `__sub__`, `__mul__` for custom classes)
- **Day 6:** Implement abstract base classes (ABC module); explore mixins
- **Project:** Build a complete application (e.g., Game with characters, items, inventory)

**Challenge problems to assign:**
- Unit Practice #11–15: Game character system, library system, inventory system, music app
- Advanced: Create a plugin system where users can define subclasses
- Challenge: Implement a drawing app with Shape hierarchy (Circle, Rectangle, Triangle)
- Challenge: Build a simulation (e.g., Ecosystem with Predators and Prey)

**Ways to deepen understanding beyond the curriculum:**
- Explore design patterns: Factory, Observer, Singleton
- Discuss SOLID principles (Single Responsibility, etc.)
- Compare OOP vs. functional approaches to same problem
- Have them review real Python source code (e.g., from popular library)
- Challenge: Refactor their own code using inheritance

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 3:** Before inheritance, ensure students can create classes and call methods confidently
- **After Day 5:** Before encapsulation, ensure inheritance is solid—many students confuse inheritance with encapsulation
- **After Day 6:** Before project, review design decisions with example scenarios

### Topics students most commonly struggle with:
1. **`self` concept:** Forgetting `self.` when accessing attributes; not passing `self` to methods
2. **`__init__` vs. other methods:** Understanding why `__init__` is special; confusion about multiple methods
3. **Inheritance mechanics:** Calling parent method with `super()`; understanding which method gets called
4. **Method overriding:** Updating parent method in child; ensuring `super()` call when needed
5. **Encapsulation purpose:** Why make attributes private? When to use properties?
6. **"Everything is an object":** Understanding that classes themselves are objects in Python

### Topics students typically move through quickly:
1. **Creating objects:** `dog = Dog("Buddy", 3)` is intuitive once class is defined
2. **Calling methods:** `dog.bark()` feels natural
3. **Accessing attributes:** `dog.name` is straightforward
4. **Inheritance syntax:** `class Child(Parent):` is easy to write; semantics take longer

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Write a class with `__init__` that stores a name attribute"
- "Create an object of your class"
- Check: Correct class syntax, `self` parameter, object instantiation

**Day 2 Check (5 min):**
- "Add a method to your class that prints the name"
- "Call that method on your object"
- Check: Method definition with `self`, correct method call syntax

**Day 3 Check (5 min):**
- "What's the difference between instance and class variables?"
- "When would you use each?"
- Check: Conceptual understanding; can identify in code

**Day 4 Check (5 min):**
- "Create a parent class and a child class that inherits from it"
- "Create an object of the child class"
- Check: Inheritance syntax, object creation

**Day 5 Check (5 min):**
- "Override a method from the parent class in your child class"
- "What does polymorphism mean?"
- Check: Correct override syntax, conceptual understanding

**Day 6 Check (5 min):**
- "Create a private attribute (using __ prefix)"
- "Create a property to access it"
- Check: Correct `@property` syntax, understanding of encapsulation

**Day 7–9 Check (Project submission):**
- Multi-class project demonstrates: inheritance, method overriding, encapsulation, design decisions
- Rubric: Appropriate class hierarchy, correct OOP syntax, clean code, comments explaining design

## STEM-Specific Pacing Notes

**Important:** Coding 2 STEM must move through OOP reasonably quickly (9 days) to reach later units.

- **Essential vs. Optional:**
  - Essential: Class definition, `__init__`, methods, inheritance, method overriding (Days 1–5)
  - Optional: Encapsulation with properties (Day 6 can be lightened), advanced special methods, design patterns

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: function definitions, parameter passing, indentation
  - These gaps compound in OOP; consider 1-on-1 review
  - Be prepared with syntax review for method definition

- **When to cut:**
  - If behind after Day 3, skip class variables entirely
  - Cut `@property` decorator; use simple getter methods instead
  - Cut multiple inheritance
  - Reduce encapsulation focus; use naming convention only

- **When to accelerate:**
  - Advanced students can skip Day 7 design patterns lecture; focus on project
  - Use excess time for Unit 3 (advanced functions) if OOP mastery is clear
  - Have fast students mentor peers or extend project with additional features

**Note on project scope:**
- Minimum: 2 related classes with inheritance (Parent/Child)
- Standard: 3+ classes with inheritance and method overriding (e.g., Library/Books/Members)
- Extended: 4+ classes with complex relationships and file I/O integration
