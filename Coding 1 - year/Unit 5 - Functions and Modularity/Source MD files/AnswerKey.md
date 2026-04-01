# Unit 5 Answer Key — 25 Problems

## Problems 1-5: Basic Function Definition and Calling

---

## Problem 1: Say Goodbye Function

Write a function called `say_goodbye()` that prints "Goodbye!" Call it once.

### Solution
```python
# Define the function
def say_goodbye():
    print("Goodbye!")

# Call the function
say_goodbye()
```

### Expected Output
```
Goodbye!
```

### Common Mistakes
- Forgetting the parentheses in the function definition and/or call
- Forgetting to indent the function body
- Not calling the function after defining it

---

## Problem 2: Print Numbers Function

Write a function called `print_numbers()` that prints the numbers 1, 2, 3 on separate lines. Call it once.

### Solution
```python
# Define the function
def print_numbers():
    print(1)
    print(2)
    print(3)

# Call the function
print_numbers()
```

### Expected Output
```
1
2
3
```

### Common Mistakes
- Using commas instead of separate print statements
- Not indenting the function body properly

---

## Problem 3: Make Box Function

Write a function called `make_box()` that prints a 3x3 box of asterisks:
```
***
***
***
```
Call it once.

### Solution
```python
# Define the function
def make_box():
    print("***")
    print("***")
    print("***")

# Call the function
make_box()
```

### Expected Output
```
***
***
***
```

### Common Mistakes
- Using loops instead of three print statements (for this simple version)
- Not maintaining the exact format

---

## Problem 4: Greet Twice Function

Write a function called `greet_twice()` that prints "Hello!" twice (two separate lines). Call it once.

### Solution
```python
# Define the function
def greet_twice():
    print("Hello!")
    print("Hello!")

# Call the function
greet_twice()
```

### Expected Output
```
Hello!
Hello!
```

### Common Mistakes
- Using a for loop instead of two print statements
- Printing on the same line

---

## Problem 5: Count Up Function

Write a function called `count_up()` that prints 1, 2, 3, 4, 5 on separate lines. Call it once.

### Solution
```python
# Define the function
def count_up():
    for i in range(1, 6):
        print(i)

# Call the function
count_up()
```

### Expected Output
```
1
2
3
4
5
```

### Common Mistakes
- Using range(1, 5) instead of range(1, 6) (off-by-one error)
- Not indenting the for loop body

---

## Problems 6-10: Parameters and Arguments

---

## Problem 6: Print Name Function

Write a function `print_name(name)` that prints "Hello, [name]!" Call it with your name.

### Solution
```python
# Define the function with parameter
def print_name(name):
    print(f"Hello, {name}!")

# Call the function with an argument
print_name("Alice")
```

### Expected Output
```
Hello, Alice!
```

### Common Mistakes
- Not using the parameter in the function body
- Not passing an argument when calling the function
- Forgetting the parentheses in the function call

---

## Problem 7: Multiply Function

Write a function `multiply(a, b)` that takes two numbers and prints their product. Call it with 5 and 7.

### Solution
```python
# Define the function with parameters
def multiply(a, b):
    print(a * b)

# Call the function
multiply(5, 7)  # Prints 35
```

### Expected Output
```
35
```

### Common Mistakes
- Not multiplying inside the function
- Not printing the result
- Calling with wrong arguments

---

## Problem 8: Repeat Function

Write a function `repeat(text, times)` that prints the text a certain number of times. Call it to print "Hi" three times.

### Solution
```python
# Define the function with parameters
def repeat(text, times):
    for i in range(times):
        print(text)

# Call the function
repeat("Hi", 3)
```

### Expected Output
```
Hi
Hi
Hi
```

### Common Mistakes
- Not using a loop to repeat
- Using wrong variable names
- Off-by-one error in the loop

---

## Problem 9: Describe Pet Function

Write a function `describe_pet(pet_type, pet_name)` that prints "I have a [pet_type] named [pet_name]." Call it with a dog and cat.

### Solution
```python
# Define the function with parameters
def describe_pet(pet_type, pet_name):
    print(f"I have a {pet_type} named {pet_name}.")

# Call the function twice
describe_pet("dog", "Buddy")
describe_pet("cat", "Whiskers")
```

### Expected Output
```
I have a dog named Buddy.
I have a cat named Whiskers.
```

### Common Mistakes
- Not calling the function twice
- Not using f-strings for formatting
- Swapping parameter order

---

## Problem 10: Print Stars Function

