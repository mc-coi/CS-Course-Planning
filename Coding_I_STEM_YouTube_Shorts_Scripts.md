# Coding I — STEM YouTube Shorts Scripts
**54 scripts, one per lesson | Target length: under 60 seconds each**

Each script is written for a casual, engaging short-form video. Aim for a conversational tone — like explaining to a friend, not reading a textbook. Estimated word count per script: ~110–130 words (~50–55 seconds at a comfortable speaking pace).

---

## UNIT 1 — Intro to Programming

---

### Day 1: What is Computer Science?

**[HOOK]**
People think coding is about computers. It's actually about *thinking*.

**[BODY]**
Computer science is the art of solving problems step by step. Those steps are called an **algorithm** — basically a recipe for a computer. Every app you use, every game you play, every website you visit — it's all just algorithms.

And here's the cool part: computers are incredibly fast, but also incredibly *literal*. They do *exactly* what you tell them — nothing more, nothing less. So the real skill isn't typing code. It's learning to think clearly and precisely enough to tell a machine what to do.

**[CLOSE]**
That's what you're learning this semester. Let's get into it.

---

### Day 2: Setting Up Python & Your First Program

**[HOOK]**
You're about to write code for the first time. It's one line.

**[BODY]**
Python is one of the most beginner-friendly languages in the world — it reads almost like English. Your very first program? `print("Hello, World!")` — that's it. Hit run, and your computer does exactly what you told it.

The `print()` function is your go-to for showing text on the screen. Whatever you put inside the quotes shows up. Python is case-sensitive though — `print` works, `Print` doesn't.

**[CLOSE]**
One line of code. That's your starting line. Everything from here builds on this moment. Run it and let's go.

---

### Day 3: Variables & Data Types

**[HOOK]**
A variable is just a labeled box. That's literally all it is.

**[BODY]**
In Python, you can store information and give it a name. `name = "Alex"` — done, that's a variable. Python has four main types of data: **strings** (text in quotes), **integers** (whole numbers), **floats** (decimals), and **booleans** (True or False).

Why does this matter? Because the type of your data affects what you can do with it. You can add two numbers together, but you can't add a number to text — at least not without converting first.

**[CLOSE]**
Variables are how your program remembers things. Get comfortable with them — you'll use them in every single program you write.

---

### Day 4: User Input

**[HOOK]**
What if your program could ask the user a question? It can.

**[BODY]**
The `input()` function pauses your program and waits for the user to type something. Whatever they type comes back as a **string** — always. Even if they type the number 42, Python sees it as the *text* "42", not the number.

So if you want to do math with user input, you have to convert it first: `int()` for whole numbers, `float()` for decimals. Forget this step and you'll get one of the most common beginner errors in Python.

**[CLOSE]**
`input()` is how your program comes alive — it stops being a one-way show and starts being a real interaction. Use it well.

---

### Day 5: The 5-Step Development Process

**[HOOK]**
Bad programmers just start typing. Good programmers plan first.

**[BODY]**
The 5-step process: **Define** the problem — what goes in, what comes out. **Plan** your solution in plain English before touching the keyboard. **Code** it. **Test** it with normal inputs *and* weird edge cases. Then **Refine** — clean it up.

Skipping step one is how you spend three hours coding the wrong thing. Skipping step four is how you ship a program that crashes the first time someone types a letter instead of a number.

**[CLOSE]**
Every professional developer follows some version of this process. Start building the habit now, while the programs are simple, so it's automatic when they get complex.

---

### Day 6: Unit 1 Project — Student Life Simulator

**[HOOK]**
Time to stop following tutorials and start building something real.

**[BODY]**
Today you're combining everything from Unit 1 — `print()`, variables, `input()`, and the development process — into a complete program. The Student Life Simulator asks for your name, grade, and a few other details, then generates a personalized output based on what you entered.

No starter code. No fill-in-the-blanks. You're planning it yourself, writing it yourself, and testing it yourself. That's what real development looks like.

**[CLOSE]**
It might feel uncomfortable. That discomfort means you're actually learning. Push through it — this is exactly what building software feels like.

---

## UNIT 2 — Variables, Data Types & Expressions

---

### Day 1: Assignment & Compound Operators

**[HOOK]**
The equals sign in Python doesn't mean "equal." It means "store this."

