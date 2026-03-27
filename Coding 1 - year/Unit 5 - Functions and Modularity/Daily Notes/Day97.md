# Day 97: Parameters and Arguments

**Learning Target:** I can write functions with parameters and call them by passing arguments.

### Key Concepts

A **parameter** is a variable that appears in the function definition. An **argument** is the actual value you pass when you call the function. Parameters let functions work with different data.

Example: In the function definition `def greet(name):`, the word `name` is the **parameter**. When you call `greet("Alice")`, the string `"Alice"` is the **argument**. Inside the function, `name` becomes `"Alice"`.

**Why parameters matter:** Without parameters, a function can only do one thing with one set of data. With parameters, the same function can work with many different inputs. A function that adds two numbers is much more useful if you can pass any two numbers to it, rather than hard-coding the same two numbers.

To define a parameter, put the variable name inside the parentheses in the `def` line:
```
def function_name(parameter):
    # Use parameter in the function body
```

To call a function with an argument, pass the value in parentheses:
```
function_name(argument)
```

The parameter acts as a **local variable** inside the function—it only exists while the function is running. Each time you call the function, the parameter gets a new value.

You can also have **multiple parameters**, separated by commas:
```
def add_numbers(a, b):
    result = a + b
    print(result)

add_numbers(5, 3)  # Prints 8
add_numbers(10, 20)  # Prints 30
```

### Code Examples

```python
# Example 1: Single parameter
def print_name(name):
    print("Hello, " + name + "!")

print_name("Alice")  # Hello, Alice!
print_name("Bob")    # Hello, Bob!
```

```python
# Example 2: Multiple parameters
def multiply(x, y):
    result = x * y
    print(f"{x} times {y} equals {result}")

multiply(4, 5)   # 4 times 5 equals 20
multiply(10, 3)  # 10 times 3 equals 30
```

```python
# Example 3: Parameters with different types
def print_info(name, age, city):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"City: {city}")

print_info("Zach", 16, "Portland")
print_info("Maya", 17, "Seattle")
```

### Guided Practice

1. Write a function `square(n)` that takes one parameter and prints the square of that number.
2. Test it by calling `square(5)` and `square(12)`.
3. Write a function `describe_pet(pet_type, pet_name)` that takes two parameters and prints a sentence like "I have a dog named Buddy."
4. Test it with at least two different animals and names.

### Practice Problems

**Problem 1 — Beginner:** Write a function `say_name(first, last)` that takes a first name and last name as parameters and prints them together (e.g., "First name: Alice, Last name: Smith"). Call it three times with different names.

```python
# Starter code
def say_name(first, last):
    # Your code here
    pass

# Call the function here
```

**Problem 2 — Intermediate:** Write a function `calculate_cost(quantity, price_per_item)` that takes a quantity and a price and prints the total cost. Call it at least three times with different values.

**Problem 3 — Challenge:** Write a function `greet_formally(title, name, year)` that takes three parameters and prints a formal greeting like "Good morning, Dr. Smith, Class of 2026." Be creative with the greeting!

<details>
<summary>💡 Hints</summary>

- Problem 1: Use string concatenation or f-strings to combine the names.
- Problem 2: Multiply the quantity by the price. Use f-strings to format the output nicely.
- Problem 3: Think about what makes a greeting formal. Use titles and dates to make it realistic.
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
def say_name(first, last):
    print(f"First name: {first}, Last name: {last}")

say_name("Alice", "Smith")
say_name("Bob", "Johnson")
say_name("Charlie", "Brown")
```

```python
# Problem 2 Example
def calculate_cost(quantity, price_per_item):
    total = quantity * price_per_item
    print(f"{quantity} items at ${price_per_item} each = ${total}")

calculate_cost(5, 10)    # 5 items at $10 each = $50
calculate_cost(3, 15)    # 3 items at $15 each = $45
calculate_cost(12, 2.50) # 12 items at $2.5 each = $30.0
```

```python
# Problem 3 Example
def greet_formally(title, name, year):
    print(f"Good morning, {title} {name}, Class of {year}.")

greet_formally("Dr.", "Smith", 2026)
greet_formally("Prof.", "Johnson", 2025)
greet_formally("Ms.", "Garcia", 2027)
```
</details>

---
