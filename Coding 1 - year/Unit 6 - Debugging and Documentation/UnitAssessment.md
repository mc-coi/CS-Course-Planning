# Unit 6 Assessment — 15 Essential Questions & Answers

## Part 1: Concept & Vocabulary Questions

**Question 1: Explain the difference between a syntax error and a runtime error. Give one example of each.**

Answer: A syntax error occurs before the program runs—Python cannot even parse the code because it violates grammar rules (like missing colons or mismatched quotes). Python immediately tells you where the syntax error is. A runtime error occurs while the program is running—the code is syntactically correct, but something happens that Python can't handle (like dividing by zero or accessing an invalid list index).

Example of syntax error: `print("hello` (missing closing quote)
Example of runtime error: `result = 10 / 0` (ZeroDivisionError)

---

**Question 2: What is a logic error? How is it different from syntax and runtime errors?**

Answer: A logic error is when the code runs without crashing, but it produces the wrong answer. The syntax is correct and no runtime error occurs, but the algorithm or condition is flawed. Logic errors are the hardest to find because Python can't alert you—you have to think through the logic yourself.

Example:
```python
average = (85 + 90 + 78) / 2  # Should divide by 3, not 2
# This runs fine but gives wrong result
```

---

**Question 3: What is a traceback? What information does it give you?**

Answer: A traceback is the error message Python displays when a runtime error occurs. It tells you:
1. The error type (e.g., ValueError, ZeroDivisionError)
2. The file and line number where the error occurred
3. The actual code on that line
4. A message explaining what went wrong

You read tracebacks starting from the bottom line (error type + message), then look at the lines above to see which function calls led to that error.

---

**Question 4: List three common runtime errors and how to fix each.**

Answer:
1. **ZeroDivisionError**: Check that the divisor is not zero before dividing. Example: `if divisor != 0: result = num / divisor`
2. **TypeError**: Wrong data type for an operation. Fix by converting types. Example: `age = int(input("Age: "))` instead of using the string directly
3. **IndexError**: List index out of range. Fix by checking list length. Example: `if index < len(list): item = list[index]`

---

**Question 5: What is a test case? What should it include?**

Answer: A test case is a specific test of a program or function. It includes:
1. **Input** — What you're testing with
2. **Expected output** — What should happen
3. **Actual output** — What really happens
4. **Status** — Pass or fail

Example:
```
Input: is_even(4)
Expected: True
Actual: True
Status: PASS
```

---

## Part 2: Bug Fixing Questions

**Question 6: Find and fix all errors in this program:**
```python
def calculate_average(scores):
    total = sum(scores)
    average = total / len(scores)

result = calculate_average([85, 90, 78]
print(result)
```

Answer: There are 2 errors:
1. **Line 5:** Missing closing parenthesis on `calculate_average([85, 90, 78]` — should be `([85, 90, 78])`
2. **Logical issue:** The function doesn't have a return statement, so it returns None

Fixed version:
```python
def calculate_average(scores):
    total = sum(scores)
    average = total / len(scores)
    return average  # Added return statement

result = calculate_average([85, 90, 78])  # Fixed: added closing paren
print(result)  # Prints 84.33...
```

---

**Question 7: Debug this program using print statements and fix the bug:**
```python
numbers = [2, 5, 8, 3, 10]
even_sum = 0
for num in numbers:
    if num % 2 == 0:
        even_sum = even_sum + num
print(f"Sum: {even_sum}")
```

Answer: Add print statements to trace:
```python
numbers = [2, 5, 8, 3, 10]
even_sum = 0
for num in numbers:
    print(f"DEBUG: Checking {num}")
    if num % 2 == 0:
        print(f"DEBUG: {num} is even, adding")
        even_sum = even_sum + num
    print(f"DEBUG: even_sum = {even_sum}")
print(f"Sum: {even_sum}")  # Should print 20
```

The code is actually correct (no bug). It prints 20, which is the sum of even numbers (2+8+10).

---

**Question 8: Fix this program to handle division by zero:**
```python
num1 = int(input("First number: "))
num2 = int(input("Second number: "))
result = num1 / num2
print(result)
```

Answer:
```python
try:
    num1 = int(input("First number: "))
    num2 = int(input("Second number: "))
    if num2 == 0:
        print("Cannot divide by zero")
    else:
        result = num1 / num2
        print(result)
except ValueError:
    print("Please enter valid numbers")
```

