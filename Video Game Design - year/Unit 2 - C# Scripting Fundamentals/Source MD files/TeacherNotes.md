# Unit 2 - C# Scripting Fundamentals: Teacher Misconception & Callout Guide

## Overview

This unit is where students transition from clicking the editor to writing code. The biggest challenge is that C# syntax is **unforgiving**—a missing semicolon or typo crashes compilation—and students blame themselves ("I'm bad at coding") instead of reading the error message. Simultaneously, they struggle with **invisible concepts**: variables as containers, the difference between declaring and initializing, and why `Time.deltaTime` matters when 60 FPS feels fast enough. For a year-long course, students will naturally debug these misconceptions as they build interactive scenes. For a semester course, you must address them head-on because physics and input units depend on solid scripting foundations.

---

## Misconceptions by Topic

### Variables & Data Types (Days 1–3)

**⚠️ Misconception:** "I declared `float speed = 5;` but it's giving me an error. The syntax must be wrong."

**What it looks like:** A student writes `float speed = 5;` and sees the error "CS1525: Unexpected symbol `;`" or similar, but can't identify the cause. Actually, the issue is `5` is an int; they need `5f` for float.

**Why students think this:** They don't understand that `5` is interpreted as an int literal and `5f` tells the compiler "this is a float." Without the suffix, the compiler rejects the assignment.

**How to address it:** Create a cheat sheet: "In C#, number literals have types. `5` is int. `5.0` is also treated as double (not float). To make a float, add `f`: `5.0f` or `5f`. Memorize this: `int speed = 5;` and `float speed = 5f;`" Have them type out 5 examples with all three types and watch compilation succeed.

---

**⚠️ Misconception:** "My variable `score` shows in the Inspector as 0, but I set it to 100 in the code. The code isn't running."

**What it looks like:** A student writes `public int score = 100;` in the code, but the Inspector shows `score = 0` (the default value was changed in the Inspector and saved to the prefab/scene).

**Why students think this:** They don't realize that **Inspector values override code defaults**. Once you set a variable in the Inspector, that value persists in the scene until explicitly changed again.

**How to address it:** Teach the priority rule. "Code sets a default value. The Inspector lets you override that default. If the Inspector has a value, it wins. To reset, delete the scene or manually change the Inspector value back." Have them change `score` in the Inspector, play, stop, and check. Show them that the code default `= 100` is ignored in favor of the Inspector value.

---

**⚠️ Misconception:** "I have two variables: `int health = 100;` and `int currentHealth = 100;`. Aren't they the same thing?"

**What it looks like:** A student creates redundant variable names and doesn't understand why they'd need separate variables for max health vs current health. They try to track state in only one variable.

**Why students think this:** The concept of tracking multiple related values isn't obvious. They see "health" as one thing, not a system (max, current, regen rate, etc.).

**How to address it:** Use a physical analogy. "A battery has a max capacity (100%) and current charge (75%). A health system has max health (100 HP) and current health (65 HP). You need both to calculate how full the bar is." Have them build a simple health bar UI that displays `currentHealth / maxHealth`.

---

### Conditionals & Logic (Days 4–7)

**⚠️ Misconception:** "I wrote `if(health = 100)` but nothing happens. The code must be broken."

**What it looks like:** A student uses `=` (assignment) instead of `==` (comparison). The compiler doesn't catch this as an error; it sets `health = 100` and the condition is always true.

**Why students think this:** The two operators are visually similar and both exist in C#. They haven't internalized the rule: `=` assigns, `==` compares.

**How to address it:** Create a muscle-memory rule. "Use `=` only when you want to **change** a variable. Use `==` only in **if statements** and **conditions**. Say the rule out loud: 'One equals sign means set. Two equals signs mean check.'" Have them write 10 if statements and verbally confirm each one uses `==`.

---

**⚠️ Misconception:** "I wrote `if(isAlive = true)` but the player is dead and the code still runs. Why?"

**What it looks like:** Again, the student uses `=` inside the condition, which overwrites `isAlive` to `true` and always evaluates as true.

