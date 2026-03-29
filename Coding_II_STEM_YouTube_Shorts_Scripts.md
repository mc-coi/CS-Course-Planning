# Coding II — STEM YouTube Shorts Scripts
**54 scripts, one per lesson | Target length: under 60 seconds each**

Same format as Coding I: conversational, hook-first, no jargon overload. ~110–130 words per script (~50–55 seconds at comfortable speaking pace).

---

## UNIT 1 — Data Structures

---

### Day 1: Lists — Indexing, Slicing & Methods

**[HOOK]**
You've used lists before. But do you actually know what they can do?

**[BODY]**
A list is an ordered, changeable collection — and it comes loaded with tools. **Indexing** lets you grab any element by position. `numbers[0]` is the first, `numbers[-1]` is the last — negative indexing counts backward from the end.

**Slicing** extracts a chunk: `numbers[1:4]` gives you a sub-list of elements at index 1, 2, and 3. Add a third number to control the step — `numbers[::2]` grabs every other element.

**[CLOSE]**
Lists are the most versatile data structure in Python. Mastering indexing and slicing now will save you hours of manual work later.

---

### Day 2: List Comprehensions & 2D Lists

**[HOOK]**
What if you could build an entire list in one line of code?

**[BODY]**
**List comprehensions** replace loops with a compact expression: `[x * 2 for x in numbers if x > 0]` — that's filter and transform in a single line. Readable once you know the pattern, and much faster to write than a traditional loop.

**2D lists** are lists of lists — think rows and columns. A game board, a seating chart, a spreadsheet. Access any cell with `grid[row][col]`. Nested loops let you iterate through every cell systematically.

**[CLOSE]**
Comprehensions and 2D lists are the kind of tools that make you feel like you leveled up. Once they click, you'll see uses for them everywhere.

---

### Day 3: Tuples

**[HOOK]**
A tuple is like a list that made a promise never to change.

**[BODY]**
Tuples use parentheses instead of brackets and are **immutable** — you can't add, remove, or change elements after creation. That sounds limiting, but it's actually a feature: immutability prevents accidental modification, makes tuples slightly faster than lists, and allows them to be used as dictionary keys.

**Unpacking** is where tuples shine: `x, y, z = (1, 2, 3)` assigns all three values in one line. Functions often return multiple values as tuples — this is how you receive them cleanly.

**[CLOSE]**
When your data shouldn't change — coordinates, RGB colors, date values — use a tuple. It signals intent and adds a layer of safety.

---

### Day 4: Dictionaries

**[HOOK]**
What if instead of looking things up by position, you could look them up by name?

**[BODY]**
A **dictionary** stores data as key-value pairs — like a real dictionary where every word has a definition. `student["name"]` is cleaner and more readable than `student[0]`. Keys must be unique and immutable; values can be anything.

Add or update with `dict[key] = value`. Check if a key exists with `"key" in dict`. Iterate over everything with `.items()`, which gives you both key and value at once.

**[CLOSE]**
Dictionaries are the go-to structure whenever data has meaningful labels. Student records, config settings, API responses — nearly all real-world data comes as dictionaries. Get very comfortable with them.

---

### Day 5: Sets & Choosing Data Structures

**[HOOK]**
Sets don't care about order and they don't allow duplicates. Sounds weird — until you need exactly that.

**[BODY]**
A **set** automatically removes duplicates. Pass in a list with repeated values and you get back only the unique ones. Sets also support mathematical operations: union, intersection, difference — useful for things like "which students are in both classes?"

The bigger skill today is knowing *which* structure to reach for. Need order and access by index? **List**. Data that shouldn't change? **Tuple**. Fast lookups by label? **Dictionary**. Unique values only? **Set**.

**[CLOSE]**
Every data structure is optimized for different operations. Choosing the right one isn't a trivial decision — it affects speed, readability, and how much code you have to write.

---

### Day 6: Unit 1 Project — Student Grade Book

**[HOOK]**
Today every data structure from this unit comes together in one program.

**[BODY]**
The Grade Book project stores student names, scores, and course info using lists, dictionaries, and tuples working together. Add students, record grades, calculate averages, and display a formatted report.

The challenge isn't any single piece — it's choosing the right structure for each type of data and making them interact cleanly. A student record as a dictionary. A list of those dictionaries. Tuples for things that shouldn't change.

**[CLOSE]**
This is what data structure mastery actually looks like — not just knowing what each one is, but knowing when to use which. Build it, test it, and notice where your choices make the code easier or harder to read.

---

## UNIT 2 — Object-Oriented Programming

---

### Day 1: Introduction to OOP