**[BODY]**
`score = 100` doesn't ask a question — it *assigns* the value 100 to the variable score. Want to update a variable using its own value? That's where compound operators come in: `score += 10` adds 10 to whatever score already is. Same idea with `-=`, `*=`, `/=`.

This matters because almost every program tracks something that changes over time — a score, a count, a running total. Compound operators make that elegant and readable.

**[CLOSE]**
One more trick: you can swap two variables in a single line — `a, b = b, a`. Python handles the juggling for you.

---

### Day 2: Integers vs. Floats

**[HOOK]**
Your calculator gives different answers depending on which type of number you use. So does Python.

**[BODY]**
**Integers** are whole numbers — no decimal. **Floats** have a decimal point. Simple enough. But here's the gotcha: in Python, dividing with `/` *always* gives you a float, even if the answer is a whole number. `10 / 2` gives `5.0`, not `5`.

If you want actual whole-number division that cuts off the decimal, use `//`. `10 // 3` gives `3`. And `%` gives you the remainder — `10 % 3` gives `1`.

**[CLOSE]**
These might seem like small details, but mixing up int and float is one of the most common sources of subtle bugs. Know your types.

---

### Day 3: Strings & Concatenation

**[HOOK]**
In Python, text is called a string. And you can do a lot more with it than just print it.

**[BODY]**
Strings go in quotes — single or double, Python doesn't care. You can stick strings together with `+`, which is called **concatenation**. `"Hello" + " " + "World"` gives you `"Hello World"`.

You can also grab individual characters. `"Python"[0]` gives `"P"` — Python counts from zero, always. And `len("Python")` tells you there are 6 characters.

**[CLOSE]**
Strings are everywhere — names, messages, file content, web data. Getting comfortable with them early will pay off constantly. Play around with indexing today.

---

### Day 4: String Methods

**[HOOK]**
Strings come with a built-in toolkit. You just have to know what's in it.

**[BODY]**
In Python, strings have **methods** — functions that are built right in. `.upper()` makes everything uppercase. `.lower()` does the opposite. `.strip()` removes extra spaces from the edges. `.replace("old", "new")` swaps out text. `.split()` breaks a string into a list of words.

Use them with dot notation: `name.upper()`. The original string doesn't change — you get back a new one.

**[CLOSE]**
These methods save you from writing tons of manual code. Next time you're cleaning up user input or formatting output, your first stop should be Python's string method library.

---

### Day 5: Booleans & Comparison Operators

**[HOOK]**
Everything your program decides comes down to a single question: True or False?

**[BODY]**
**Booleans** have exactly two values — `True` or `False`. You get them by comparing things: `5 > 3` is `True`, `10 == 7` is `False`. The six comparison operators are `==`, `!=`, `>`, `<`, `>=`, `<=`.

One critical detail: `==` checks if two things are *equal*. `=` *assigns* a value. Mixing these up is one of the most common beginner bugs in any language.

**[CLOSE]**
Booleans are the foundation of every decision your program makes. If-statements, while loops, input validation — all of it runs on True and False. This is the concept that unlocks everything.

---

### Day 6: Type Conversion (Casting)

**[HOOK]**
Python doesn't automatically switch between types for you. That's your job.

**[BODY]**
Need to turn a string into a number? `int("42")` gives you `42`. Want a decimal? `float("3.14")` gets you there. Going the other way — `str(100)` gives you the text `"100"`.

There's a catch: `int()` truncates, it doesn't round. `int(3.9)` gives `3`, not `4`. And you can't convert something that doesn't make sense — `int("hello")` will crash your program.

**[CLOSE]**
Casting is the fix for one of the most frustrating beginner errors — trying to do math with something that's still a string. When your program breaks, check your types first.

---

### Day 7: f-Strings & Formatting

**[HOOK]**
Stop using plus signs to build strings. There's a much better way.

**[BODY]**
**f-strings** let you embed variables directly inside a string. Put `f` before the quote, then drop variables into curly braces: `f"Hello, {name}! You scored {score} points."` — clean, readable, no concatenation gymnastics.

You can also format numbers right inside the braces. `{price:.2f}` rounds to 2 decimal places. `{value:10}` pads the output to 10 characters wide. Perfect for building tables or aligning output.

**[CLOSE]**
f-strings are how modern Python code is written. Once you start using them you'll never go back to pasting strings together with `+`.

---

### Day 8: Constants & the Math Module

