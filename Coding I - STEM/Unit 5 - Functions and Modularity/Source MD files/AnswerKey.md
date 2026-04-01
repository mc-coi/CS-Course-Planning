# Unit 5: Functions and Modularity - Answer Key

---

## Problem 1: Say Hello Function

### Solution
```python
def say_hello(name):
    """Print a greeting with the given name."""
    print(f"Hello, {name}!")

# Call it three times
say_hello("Alice")
say_hello("Bob")
say_hello("Charlie")
```

### Expected Output
```
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

### Common Mistakes
- Returning instead of printing
- Not using f-strings or string formatting
- Forgetting to define the function before calling it
- Not passing the parameter correctly

---

## Problem 2: Square Function (Return)

### Solution
```python
def square(n):
    """Return n squared."""
    return n ** 2

# Store and print the result
result = square(5)
print(f"5 squared = {result}")

# Try with other values
print(f"10 squared = {square(10)}")
print(f"3 squared = {square(3)}")
```

### Expected Output
```
5 squared = 25
10 squared = 100
3 squared = 9
```

### Common Mistakes
- Using print instead of return
- Not storing the result in a variable
- Forgetting to actually call the function
- Using wrong operator (square root instead of squaring)

---

## Problem 3: Is Odd Function

### Solution
```python
def is_odd(n):
    """Return True if n is odd, False if even."""
    return n % 2 == 1

# Test the function
print(f"5 is odd: {is_odd(5)}")
print(f"4 is odd: {is_odd(4)}")
print(f"0 is odd: {is_odd(0)}")
print(f"-3 is odd: {is_odd(-3)}")
```

### Expected Output
```
5 is odd: True
4 is odd: False
0 is odd: False
-3 is odd: True
```

### Common Mistakes
- Using "odd" as the condition (% 2 != 0 is more reliable)
- Not returning a boolean value
- Using == 1 which fails for negative odd numbers
- Printing instead of returning

---

## Problem 4: Full Name Function

### Solution
```python
def full_name(first, last):
    """Return the full name by combining first and last names."""
    return f"{first} {last}"

# Test the function
name1 = full_name("John", "Doe")
print(name1)

name2 = full_name("Alice", "Smith")
print(name2)

print(full_name("Robert", "Johnson"))
```

### Expected Output
```
John Doe
Alice Smith
Robert Johnson
```

### Common Mistakes
- Printing instead of returning
- Forgetting the space between first and last names
- Not using proper string formatting
- Returning the parameters in wrong order

---

## Problem 5: Bigger Function

### Solution
```python
def bigger(a, b):
    """Return the larger of two numbers."""
    if a > b:
        return a
    else:
        return b

# Test the function
print(f"bigger(10, 5) = {bigger(10, 5)}")
print(f"bigger(3, 8) = {bigger(3, 8)}")
print(f"bigger(7, 7) = {bigger(7, 7)}")

# Alternative using max()
def bigger_alt(a, b):
    return max(a, b)

print(f"Using max: {bigger_alt(10, 5)}")
```

### Expected Output
```
bigger(10, 5) = 10
bigger(3, 8) = 8
bigger(7, 7) = 7
Using max: 10
```

### Common Mistakes
- Returning both values instead of one
- Using wrong comparison operator (< instead of >)
- Not handling equal values correctly
- Forgetting to return anything

---

## Problem 6: Clamp Function

### Solution
```python
def clamp(value, low, high):
    """Return value clamped between low and high."""
    if value < low:
        return low
    elif value > high:
        return high
    else:
        return value

# Test the function
print(f"clamp(50, 0, 100) = {clamp(50, 0, 100)}")   # Returns 50
print(f"clamp(-10, 0, 100) = {clamp(-10, 0, 100)}") # Returns 0
print(f"clamp(150, 0, 100) = {clamp(150, 0, 100)}") # Returns 100
```

### Expected Output
```
clamp(50, 0, 100) = 50
clamp(-10, 0, 100) = 0
clamp(150, 0, 100) = 100
```

### Common Mistakes
- Checking conditions in wrong order
- Returning the wrong value for each case
- Not handling all three cases (below, within, above)
- Using wrong comparison operators

---

## Problem 7: Count Vowels Function

### Solution
```python
def count_vowels(text):
    """Return the number of vowels in a string."""
    vowels = "aeiouAEIOU"
    count = 0
    for char in text:
        if char in vowels:
            count += 1
    return count