**[HOOK]**
You've been writing functions. Now let's talk about a completely different way to organize code.

**[BODY]**
**Object-oriented programming** bundles data and behavior together into objects. A **class** is the blueprint — it defines what an object knows (attributes) and what it can do (methods). An **object** is an instance of that blueprint.

Think of a class as the design for a car and each actual car as an object built from that design. Every car has the same structure but different values — different color, different mileage.

**[CLOSE]**
OOP is how most large-scale software is built. Games, operating systems, web frameworks — they're all organized around objects. This unit is where your programming thinking makes a significant shift.

---

### Day 2: Defining Classes & `__init__`

**[HOOK]**
Every object needs to be set up when it's created. That's what `__init__` is for.

**[BODY]**
`__init__` is the **constructor** — it runs automatically the moment you create an object. You use it to set the object's starting attributes. The first parameter is always `self`, which refers to the specific object being created.

`self.name = name` stores the name *on this particular object* — not shared with every other object of the same class. Each instance gets its own copy.

**[CLOSE]**
Every class you write will almost certainly have an `__init__`. It's the setup phase — like filling in the fields on a form the moment a new record is created. Get this pattern down cold.

---

### Day 3: Instance Methods

**[HOOK]**
Attributes store what an object *knows*. Methods define what it can *do*.

**[BODY]**
An **instance method** is a function inside a class. It takes `self` as the first parameter, which gives it access to the object's attributes. Call it with `object.method()` — dot notation connects the action to the specific object.

Methods can read attributes, modify them, return calculated values, or print formatted output. The key idea: the method and the data it operates on live together in the same class. That's the whole point of OOP.

**[CLOSE]**
When you find yourself writing functions that always take the same object as their first argument — that's a signal those functions belong inside a class as methods.

---

### Day 4: Class vs. Instance Variables

**[HOOK]**
Some data belongs to every object. Some data belongs to all of them equally.

**[BODY]**
An **instance variable** (`self.name`) is unique to each object — every instance gets its own copy. A **class variable** is defined outside `__init__` and is *shared* by every object of that class.

If you change a class variable, every instance sees the change. If you change an instance variable, only that one object is affected. Use class variables for things that are genuinely universal — a species count, a tax rate, a version number.

**[CLOSE]**
Mixing these up is a source of very confusing bugs. Understand the difference now and you'll avoid a whole category of problems that trip up intermediate programmers for years.

---

### Day 5: Encapsulation & Properties

**[HOOK]**
What if you want to control *how* someone reads or changes your object's data?

**[BODY]**
**Encapsulation** is the OOP principle of hiding internal details and exposing only what's necessary. In Python, prefix an attribute with an underscore (`_balance`) to signal: *this is internal, don't touch it directly.*

The `@property` decorator lets you define a getter method that looks like an attribute from the outside — `account.balance` instead of `account.get_balance()`. Pair it with a setter to add validation: if someone tries to set a negative balance, you can block it.

**[CLOSE]**
Encapsulation protects your objects from being put in invalid states. It's the difference between a locked safe and leaving cash on the table.

---

### Day 6: Inheritance

**[HOOK]**
Why rewrite code you already wrote?

**[BODY]**
**Inheritance** lets a child class get all the attributes and methods of a parent class for free. `class SavingsAccount(BankAccount):` — SavingsAccount inherits everything BankAccount has and can add its own on top.

`super()` calls the parent's version of a method. Most commonly you'll see it in `__init__`: call `super().__init__()` to run the parent's setup, then add the child's specific setup below it.

**[CLOSE]**
Inheritance is how you model "is a" relationships in code. A SavingsAccount *is a* BankAccount. A Dog *is an* Animal. Every shared behavior lives once, in the parent. No copying, no divergence.

---

### Day 7: Polymorphism & Method Overriding

**[HOOK]**
Same method name, completely different behavior. That's polymorphism.

**[BODY]**
When a child class defines a method with the same name as one in the parent, it **overrides** it — the child's version runs instead. Different classes can each have a `speak()` method that does something entirely different. That's polymorphism: many forms, one interface.

This means you can write code that works on any object as long as it has the right method — without knowing or caring which specific class the object is.

**[CLOSE]**
Polymorphism is what makes code extensible. You can add new classes later and existing code still works — as long as the new class has the same method names. No rewrites needed.

---

### Day 8: Dunder Methods

**[HOOK]**
Ever wonder why Python's built-in types behave so naturally? It's all dunder methods.

**[BODY]**
**Dunder methods** — double underscores on both sides — let your custom objects behave like built-in types. `__str__` controls what `print(object)` displays. `__len__` makes `len(object)` work. `__eq__` defines what `object == other` means. `__lt__` and `__gt__` enable sorting.