**[HOOK]**
Python comes with a math library. You don't have to reinvent the wheel.

**[BODY]**
If you have a value that should never change — like a tax rate or a max score — make it a **constant**. By convention, write it in ALL_CAPS: `TAX_RATE = 0.0925`. That signals to anyone reading your code: *don't touch this.*

For heavy math, import the `math` module. `math.sqrt(16)` gives `4.0`. `math.pi` gives π. `math.ceil()` rounds up, `math.floor()` rounds down.

**[CLOSE]**
Good programmers don't write the same math from scratch every time. They import what Python already built. One line at the top of your file: `import math`. Done.

---

### Day 9: Unit 2 Project — Personal Finance Tracker

**[HOOK]**
Let's build something you could actually use.

**[BODY]**
The Unit 2 project is a Personal Finance Tracker. It collects your income, your expenses, and your savings goal — then crunches the numbers and tells you where you stand.

You'll use everything from this unit: variables, int and float, string methods, f-strings, user input, type conversion, and the math module. The challenge is combining all of these cleanly into a program that feels polished, not patched together.

**[CLOSE]**
This is your proof that you can build something real from scratch. Plan it before you code it, test it with realistic numbers, and make the output look clean. Show your work.

---

## UNIT 3 — Conditionals

---

### Day 1: Boolean Expressions

**[HOOK]**
Comparison operators don't do math — they ask questions.

**[BODY]**
`5 > 3` — is five greater than three? Yes, so Python says `True`. `10 == 7`? Nope — `False`. The six comparison operators — `==`, `!=`, `>`, `<`, `>=`, `<=` — all return a boolean.

One subtle thing: Python compares strings alphabetically. `"apple" < "banana"` is `True` because "a" comes before "b". That matters when you're sorting names or checking text input.

**[CLOSE]**
Booleans are the atoms of logic in your programs. Everything you'll learn about if-statements, loops, and validation is built from True and False comparisons just like these.

---

### Day 2: if Statements

**[HOOK]**
Your program has been doing the same thing every time. Time to give it choices.

**[BODY]**
An **if statement** runs a block of code *only* if a condition is True. The syntax: `if condition:` — then indent your code underneath. That indentation isn't optional in Python. It's how Python knows what's "inside" the if.

If the condition is False, Python skips the whole indented block and keeps going. No drama — just a fork in the road.

**[CLOSE]**
This one concept — branching based on a condition — is the backbone of nearly every program you'll ever write. Keep it simple today, because tomorrow it gets more powerful.

---

### Day 3: if/else

**[HOOK]**
What happens when your condition is False? That's what else is for.

**[BODY]**
`if/else` gives you two paths: one for True, one for False. Exactly one branch runs — never both. It's a fork, not a toggle.

Think of it like a bouncer at a door: if you're on the list, you're in. Otherwise, you're not. The bouncer doesn't stand there confused — they always make a decision.

**[CLOSE]**
If your program needs to handle both possibilities, else is your tool. Don't just write an if and leave the False case undefined — that's how you get programs that silently do nothing when something goes wrong.

---

### Day 4: elif — Multiple Branches

**[HOOK]**
Real decisions aren't just yes or no. Sometimes there are five options.

**[BODY]**
`elif` — short for "else if" — lets you chain multiple conditions together. Python checks them top to bottom and executes the *first one that's True*, then skips the rest. Order matters enormously here.

Grade boundaries are the classic example: if score >= 90 it's an A, elif >= 80 it's a B, elif >= 70 it's a C, and so on. If you put the conditions in the wrong order, you'll get wrong answers every time.

**[CLOSE]**
When you have more than two possible outcomes, `elif` is how you handle them cleanly. Think of it as a checklist — Python works down it until it finds a match.

---

### Day 5: Logical Operators — and, or, not

**[HOOK]**
Sometimes one condition isn't enough. Python lets you combine them.

**[BODY]**
**`and`** requires *both* conditions to be True. **`or`** requires *at least one* to be True. **`not`** flips the result — True becomes False and vice versa.

There's a performance trick called **short-circuit evaluation**: with `and`, if the first condition is already False, Python doesn't even check the second one. With `or`, if the first is True, it stops there. Your programs are faster than you think.

**[CLOSE]**
Logical operators let you express complex real-world rules in clean, readable code. Is the user old enough AND do they have a ticket? That's one line: `if age >= 18 and has_ticket:`.