**Why students think this:** Same root cause as above, but it leads to silent, harder-to-debug failures.

**How to address it:** Catch this early. Create a lint rule or habit: "Every `if` statement must use `==` or `!=` or `>`, never `=`." Have them grep their code for `if(` patterns and verify no assignments.

---

**⚠️ Misconception:** "My code has `if(score > 10) { ... } else if(score > 5) { ... }`. Both blocks should run if score is 12."

**What it looks like:** A student expects `else if` to be independent, like two separate `if` statements. They think both will trigger.

**Why students think this:** They haven't grasped that `else if` is a **fallthrough structure**—only one block runs per evaluation.

**How to address it:** Use a flowchart. Draw a decision tree: "Is score > 10? YES → run block A, stop. NO → is score > 5? YES → run block B, stop." Emphasize the stop. Have them trace through with score = 12, 7, and 3, writing out which block runs each time.

---

### Loops (Days 4–7)

**⚠️ Misconception:** "I wrote a `for` loop, but I don't understand what `i` is. Why do we need it?"

**What it looks like:** A student writes a loop but treats `i` as magic, not as a counter. They can copy the pattern but can't modify it.

**Why students think this:** The loop syntax is dense and unfamiliar. `i` appears to have no semantic meaning.

**How to address it:** Demystify `i`. "The loop variable `i` is just a counter. It starts at 0 (or any number), increments each loop, and stops when the condition is false. You **use** `i` inside the loop to do something different each time." Have them write a loop that prints `i`, then a loop that accesses an array using `i`, then a loop that calculates `i * 2`.

---

**⚠️ Misconception:** "My `for` loop only runs once, not 10 times. It must be broken."

**What it looks like:** A student writes `for(int i = 0; i < 10; i++)` but the loop runs 10 times and they didn't count. Or they have a `break;` statement they forgot about.

**Why students think this:** They expect the loop to feel slow or noticeable. A modern computer runs 10 iterations in microseconds.

**How to address it:** Add `Debug.Log()` output. Have them write:
```csharp
for(int i = 0; i < 10; i++)
{
    Debug.Log("Loop iteration: " + i);
}
```
Open the Console and count the prints. Show them there are 10 lines: 0, 1, 2, ..., 9.

---

**⚠️ Misconception:** "I used `foreach` to loop through an array, but now I can't modify the array elements inside the loop."

**What it looks like:** A student writes:
```csharp
foreach(int num in numbers)
{
    num = num * 2;  // This doesn't change the array
}
```
The array is unchanged because `num` is a local copy, not a reference.

**Why students think this:** In a `foreach`, the loop variable is a **copy** of each element, not a reference (for value types like int, float, bool).

**How to address it:** Explain the difference. "Use `foreach` when you just want to read values. Use `for` when you want to change them." Have them solve the same problem twice: `foreach` to print every element, `for` to double every element.

---

### Methods & Communication (Days 8–11)

**⚠️ Misconception:** "I wrote a method `void Jump()`, but it doesn't do anything when I call `Jump();`"

**What it looks like:** The student has a method that compiles and is called, but they see no output in the game. They think it's not running.

**Why students think this:** The method might be doing something (like applying force to a Rigidbody), but without visual feedback or Console output, they can't tell it's working.

**How to address it:** Add debugging. "Always add `Debug.Log()` at the start of a method to confirm it's being called." Have them rewrite:
```csharp
void Jump()
{
    Debug.Log("Jump() called!");
    rb.velocity = new Vector3(rb.velocity.x, jumpForce, 0);
}
```
Run, call the method, and watch the Console print. Now they know it's running.

---

**⚠️ Misconception:** "I have a method `GetHealth()` that returns `health`, but I never use the return value. So I don't need to write `return`."

**What it looks like:** A student writes:
```csharp
int GetHealth()
{
    // No return statement!
}
```
And gets a compiler error.

**Why students think this:** They don't understand that a method that declares a return type (`int`) must actually return that type.

