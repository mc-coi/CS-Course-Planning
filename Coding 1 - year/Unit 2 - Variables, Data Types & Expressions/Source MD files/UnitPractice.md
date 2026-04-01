# Unit 2 Practice Problems (25 Total)

## Tier 1: Beginner (Problems 1-10)

**1. Variable Declaration & Reassignment**
Declare a variable `color` with the value `"blue"`, reassign it to `"red"`, then print it.

**2. Basic Arithmetic**
Calculate `(15 + 5) * 2 - 10` step by step, showing operator precedence.

**3. String Concatenation**
Combine three strings: `"Hello"`, `" "`, `"World"` into a single string and print.

**4. String Indexing**
Given `word = "Programming"`, print the character at index 3.

**5. String Length**
Find and print the length of the string `"Computer Science"`.

**6. String Slicing**
Given `text = "Python"`, extract and print `"tho"` using slicing.

**7. Type Conversion**
Convert the string `"99"` to an integer, add 1, and print the result.

**8. String Method: uppercase**
Take the string `"hello world"` and print it in uppercase.

**9. Comparison Operator**
Evaluate `10 < 15` and print the result (should be `True`).

**10. Simple F-String**
Format the price `19.99` as currency using an f-string: `f"${price:.2f}"`.

---

## Tier 2: Intermediate (Problems 11-20)

**11. Compound Assignment**
Starting with `x = 50`, use `+=`, `-=`, and `*=` to modify it, printing after each operation.

**12. String Slicing with Step**
Given `word = "Programming"`, use slicing with step to print every 2nd character.

**13. Method Chaining**
Apply three string methods in sequence: `.strip()`, `.lower()`, `.title()` to `"  HELLO  "`.

**14. Multiple Assignment & Swapping**
Create two variables, swap their values using `a, b = b, a`, and print before/after.

**15. Operator Precedence**
Calculate `2 + 3 * 4 - 5 // 2`. Show step-by-step with correct order of operations.

**16. Float to Integer Conversion**
Convert `7.8` to an integer using `int()`. Explain why the result is 7, not 8.

**17. Circle Area Calculation**
Ask the user for a radius and calculate area using `π * r²`. Display with 2 decimal places.

**18. String Finding**
Use `.find()` to locate the first occurrence of `"an"` in `"banana"`.

**19. String Counting**
Use `.count()` to count how many times `"l"` appears in `"hello world"`.

**20. Formatted Currency Output**
Format these amounts as currency with thousands separator: `1234.5`, `50.1`, `999999.99`.

---

## Tier 3: Challenge (Problems 21-25)

**21. String Manipulation Program**
Write a program that:
- Asks for a sentence
- Prints it in uppercase
- Prints the first 5 characters
- Prints the last 5 characters
- Prints it reversed

**22. Temperature Converter**
Write a program that:
- Asks for temperature in Celsius
- Converts to Fahrenheit: F = (C × 9/5) + 32
- Displays result formatted to 1 decimal place

**23. Discount Calculator**
Write a program that:
- Asks for original price and discount percentage
- Calculates discount amount
- Calculates final price
- Displays itemized breakdown with proper currency formatting

**24. Pythagorean Theorem Solver**
Write a program that:
- Asks for two sides of a right triangle (a and b)
- Calculates hypotenuse: c = √(a² + b²)
- Uses `math.sqrt()`
- Displays result with 2 decimal places

**25. Comprehensive Calculator**
Write a program that:
- Asks user to choose: Temperature, Distance, or Price calculation
- Performs the selected conversion/calculation
- Displays formatted results
- Asks if user wants another calculation
- Repeats until user quits

---

## Answer Key

### Tier 1 Solutions

**1. Variable Declaration:**
```python
color = "blue"
color = "red"
print(color)  # "red"
```

**2. Order of Operations:**
```
(15 + 5) * 2 - 10
= 20 * 2 - 10
= 40 - 10
= 30
```