---

### Day 6: Nested Conditionals

**[HOOK]**
What if the answer to your if-statement leads to *another* question?

**[BODY]**
**Nested conditionals** are if-statements inside if-statements. The indentation tells Python how deep you are. An outer if checks one thing; an inner if checks something that only matters *if* the outer condition was True.

Think of it like a flow chart with multiple levels: Are you a student? Yes → Are you a full-time student? Yes → Do you have a meal plan?

**[CLOSE]**
Nesting works, but don't go more than two or three levels deep before things get hard to read. Often, you can replace deep nesting with logical operators and keep everything flatter and cleaner.

---

### Day 7: Input Validation

**[HOOK]**
Users will type anything. Your job is to make sure they type the *right* thing.

**[BODY]**
**Input validation** means checking what the user gives you before you use it. A program that asks for a number between 1 and 10 should reject "banana", negative numbers, and 99. Without validation, bad input crashes your program — or worse, silently produces wrong answers.

The pattern: ask for input, check if it's valid, and if it's not — tell the user and ask again. Python's `isdigit()` method and comparison operators are your tools.

**[CLOSE]**
Validated input is the difference between a program that works in a demo and one that survives real users. Add validation as a habit, not an afterthought.

---

### Day 8: Common Conditional Errors

**[HOOK]**
There are a handful of mistakes almost every beginner makes with conditionals. Let's just cover them now.

**[BODY]**
Number one: `=` versus `==`. Single equals *assigns*. Double equals *compares*. Using the wrong one is a classic typo that Python sometimes catches and sometimes silently mishandles.

Number two: off-by-one errors. Is it `>= 18` or `> 18`? One includes 18, one doesn't. Number three: wrong logical operator — using `and` when you need `or`.

**[CLOSE]**
These aren't signs you're bad at coding. They're rites of passage. Now that you know what to look for, you'll spot them in your own code before they become a headache.

---

### Day 9: Unit 3 Project — Arcade Access Control

**[HOOK]**
Let's build a real decision-making system.

**[BODY]**
The Unit 3 project is an Arcade Access Control System. Your program checks age, asks if there's parental consent for younger users, applies different pricing tiers, and can handle edge cases like invalid input.

Every branching concept from this unit lives in this project: if/elif/else, logical operators, nested conditions, input validation. The challenge isn't any single piece — it's wiring them all together into something that handles every scenario gracefully.

**[CLOSE]**
When you're done, walk through your own program and try to break it. Enter zero, negative ages, letters instead of numbers. If it handles everything — you've built something solid.

---

## UNIT 4 — Loops and Iteration

---

### Day 1: while Loops

**[HOOK]**
What if you need your program to keep doing something until a condition changes? That's a while loop.

**[BODY]**
A **while loop** runs its block of code over and over as long as a condition stays True. The moment that condition becomes False, the loop stops. The key ingredient is a **loop control variable** — something that changes each time through, so the loop eventually ends.

Forget to change it? You get an infinite loop. The program runs forever and you have to force-quit it. It happens to everyone at least once.

**[CLOSE]**
While loops are perfect when you don't know ahead of time how many times something needs to repeat. Keep asking until you get a valid answer. Keep running until the game ends.

---

### Day 2: for Loops & range()

**[HOOK]**
When you know exactly how many times to repeat something, use a for loop.

**[BODY]**
A `for` loop combined with `range()` runs a fixed number of times. `range(5)` gives you 0, 1, 2, 3, 4 — five values starting at zero. `range(1, 11)` gives you 1 through 10. Add a third argument for the step size: `range(0, 100, 10)` counts by tens.

The loop variable holds the current number each iteration. You don't have to manually update it — Python handles that automatically.

**[CLOSE]**
For loops feel more elegant than while loops when the repetition count is known. Get comfortable with range() — it shows up everywhere.

---

### Day 3: User Input Inside Loops

**[HOOK]**
What if you want to keep asking the user a question until they're ready to stop?

**[BODY]**
Loops and user input are a natural pair. The **sentinel pattern** keeps looping until the user enters a special exit value — like typing "quit" or entering -1. Every time through the loop, you collect input, process it, and check if it's time to stop.

This is how menus work. This is how calculators that don't close after one calculation work. This is how any interactive program that serves multiple queries in a session works.