# Test the function
print(f"count_vowels('Hello') = {count_vowels('Hello')}")
print(f"count_vowels('Python') = {count_vowels('Python')}")
print(f"count_vowels('aeiou') = {count_vowels('aeiou')}")
print(f"count_vowels('xyz') = {count_vowels('xyz')}")

# Alternative using sum
def count_vowels_alt(text):
    vowels = "aeiouAEIOU"
    return sum(1 for char in text if char in vowels)

print(f"Alternative: {count_vowels_alt('Hello')}")
```

### Expected Output
```
count_vowels('Hello') = 2
count_vowels('Python') = 1
count_vowels('aeiou') = 5
count_vowels('xyz') = 0
Alternative: 2
```

### Common Mistakes
- Not including both uppercase and lowercase vowels
- Starting count at 1 instead of 0
- Not checking if character is in vowels correctly
- Returning inside the loop instead of after

---

## Problem 8: List Stats Function

### Solution
```python
def list_stats(numbers):
    """Return tuple of (sum, average, min, max) for a list."""
    if not numbers:
        return None

    total = sum(numbers)
    average = total / len(numbers)
    minimum = min(numbers)
    maximum = max(numbers)

    return (total, average, minimum, maximum)

# Test the function
result = list_stats([10, 20, 30, 40, 50])
print(f"Stats for [10, 20, 30, 40, 50]:")
print(f"  Sum: {result[0]}")
print(f"  Average: {result[1]}")
print(f"  Min: {result[2]}")
print(f"  Max: {result[3]}")

# Using tuple unpacking
total, avg, min_val, max_val = list_stats([5, 15, 25])
print(f"\nStats for [5, 15, 25]:")
print(f"  Sum: {total}, Average: {avg}, Min: {min_val}, Max: {max_val}")
```

### Expected Output
```
Stats for [10, 20, 30, 40, 50]:
  Sum: 150
  Average: 30.0
  Min: 10
  Max: 50

Stats for [5, 15, 25]:
  Sum: 45, Average: 15.0, Min: 5, Max: 25
```

### Common Mistakes
- Not returning a tuple (returning list or unpacked values)
- Not checking for empty list
- Wrong order in tuple
- Returning wrong calculations

---

## Problem 9: Temperature Converter with Default Parameter

### Solution
```python
def temperature_converter(temp, scale="C"):
    """Convert temperature.
    If scale='C', convert Celsius to Fahrenheit.
    If scale='F', convert Fahrenheit to Celsius.
    """
    if scale == "C":
        # Convert Celsius to Fahrenheit: F = C * 9/5 + 32
        return temp * 9/5 + 32
    elif scale == "F":
        # Convert Fahrenheit to Celsius: C = (F - 32) * 5/9
        return (temp - 32) * 5/9
    else:
        return None

# Test the function
print(f"0°C = {temperature_converter(0)}°F")      # Default scale="C"
print(f"100°C = {temperature_converter(100)}°F")  # Default scale="C"
print(f"32°F = {temperature_converter(32, 'F')}°C")
print(f"212°F = {temperature_converter(212, 'F')}°C")
```

### Expected Output
```
0°C = 32.0°F
100°C = 212.0°F
32°F = 0.0°C
212°F = 100.0°C
```

### Common Mistakes
- Forgetting the default parameter (scale="C")
- Using wrong conversion formulas
- Forgetting to handle both directions (C to F and F to C)
- Not checking the scale parameter correctly

---

## Problem 10: Calculator with Function Dispatch

### Solution
```python
def add(a, b):
    """Return sum of a and b."""
    return a + b

def subtract(a, b):
    """Return difference of a and b."""
    return a - b

def multiply(a, b):
    """Return product of a and b."""
    return a * b

def calculate(a, op, b):
    """Call the appropriate function based on operator."""
    if op == "+":
        return add(a, b)
    elif op == "-":
        return subtract(a, b)
    elif op == "*":
        return multiply(a, b)
    else:
        return None