**3. String Concatenation:**
```python
result = "Hello" + " " + "World"
print(result)  # "Hello World"
```

**4. Indexing:**
```python
word = "Programming"
print(word[3])  # "g"
```

**5. Length:**
```python
print(len("Computer Science"))  # 17
```

**6. Slicing:**
```python
text = "Python"
print(text[2:5])  # "tho"
```

**7. Type Conversion:**
```python
result = int("99") + 1
print(result)  # 100
```

**8. Uppercase:**
```python
print("hello world".upper())  # "HELLO WORLD"
```

**9. Comparison:**
```python
print(10 < 15)  # True
```

**10. F-String:**
```python
price = 19.99
print(f"${price:.2f}")  # "$19.99"
```

### Tier 2 Solutions

**11. Compound Assignment:**
```python
x = 50
x += 10   # x = 60
print(x)
x -= 5    # x = 55
print(x)
x *= 2    # x = 110
print(x)
```

**12. Slicing with Step:**
```python
word = "Programming"
print(word[::2])  # "Pormig"
```

**13. Method Chaining:**
```python
result = "  HELLO  ".strip().lower().title()
print(result)  # "Hello"
```

**14. Multiple Assignment & Swap:**
```python
a, b = 10, 20
print(f"Before: a={a}, b={b}")
a, b = b, a
print(f"After: a={a}, b={b}")
```

**15. Operator Precedence:**
```
2 + 3 * 4 - 5 // 2
= 2 + 12 - 2
= 14 - 2
= 12
```

**16. Float Conversion:**
```python
print(int(7.8))  # 7
# Truncates (cuts off) decimals, doesn't round
```

**17. Circle Area:**
```python
import math
radius = float(input("Radius: "))
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")
```

**18. String Finding:**
```python
index = "banana".find("an")
print(index)  # 1
```

**19. String Counting:**
```python
count = "hello world".count("l")
print(count)  # 3
```

**20. Currency Formatting:**
```python
amounts = [1234.5, 50.1, 999999.99]
for amt in amounts:
    print(f"${amt:,.2f}")
# Output: $1,234.50 | $50.10 | $999,999.99
```

### Tier 3 Solutions

**21. String Manipulation:**
```python
sentence = input("Enter a sentence: ")
print(sentence.upper())
print(sentence[:5])
print(sentence[-5:])
print(sentence[::-1])
```

**22. Temperature Converter:**
```python
celsius = float(input("Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"Fahrenheit: {fahrenheit:.1f}")
```

**23. Discount Calculator:**
```python
original = float(input("Original price: $"))
discount_pct = float(input("Discount (%): "))
discount_amt = original * (discount_pct / 100)
final = original - discount_amt

print(f"Original: ${original:.2f}")
print(f"Discount ({discount_pct}%): ${discount_amt:.2f}")
print(f"Final: ${final:.2f}")
```

**24. Pythagorean Theorem:**
```python
import math
a = float(input("Side a: "))
b = float(input("Side b: "))
c = math.sqrt(a**2 + b**2)
print(f"Hypotenuse: {c:.2f}")
```

**25. Comprehensive Calculator:**
```python
while True:
    print("\n=== Calculator Menu ===")
    print("1) Temperature")
    print("2) Distance")
    print("3) Price")
    print("4) Exit")

    choice = input("Choose (1-4): ")

    if choice == "1":
        c = float(input("Celsius: "))
        f = (c * 9/5) + 32
        print(f"Fahrenheit: {f:.1f}")
    elif choice == "2":
        m = float(input("Meters: "))
        ft = m * 3.28084
        print(f"Feet: {ft:.2f}")
    elif choice == "3":
        price = float(input("Price: $"))
        tax = price * 0.08
        total = price + tax
        print(f"Total: ${total:.2f}")
    elif choice == "4":
        break
    else:
        print("Invalid choice")
```

---

**Use these problems to practice daily. Mastery comes from repetition and testing your understanding!**
