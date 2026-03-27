# Day 86: Lists Intro — Creating, Indexing, and Length

**Learning Target:** I can create lists, access elements by index, and determine list length using len().

### Key Concepts

A **list** is a container that holds multiple values in a single variable. Lists are ordered, indexed starting at 0, and can be modified.

**Creating a list:**
```python
numbers = [1, 2, 3, 4, 5]           # List of integers
names = ["Alice", "Bob", "Charlie"]  # List of strings
mixed = [42, "hello", 3.14, True]    # Mixed types
empty = []                            # Empty list
```

**Indexing:** Access elements by position (0-based).
```python
names = ["Alice", "Bob", "Charlie"]
print(names[0])   # "Alice" (first element)
print(names[1])   # "Bob" (second element)
print(names[-1])  # "Charlie" (last element)
print(names[-2])  # "Bob" (second to last)
```

**Negative indexing:** `-1` is the last element, `-2` is second-to-last, etc.

**Length:** Use `len()` to get the number of elements.
```python
print(len(names))  # 3
```

**Slicing:** Get a subset of a list.
```python
numbers = [1, 2, 3, 4, 5]
print(numbers[1:4])   # [2, 3, 4] (from index 1 to 3, 4 is exclusive)
print(numbers[:3])    # [1, 2, 3] (from start to index 2)
print(numbers[2:])    # [3, 4, 5] (from index 2 to end)
```

### Code Examples

```python
# Example 1: Create and access a list
fruits = ["apple", "banana", "cherry", "date"]
print(f"First fruit: {fruits[0]}")
print(f"Last fruit: {fruits[-1]}")
print(f"Total fruits: {len(fruits)}\n")

# Example 2: Check if a value is in a list
if "banana" in fruits:
    print("We have bananas!\n")

# Example 3: Create a list from input
numbers = []
for i in range(3):
    num = int(input(f"Number {i+1}: "))
    numbers.append(num)  # We'll learn append tomorrow
print(f"You entered: {numbers}\n")

# Example 4: Loop through a list with index
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")
```

### Guided Practice

1. Create a list of 5 favorite movies (or books, games, etc.)
2. Print the first and last element
3. Print the length
4. Access an element at a specific index (ask the user)
5. Print all elements, one per line

### Practice Problems

**Problem 1 — Beginner:** Create a list of 5 numbers and print:
- The first element
- The last element
- The length
- The middle element (if list has odd length)

```python
numbers = [10, 20, 30, 40, 50]
# Your code here
```

**Problem 2 — Intermediate:** Create a list of names. Ask the user for an index, then print the name at that position. Include error handling (check if index is valid).

**Problem 3 — Challenge:** Create a list of 10 numbers. Find and print:
- The value at the middle index
- All values in the first half
- All values in the second half

<details>
<summary>💡 Hints</summary>

- Problem 1: Use indexing `[0]`, `[-1]`, and `len()`. Middle index is `len(list) // 2`
- Problem 2: Check `if 0 <= index < len(names)` before accessing
- Problem 3: Use slicing: `list[:len(list)//2]` for first half, `list[len(list)//2:]` for second half

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [10, 20, 30, 40, 50]
print(f"First: {numbers[0]}")
print(f"Last: {numbers[-1]}")
print(f"Length: {len(numbers)}")
middle = len(numbers) // 2
print(f"Middle: {numbers[middle]}")

# Problem 2 Example
names = ["Alice", "Bob", "Charlie", "David"]
index = int(input("Index (0-3): "))
if 0 <= index < len(names):
    print(f"Name: {names[index]}")
else:
    print("Invalid index")

# Problem 3 Example
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
mid = len(numbers) // 2
print(f"Middle value: {numbers[mid]}")
print(f"First half: {numbers[:mid]}")
print(f"Second half: {numbers[mid:]}")
```

</details>

---
