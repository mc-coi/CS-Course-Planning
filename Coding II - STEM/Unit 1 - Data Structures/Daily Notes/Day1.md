# Day 1: Review & Lists (Creation, Indexing, Slicing, Methods)
**Learning Target:** I can create lists, access elements using indexing and slicing, and use built-in list methods.

### Key Concepts
A **list** is an ordered, mutable (changeable) collection of items. Lists can contain any data type: integers, strings, floats, even other lists. Elements are accessed by **index**, starting at 0.

**Indexing:** Access a single element using its position
- `numbers[0]` gets the first element
- `numbers[-1]` gets the last element (negative indexing counts backward)

**Slicing:** Extract a sub-list using `list[start:stop:step]`
- `numbers[1:4]` gets elements at indices 1, 2, 3 (stop is exclusive)
- `numbers[::2]` gets every 2nd element
- `numbers[::-1]` reverses the list

**Common list methods:**
- `append(item)` — add to end
- `insert(index, item)` — insert at specific position
- `remove(item)` — remove first occurrence of value
- `pop(index)` — remove and return element at index
- `sort()` — sort in place
- `reverse()` — reverse in place
- `len(list)` — get length
- `list.count(item)` — count occurrences
- `list.index(item)` — find first index of item

### Code Examples
```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
fruits = ["apple", "banana", "cherry"]
mixed = [1, "hello", 3.14, True]
empty = []

# Indexing
print(numbers[0])     # 1
print(numbers[-1])    # 5
print(numbers[2])     # 3

# Slicing
print(numbers[1:4])   # [2, 3, 4]
print(numbers[:3])    # [1, 2, 3]
print(numbers[2:])    # [3, 4, 5]
print(numbers[::2])   # [1, 3, 5]
print(numbers[::-1])  # [5, 4, 3, 2, 1]

# List methods
fruits = ["apple", "banana"]
fruits.append("cherry")           # ["apple", "banana", "cherry"]
fruits.insert(1, "date")          # ["apple", "date", "banana", "cherry"]
fruits.remove("date")             # ["apple", "banana", "cherry"]
item = fruits.pop()               # ["apple", "banana"], item = "cherry"

# Sorting
numbers = [3, 1, 4, 1, 5, 9]
numbers.sort()                    # [1, 1, 3, 4, 5, 9]
print(len(numbers))               # 6
print(numbers.count(1))           # 2
print(numbers.index(4))           # 2

# Iterating through a list
for fruit in fruits:
    print(fruit)

# Using range to create a list
range_list = list(range(10))      # [0, 1, 2, ..., 9]
```

### Guided Practice
Create a shopping list program:
1. Start with a list of 5 grocery items
2. Print the first and last items
3. Slice out the middle 3 items
4. Add a new item
5. Remove an item by index
6. Sort the list and print it
7. Reverse and print it

### Practice Problems
**Problem 1 — Beginner:** Create a list of your 5 favorite numbers, then print each one using a loop.

```python
# Starter code
numbers = []

for num in numbers:
    print(num)
```

**Problem 2 — Intermediate:** Create a list, add 3 elements, remove one, then print the final list and its length.

**Problem 3 — Challenge:** Create a list of 10 integers. Using slicing, print the first 3, last 3, every other element, and the reversed list.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use square brackets and commas to separate values
- Problem 2: Remember to use methods like append() and remove()
- Problem 3: Remember negative indexing and step values in slicing
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
numbers = [5, 10, 15, 20, 25]
for num in numbers:
    print(num)

# Problem 2 Example
inventory = []
inventory.append("milk")
inventory.append("eggs")
inventory.append("bread")
inventory.remove("eggs")
print(inventory)       # ['milk', 'bread']
print(len(inventory))  # 2

# Problem 3 Example
nums = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
print(nums[:3])        # [10, 20, 30]
print(nums[-3:])       # [80, 90, 100]
print(nums[::2])       # [10, 30, 50, 70, 90]
print(nums[::-1])      # [100, 90, 80, ..., 10]
```
</details>

---
