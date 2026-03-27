# Unit 2: C# Scripting Fundamentals

> C# is the language that brings Unity games to life. Master variables, conditionals, loops, and script communication to make your games interactive and responsive.

## Unit Overview

- **Duration:** 25 days / 5 weeks
- **TN Standard:** 9-12.VGD.2 — Write C# scripts to implement game logic and behavior

---

## Learning Objectives

By the end of this unit, you will:

1. **Data Management**
   - Declare and use variables of all common types
   - Work with arrays and Lists for collections
   - Understand public vs private visibility

2. **Control Flow**
   - Write conditionals (if/else) to make decisions
   - Use loops (for, foreach, while) to repeat code
   - Handle input from keyboard and mouse

3. **Scripting Fundamentals**
   - Manipulate Transform and Rigidbody properties
   - Call methods and pass parameters
   - Understand Time.deltaTime and frame-independent movement

4. **Advanced Scripting**
   - Use GetComponent to access other components
   - Communicate between scripts
   - Use coroutines for delayed actions and sequences

5. **Game Implementation**
   - Build interactive game mechanics
   - Handle collisions and physics
   - Create responsive, player-controlled systems

---

## Unit Structure

### Days 1-3: Variables & Data Types
- Variable declaration, types (int, float, string, bool, Vector3)
- Public vs private, Inspector serialization
- Arithmetic operators and string operations

### Days 4-7: Control Flow (Conditionals & Loops)
- if/else conditions and comparison operators
- for and foreach loops
- Input handling (GetKey, GetAxis)

### Days 8-11: Methods & Communication
- Writing and calling methods
- Parameters and return values
- GetComponent and script interaction

### Days 12-15: Advanced Collections & Movement
- Arrays, Lists, and iteration
- Transform manipulation (position, rotation, scale)
- Smooth movement with Vector3.Lerp and MoveTowards

### Days 16-19: Input & Time Management
- Advanced input handling
- Time-based systems (Time.deltaTime, Time.time)
- Delayed actions and timers

### Days 20-23: Component Communication & Coroutines
- GetComponent patterns
- FindGameObjectWithTag and searching
- IEnumerator and yield return for sequences

### Days 24-25: Integration & Assessment
- Mini-project (interactive scene)
- Unit Assessment (MC, short answer, coding)

---

## Key Vocabulary

- **Variable** — Named container for a value
- **Method** — Function that performs a task
- **Parameter** — Input to a method
- **Return Value** — Output from a method
- **Component** — Functionality module on a GameObject
- **Coroutine** — Delayed or multi-frame action
- **Iteration** — One cycle of a loop
- **Condition** — Test that is true or false

---

## C# Syntax Quick Reference

### Variables
```csharp
int health = 100;              // Whole number
float speed = 5.5f;            // Decimal
string name = "Hero";          // Text
bool isAlive = true;           // True/False
Vector3 pos = new Vector3(1, 2, 3);  // 3D position
```

### Conditionals
```csharp
if(health > 50)
{
    Debug.Log("Healthy");
}
else if(health > 20)
{
    Debug.Log("Hurt");
}
else
{
    Debug.Log("Critical");
}
```

### Loops
```csharp
for(int i = 0; i < 10; i++)
{
    Debug.Log(i);
}

foreach(int num in numbers)
{
    Debug.Log(num);
}
```

### Methods
```csharp
void PrintMessage(string msg)
{
    Debug.Log(msg);
}

int Add(int a, int b)
{
    return a + b;
}
```

---

## Resources

- **Daily Notes:** Day 1–25 with Learning Targets, Code Examples, Guided Practice
- **ReferenceGuide.md:** Data types cheat sheet, common methods, Transform reference
- **UnitPractice.md:** 15 practice problems with solutions
- **UnitAssessment.md:** Comprehensive test (MC, short answer, coding)

---

## How to Use This Unit

1. **Complete each daily note in order** — Build on previous concepts
2. **Write code every day** — Don't just read; hands-on practice
3. **Test in the editor** — Run scripts and verify output in Console
4. **Use the ReferenceGuide** — Look up syntax, method names, type info
5. **Work through UnitPractice problems** — Reinforce concepts
6. **Take UnitAssessment** — Evaluate readiness for next unit

---

## Tips for Success

- **Write working code daily** — Consistent practice is essential
- **Read error messages** — They tell you exactly what's wrong
- **Use Debug.Log() liberally** — Print values to understand your code
- **Start simple** — Get one concept working before adding complexity
- **Experiment** — Change values, test edge cases, break things intentionally
- **Ask questions** — Use Console errors to debug
- **Save frequently** — Don't lose work

---

## Common Mistakes to Avoid

| Mistake | Fix |
|---------|-----|
| Forgetting `f` suffix on float | Use `5.5f`, not `5.5` |
| Using `=` in conditions | Use `==` for comparison, `=` for assignment |
| Array index out of bounds | Check `array.Length` before accessing |
| Comparing strings with `==` | Use `.Equals()` for strings in some cases |
| Forgetting `Time.deltaTime` | Always use for smooth frame-independent movement |
| GetComponent returning null | Check the GameObject actually has that component |

---

## Next Steps (Unit 3)

After mastering C# scripting, you'll move into advanced topics: physics systems, collision detection, UI programming, and asset management. The foundation you build here is essential for everything that follows.