**[CLOSE]**
Combine `while True:` with a `break` when the exit condition is hit, or write the condition directly in the while clause. Either way, you've just built your first interactive loop.

---

### Day 4: Nested Loops

**[HOOK]**
What if you need a loop inside a loop? It works exactly like you'd expect.

**[BODY]**
A **nested loop** runs an inner loop completely for every single iteration of the outer loop. If the outer runs 5 times and the inner runs 3 times, you get 15 total executions. Multiplication.

The classic example is a multiplication table: for each row (outer), print each column (inner). Or a grid — for each row, check each cell. Or checking every combination of two things.

**[CLOSE]**
Nested loops are powerful and common, but be careful — they can get slow fast. 100 × 100 is 10,000 iterations. 1,000 × 1,000 is a million. Think before you nest.

---

### Day 5: break & continue

**[HOOK]**
Sometimes you need to escape a loop early. Or skip just one iteration. Python has buttons for both.

**[BODY]**
**`break`** exits the entire loop immediately — no matter what the condition says. Found what you were looking for? Break out.

**`continue`** skips the rest of the current iteration and jumps straight to the next one. Skip this one item, but keep looping.

They're both useful in search algorithms, filtering, and any loop where not every iteration should execute the same code.

**[CLOSE]**
Use `break` and `continue` deliberately, not randomly. Overusing them can make your loop logic hard to follow. But when the moment calls for it, they're exactly the right tool.

---

### Day 6: Iterating Over Strings

**[HOOK]**
You can loop over more than just numbers. Strings are iterable too.

**[BODY]**
`for ch in "Python":` gives you each character one at a time — first `"P"`, then `"y"`, then `"t"`, and so on. This opens up a world of string analysis: count vowels, search for a character, reverse a string, check if it's a palindrome.

Combine this with the **accumulator pattern**: start with an empty string or a zero counter, update it each iteration, and you've built a running result from scratch.

**[CLOSE]**
String iteration is something a lot of beginners skip over, but it's behind a huge number of real programming tasks — data cleaning, text processing, password validation. Get comfortable looping over text.

---

### Day 7: The Accumulator Pattern

**[HOOK]**
One of the most important patterns in programming has a boring name: the accumulator.

**[BODY]**
The idea is simple: initialize a variable before the loop, update it inside the loop, use the result after the loop. Add numbers for a total. Concatenate strings for a sentence. Append items for a list.

`total = 0`, then `total += number` each iteration — at the end, `total` holds the sum of everything. The pattern works for sum, product, count, maximum, minimum, and more.

**[CLOSE]**
This isn't just a beginner technique. Accumulation shows up in algorithms, data analysis, and software at every level. Recognizing the pattern makes you faster at solving problems.

---

### Day 8: FizzBuzz

**[HOOK]**
FizzBuzz is the most famous beginner programming challenge. Let's break it down.

**[BODY]**
Print numbers 1 to 100. But: multiples of 3 print "Fizz." Multiples of 5 print "Buzz." Multiples of both print "FizzBuzz." Everything else prints the number.

The trick is order. Check for 15 (or use `and`) *first*, before checking for 3 or 5 alone. Otherwise the specific case gets swallowed by the general one. The `%` (modulo) operator — which gives the remainder — is the key math move here.

**[CLOSE]**
FizzBuzz gets used in technical interviews to this day. It's simple enough to solve in minutes once you understand loops and conditionals — and a dead giveaway when someone can't. Now you can.

---

### Day 9: Unit 4 Project — Number Guessing Game

**[HOOK]**
Every loop concept you've learned fits into one game. Let's build it.

**[BODY]**
The Unit 4 project is a Number Guessing Game with statistics. The computer picks a secret number, you guess, and it tells you higher or lower. The loop keeps running until you get it right — then it reports how many guesses it took.

Advanced version: track your total games, total guesses across all games, and best score. That's accumulator patterns, while loops, nested loops, break, and input validation all working together.

**[CLOSE]**
This project is deceptively simple on the surface but has a lot of interesting problems underneath. The best version handles bad input gracefully and gives the player a satisfying experience. Build the version you'd actually want to play.

---

## UNIT 5 — Functions and Modularity

---

### Day 1: Defining & Calling Functions

**[HOOK]**
What if you could write a block of code once and use it anywhere?

**[BODY]**
That's a **function**. Use `def` to define it, give it a name, indent the body, and call it whenever you need it. `def greet():` then `    print("Hello!")` — now `greet()` anywhere in your program runs that code.

