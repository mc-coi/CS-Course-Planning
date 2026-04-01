# Unit 2 - C# Scripting Fundamentals: Teacher Misconception & Callout Guide

## Overview

In a semester-length STEM course, this unit is **make-or-break**. Students must master C# syntax and debugging quickly because they don't have time to "discover" mistakes in later units. The biggest challenge is that C# is **unforgiving**—a typo breaks compilation—and students blame themselves instead of reading error messages. They also struggle with invisible concepts: variables as containers, why `Time.deltaTime` matters, and how `GetComponent()` can return `null`. Unlike a year-long course where iteration teaches these lessons naturally, a STEM course must address misconceptions **immediately and explicitly** with zero tolerance for mistakes. Every student must be able to write a working script by the end of this unit.

---

## Misconceptions by Topic

### Variables & Data Types (Days 1–3)

**⚠️ Misconception:** "I declared `float speed = 5;` but it's giving me an error. The syntax must be wrong."

**What it looks like:** A student writes `float speed = 5;` and sees "CS1525: Unexpected symbol `;`" or similar. They're stuck.

**Why students think this:** They don't understand that `5` is interpreted as `int`, not `float`. They need `5f`.

**How to address it:** **Immediate, explicit rule.** Make a class poster: "In C#, number types matter. `5` = int. `5.0f` = float. `5.0` = double (not float!). Memorize: always use `f` suffix for floats." Have them write out 10 examples: `5`, `5f`, `5.0f`, etc., and compile each one. No moving on until this is solid. This is a STEM course; there's no room for "I'll learn this later."

---

**⚠️ Misconception:** "My variable `score` shows in the Inspector as 0, but I set it to 100 in the code. I'm confused."**

**What it looks like:** Code says `public int score = 100;`, Inspector shows `score = 0`.

**Why students think this:** Inspector values override code. They don't realize this is correct behavior.

**How to address it:** **Enforce as a rule.** "Inspector values always win over code defaults. Once you set a value in the Inspector, that value persists. To reset, either delete the scene and rebuild, or manually change the Inspector value back. This is intentional—it's how designers customize game objects." Have them deliberately change a variable in the Inspector, save, stop, and verify it persists.

---

### Operators & Logic (Days 4–5)

**⚠️ Misconception:** "I wrote `if(health = 100)` in my code but nothing happens. Why?"**

**What it looks like:** A student uses `=` instead of `==`. The compiler doesn't error; it assigns and evaluates to true.

**Why students think this:** The mistake is silent and harder to debug than syntax errors.

**How to address it:** **Zero tolerance policy.** "In a STEM course, this mistake costs points. Memorize: `=` is assignment, `==` is comparison. Every `if` statement uses `==`. Write the rule on the whiteboard and have them repeat it. Every graded script will be checked for this error." Then check every submission for this specific mistake. When you find it, mark it and explain why it's wrong.

---

**⚠️ Misconception:** "I wrote `if(isAlive = true)` and the code doesn't behave right. Why?"**

**What it looks like:** Same as above—using `=` in a condition.

**Why students think this:** Same root cause but even harder to debug because it silently overwrites the variable.

**How to address it:** **Same enforcement.** Show the difference side-by-side:
```csharp
// WRONG: sets isAlive = true, condition always true
if(isAlive = true) { ... }

// RIGHT: checks if isAlive is true
if(isAlive == true) { ... }

// ALSO RIGHT: simpler
if(isAlive) { ... }
```
All three should be compiled and tested. Then create a rule: "In this class, we always use `==` for comparisons. No exceptions."

---

### Loops (Days 4–6)

**⚠️ Misconception:** "I wrote a `for` loop, but it only runs once, not 10 times. It must be broken."**

**What it looks like:** A loop with `i < 10` runs and the student expects 10 outputs but doesn't see them (because they're printing to Console at 120 FPS).

**Why students think this:** The output is invisible unless they look in the Console.

**How to address it:** **Teach Console early.** "Always use `Debug.Log()` to verify code is running. A loop that runs 10 times should print 10 lines in the Console. Go to Window → TextEditorAndSourceCodeTools → Console and watch." Then require every loop to have a `Debug.Log()` inside. No loop without Console output.

---

**⚠️ Misconception:** "My `foreach` loop modifies array elements, but the array doesn't change."**

**What it looks like:** A student writes:
```csharp
foreach(int num in numbers)
{
    num = num * 2;
}
```
The array is unchanged.

**Why students think this:** For value types, `foreach` creates a local copy.

**How to address it:** **Teach the distinction.** "Use `for` to modify arrays. Use `foreach` to read. For value types (int, float, bool), `foreach` gives you a copy, not a reference." Have them rewrite the same loop twice: `foreach` (read-only), `for` (with modification). Both should compile and run.

