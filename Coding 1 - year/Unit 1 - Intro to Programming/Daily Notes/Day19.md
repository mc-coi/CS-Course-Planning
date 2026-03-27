# Day 19: Unit Review — Vocabulary, Concepts & Practice Problems
**Learning Target:** I can review and consolidate all Unit 1 concepts in preparation for assessment.

### Key Concepts Review

**Computer Science Fundamentals**
- Computer science = problem-solving with computers
- Algorithm = step-by-step procedure to solve a problem
- Program = algorithm written in code
- Pseudocode & flowcharts = planning tools before coding

**Python Basics**
- Python interpreter reads and executes code line-by-line
- `print()` displays output
- Comments start with `#`
- Python is case-sensitive (python ≠ Python)

**Variables & Data Types**
- Variable = named container for a value
- str = text (in quotes)
- int = whole numbers
- float = decimal numbers
- bool = True or False
- `type()` function identifies data types

**Input & Conversion**
- `input()` always returns a string
- `int()`, `float()`, `str()` convert between types
- Must convert input before using in math

**Operators & Order of Operations**
- Arithmetic: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- Order: Parentheses → Exponents → Mult/Div → Add/Sub
- PEMDAS with left-to-right for same precedence

**Formatting & Functions**
- F-strings: `f"Text {variable} more"`
- Decimal formatting: `f"{value:.2f}"`
- `round()` function: rounds to decimal places
- Escape characters: `\n`, `\t`, `\\`, etc.

**Development Process**
- Define (understand problem)
- Plan (write pseudocode)
- Code (write Python)
- Test (try different inputs)
- Refine (fix and improve)

### Practice Problems (All Tiers)

**Beginner Problems:**
1. Write a program that prints your name, age, and favorite hobby, each on a separate line.
2. Create variables for name (str), age (int), height (float), and is_student (bool). Print each with its type.
3. Ask user for two numbers and print their sum, difference, product, and quotient.
4. Write a program that converts 120 minutes to hours and remaining minutes.
5. Predict the output: `print(2 + 3 * 4)` and explain using PEMDAS.

**Intermediate Problems:**
6. Create a miles-to-kilometers converter. Ask for miles, display kilometers (1 mile = 1.609 km).
7. Write a program that asks for a price and calculates total with 7% tax.
8. Create a program that asks for hours worked and hourly rate, calculates gross pay.
9. Debug this code: `name = input("Name: ); age = int(input("Age: ")); print(name age)`
10. Write a program that calculates the area and perimeter of a rectangle given length and width.

**Challenge Problems:**
11. Create a compound interest calculator: A = P(1 + r/100)^n
12. Write a program that calculates your age in days (approximate).
13. Create a "student profile" program that collects info and displays a formatted card.
14. Fix this code and explain the 3 errors: `GPA = Float(input("GPA: ")); print("Your GPA is" GPA)`
15. Create any calculator program of your choice following the 5-step process.

### Practice Answers

**Beginner Answers:**
1. Three print statements with your personal info
2. Four variables declared and printed with type()
3. Two numbers, four operations
4. 120 // 60 = 2 hours, 120 % 60 = 0 minutes
5. 14 (multiplication first: 3 * 4 = 12, then 2 + 12 = 14)

**Intermediate Answers:**
6. kilometers = miles * 1.609
7. total = price * 1.07
8. gross_pay = hours * rate
9. Missing quote on "Name: and missing + between name and age
10. area = length * width, perimeter = 2 * (length + width)

**Challenge Answers:**
11. Use ** for exponentiation, proper parentheses: P * (1 + r/100) ** n
12. Age in years * 365 (approximate, doesn't account for leap years)
13. Multiple inputs, formatted output with print()
14. Errors: Float should be float, missing + between "is" and GPA
15. Any working program with inputs, calculations, and formatted output

---