Without these, Python doesn't know how to display your object or compare it with anything. With them, your class feels native — like it was built into the language.

**[CLOSE]**
Dunder methods are the finishing touch on a well-designed class. They're what separates an object that works from one that feels polished and professional.

---

### Day 9: Unit 2 Project — Bank Account System

**[HOOK]**
OOP isn't a theory. Today you build a working system with it.

**[BODY]**
The Bank Account System uses a class hierarchy: a base `BankAccount` class and child classes for checking and savings accounts. Each has its own deposit, withdraw, and interest logic. Objects track real balances, enforce rules through encapsulation, and display nicely through dunder methods.

You'll design the class hierarchy before writing a single line — decide what the parent has, what each child adds, and what each method does.

**[CLOSE]**
This is OOP in practice: shared structure in the parent, specialized behavior in the children, clean interfaces, protected data. When it works, it reads almost like a description of the real thing.

---

## UNIT 3 — Advanced Functions & Algorithms

---

### Day 1: Lambda Functions

**[HOOK]**
Sometimes a function is so small it doesn't need a name.

**[BODY]**
A **lambda** is a one-line anonymous function. Syntax: `lambda x: x * 2`. That's it. No `def`, no function name, no `return` keyword — the expression after the colon *is* the return value.

Lambdas are most useful when you need a short function just once — especially when passing a function as an argument to something like `sorted()` or `map()`. `sorted(students, key=lambda s: s["gpa"])` sorts by GPA in one clean line.

**[CLOSE]**
Don't overuse lambdas — if the logic is more than one expression, write a real function. But for quick, throwaway operations, they're clean and elegant.

---

### Day 2: Higher-Order Functions — map, filter, zip

**[HOOK]**
In Python, functions can take other functions as arguments. That unlocks a whole new style of programming.

**[BODY]**
**`map(function, list)`** applies a function to every element and returns the results. **`filter(function, list)`** keeps only elements where the function returns True. **`zip(list1, list2)`** pairs up elements from two lists side by side.

These are **higher-order functions** — they treat functions as data that can be passed around. Combined with lambdas, you can transform and filter data in single, readable lines without writing explicit loops.

**[CLOSE]**
This is the functional programming style that's become extremely popular in modern Python. Once you see the pattern, loops start to feel verbose by comparison.

---

### Day 3: Advanced Comprehensions

**[HOOK]**
Comprehensions go deeper than you might think.

**[BODY]**
You can filter inside a list comprehension: `[x for x in data if x > 0]` — only positive values. You can nest them: `[row[i] for row in matrix]` extracts a column from a 2D list.

**Dictionary comprehensions** flip key-value pairs, transform values, or build a lookup from two lists: `{name: score for name, score in zip(names, scores)}` — done.

**[CLOSE]**
Advanced comprehensions replace code that used to take 5–8 lines. If you're writing a loop just to build a new list or dictionary, there's almost certainly a comprehension that does it in one. Train yourself to look for the pattern.

---

### Day 4: Recursion Introduction

**[HOOK]**
A function that calls itself. It sounds like a logic paradox. It's actually one of the most elegant tools in programming.

**[BODY]**
**Recursion** breaks a problem down until it's trivially simple. Every recursive function needs two things: a **base case** that stops the recursion, and a **recursive case** that calls itself with a smaller version of the problem.

Factorial is the classic example: `factorial(5)` = 5 × `factorial(4)` = 5 × 4 × `factorial(3)`... until you hit `factorial(0)` = 1. Then the whole chain multiplies back out.

**[CLOSE]**
The trickiest part isn't writing the recursion — it's trusting that it works. Define your base case clearly, make sure each call gets closer to it, and let the function handle the rest.

---

### Day 5: Recursion Applied

**[HOOK]**
Recursion isn't just factorial examples. It's behind some of the most powerful algorithms in CS.

**[BODY]**
The Fibonacci sequence is a natural recursive problem — each number is the sum of the two before it. Tree and folder traversal is recursive — a folder contains files and more folders, each of which contains files and more folders... Divide-and-conquer algorithms like binary search cut problems in half recursively.

The catch: recursion can be slow if it recalculates the same values over and over. **Memoization** — caching results you've already computed — can turn an exponential-time recursive solution into a fast one.

**[CLOSE]**
When a problem naturally breaks into smaller versions of itself, recursion is often the clearest way to express the solution. That clarity is worth a lot.

---

### Day 6: Algorithm Design & Pseudocode

**[HOOK]**
The best programmers don't jump straight to code. They think first.

