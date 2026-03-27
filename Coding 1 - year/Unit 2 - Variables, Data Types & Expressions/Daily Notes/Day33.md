# Day 33: Multiple Assignment, Swapping Variables, Unpacking

**Learning Target:** I can use multiple assignment and unpacking to work with multiple variables efficiently.

### Key Concepts

**Multiple assignment** lets you assign values to multiple variables in a single statement.

**Same value assignment:** `a = b = c = 0` assigns 0 to all three variables.

**Different value assignment:** `x, y, z = 1, 2, 3` assigns 1 to x, 2 to y, 3 to z. The values on the right are packed into a tuple, then unpacked to the left.

**Swapping variables:** `a, b = b, a` swaps the values of a and b without needing a temporary variable. This works because Python evaluates the right side first, then assigns left to right.

**Unpacking:** When you have multiple values on the right and multiple variables on the left, Python unpacks them. `a, b = [10, 20]` assigns 10 to a and 20 to b.

**Ignoring values with `_`:** If you don't need a value, use underscore: `a, _, c = 1, 2, 3` assigns 1 to a, 3 to c, and ignores 2.

### Code Examples

```python
# Same value to multiple variables
x = y = z = 0
print(x, y, z)  # 0 0 0

# Different values
a, b, c = 10, 20, 30
print(a, b, c)  # 10 20 30

# Swapping
x = 5
y = 10
print(f"Before: x={x}, y={y}")
x, y = y, x
print(f"After: x={x}, y={y}")  # x=10, y=5

# Swapping three variables (rotation)
a, b, c = 1, 2, 3
print(f"Before: a={a}, b={b}, c={c}")
a, b, c = b, c, a
print(f"After: a={a}, b={b}, c={c}")  # a=2, b=3, c=1

# Unpacking from lists (you'll use this more with lists)
values = [100, 200, 300]
x, y, z = values
print(f"x={x}, y={y}, z={z}")

# Ignoring values
first, _, third = ["Alice", "Bob", "Charlie"]
print(first, third)  # Alice Charlie

# From input (you can input multiple values if separated by space)
# data = input("Enter three numbers separated by spaces: ").split()
# a, b, c = data

# Unpacking with type conversion
input_data = "42 3.14 hello".split()
num1, num2, text = input_data
num1 = int(num1)
num2 = float(num2)
print(num1, num2, text)  # 42 3.14 hello

# Using unpacking with calculations
width = 10
height = 20
width, height = height, width  # Swap dimensions
print(f"New width: {width}, height: {height}")
```

### Guided Practice

1. Create three variables using multiple assignment.
2. Swap the values of two variables.
3. Rotate three variables: `a → b → c → a`.
4. Ask the user for three numbers and use unpacking to assign them.
5. Use `_` to unpack a list and ignore the middle value.

### Practice Problems

**Problem 1 — Beginner:**
Use multiple assignment to create three variables, then swap two of them:

```python
x, y, z = 1, 2, 3
# Swap x and y
print(f"x={x}, y={y}, z={z}")
```

**Problem 2 — Intermediate:**
Write a program that:
- Creates two variables (temperature and humidity)
- Swaps them
- Prints before and after

**Problem 3 — Challenge:**
Create a program that:
- Asks the user for three measurements
- Uses unpacking to assign them
- Swaps the first and last
- Prints all three in order

<details>
<summary>💡 Hints</summary>

- Problem 1: After `x, y, z = 1, 2, 3`, use `x, y = y, x` to swap.
- Problem 2: Print before swap, swap using `a, b = b, a`, print after.
- Problem 3: Use `input().split()` to get multiple values, then unpack and convert if needed.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
x, y, z = 1, 2, 3
print(f"Before: x={x}, y={y}, z={z}")
x, y = y, x
print(f"After: x={x}, y={y}, z={z}")

# Problem 2 Example
temp = 72
humidity = 65
print(f"Before: temp={temp}, humidity={humidity}")
temp, humidity = humidity, temp
print(f"After: temp={temp}, humidity={humidity}")

# Problem 3 Example
m1_str, m2_str, m3_str = input("Three measurements: ").split()
m1 = float(m1_str)
m2 = float(m2_str)
m3 = float(m3_str)
print(f"Original: {m1}, {m2}, {m3}")
m1, m3 = m3, m1
print(f"After swap: {m1}, {m2}, {m3}")
```

</details>

---