Functions without a `return` statement give back `None` automatically. They're great for tasks like printing output, but not for calculations you need to use later.

**[CLOSE]**
Functions are how you stop copying and pasting the same code. Write it once, name it well, call it everywhere. That's the foundation of clean programming.

---

### Day 2: Parameters & Arguments

**[HOOK]**
A function that always does the same thing isn't very flexible. Parameters fix that.

**[BODY]**
A **parameter** is the placeholder variable in the function definition. An **argument** is the actual value you pass when you call it. `def greet(name):` — `name` is the parameter. `greet("Alex")` — `"Alex"` is the argument.

Multiple parameters? Separate them with commas and match them in order. Or use keyword arguments — `greet(name="Alex", age=16)` — to pass them in any order.

**[CLOSE]**
Parameters are what make functions *reusable*. The same `calculate_tax(price, rate)` function works for any price and any tax rate. One function, infinite uses.

---

### Day 3: Return Values

**[HOOK]**
A function can give something back. That's what `return` is for.

**[BODY]**
`return` sends a value back to whoever called the function. Once Python hits `return`, the function stops — no more code runs in that call. You can store the result: `result = add(3, 5)`, or use it directly: `print(add(3, 5))`.

Big distinction: `print()` shows something on screen. `return` sends data back to your code. A function that only prints can't be used in a calculation. A function that returns can.

**[CLOSE]**
Well-designed functions take inputs, do one thing with them, and return a result. That's the model. If your function is printing *and* calculating *and* asking for input, it's probably doing too much.

---

### Day 4: Scope

**[HOOK]**
Not every variable can be seen from everywhere in your code. Scope controls that.

**[BODY]**
A **local variable** lives inside a function — it's born when the function runs and disappears when it ends. A **global variable** lives outside all functions — everything can see it.

Functions are their own little bubble. Changes inside don't affect the outside unless you specifically design them to. The best way to "pass" information in and out of a function is through parameters and return values — not by relying on globals.

**[CLOSE]**
Understanding scope prevents some of the most confusing bugs in Python. If you change a variable inside a function and it doesn't seem to update outside it, scope is probably why.

---

### Day 5: Modular Design

**[HOOK]**
One big function that does everything is a nightmare to read, fix, and reuse.

**[BODY]**
**Modular design** means breaking your program into small, focused functions — each one does exactly one thing. `get_input()` handles input. `calculate_total()` does the math. `display_result()` prints the output. They call each other, but each is testable on its own.

Signs you're doing it right: your functions are short (roughly 5–15 lines), named so clearly you can tell what they do without reading them, and easy to test in isolation.

**[CLOSE]**
This is the principle that separates programs that work from programs that are *maintainable*. When something breaks, a well-modularized program tells you exactly where to look.

---

### Day 6: Functions & Lists

**[HOOK]**
Functions aren't just for numbers — you can pass lists through them too.

**[BODY]**
Pass a list as a parameter the same way you'd pass anything else. Inside the function, you can loop through it, filter it, transform it, or calculate something from it. Return a new list when you want to give transformed data back.

The important distinction: when you pass a list to a function and modify it *in place* (using `.append()` or direct assignment), the original list outside the function *does* change. Lists are mutable and passed by reference.

**[CLOSE]**
List-processing functions are incredibly common in real code — sorting, filtering, averaging, searching. Build a few today and you'll have reusable tools for every project that follows.

---

### Day 7: Default Parameters & Multiple Returns

**[HOOK]**
Two small features that make functions dramatically more flexible.

**[BODY]**
**Default parameters** let you set a fallback value for a parameter in case the caller doesn't provide one. `def greet(name, greeting="Hello"):` — call it with just a name, and it uses "Hello" automatically. Override it whenever you want something different.

**Multiple return values** let a function hand back more than one thing at once. `return min_val, max_val` — unpack it on the other end: `low, high = find_range(numbers)`. Python packs them into a tuple automatically.

**[CLOSE]**
These two features reduce the number of functions you need to write and make your existing ones more versatile. Less code, more capability.

---

### Day 8: Debugging Functions

**[HOOK]**
Functions introduce a new category of bugs. Let's know them before they hit us.