**[BODY]**
**Pseudocode** is a structured way to describe your algorithm in plain English before writing a single line of Python. It forces you to think through the logic — the steps, the edge cases, the decision points — without getting tangled in syntax.

**Problem decomposition** breaks a big problem into smaller sub-problems, each solvable independently. Define each piece clearly, solve it, then connect them.

**[CLOSE]**
An hour planning on paper saves three hours debugging code that was built on a shaky foundation. Professional developers write pseudocode. Architects draw blueprints. The thinking happens before the building.

---

### Day 7: Big O Notation

**[HOOK]**
Two programs that both give the right answer can have wildly different performance. Big O tells you why.

**[BODY]**
**Big O notation** describes how an algorithm's runtime grows as the input gets larger. O(1) is instant — doesn't matter if you have 10 items or 10 million. O(n) scales linearly. O(n²) gets painful fast — 1,000 items means 1,000,000 operations.

O(log n) — like binary search — is nearly magic: doubling the input only adds one more step. O(n log n) is the sweet spot for sorting algorithms.

**[CLOSE]**
This is how engineers decide which algorithm to use when performance actually matters. A working solution that's O(n²) on a dataset of a million items isn't just slow — it might be unusable. Know your complexity.

---

### Day 8: Decorators & Closures

**[HOOK]**
What if you could modify what a function does — without changing the function itself?

**[BODY]**
A **closure** is a function that "remembers" variables from the scope where it was created, even after that scope is gone. It's how you build functions that carry state.

A **decorator** wraps a function in another function — adding behavior before or after it runs. `@timer` measures how long a function takes. `@log` records every call. `@retry` re-runs it if it fails. You've already been using decorators — `@property` from OOP is one.

**[CLOSE]**
Decorators are one of Python's most powerful features. They let you add cross-cutting behavior — logging, timing, validation — without cluttering your core logic. Clean, reusable, elegant.

---

### Day 9: Unit 3 Project — Recursive Calculator & Algorithm Showcase

**[HOOK]**
Lambdas, recursion, Big O, decorators — time to put them all in one place.

**[BODY]**
The project combines a recursive calculator that handles complex operations with an algorithm showcase that demonstrates and benchmarks different approaches to the same problem. A timing decorator measures performance. Comprehensions handle data transformation. Big O analysis justifies the choices you made.

This one rewards people who understood *why* — not just people who can copy syntax. The algorithm choices, the decorator design, the recursive structure — these should all reflect deliberate decisions.

**[CLOSE]**
This is the unit where Coding II starts feeling genuinely advanced. If you built something you're proud of today, that's not an accident — you've developed real algorithmic thinking.

---

## UNIT 4 — File I/O & Data Processing

---

### Day 1: File Reading & Writing

**[HOOK]**
Your programs have been living entirely in RAM. Today they learn to save things.

**[BODY]**
`open(filename, mode)` opens a file. `"r"` reads, `"w"` writes (and overwrites everything), `"a"` appends without deleting. Always use a `with` statement — it guarantees the file closes properly even if something goes wrong mid-operation.

`f.write(text)` writes a string. `f.read()` reads the whole file back. One important detail: write doesn't add newlines automatically — you have to include `"\n"` yourself.

**[CLOSE]**
File I/O is how programs persist data between runs. Scores, logs, settings, user data — anything that needs to survive after the program closes lives in a file. This is a foundational skill.

---

### Day 2: Text File Processing

**[HOOK]**
Reading a file is easy. Doing something useful with what's in it is the real skill.

**[BODY]**
Real text files are messy — extra whitespace, inconsistent capitalization, mixed formats. The workflow: read line by line, `.strip()` each line to remove trailing newlines and spaces, then parse or transform the content.

`for line in f:` is the most memory-efficient way to process large files — it reads one line at a time instead of loading everything into memory. Split lines into parts, extract what you need, and build your data structures as you go.

**[CLOSE]**
Text processing is behind log analysis, data imports, config file parsing, and a hundred other real tasks. The pattern — read, clean, parse, use — shows up constantly.

---

### Day 3: CSV Files

**[HOOK]**
Most real-world data comes in spreadsheets. Python has a module for that.

**[BODY]**
**CSV** — Comma-Separated Values — is the universal format for tabular data. Python's `csv` module handles the parsing for you. `csv.reader()` gives you rows as lists. `csv.DictReader()` gives you rows as dictionaries, where the header row becomes the key names — much more readable.

Writing back is just as easy: `csv.writer()` for lists, `csv.DictWriter()` for dictionaries.

**[CLOSE]**
Any data that lives in Excel or Google Sheets can be exported as a CSV and processed with Python. Once you're comfortable with this module, you can work with virtually any structured dataset.

