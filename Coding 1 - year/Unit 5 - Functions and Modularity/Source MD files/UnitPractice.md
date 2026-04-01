# Unit 5: Practice Problems (25 Problems with Solutions)

Extra practice problems covering all topics in Unit 5. Use these to prepare for assessment or to deepen your understanding.

---

## Problems 1–5: Basic Function Definition and Calling

### Problem 1
Write a function called `say_goodbye()` that prints "Goodbye!" Call it once.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def say_goodbye():
    print("Goodbye!")

say_goodbye()
```
</details>

---

### Problem 2
Write a function called `print_numbers()` that prints the numbers 1, 2, 3 on separate lines. Call it once.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def print_numbers():
    print(1)
    print(2)
    print(3)

print_numbers()
```
</details>

---

### Problem 3
Write a function called `make_box()` that prints a 3x3 box of asterisks:
```
***
***
***
```
Call it once.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def make_box():
    print("***")
    print("***")
    print("***")

make_box()
```
</details>

---

### Problem 4
Write a function called `greet_twice()` that prints "Hello!" twice (two separate lines). Call it once.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def greet_twice():
    print("Hello!")
    print("Hello!")

greet_twice()
```
</details>

---

### Problem 5
Write a function called `count_up()` that prints 1, 2, 3, 4, 5 on separate lines. Call it once.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def count_up():
    for i in range(1, 6):
        print(i)

count_up()
```
</details>

---

## Problems 6–10: Parameters and Arguments

### Problem 6
Write a function `print_name(name)` that prints "Hello, [name]!" Call it with your name.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def print_name(name):
    print(f"Hello, {name}!")

print_name("Alice")
```
</details>

---

### Problem 7
Write a function `multiply(a, b)` that takes two numbers and prints their product. Call it with 5 and 7.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def multiply(a, b):
    print(a * b)

multiply(5, 7)  # Prints 35
```
</details>

---

### Problem 8
Write a function `repeat(text, times)` that prints the text a certain number of times. Call it to print "Hi" three times.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def repeat(text, times):
    for i in range(times):
        print(text)

repeat("Hi", 3)
```
</details>

---

### Problem 9
Write a function `describe_pet(pet_type, pet_name)` that prints "I have a [pet_type] named [pet_name]." Call it with a dog and cat.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def describe_pet(pet_type, pet_name):
    print(f"I have a {pet_type} named {pet_name}.")

describe_pet("dog", "Buddy")
describe_pet("cat", "Whiskers")
```
</details>

---

### Problem 10
Write a function `print_stars(n)` that prints a line of n stars. Call it with n=5, then n=8.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def print_stars(n):
    print("*" * n)

print_stars(5)  # *****
print_stars(8)  # ********
```
</details>

---

## Problems 11–15: Return Values

### Problem 11
Write a function `add(a, b)` that returns the sum of a and b. Store the result in a variable and print it.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)  # 30
```
</details>

---

### Problem 12
Write a function `double(n)` that returns n multiplied by 2. Call it with 5 and print the result.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def double(n):
    return n * 2

result = double(5)
print(result)  # 10
```
</details>

---

### Problem 13
Write a function `is_positive(n)` that returns `True` if n > 0, `False` otherwise. Test with 5, 0, and -3.

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def is_positive(n):
    return n > 0

print(is_positive(5))   # True
print(is_positive(0))   # False
print(is_positive(-3))  # False
```
</details>

---

### Problem 14
Write a function `first_letter(word)` that returns the first letter of a word. Test with "Python" and "Code".

**Difficulty:** Beginner

<details>
<summary>Solution</summary>

```python
def first_letter(word):
    return word[0]

print(first_letter("Python"))  # P
print(first_letter("Code"))    # C
```
</details>

---

### Problem 15
Write a function `absolute_value(n)` that returns the absolute value of n (use abs() or if/else). Test with -7 and 3.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def absolute_value(n):
    if n < 0:
        return -n
    else:
        return n

print(absolute_value(-7))  # 7
print(absolute_value(3))   # 3
```
</details>

---

## Problems 16–20: Scope and Composition

### Problem 16
What does this print? Explain why.
```python
x = 5

def test():
    x = 10
    print(x)

test()
print(x)
```

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

Prints:
```
10
5
```