Write a function `print_stars(n)` that prints a line of n stars. Call it with n=5, then n=8.

### Solution
```python
# Define the function with parameter
def print_stars(n):
    print("*" * n)

# Call the function twice
print_stars(5)  # *****
print_stars(8)  # ********
```

### Expected Output
```
*****
********
```

### Common Mistakes
- Using a loop instead of string multiplication
- Not calling the function twice
- Missing one of the required calls

---

## Problems 11-15: Return Values

---

## Problem 11: Add Function

Write a function `add(a, b)` that returns the sum of a and b. Store the result in a variable and print it.

### Solution
```python
# Define the function with return
def add(a, b):
    return a + b

# Call the function and store result
result = add(10, 20)
print(result)  # 30
```

### Expected Output
```
30
```

### Common Mistakes
- Using print instead of return
- Not storing the result in a variable
- Forgetting to print the result

---

## Problem 12: Double Function

Write a function `double(n)` that returns n multiplied by 2. Call it with 5 and print the result.

### Solution
```python
# Define the function with return
def double(n):
    return n * 2

# Call the function and print result
result = double(5)
print(result)  # 10
```

### Expected Output
```
10
```

### Common Mistakes
- Using += instead of * 2
- Printing inside the function instead of returning
- Not calling the function

---

## Problem 13: Is Positive Function

Write a function `is_positive(n)` that returns `True` if n > 0, `False` otherwise. Test with 5, 0, and -3.

### Solution
```python
# Define the function returning boolean
def is_positive(n):
    return n > 0

# Test with three values
print(is_positive(5))   # True
print(is_positive(0))   # False
print(is_positive(-3))  # False
```

### Expected Output
```
True
False
False
```

### Common Mistakes
- Using if/else instead of directly returning comparison
- Testing with wrong values
- Not printing all three test cases

---

## Problem 14: First Letter Function

Write a function `first_letter(word)` that returns the first letter of a word. Test with "Python" and "Code".

### Solution
```python
# Define the function returning character
def first_letter(word):
    return word[0]

# Test with two values
print(first_letter("Python"))  # P
print(first_letter("Code"))    # C
```

### Expected Output
```
P
C
```

### Common Mistakes
- Using word[1] instead of word[0]
- Not testing with both examples
- Printing inside the function instead of returning

---

## Problem 15: Absolute Value Function

Write a function `absolute_value(n)` that returns the absolute value of n (use abs() or if/else). Test with -7 and 3.

### Solution
```python
# Define the function returning absolute value
def absolute_value(n):
    if n < 0:
        return -n
    else:
        return n

# Test with two values
print(absolute_value(-7))  # 7
print(absolute_value(3))   # 3
```

### Expected Output
```
7
3
```