---

### Day 4: JSON Files

**[HOOK]**
APIs send data as JSON. Config files are often JSON. It's everywhere — so learn to read it.

**[BODY]**
**JSON** — JavaScript Object Notation — looks almost exactly like Python dictionaries and lists. `json.load(f)` reads a JSON file into a Python object. `json.dump(data, f)` writes a Python object out as JSON. `indent=2` makes it human-readable.

The tricky part is **nested JSON**: data inside data inside data. Navigate it with chained keys: `data["student"]["grades"]["math"]`. Loops let you process arrays of objects systematically.

**[CLOSE]**
JSON is the language of the web. Every API response you'll ever work with arrives as JSON. Getting fast at reading and navigating it is one of the most immediately useful skills in this course.

---

### Day 5: Advanced Exception Handling

**[HOOK]**
A `try/except` block is the minimum. Let's talk about doing it properly.

**[BODY]**
`try` contains the risky code. `except SpecificError` catches only that type — be specific, not generic. `else` runs only if no exception occurred — great for success-path code. `finally` always runs, error or not — use it for cleanup like closing connections.

`raise` lets you trigger exceptions deliberately — useful for enforcing rules in your own code: if someone passes invalid data, raise a `ValueError` with a clear message.

**[CLOSE]**
Sloppy exception handling hides bugs. A bare `except:` that swallows everything makes debugging a nightmare. Handle specific errors, let unexpected ones surface, and always clean up after yourself.

---

### Day 6: Custom Exceptions

**[HOOK]**
Python's built-in exceptions are general. Sometimes you need one that's yours.

**[BODY]**
Create a custom exception by inheriting from `Exception`: `class InsufficientFundsError(Exception): pass`. Now you can `raise InsufficientFundsError("Balance too low")` and catch it specifically — `except InsufficientFundsError:` — while letting unrelated errors bubble up normally.

Custom exceptions make your code's error messages meaningful. "InsufficientFundsError" tells you exactly what went wrong. "Exception" tells you almost nothing.

**[CLOSE]**
Good exception design is part of good API design. If other code is going to call your functions, give them exceptions they can catch and handle specifically. It's the professional way to communicate failure.

---

### Day 7: Data Cleaning

**[HOOK]**
Real data is messy. Cleaning it before using it isn't optional.

**[BODY]**
Data cleaning means handling the gaps and inconsistencies in real datasets: missing values, wrong data types, extra whitespace, duplicate entries, out-of-range numbers. The workflow: detect the problem, decide how to handle it (skip? fill in? flag?), then process.

Validation functions check whether a value is acceptable before it enters your system. Normalization standardizes formats — all dates as `YYYY-MM-DD`, all names in title case.

**[CLOSE]**
"Garbage in, garbage out" is an old CS saying, but it's still true. A data analysis program that skips cleaning will produce confident-looking wrong answers. Clean first, analyze second.

---

### Day 8: Data Analysis Basics

**[HOOK]**
You've collected data. You've cleaned it. Now make it tell you something.

**[BODY]**
The basics: **mean** (average), **median** (middle value), **mode** (most frequent), **min**, **max**, **range**, **standard deviation** (how spread out the data is). These statistics summarize what's in a dataset and reveal patterns that aren't obvious from raw numbers.

Python's built-in `sum()`, `min()`, `max()`, and `sorted()` get you far. The `statistics` module covers mean, median, and more. For heavy analysis, numpy handles it all efficiently.

**[CLOSE]**
Data analysis isn't magic — it's asking the right questions and computing the right numbers. The five stats from today describe almost any dataset at a useful level. Start there.

---

### Day 9: Unit 4 Project — Student Data Analyzer

**[HOOK]**
File I/O, CSV, JSON, exception handling, data cleaning, statistics — all in one program.

**[BODY]**
The Student Data Analyzer reads a CSV of student records, validates and cleans the data, computes statistics for each subject, and writes a formatted report to a JSON output file. Edge cases — missing fields, invalid numbers, empty files — are all handled gracefully.

This mirrors what real data engineers do. The pipeline: ingest → validate → clean → analyze → output. Each stage is a function. The whole thing connects in `main()`.

**[CLOSE]**
If this project works cleanly from start to finish, you've built something that resembles production-level data tooling. That's not a small thing. Run it against messy data and see how it holds up.

---

## UNIT 5 — Sorting, Searching & Recursion

---

### Day 1: Linear Search

**[HOOK]**
The simplest search algorithm is also the most obvious — and sometimes the right choice.

**[BODY]**
**Linear search** checks each element one by one, from the start, until it finds the target or runs out of list. That's it. Complexity: O(n) — in the worst case, you check every single item.