**[BODY]**
Common function bugs: calling a function *before* defining it. Passing the wrong number of arguments. Expecting a return value from a function that only prints. Using a local variable outside the function that created it. And the scariest one — a function that accidentally calls itself without a stopping condition. That's **infinite recursion**, and it crashes the program.

Debug strategy: add `print()` calls at the top of functions to confirm they're being called with the right values, and just before `return` to confirm what they're sending back.

**[CLOSE]**
Functions are where bugs get sneaky. The more isolated your functions are — clear inputs, clear outputs — the easier they are to debug one piece at a time.

---

### Day 9: Unit 5 Project — Modular Application

**[HOOK]**
One function was cool. Building a whole program out of them? That's the project.

**[BODY]**
The Unit 5 project is a full modular application — a grade calculator, a text analyzer, or a statistics tool, depending on what you choose. No monolithic code blocks. Every logical step lives in its own function, functions call each other cleanly, and `main()` orchestrates the whole thing.

The challenge: before writing a single line of code, document every function you plan to write — its name, parameters, and what it returns. Then build them one at a time and test each independently.

**[CLOSE]**
This is top-down design in action. Plan the architecture first, build the pieces second, wire them together third. That's how real software gets written.

---

## UNIT 6 — Debugging and Documentation

---

### Day 1: Types of Errors

**[HOOK]**
Not all bugs are created equal. Knowing the type tells you where to look.

**[BODY]**
There are three kinds: **syntax errors** stop the program before it even runs — a typo, a missing colon, a mismatched quote. Python catches these and tells you the line. **Runtime errors** crash the program while it's running — like dividing by zero or using a variable that doesn't exist yet. **Logic errors** are the sneaky ones — the program runs fine but gives the wrong answer.

Logic errors are the hardest because Python doesn't help you. The program thinks everything is fine.

**[CLOSE]**
When your program breaks, your first question should be: which type of error is this? That narrows down your debugging strategy immediately.

---

### Day 2: File I/O — Writing Files

**[HOOK]**
Your program can save data to a file — and read it back later.

**[BODY]**
`open(filename, mode)` opens a file. Use `"w"` to write (warning: overwrites everything), `"a"` to append without deleting what's there, `"r"` to read. Always wrap it in a `with` statement — it automatically closes the file when you're done, even if something goes wrong.

`f.write(text)` writes a string. You have to add `"\n"` yourself if you want a newline. It won't put one there automatically.

**[CLOSE]**
File I/O is how programs remember things between runs. Scores, preferences, logged data — anything that needs to persist after the program closes lives in a file.

---

### Day 3: File I/O — Reading Files

**[HOOK]**
Writing to a file is half the story. Reading it back is the other half.

**[BODY]**
`f.read()` gives you the entire file as one big string. `f.readlines()` gives you a list where each element is one line. Or iterate directly: `for line in f:` — this is the most memory-efficient way, especially for large files.

Important detail: each line has a newline character `"\n"` at the end. If you're processing the text, chain `.strip()` onto each line to remove it.

**[CLOSE]**
Reading files is how your programs work with real-world data — log files, CSVs, config files, user data. Get comfortable with this pattern and the rest of data processing starts to make sense.

---

### Day 4: Exception Handling

**[HOOK]**
What happens when your program encounters an error at runtime? It crashes — unless you handle it.

**[BODY]**
`try/except` is Python's way of catching errors before they crash everything. Put the risky code in the `try` block. If something goes wrong, the `except` block catches it and runs your recovery plan instead.

Be specific: `except ValueError:` catches conversion errors, `except FileNotFoundError:` catches missing files. A bare `except:` catches everything — but it also hides real bugs, so use it carefully.

**[CLOSE]**
Exception handling is the difference between a program that crashes and one that says "that didn't work — try again." Add it whenever your program touches user input, files, or network connections.

---

### Day 5: Comments & Docstrings

**[HOOK]**
You're not just writing code for computers. You're writing it for humans — including future you.

**[BODY]**
**Inline comments** with `#` explain *why* something works the way it does. Don't explain what the code obviously does — explain why you made that choice.

**Docstrings** go right under a function definition, wrapped in triple quotes. They describe what the function does, what parameters it expects, and what it returns. Call `help(your_function)` and Python will display it.

**[CLOSE]**
A codebase without documentation is a liability. Future you — six months from now — will have no idea why you made that weird conditional on line 47. Write it down now while you still know.

---

### Day 6: Unit 6 Project — Data Analyzer