---

### Methods & Communication (Days 8–11)

**⚠️ Misconception:** "I wrote a method `void Jump()`, but when I call `Jump();` nothing happens."**

**What it looks like:** A method is defined and called, but no visible effect.

**Why students think this:** The method is running but has no visual feedback.

**How to address it:** **Mandate Debug.Log() in every method.** "The first line of every method is `Debug.Log("Method called");`. No exceptions. This proves the method runs. Then add the real logic." This makes debugging automatic and teaches students to verify their code works.

---

**⚠️ Misconception:** "I have a method `GetHealth()` that returns `health`, but I never use the return value. Do I need to return anything?"**

**What it looks like:** A student writes:
```csharp
int GetHealth()
{
    // No return statement
}
```
Compiler error.

**Why students think this:** They don't understand that declaring a return type requires a return statement.

**How to address it:** **Explicit rule.** "If you write `int GetHealth()`, you MUST return an int. If you don't want to return anything, use `void` instead. No exceptions." Make this a grading rubric: "Every method has correct return type and returns the correct type." Check every script.

---

### GetComponent & Null References (Days 8–11)

**⚠️ Misconception:** "`GetComponent<Rigidbody>()` returns null and crashes my game. The method is broken."**

**What it looks like:** A student calls `GetComponent()` on an object without a Rigidbody, and the game crashes with NullReferenceException.

**Why students think this:** They don't expect `GetComponent()` to fail.

**How to address it:** **Mandatory null checks.** "Every `GetComponent()` must have a null check. No exceptions. Always write:
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
if(rb == null)
{
    Debug.LogError("No Rigidbody found!");
    return;
}
```
This prevents crashes and helps debug. In STEM, a script without null checks loses points." Make this a grading requirement.

---

### Time & Frame-Independence (Days 16–19)

**⚠️ Misconception:** "`Time.deltaTime` is around 0.016 at 60 FPS. Why do I need it if my test environment is always 60 FPS?"**

**What it looks like:** A student hardcodes movement without `Time.deltaTime` and it works in testing.

**Why students think this:** They don't see the problem because they always test at 60 FPS.

**How to address it:** **Demonstrate immediately.** "Write two versions side-by-side:
```csharp
// Version 1: WITH deltaTime
transform.position += Vector3.forward * 5 * Time.deltaTime;

// Version 2: WITHOUT deltaTime
transform.position += Vector3.forward * 5;
```
Change Project Settings → Time → Fixed Timestep to 0.03 (simulates 30 FPS). Version 1 moves at the same speed. Version 2 is twice as fast. This is not optional—always use `Time.deltaTime`." Make this a strict grading rule: any movement without `Time.deltaTime` is marked wrong.

---

## Whole-Class Warning Signs

**Immediate action required (do not proceed to next unit):**

- **Multiple students have scripts that don't compile.** They're not reading error messages or understanding syntax. Stop, review error messages line-by-line, and require every student to compile a working script before moving on.

- **Everyone forgets to attach scripts to GameObjects.** Make it a ritual: write script, save, go back to editor, drag script to Hierarchy, press Play. If a student's script doesn't run, the first question is always: "Is the script attached?"

- **Lots of NullReferenceExceptions in Console.** Students aren't checking null or they're calling methods on null objects. Make null checking mandatory for every `GetComponent()` call. Check scripts for compliance.

- **No one multiplies by `Time.deltaTime`.** This will break in later units. Make it a rule from day 1. Every script that moves something must use `Time.deltaTime`. Check every submission.

---

## Questions That Reveal Understanding

1. **"What's the difference between `int health = 50;` and `health = 50;` in a method?"**
   - Good answer: "The first declares and initializes a new variable. The second modifies an existing variable."
   - Red flag: "They're the same" → remediation needed before moving on.

2. **"You wrote `if(score == 10)` and it printed. Then you wrote `if(score = 10)` and it printed twice. Why?"**
   - Good answer: "The first checks if score equals 10. The second sets score to 10 (which is always true) and prints. Then the real code runs again."
   - Red flag: "I don't know" or "They're the same" → this student needs 1-on-1 tutoring on operators.

3. **"Why multiply movement by `Time.deltaTime`? Give a specific example."**
   - Good answer: "So movement speed is consistent regardless of frame rate. At 60 FPS, moving 5 * (1/60) = 0.083 units/frame. At 30 FPS, 5 * (1/30) = 0.167 units/frame, but still 5 units/second total."
   - Red flag: "Because the teacher said to" → they don't understand the principle; remediate with examples.

---

## Common Student Questions & How to Answer Them

**Q1: "Why do I keep getting compiler errors? My code looks right."**

*A:* "Read the error message. It tells you the exact line and what's wrong. Click the error in the Console and it takes you to the line. Check: (1) Missing semicolon? (2) Mismatched braces? (3) Wrong type (float vs int)? (4) Misspelled variable name? The error message will tell you. If it says 'CS1002: ; expected,' look at that line—there's a missing semicolon or brace."

---

**Q2: "My script compiles but nothing happens when I run it. How do I know if it's working?"**

*A:* "Add `Debug.Log()` statements. Put them at the start of methods and in loops. Open the Console (Window → TextEditorAndSourceCodeTools → Console). Run the game. If you see Console output, the code is running. If you don't, the code isn't running. Check: (1) Is the script attached to a GameObject? (2) Is the GameObject active? (3) Are you in the right event (Start, Update, etc.)?"

---

**Q3: "I want to move a Rigidbody, but I'm using `transform.position +=`. Should I use `rb.velocity` instead?"**

*A:* "Yes. For physics objects, use `rb.velocity = ...` or `rb.AddForce()`. For non-physics objects, `transform.position` is fine. Using `transform.position` on a Rigidbody bypasses physics, which can cause bugs. Always use the right component for the job."

---

**Q4: "What does `using UnityEngine;` do?"**

*A:* "`using` imports a namespace. `UnityEngine` contains all Unity classes (GameObject, Transform, Rigidbody, etc.). Without `using UnityEngine;`, you'd have to write `UnityEngine.GameObject` every time. The `using` statement saves typing. Most scripts start with several `using` statements."

---

**Q5: "I have multiple `Debug.Log()` statements but the Console is cluttered. Can I disable them?"**

*A:* "Yes. In the Console tab, uncheck 'Logs'. You'll still see errors and warnings. Or comment out the `Debug.Log()` lines: `// Debug.Log(...);`. But in development, logs are useful. Don't disable them if you're still debugging."