No requirements on the data — the list doesn't need to be sorted. That's the advantage. The disadvantage: on a list of a million items, you might check a million items.

**[CLOSE]**
For short lists or unsorted data, linear search is completely fine. Don't overthink it. The skill is knowing when it's *not* enough — and what to reach for instead.

---

### Day 2: Binary Search

**[HOOK]**
What if instead of checking items one by one, you eliminated half the list with every step?

**[BODY]**
**Binary search** works on sorted data. Check the middle — if the target is smaller, ignore the right half. If larger, ignore the left. Repeat on the remaining half. Each step cuts the problem in half.

The result: O(log n) complexity. That means searching one billion items takes only about 30 steps. Compare that to linear search's one billion steps worst case.

**[CLOSE]**
Binary search is a masterclass in algorithm design — simple logic, dramatic results. The catch: your data must be sorted first. If it is, binary search is almost always the right choice.

---

### Day 3: Bubble Sort

**[HOOK]**
Bubble sort is not the fastest sorting algorithm. It's the one you learn first because the logic is crystal clear.

**[BODY]**
Bubble sort repeatedly compares adjacent elements and swaps them if they're in the wrong order. After one full pass, the largest element has "bubbled" to the end. Repeat for the rest of the list. Keep going until no swaps happen in a full pass.

Complexity: O(n²). On 1,000 items, that's up to a million comparisons. On 10,000 items — 100 million.

**[CLOSE]**
Nobody uses bubble sort on real data. But implementing it teaches you what sorting *is* — comparison, swapping, iteration — which makes the faster algorithms easier to understand.

---

### Day 4: Selection Sort

**[HOOK]**
Instead of bubbling the big values up, what if you found the smallest value and pulled it to the front?

**[BODY]**
**Selection sort** scans the unsorted portion of the list for the minimum value, then swaps it into the next position. After each pass, the sorted section grows by one.

Also O(n²) like bubble sort, but with fewer swaps — selection sort makes exactly n swaps total, where bubble sort can make far more. For operations where writes are expensive, that matters.

**[CLOSE]**
Selection sort and bubble sort both run in the same Big O class, but they behave differently in practice. Understanding *why* helps you think critically about algorithm design beyond just the complexity label.

---

### Day 5: Insertion Sort

**[HOOK]**
Here's the sorting algorithm that works the way you'd sort a hand of playing cards.

**[BODY]**
**Insertion sort** takes each new element and inserts it into the correct position among the already-sorted elements to its left. Pick up a card, slide it into the right spot.

Average case: O(n²). But best case — already sorted data — is O(n). That makes insertion sort uniquely good for lists that are *almost* sorted, or for small lists where the overhead of fancier algorithms isn't worth it.

**[CLOSE]**
Python's built-in sort actually uses insertion sort for small sub-arrays within its larger algorithm. It's not a toy — it's the right tool for specific situations.

---

### Day 6: Merge Sort

**[HOOK]**
O(n²) sorting is fine for small data. For large data, you need a fundamentally different approach.

**[BODY]**
**Merge sort** uses divide-and-conquer: split the list in half, sort each half recursively, then merge the two sorted halves back together. The merge step is the elegant part — walk through both halves simultaneously and always pick the smaller element.

Complexity: O(n log n) — dramatically better than O(n²) for large inputs. The trade-off: it uses extra memory for the temporary arrays during merging.

**[CLOSE]**
Merge sort is recursive, efficient, and stable — equal elements stay in their original order. It's the foundation for understanding fast sorting. Once you implement it yourself, the logic clicks permanently.

---

### Day 7: Python's Built-in Sorting

**[HOOK]**
Real talk: you should almost never write your own sorting algorithm. Here's what to use instead.

**[BODY]**
Python's `sorted()` returns a new sorted list. `list.sort()` sorts in place. Both use **Timsort** — a hybrid of merge sort and insertion sort developed specifically for real-world data. It's faster than anything you'd write from scratch.

The `key` parameter is where the power is: `sorted(students, key=lambda s: s["gpa"], reverse=True)` sorts a list of dictionaries by GPA, descending. One line.

**[CLOSE]**
Study the sorting algorithms to understand how sorting works. Use Python's built-in for everything else. Knowing *when* to use existing tools is just as important as knowing how to build your own.

---

### Day 8: Algorithm Benchmarking

**[HOOK]**
Theoretical complexity is a prediction. Benchmarking is the proof.

**[BODY]**
Big O tells you how an algorithm *scales*, but actual runtime depends on hardware, data patterns, and implementation details. Python's `time` module lets you measure real execution time: record the time before, run the algorithm, record after, subtract.