### Common Mistakes
- Using abs() (though it's fine, the problem might ask for if/else)
- Not returning both positive and negative cases
- Forgetting negative sign reversal

---

## Problems 16-20: Scope and Composition

---

## Problem 16: Scope Question

What does this print? Explain why.
```python
x = 5

def test():
    x = 10
    print(x)

test()
print(x)
```

### Solution
```python
# Global variable
x = 5

def test():
    # Local variable shadows global x
    x = 10
    print(x)  # Prints 10 (local x)

test()
print(x)  # Prints 5 (global x)
```

### Expected Output
```
10
5
```

### Common Mistakes
- Thinking the function modifies the global x
- Not understanding variable scope
- Expecting both print statements to print the same value

---

## Problem 17: Function Composition

Write a function `square(n)` that returns n². Write a function `add_ten(n)` that returns n+10. Then write a function that returns square(add_ten(n)). Test with n=5.

### Solution
```python
# Define helper functions
def square(n):
    return n * n

def add_ten(n):
    return n + 10

# Define composite function
def compose(n):
    return square(add_ten(n))

# Test with n=5
print(compose(5))  # square(15) = 225
```

### Expected Output
```
225
```

### Common Mistakes
- Swapping function order (add_ten(square(n)) gives different result)
- Not nesting function calls correctly
- Not testing with the specified value

---

## Problem 18: Nested Function Calls

What does this print?
```python
def double(x):
    return x * 2

def add_five(x):
    return x + 5

result = add_five(double(3))
print(result)
```

### Solution
```python
def double(x):
    return x * 2

def add_five(x):
    return x + 5

# Step 1: double(3) returns 6
# Step 2: add_five(6) returns 11
result = add_five(double(3))
print(result)
```

### Expected Output
```
11
```

### Common Mistakes
- Calculating wrong order (maybe 20 if you add first)
- Not understanding nested function evaluation

---

## Problem 19: Helper Function (Get Initials)

Write a function `get_initials(first, last)` that returns the initials (e.g., "John Doe" → "JD"). Use a helper function `first_letter()`.

### Solution
```python
# Define helper function
def first_letter(word):
    return word[0]

# Define main function using helper
def get_initials(first, last):
    return first_letter(first) + first_letter(last)

# Test
print(get_initials("John", "Doe"))  # JD
```

### Expected Output
```
JD
```

### Common Mistakes
- Not using the helper function
- Not concatenating the letters
- Using word[0:1] instead of word[0]

---

## Problem 20: Temperature Conversion (Multiple Functions)

Write three functions: `celsius_to_fahrenheit(c)`, `round_temp(f)`, and `convert_and_round(c)` that combines them. Test with 0°C.

### Solution
```python
# Define individual conversion functions
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

def round_temp(f):
    return round(f, 1)

# Define composite function
def convert_and_round(c):
    f = celsius_to_fahrenheit(c)
    return round_temp(f)

# Test
print(convert_and_round(0))    # 32.0
print(convert_and_round(100))  # 212.0
```

### Expected Output
```
32.0
212.0
```

### Common Mistakes
- Wrong conversion formula
- Not using the helper functions
- Not rounding correctly

---

## Problems 21-25: Lists, Loops, and Conditionals in Functions

---

## Problem 21: Sum List Function

Write a function `sum_list(numbers)` that returns the sum of all numbers in a list. Test with [1, 2, 3, 4, 5].

### Solution
```python
# Define the function
def sum_list(numbers):
    total = 0
    for num in numbers:
        total = total + num
    return total

# Test
print(sum_list([1, 2, 3, 4, 5]))  # 15
```

### Expected Output
```
15
```

### Common Mistakes
- Using sum() function (though it works, defeats the learning purpose)
- Not initializing total to 0
- Printing instead of returning

---

## Problem 22: Count Evens Function

Write a function `count_evens(numbers)` that returns how many even numbers are in a list. Test with [1, 2, 3, 4, 5, 6].

### Solution
```python
# Define the function
def count_evens(numbers):
    count = 0
    for num in numbers:
        if num % 2 == 0:
            count = count + 1
    return count

# Test
print(count_evens([1, 2, 3, 4, 5, 6]))  # 3
```

### Expected Output
```
3
```

### Common Mistakes
- Using wrong modulo logic (checking for odd instead)
- Not incrementing count
- Printing instead of returning

---

## Problem 23: Get Long Words Function

Write a function `get_long_words(words, min_length)` that returns only words with at least min_length characters. Test with ["hi", "hello", "bye", "goodbye"] and min_length=4.

### Solution
```python
# Define the function
def get_long_words(words, min_length):
    result = []
    for word in words:
        if len(word) >= min_length:
            result.append(word)
    return result

# Test
print(get_long_words(["hi", "hello", "bye", "goodbye"], 4))
# ['hello', 'goodbye']
```

### Expected Output
```
['hello', 'goodbye']
```

### Common Mistakes
- Not creating a new list for results
- Using wrong comparison (< instead of >=)
- Not appending to result list

---

## Problem 24: Classify Score Function

Write a function `classify_score(score)` that returns:
- "A" if score >= 90
- "B" if score >= 80
- "C" if score >= 70
- "D" if score >= 60
- "F" otherwise

Test with 85, 92, 70, and 55.

### Solution
```python
# Define the function
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

# Test all cases
print(classify_score(85))  # B
print(classify_score(92))  # A
print(classify_score(70))  # C
print(classify_score(55))  # F
```

### Expected Output
```
B
A
C
F
```

### Common Mistakes
- Using overlapping conditions
- Not testing all cases
- Printing inside function instead of returning

---

## Problem 25: Remove Duplicates Function (Challenge)

Write a function `remove_duplicates(items)` that returns a new list with duplicate items removed, preserving order. Test with [1, 2, 2, 3, 1, 4, 3].

### Solution
```python
# Define the function
def remove_duplicates(items):
    seen = []
    result = []
    for item in items:
        if item not in seen:
            result.append(item)
            seen.append(item)
    return result

# Test
print(remove_duplicates([1, 2, 2, 3, 1, 4, 3]))
# [1, 2, 3, 4]
```

### Expected Output
```
[1, 2, 3, 4]
```

### Common Mistakes
- Not preserving order (using set loses order)
- Not checking if item already seen
- Using wrong data structure for tracking seen items

---