**[HOOK]**
Every skill from this unit lives in this one project. Let's build it.

**[BODY]**
The Data Analyzer reads scores from a file, processes them with functions, handles file errors gracefully, and produces a formatted report with statistics — average, min, max, count. Everything is documented with docstrings and clear comments.

This is the hardest type of program to get right: it has to handle missing files, bad data, and edge cases like an empty file — without crashing at any point.

**[CLOSE]**
When you can build something that reads real data, processes it reliably, and handles errors gracefully — you've crossed into territory that actually looks like professional software development. That's the goal today.

---

## UNIT 7 — Project Development

---

### Day 1: Planning & Design

**[HOOK]**
The most important part of building software happens before you open a code editor.

**[BODY]**
The Software Development Process: **Define** the problem clearly — what problem are you solving, who's it for, and what does success look like? **Plan** before you code — write pseudocode, draw flowcharts, document your function signatures. **Code** from that plan. **Test** systematically. **Refine** until it's solid.

Skipping the planning phase is the single most common reason student projects get stuck. You end up writing code, then rewriting it, then rewriting it again because you didn't know where you were going.

**[CLOSE]**
Spend today on paper. Your project will be better for it. Every professional developer knows this — now you do too.

---

### Day 2: Bottom-Up Development

**[HOOK]**
Build the smallest pieces first. Then connect them.

**[BODY]**
**Bottom-up development** means starting with the helper functions — the small, isolated, testable pieces — and building upward toward `main()`. Write `get_user_input()`, test it. Write `calculate_result()`, test it. Then wire them together.

The alternative — writing everything top-down from main and hoping it works — means you can't test anything until the whole program is done. And when it breaks, you don't know which piece broke it.

**[CLOSE]**
Build small, test small, connect small pieces into bigger ones. The program grows one confirmed, working piece at a time. Less guessing, fewer catastrophic bugs.

---

### Day 3: Integration

**[HOOK]**
You have working pieces. Now make them work together.

**[BODY]**
**Integration** is the process of connecting your individual functions into a program that flows from start to finish. `main()` is the conductor — it calls your functions in the right order, passes output from one as input to the next.

Integration is often where surprises happen. Two functions that work perfectly in isolation can clash when connected — mismatched data types, unexpected None returns, variable scope issues. This is why you built and tested each piece first.

**[CLOSE]**
Work through your program from input to output. Test each connection as you make it. Don't integrate everything at once and hope for the best — connect one function at a time and verify it before moving on.

---

### Day 4: Refactoring & Polish

**[HOOK]**
The program works. Now make it *good*.

**[BODY]**
**Refactoring** means improving the structure of your code without changing what it does. Rename vague variables. Extract repeated code into functions. Shorten logic that became unnecessarily complex during rapid development. Delete comments that just describe what the code obviously does.

Polish the user experience too: are your prompts clear? Is your output readable? Does the program handle bad input gracefully or crash at the first unexpected letter?

**[CLOSE]**
Working code is the minimum. Readable, clean, well-structured code is what you're aiming for. Refactoring is how you close the gap between "it runs" and "it's good."

---

### Day 5: Presentations

**[HOOK]**
You built something. Now you have to show people what you built — and why.

**[BODY]**
A strong project presentation has three parts: tell them what problem your program solves, *show* them a live demo with real input including an edge case, and explain one key technical decision you made and why.

Don't read your code. Don't apologize for what it can't do. Show what it *can* do, clearly and confidently. The demo is the heart of it — let the program speak.

**[CLOSE]**
Presenting your work is a skill as important as building it. Engineers who can explain what they made and why they made it that way stand out. Practice saying it out loud before the real thing.

---

### Day 6: Wrap-Up & Reflection

**[HOOK]**
You just completed a full semester of programming. Let's actually sit with that for a second.

**[BODY]**
You went from `print("Hello, World!")` to building a project with multiple functions, file I/O, error handling, and a user interface. You learned to think algorithmically. You debugged code at two in the afternoon and maybe at eleven at night. You built things that didn't exist before you wrote them.

That's not a small thing. Programming is one of the few skills where you create something real from nothing but logic and patience.

**[CLOSE]**
You're not done learning — you're just getting started. Coding II is next. But take a moment to recognize what this semester actually was. You earned it.

---

*End of Scripts — 54 total*
*Coding I STEM | Full Semester*