Test the same algorithm on small, medium, and large inputs. Compare different algorithms on identical data. A chart of input size vs. runtime makes the complexity classes visually obvious — O(n²) curves up dramatically while O(n log n) stays nearly flat.

**[CLOSE]**
Benchmarking is how engineers make informed decisions. Theory tells you what to expect; measurement confirms whether reality matches. Both together give you the full picture.

---

### Day 9: Unit 5 Project — Sort & Search Visualizer

**[HOOK]**
You've implemented sorting algorithms. Now make them visible.

**[BODY]**
The Sort & Search Visualizer shows each algorithm in action — printing the list state after each swap or pass so you can watch it sort in real time. Compare execution times across algorithms on the same dataset. Add binary vs. linear search with step counts so the O(log n) advantage is impossible to miss.

The best versions include a menu that lets the user choose algorithm, input size, and whether the data starts sorted, random, or reversed.

**[CLOSE]**
Visualization turns abstract complexity analysis into something you can actually see. When you watch bubble sort crawl through 1,000 elements while merge sort finishes instantly — the theory becomes undeniable.

---

## UNIT 6 — APIs & External Libraries

---

### Day 1: pip & Package Management

**[HOOK]**
Python has 400,000+ open-source libraries. Here's how you use them.

**[BODY]**
**pip** is Python's package installer. `pip install requests` downloads and installs a library. **Virtual environments** create an isolated Python setup for each project — so different projects can use different library versions without conflicting.

A `requirements.txt` file lists every package your project needs. `pip install -r requirements.txt` installs all of them at once. This is how you share your project and make sure it works the same on every machine.

**[CLOSE]**
The Python ecosystem is one of the language's biggest advantages. Data science, web scraping, machine learning, game development — there's a library for all of it. Knowing how to install and manage packages is your access key.

---

### Day 2: The requests Library

**[HOOK]**
Your Python program can talk to the internet. That's what the requests library does.

**[BODY]**
`requests.get(url)` sends an HTTP GET request and returns a response object. Check `response.status_code` — 200 means success, 404 means not found, 500 means server error. The actual data lives in `response.text` (plain text) or `response.json()` (auto-parsed dictionary).

Always handle failure: if the status code isn't 200, something went wrong. Wrap requests in try/except to handle network errors that could crash your program.

**[CLOSE]**
One library, one line, and your program has access to live data from anywhere on the internet. That's the power of APIs — and requests is your front door.

---

### Day 3: Working with JSON APIs

**[HOOK]**
The internet is full of data just waiting to be pulled into your programs.

**[BODY]**
A **REST API** is a web service you communicate with using HTTP. Send a GET request to the right URL — often with an **API key** for authentication — and you get back a JSON response with real data: weather, sports scores, currency exchange rates, astronomy picture of the day.

Navigating the response is the skill: `data["main"]["temp"]` for a weather API, `data["results"][0]["name"]` for a search API. Read the documentation, understand the structure, then extract what you need.

**[CLOSE]**
APIs turn your programs into windows to the real world. Once you've successfully pulled live data into Python, the possibilities open up dramatically.

---

### Day 4: Data Visualization with matplotlib

**[HOOK]**
Numbers in a list don't tell a story. A chart does.

**[BODY]**
**matplotlib** is Python's most popular plotting library. `plt.plot()` draws a line chart. `plt.bar()` makes a bar chart. `plt.scatter()` plots individual data points. Add `plt.xlabel()`, `plt.ylabel()`, and `plt.title()` for labeling. Call `plt.show()` and your chart appears.

The real power is when you connect it to real data — API responses, CSV files, calculations — and let the visualization reveal patterns that raw numbers hide.

**[CLOSE]**
Data visualization is a communication skill as much as a technical one. A clear chart tells a story in seconds that a table of numbers never could. This is why data scientists spend so much time on it.

---

### Day 5: numpy Basics

**[HOOK]**
Python lists are flexible but slow for math. numpy arrays are fast.

**[BODY]**
**numpy** (Numerical Python) provides arrays that are optimized for mathematical operations. The big difference: **vectorized operations** let you do math on the entire array at once — no loop needed. `array * 2` doubles every element simultaneously. It's not just cleaner — it's dramatically faster than a for loop.

numpy also handles multi-dimensional arrays, matrix operations, statistical functions like `mean()`, `std()`, `min()`, `max()`, and random number generation.

**[CLOSE]**
numpy is the backbone of Python's scientific computing ecosystem. Data science, machine learning, engineering simulation — all of it runs on numpy under the hood. Even if you don't use it directly, you'll encounter it everywhere.

---