**Explanation:** Inside test(), `x = 10` creates a local variable that shadows the global `x`. The function prints the local 10. Outside the function, the global `x` is still 5.
</details>

---

### Problem 17
Write a function `square(n)` that returns n². Write a function `add_ten(n)` that returns n+10. Then write a function that returns square(add_ten(n)). Test with n=5.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def square(n):
    return n * n

def add_ten(n):
    return n + 10

def compose(n):
    return square(add_ten(n))

print(compose(5))  # square(15) = 225
```
</details>

---

### Problem 18
What does this print?
```python
def double(x):
    return x * 2

def add_five(x):
    return x + 5

result = add_five(double(3))
print(result)
```

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

Prints:
```
11
```

**Explanation:** double(3) = 6, add_five(6) = 11
</details>

---

### Problem 19
Write a function `get_initials(first, last)` that returns the initials (e.g., "John Doe" → "JD"). Use a helper function `first_letter()`.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def first_letter(word):
    return word[0]

def get_initials(first, last):
    return first_letter(first) + first_letter(last)

print(get_initials("John", "Doe"))  # JD
```
</details>

---

### Problem 20
Write three functions: `celsius_to_fahrenheit(c)`, `round_temp(f)`, and `convert_and_round(c)` that combines them. Test with 0°C.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

def round_temp(f):
    return round(f, 1)

def convert_and_round(c):
    f = celsius_to_fahrenheit(c)
    return round_temp(f)

print(convert_and_round(0))    # 32.0
print(convert_and_round(100))  # 212.0
```
</details>

---

## Problems 21–25: Lists, Loops, and Conditionals in Functions

### Problem 21
Write a function `sum_list(numbers)` that returns the sum of all numbers in a list. Test with [1, 2, 3, 4, 5].

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def sum_list(numbers):
    total = 0
    for num in numbers:
        total = total + num
    return total

print(sum_list([1, 2, 3, 4, 5]))  # 15
```
</details>

---

### Problem 22
Write a function `count_evens(numbers)` that returns how many even numbers are in a list. Test with [1, 2, 3, 4, 5, 6].

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def count_evens(numbers):
    count = 0
    for num in numbers:
        if num % 2 == 0:
            count = count + 1
    return count

print(count_evens([1, 2, 3, 4, 5, 6]))  # 3
```
</details>

---

### Problem 23
Write a function `get_long_words(words, min_length)` that returns only words with at least min_length characters. Test with ["hi", "hello", "bye", "goodbye"] and min_length=4.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def get_long_words(words, min_length):
    result = []
    for word in words:
        if len(word) >= min_length:
            result.append(word)
    return result

print(get_long_words(["hi", "hello", "bye", "goodbye"], 4))
# ['hello', 'goodbye']
```
</details>

---

### Problem 24
Write a function `classify_score(score)` that returns:
- "A" if score >= 90
- "B" if score >= 80
- "C" if score >= 70
- "D" if score >= 60
- "F" otherwise

Test with 85, 92, 70, and 55.

**Difficulty:** Intermediate

<details>
<summary>Solution</summary>

```python
def classify_score(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

print(classify_score(85))  # B
print(classify_score(92))  # A
print(classify_score(70))  # C
print(classify_score(55))  # F
```
</details>

---

### Problem 25 (Challenge)
Write a function `remove_duplicates(items)` that returns a new list with duplicate items removed, preserving order. Test with [1, 2, 2, 3, 1, 4, 3].

**Difficulty:** Challenge

<details>
<summary>Solution</summary>

```python
def remove_duplicates(items):
    seen = []
    result = []
    for item in items:
        if item not in seen:
            result.append(item)
            seen.append(item)
    return result

print(remove_duplicates([1, 2, 2, 3, 1, 4, 3]))
# [1, 2, 3, 4]
```
</details>

---

## Answer Summary

| Problem | Topic | Solution Concept |
|---------|-------|------------------|
| 1–5 | Basic Functions | Function definition, calling, loops |
| 6–10 | Parameters | Passing arguments, using parameters |
| 11–15 | Return Values | Returning data, capturing results |
| 16–20 | Scope & Composition | Local/global scope, function calls |
| 21–25 | Data Structures | Lists, loops, conditionals in functions |

---

*These problems are cumulative. Later problems combine skills from earlier topics.*

---