# Test the functions
print(f"5 + 3 = {calculate(5, '+', 3)}")
print(f"5 - 3 = {calculate(5, '-', 3)}")
print(f"5 * 3 = {calculate(5, '*', 3)}")

# Test individual functions
print(f"\nDirect calls:")
print(f"add(10, 20) = {add(10, 20)}")
print(f"subtract(20, 5) = {subtract(20, 5)}")
print(f"multiply(4, 7) = {multiply(4, 7)}")
```

### Expected Output
```
5 + 3 = 8
5 - 3 = 2
5 * 3 = 15

Direct calls:
add(10, 20) = 30
subtract(20, 5) = 15
multiply(4, 7) = 28
```

### Common Mistakes
- Not defining separate helper functions
- Using wrong operators in calculate function
- Not checking all operation types
- Hardcoding logic instead of calling functions

---

## Problem 11: Modular Word Counter

### Solution
```python
def get_text():
    """Prompt user for text input."""
    return input("Enter some text: ")

def count_words(text):
    """Return the total number of words."""
    return len(text.split())

def count_unique(text):
    """Return the number of unique words."""
    words = text.lower().split()
    return len(set(words))

def print_word_report(text):
    """Print a report of word statistics."""
    total = count_words(text)
    unique = count_unique(text)
    print(f"\nWord Report:")
    print(f"  Total words: {total}")
    print(f"  Unique words: {unique}")

# Main program
text = get_text()
print_word_report(text)
```

### Expected Output
```
Enter some text: the quick brown fox jumps over the lazy dog
Word Report:
  Total words: 8
  Unique words: 8
```

### Common Mistakes
- Not separating concerns into different functions
- Not converting to lowercase before finding unique words
- Using list instead of set for unique counting
- Not handling punctuation

---

## Problem 12: Flatten Nested List

### Solution
```python
def flatten(nested_list):
    """Convert a list of lists into a single flat list."""
    result = []
    for sublist in nested_list:
        for item in sublist:
            result.append(item)
    return result

# Test the function
result1 = flatten([[1, 2], [3, 4], [5]])
print(f"flatten([[1, 2], [3, 4], [5]]) = {result1}")

result2 = flatten([['a', 'b'], ['c'], ['d', 'e', 'f']])
print(f"flatten([['a', 'b'], ['c'], ['d', 'e', 'f']]) = {result2}")

# Alternative using list comprehension
def flatten_alt(nested_list):
    return [item for sublist in nested_list for item in sublist]

print(f"Alternative: {flatten_alt([[1, 2], [3, 4]])}")
```

### Expected Output
```
flatten([[1, 2], [3, 4], [5]]) = [1, 2, 3, 4, 5]
flatten([['a', 'b'], ['c'], ['d', 'e', 'f']]) = ['a', 'b', 'c', 'd', 'e', 'f']
Alternative: [1, 2, 3, 4]
```

### Common Mistakes
- Using one loop instead of nested loops
- Not appending items to result list
- Appending the sublist instead of individual items
- Not returning the flattened list

---

## Problem 13: Run Length Encoding

### Solution
```python
def run_length_encode(text):
    """Return list of (char, count) tuples for run-length encoding."""
    if not text:
        return []

    result = []
    current_char = text[0]
    count = 1

    for i in range(1, len(text)):
        if text[i] == current_char:
            count += 1
        else:
            result.append((current_char, count))
            current_char = text[i]
            count = 1

    # Don't forget the last run
    result.append((current_char, count))
    return result

# Test the function
print(f"run_length_encode('aaabbc') = {run_length_encode('aaabbc')}")
print(f"run_length_encode('aabbccddee') = {run_length_encode('aabbccddee')}")
print(f"run_length_encode('aaaa') = {run_length_encode('aaaa')}")
print(f"run_length_encode('a') = {run_length_encode('a')}")
```

### Expected Output
```
run_length_encode('aaabbc') = [('a', 3), ('b', 2), ('c', 1)]
run_length_encode('aabbccddee') = [('a', 2), ('b', 2), ('c', 2), ('d', 2), ('e', 2)]
run_length_encode('aaaa') = [('a', 4)]
run_length_encode('a') = [('a', 1)]
```

### Common Mistakes
- Not appending the last run after loop ends
- Resetting count to 0 instead of 1
- Not checking if characters match before incrementing
- Creating tuples in wrong order (count, char) instead of (char, count)

---

## Problem 14: Caesar Cipher

### Solution
```python
def encode_char(c, shift):
    """Encode a single character by shifting it."""
    if c.isalpha():
        if c.isupper():
            return chr((ord(c) - ord('A') + shift) % 26 + ord('A'))
        else:
            return chr((ord(c) - ord('a') + shift) % 26 + ord('a'))
    else:
        return c