### Day 6: Unit 6 Project — API Data Dashboard

**[HOOK]**
Fetch real data, process it, visualize it. This is the project where everything comes together.

**[BODY]**
The API Data Dashboard calls at least one real API, processes the JSON response, cleans and organizes the data, runs basic analysis with numpy, and generates charts with matplotlib. The result is a program that produces a meaningful visual snapshot of live data — weather trends, financial data, sports stats, whatever you chose.

The challenge: the API is unpredictable, the data needs cleaning, and the visualization has to actually be readable.

**[CLOSE]**
This is the kind of project you put in a portfolio. It touches every modern Python skill — networking, data processing, analysis, visualization — and produces something visually impressive. Build something you actually care about.

---

## UNIT 7 — Capstone Project

---

### Day 1: Project Planning

**[HOOK]**
This is the unit where everything you've learned gets combined into one serious project.

**[BODY]**
Before writing a single line, you're defining what you're building. That means clear **requirements** — what must the program do? — and **user stories** — "As a user, I want to _____ so that _____." These force you to think from the user's perspective, not the programmer's.

Also define what's *out of scope*. Knowing what you're not building prevents scope creep — the slow death of projects that try to do everything.

**[CLOSE]**
Great projects are built on clear requirements. Vague projects drift. Spend today getting specific: what does "done" actually look like? Write it down before you open a code editor.

---

### Day 2: Architecture & Design Patterns

**[HOOK]**
Before you build a house, you draw blueprints. Software is the same.

**[BODY]**
**MVC** — Model, View, Controller — separates your data (Model), your display (View), and your logic (Controller). Changes to how data is stored don't break the display. Changes to the UI don't break the logic. Each piece has one responsibility.

Design patterns like **Factory** (flexible object creation) and **Singleton** (exactly one instance of something) are reusable solutions to problems that come up again and again in software design. You don't invent these — you recognize when they apply and use them.

**[CLOSE]**
Architecture decisions made on day one shape the entire project. A clean architecture means features are easy to add. A tangled one means every new feature breaks something else.

---

### Day 3: Implementation — Core Features

**[HOOK]**
Planning is done. Now you build — but carefully, one verified piece at a time.

**[BODY]**
**Incremental development**: implement one core feature, test it until it works, then move to the next. Don't implement five things at once and test at the end — when something breaks, you won't know which of the five caused it.

Start with the most essential functionality — the thing your program can't exist without. Everything else is an enhancement. Get the core working first, even if it's bare and unpolished.

**[CLOSE]**
Discipline during implementation is what separates projects that finish from projects that collapse under their own complexity. One feature at a time. Test as you go. Commit when it works.

---

### Day 4: Implementation — Features & Polish

**[HOOK]**
Core works. Time to make it complete — and handle the ugly edge cases.

**[BODY]**
**Edge cases** are where programs fail: empty input, negative numbers, files that don't exist, network timeouts, a user who presses Enter without typing anything. Your program shouldn't crash on any of these — it should handle them gracefully with a clear message.

Polish is the difference between software that works and software that's *pleasant to use*. Clear prompts, formatted output, helpful error messages. These aren't decoration — they define the user experience.

**[CLOSE]**
A program that handles edge cases cleanly and communicates clearly is a program people will trust. The core features got it running; the polish makes it real.

---

### Day 5: Refactoring & Documentation

**[HOOK]**
Your program works. Now make the code worthy of the result.

**[BODY]**
**Refactoring** means improving structure without changing behavior. Rename vague variables. Extract repeated code into functions. Simplify logic that got complicated during fast development. Remove dead code. Make each function do exactly one thing.

Documentation: every function gets a docstring — what it does, what parameters it takes, what it returns. A **README** explains what the project is, how to run it, and what it does. Write it as if a stranger will pick up this project in six months.

**[CLOSE]**
Code you wrote three weeks ago is already "someone else's code." Good documentation is the gift you give your future self — and anyone else who ever reads this.

---

### Day 6: Presentations & Showcase

**[HOOK]**
You built something this semester. Today you show it to the world.

**[BODY]**
A strong final presentation: introduce the problem your project solves, demo it live with real inputs including at least one interesting edge case, and explain one technical decision you made and why. Don't read your code — run it and narrate what's happening.

This semester you covered data structures, OOP, algorithms, file I/O, recursion, sorting, searching, APIs, and data visualization. Each unit built on the last. The capstone is where it all connects.

**[CLOSE]**
What you built represents a significant amount of technical capability. That's real — take a moment to own it. Coding II is the foundation for everything in computer science that comes next.

---

*End of Scripts — 54 total*
*Coding II STEM | Full Semester*