---

## Analogies That Work

1. **"Variables are labeled boxes. `int health = 100;` creates a box labeled 'health' with value 100. `health = 50;` changes what's in the box. `=` is 'put in.' `==` is 'is it the same?' Every time you read `health`, you look in the box."**
   - This cements the variable-as-container metaphor.

2. **"Methods are recipes. You write the recipe once (`void MakeCoffee()`). You can follow it many times (call the method). Parameters are ingredients you add (taste control). Return values are the final drink you get to use."**
   - This maps programming to a familiar process.

3. **"`Time.deltaTime` is like a stopwatch. At 60 FPS, the stopwatch ticks every ~0.016 seconds. If you move 5 units per tick without multiplying by time, you move 5 * 60 = 300 units per second. Multiply by time: 5 * 0.016 * 60 = 5 units per second. The stopwatch keeps you honest."**
   - This makes frame-independence concrete.

---

## Unity-Specific Gotchas

- **Inspector values override code defaults.** Once set, they persist. This is correct but confusing. Teach it explicitly.

- **Scripts must be compiled before changes take effect.** Saving in the code editor doesn't auto-compile. Unity compiles when you switch focus. Wait for the spinning gear icon to finish.

- **Play mode changes aren't saved.** If you change variables in Play mode and expect them to save, you'll be disappointed. Stop, edit in the code editor, then Play.

- **GetComponent is slow in loops.** Cache it in Start(): `Rigidbody rb = GetComponent<Rigidbody>();` in Start(), then use `rb` in Update().

- **Null reference exceptions crash the game.** A common error. Always null-check `GetComponent()` results.

- **Variable scope matters.** A variable declared in a method only exists inside that method. Declare public variables if you need them in the Inspector.

---

## STEM-Specific Strategies

**Whole-Class Accountability:**
- Check every script for: `==` (not `=`) in conditions, `Time.deltaTime` in movement, null checks on `GetComponent()`, correct return types on methods.
- Return scripts with specific errors marked and require resubmission.
- No script with a compiler error gets credit. Period. This forces rigor.

**Pair Programming:**
- Have students work in pairs on first few scripts. One writes, one checks. Catches mistakes immediately.

**Debugging Checklist:**
- Create a worksheet: "Script not running? (1) Is it attached? (2) Is GameObject active? (3) Did it compile? (4) Are there errors in Console?"
- Every student must complete this checklist before asking for help.

**Grading Rubric:**
- Compile with no errors: 30%
- Uses correct types and syntax: 20%
- Includes null checks and Debug.Log(): 20%
- Logic works correctly: 20%
- Uses Time.deltaTime where needed: 10%

This rubric rewards process, not just correctness.

---

**Created for:** Video Game Design course (STEM semester-length version)
**Last updated:** 2026
**Note:** For STEM courses, address misconceptions immediately and explicitly. There's no time for slow discovery. Every student must be proficient in C# by the end of this unit.