---

## Part 3: File I/O Questions

**Question 9: Write a program that reads a file called `grades.txt` (one grade per line) and prints the average.**

Answer:
```python
try:
    with open("grades.txt", "r") as file:
        grades = []
        for line in file:
            grades.append(float(line.strip()))

        if grades:
            average = sum(grades) / len(grades)
            print(f"Average: {average:.2f}")
        else:
            print("No grades found")
except FileNotFoundError:
    print("File not found")
except ValueError:
    print("File contains non-numeric values")
```

---

**Question 10: Write a program that reads a CSV file with format `name,score` and writes a new file with only students who scored above 80.**

Answer:
```python
try:
    with open("scores.csv", "r") as input_file:
        with open("high_scores.csv", "w") as output_file:
            for line in input_file:
                parts = line.strip().split(",")
                if len(parts) == 2:
                    name = parts[0]
                    score = int(parts[1])
                    if score > 80:
                        output_file.write(f"{name},{score}\n")
    print("High scores written to high_scores.csv")
except FileNotFoundError:
    print("Input file not found")
except ValueError:
    print("Invalid score format")
```

---

## Part 4: Documentation Questions

**Question 11: Add a docstring and comments to this function:**
```python
def is_palindrome(text):
    text = text.lower().replace(" ", "")
    return text == text[::-1]
```

Answer:
```python
def is_palindrome(text):
    """
    Check if a text string is a palindrome (reads same forwards and backwards).

    Args:
        text: The string to check

    Returns:
        True if the text is a palindrome, False otherwise
    """
    # Convert to lowercase and remove spaces
    text = text.lower().replace(" ", "")
    # Check if text equals its reverse ([::-1])
    return text == text[::-1]
```

---

**Question 12: What naming convention should be used for each of these?**
- a) A variable that stores a student's GPA
- b) A function that calculates total cost
- c) A constant for the maximum grade

Answer:
- a) `student_gpa` (lowercase with underscores)
- b) `calculate_total_cost()` (lowercase with underscores)
- c) `MAX_GRADE` (UPPERCASE with underscores)

---

**Question 13: Write three "good" comments for this code:**
```python
total = 0
for item in cart:
    total = total + item["price"]
```

Answer:
```python
# Initialize total to zero
total = 0
# Loop through each item in the shopping cart
for item in cart:
    # Add this item's price to the running total
    total = total + item["price"]
```

---

**Question 14: Identify edge cases for a function that calculates the maximum in a list. Provide test cases.**

Answer: Edge cases:
1. Empty list — should handle gracefully (return None or error)
2. Single item — should return that item
3. All same values — should return that value
4. Negative numbers — should work correctly
5. Mixed positive and negative — should work correctly

Test cases:
```
Input: [], Expected: None (or error)
Input: [5], Expected: 5
Input: [3, 3, 3], Expected: 3
Input: [-5, -10, -2], Expected: -2
Input: [-5, 10, 3, -2], Expected: 10
```

---

**Question 15: Create a complete, well-documented program that:**
- Reads numbers from a file (one per line)
- Calculates the sum, average, and count
- Handles all errors gracefully
- Has clear variable names, comments, and a docstring

Answer:
```python
def analyze_numbers(filename):
    """
    Read numbers from a file and calculate statistics.

    Args:
        filename: Name of file containing numbers (one per line)

    Returns:
        Dictionary with keys: count, sum, average
        Returns None if file not found or is empty
    """
    try:
        with open(filename, "r") as file:
            numbers = []
            # Read each line and convert to float
            for line in file:
                try:
                    number = float(line.strip())
                    numbers.append(number)
                except ValueError:
                    print(f"Skipping invalid value: {line.strip()}")

        # Handle empty file
        if not numbers:
            print("No valid numbers found")
            return None

        # Calculate statistics
        count = len(numbers)
        total_sum = sum(numbers)
        average = total_sum / count

        return {
            "count": count,
            "sum": total_sum,
            "average": average
        }

    except FileNotFoundError:
        print(f"Error: {filename} not found")
        return None
    except IOError:
        print("Error reading file")
        return None

# Main program
result = analyze_numbers("numbers.txt")
if result:
    print(f"Count: {result['count']}")
    print(f"Sum: {result['sum']}")
    print(f"Average: {result['average']:.2f}")
```

---