def decode_char(c, shift):
    """Decode a single character by shifting back."""
    return encode_char(c, -shift)

def encode_message(message, shift):
    """Encode an entire message."""
    return ''.join(encode_char(c, shift) for c in message)

def decode_message(message, shift):
    """Decode an entire message."""
    return ''.join(decode_char(c, shift) for c in message)

# Test the functions
original = "Hello World"
shift = 3

encoded = encode_message(original, shift)
print(f"Original: {original}")
print(f"Encoded (shift {shift}): {encoded}")

decoded = decode_message(encoded, shift)
print(f"Decoded: {decoded}")
```

### Expected Output
```
Original: Hello World
Encoded (shift 3): Khoor Zruog
Decoded: Hello World
```

### Common Mistakes
- Not handling uppercase and lowercase separately
- Not handling non-alphabetic characters
- Not using modulo to wrap around the alphabet
- Using wrong shift direction for decoding

---

## Problem 15: ATM Simulation

### Solution
```python
def check_balance(account):
    """Return the current balance."""
    return account["balance"]

def deposit(account, amount):
    """Add amount to account and return confirmation message."""
    if amount <= 0:
        return "Invalid amount"
    account["balance"] += amount
    return f"Deposited ${amount:.2f}. New balance: ${account['balance']:.2f}"

def withdraw(account, amount):
    """Remove amount from account and return confirmation or error."""
    if amount <= 0:
        return "Invalid amount"
    if amount > account["balance"]:
        return "Insufficient funds"
    account["balance"] -= amount
    return f"Withdrew ${amount:.2f}. New balance: ${account['balance']:.2f}"

def transaction_menu(account):
    """Present menu and process transactions."""
    while True:
        print("\n" + "="*40)
        print(f"Current Balance: ${check_balance(account):.2f}")
        print("="*40)
        print("1. Check Balance")
        print("2. Deposit")
        print("3. Withdraw")
        print("4. Exit")
        choice = input("Choose: ").strip()

        if choice == "1":
            print(f"Balance: ${check_balance(account):.2f}")
        elif choice == "2":
            try:
                amt = float(input("Amount to deposit: "))
                print(deposit(account, amt))
            except ValueError:
                print("Invalid input")
        elif choice == "3":
            try:
                amt = float(input("Amount to withdraw: "))
                print(withdraw(account, amt))
            except ValueError:
                print("Invalid input")
        elif choice == "4":
            print("Thank you for banking with us!")
            break
        else:
            print("Invalid choice")

def main():
    """Start the ATM application."""
    account = {"name": "Student", "balance": 500.00}
    print(f"Welcome, {account['name']}!")
    transaction_menu(account)

if __name__ == "__main__":
    main()
```

### Expected Output
```
Welcome, Student!

========================================
Current Balance: $500.00
========================================
1. Check Balance
2. Deposit
3. Withdraw
4. Exit
Choose: 2
Amount to deposit: 100
Deposited $100.00. New balance: $600.00

========================================
Current Balance: $600.00
========================================
1. Check Balance
2. Deposit
3. Withdraw
4. Exit
Choose: 3
Amount to withdraw: 50
Withdrew $50.00. New balance: $550.00

========================================
Current Balance: $550.00
========================================
1. Check Balance
2. Deposit
3. Withdraw
4. Exit
Choose: 4
Thank you for banking with us!
```

### Common Mistakes
- Not modularizing operations into separate functions
- Not checking for insufficient funds
- Not handling invalid input with try/except
- Not providing clear menu interface
- Not maintaining state in the account dictionary

---