**How to address it:** State the rule clearly. "If you write `int GetHealth()`, you **must** write `return something;` inside. The `return` says 'this method produces an int value that the caller can use.' If you don't want to return anything, use `void` instead." Have them refactor a few methods with wrong return types.

---

**⚠️ Misconception:** "I passed a variable to a method: `UpdateScore(score);` but changes inside the method don't affect the `score` variable outside."

**What it looks like:** A student passes `score` to a method that modifies it, expects the external `score` to change, and it doesn't.

**Why students think this:** For primitive types (int, float, bool), C# passes by **value**, not by reference. The method gets a copy, not the original.

**How to address it:** Teach the distinction. "When you pass an int to a method, C# makes a copy. Changes to the copy don't affect the original. This is 'pass by value.' To modify the original, either return a new value and assign it: `score = UpdateScore(score);` or use a reference type like a class." Have them practice both patterns.

---

### Time & Frame-Independence (Days 16–19)

**⚠️ Misconception:** "`Time.deltaTime` is always around 0.016 at 60 FPS. Why do I need to multiply by it if I'm already testing at 60 FPS?"

**What it looks like:** A student hardcodes movement without `Time.deltaTime` and the game runs fine in testing. Later, when frame rate changes (lower-end device, VSync off), movement is inconsistent, and they blame the frame rate.

**Why students think this:** They test in a controlled environment and don't experience frame rate variation.

**How to address it:** Demonstrate the problem. Write two versions side-by-side:
```csharp
// BAD: frame-dependent
transform.position += Vector3.forward * 5;

// GOOD: frame-independent
transform.position += Vector3.forward * 5 * Time.deltaTime;
```
At 60 FPS, the object moves 5 * (1/60) ≈ 0.083 units per frame.
At 30 FPS, without `deltaTime`, it moves 5 units per frame (2.5× faster per second).
With `deltaTime`, it moves 5 * (1/30) ≈ 0.167 units per frame (same speed per second).

Change the target frame rate in Project Settings (Ctrl/Cmd+,) and show the difference. The bad version slows down; the good version maintains speed.

---

### GetComponent & Null References (Days 8–11, 16–19)

**⚠️ Misconception:** "I wrote `GetComponent<Rigidbody>();` but got a NullReferenceException. The method must be broken."

**What it looks like:** A student calls `GetComponent<Rigidbody>()` on a GameObject that doesn't have a Rigidbody, the method returns `null`, and they try to access a property on `null`, causing a crash.

**Why students think this:** They don't understand that `GetComponent()` can return `null` if the component doesn't exist.

**How to address it:** Teach defensive programming. "Always check if `GetComponent()` returned something before using it:"
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
if(rb != null)
{
    rb.velocity = Vector3.zero;
}
else
{
    Debug.LogError("No Rigidbody found!");
}
```
Have them add null checks to all `GetComponent()` calls. This prevents crashes and helps debugging.

---

## Whole-Class Warning Signs

- **Everyone's code has syntax errors in the first few days, and they're frustrated.** This is normal. Red squiggly lines are your friend—they tell you exactly what's wrong. Teach them to read the error message line number and fix that exact line.

- **Students use `Update()` for everything but never use `FixedUpdate()`.** Physics calculations should happen in `FixedUpdate()`. Point out that they should use `FixedUpdate()` when accessing Rigidbody, `Update()` for input and game logic.

- **No one multiplies by `Time.deltaTime`, and the game "feels fast" to some students and "feels slow" to others.** Frame rate variation is silent unless you check the Profiler. Make it a rule from day 1: all movement multiplies by `Time.deltaTime`.

- **Several students declare public variables they never set in the Inspector, then don't understand why the game doesn't work.** They expect variables to auto-populate. Show them that `public int speed = 5;` gives a default, but if they leave the Inspector value at 0, that 0 is used instead.

- **Students write scripts but forget to attach them to GameObjects, then wonder why nothing happens.** A script file by itself does nothing. It must be attached as a component. Make it a ritual: write script, save, go back to editor, drag script to a GameObject in the Hierarchy, press Play.

---

## Questions That Reveal Understanding

1. **"You have a method `void TakeDamage(int amount)`. A GameObject with this script calls `TakeDamage(10)`. What happens?"**
   - Good answer: "The method runs and does whatever is inside the `TakeDamage()` function. If it reduces health by 10, then health decreases by 10."
   - Red flag: "I don't know" or "The script breaks." (They haven't understood method calling.)

2. **"Explain the difference between `int health = 50;` and `health = 50;` in a method."**
   - Good answer: "The first declares a new variable and initializes it. The second just sets an existing variable to 50. The first creates the variable; the second changes it."
   - Red flag: "They're the same." (They haven't grasped declaration vs assignment.)

3. **"A `for` loop runs 5 times with `i = 0, 1, 2, 3, 4`. Why is the 5th iteration when `i = 4`?"**
   - Good answer: "Because arrays and counters start at 0. If you want 5 iterations, you count 0, 1, 2, 3, 4—that's 5 numbers."
   - Red flag: "I thought it would be 1, 2, 3, 4, 5." (They haven't internalized zero-indexing.)

4. **"You wrote `rb.velocity = Vector3.zero;` to stop the Rigidbody. Why would you use this instead of `rb.velocity.y = 0;`?"**
   - Good answer: "`Vector3.zero` stops all axes. `rb.velocity.y = 0;` only stops vertical motion—the Rigidbody still has sideways velocity. Use the right one for your game."
   - Red flag: "They're the same." (They haven't thought about which component of velocity to modify.)

5. **"A script has `void Start()` and `void Update()`. Which runs first? Do they run every frame?"**
   - Good answer: "`Start()` runs once, on the first frame. `Update()` runs every frame after that. So `Start()` runs 1 time total; `Update()` runs 60+ times per second."
   - Red flag: "They both run every frame" or "I don't know when they run." (They haven't grasped MonoBehaviour lifecycle.)

6. **"Why do you multiply movement by `Time.deltaTime`? What happens if you don't?"**
   - Good answer: "Without it, movement depends on frame rate. At 60 FPS, the object moves a certain distance per second. At 30 FPS, it moves half as far. Multiplying by `Time.deltaTime` makes movement frame-independent."
   - Red flag: "Because the teacher said to" or "I don't know." (They haven't connected frame rate to game feel.)

7. **"You have an array `int[] scores = { 10, 20, 30 };`. What does `scores[1]` return?"**
   - Good answer: "`20`, because arrays are zero-indexed. Index 0 is the first element (10), index 1 is the second (20)."
   - Red flag: "`30`" or "30 (the third element)." (They're thinking 1-indexed.)

---

## Common Student Questions & How to Answer Them

**Q1: "I have an error `CS1002: ; expected` but I do have a semicolon. Where's the error?"**

*A:* "This error means the compiler found something wrong on or before that line. It's usually on the line **above** where it says. Look at the whole block—maybe a brace is missing, or a method is unclosed. Copy the line number from the error message and look at that line in the code editor. The error location isn't always obvious."

---

**Q2: "What's the difference between `GetKey`, `GetKeyDown`, and `GetKeyUp`?"**

*A:* "`GetKey` is true every frame the key is held. `GetKeyDown` is true only on the frame you first press it. `GetKeyUp` is true only on the frame you release it. Think of it like: holding, pressing, releasing. For movement, use `GetKey` (hold forward = keep moving). For jumping, use `GetKeyDown` (press space once = jump once, not 60 times per second)."

---

**Q3: "I wrote `List<int> numbers = new List<int>();` but it says `List is not found`. Why?"**

*A:* "You need to import the right namespace. At the top of your script, add `using System.Collections.Generic;`. That tells C# where to find the `List` class. Some things in C# are built-in (like `int`, `string`), but others (like `List`) are in separate libraries called namespaces."

---

**Q4: "Why should I use `List` instead of an array?"**

*A:* "Arrays have a fixed size. If you don't know how many items you need ahead of time, use a `List`. You can add and remove items with `Add()` and `Remove()`. Arrays are for when you know the size in advance; Lists are for dynamic, changing collections."

---

**Q5: "I'm calling a method but the error says it doesn't exist. But I wrote it in the script!"**

*A:* "Methods are case-sensitive. If you wrote `void DoSomething()` but called `dosomething()`, C# won't find it. Also, check if the method is `public` or if you're calling it from outside the class. Finally, if you're in a different script, the method must be `public` and you need a reference to the GameObject with that script."

---

## Analogies That Work

1. **"Variables are like labeled boxes. The label is the name (`health`, `score`). The contents are the value (100, 50). When you reassign (`health = 50`), you change what's in the box, not the label. Different variables are different boxes."**
   - This helps students think of variables as persistent storage, not one-time declarations.

2. **"A method is like a recipe. You write the steps once (`void MakeCake()`). You can call it (make the cake) as many times as you want. Return values are like the final dish—you can use it for something else (eat it, decorate it, serve it). Parameters are ingredients you pass in to customize the recipe."**
   - This maps programming constructs to familiar processes.

3. **"Time.deltaTime is like the speed of a video. If you move 5 pixels per frame, and the video is 60 FPS, you move 5 * (1/60) = 0.083 pixels per millisecond. At 30 FPS, you move 0.167 pixels per millisecond—twice as fast! To make speed consistent, multiply by deltaTime. It's like saying 'move this many pixels per second, regardless of how many frames that takes.'"**
   - This connects frame rate to actual time.

---

## Unity-Specific Gotchas

- **Inspector values override code defaults.** If a student sets `public int health = 100;` and then sets health to 50 in the Inspector, the game starts with 50 (not 100). This is correct behavior, but they'll be confused if they change the code and don't see the change. Teach them: "The Inspector is the 'live' value. The code is the default if the Inspector hasn't been touched."

- **Scripts must compile before changes take effect.** If a student edits a script while the game is running and saves without stopping, the changes are lost when they stop playing. Set a rule: "Stop, edit, save, Play."

- **Null reference exceptions crash the game.** A common scenario: `GetComponent<Rigidbody>().velocity = Vector3.zero;` crashes if there's no Rigidbody. Teach defensive null checks: `if(rb != null) { ... }`.

- **GetComponent() is slow in loops.** If a student calls `GetComponent()` inside an `Update()` method every frame, it works but is inefficient. Teach them to cache it: `Rigidbody rb = GetComponent<Rigidbody>();` in `Start()`, then use `rb` in `Update()`.

- **Input.GetAxis() is smooth; Input.GetAxisRaw() is discrete.** Students often use the wrong one. `GetAxis()` is good for acceleration-based movement; `GetAxisRaw()` is good for tap-based or grid-based movement.

- **Strings are compared with `.Equals()` or `==` carefully.** `==` can work, but `.Equals()` is safer. This is a C# quirk that surprises students.

- **Array index out of bounds crashes silently.** A student writes `numbers[numbers.Length]` (off by one) and gets an IndexOutOfRangeException. Teach them: arrays are 0-indexed, so the last valid index is `Length - 1`.

- **Debug.Log() is your friend for debugging.** Some students are embarrassed to use it, thinking it's "lazy." Emphasize: professional programmers print debug information all the time. Use it to understand your code.

---

## Year-Long vs. Semester Differentiators

**For Year-Long:**
- Let students discover bugs through trial-and-error. Don't explain every gotcha upfront. When they hit a NullReferenceException, help them read the stack trace and figure out why.
- Use misconceptions as teaching opportunities. Don't prevent all mistakes—create safe conditions for them to fail and learn.
- Spiral back to these concepts in Units 3, 4, and 5. Reinforce frame-independent movement when teaching physics. Reinforce null checks when teaching collision callbacks.

**For Semester-Length (STEM):**
- Preemptively address each misconception in the first week. Frame rate independence, null checking, and method calling are non-negotiable.
- Use step-by-step scripts and templates. Students don't have time to debug syntax errors; provide starter code that compiles.
- Make it a rule: every method has `Debug.Log()` at the start. Every `GetComponent()` has a null check. These are not optional; they're standard practice.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
