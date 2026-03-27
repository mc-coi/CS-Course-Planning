# Day 2: List Indexing & Accessing Elements

**Learning Target:** I can access and modify individual list elements using positive and negative indexing.

---

## Key Concepts

**Indexing** is how you retrieve a specific element from a list using its position. In Python, **indexing starts at 0**, not 1. The first element is at index 0, the second at index 1, and so on.

**Positive indexing** counts from the beginning: `list[0]`, `list[1]`, etc.

**Negative indexing** counts from the end: `list[-1]` gets the last element, `list[-2]` gets the second-to-last, etc. This is incredibly useful and is a Python feature many programmers love.

**IndexError** occurs when you try to access an index that doesn't exist. Always check your list length first!

---

## Code Examples

```python
fruits = ["apple", "banana", "cherry", "date"]

# Positive indexing
print(fruits[0])   # "apple"
print(fruits[2])   # "cherry"

# Negative indexing
print(fruits[-1])  # "date" (last element)
print(fruits[-2])  # "cherry" (second-to-last)

# Modifying elements
fruits[1] = "blueberry"
print(fruits)  # ['apple', 'blueberry', 'cherry', 'date']

# What happens with out-of-bounds access?
# print(fruits[10])  # IndexError: list index out of range

# Check list length
print(len(fruits))  # 4

# Access with bounds checking
if len(fruits) > 3:
    print(fruits[3])  # "date"
```

---

## Guided Practice

**Activity: Inventory Manager**

1. Create a list of 5 product names: `products = ["laptop", "mouse", "keyboard", "monitor", "headphones"]`
2. Print the first and last product using positive and negative indexing
3. Update the second product to "wireless mouse"
4. Print the updated list
5. Add code to safely access the 10th item (if it exists) without causing an error

---

## Practice Problems

**Beginner:** Given the list `colors = ["red", "green", "blue", "yellow", "purple"]`, use indexing to print "green" and "purple".

**Intermediate:** Create a list of 8 numbers. Write code that swaps the first and last elements, then prints the modified list.

**Challenge:** Write a function `reverse_list_manual(lst)` that returns a reversed version of a list using only indexing and a new list (don't use the `.reverse()` method). For example, `reverse_list_manual([1, 2, 3, 4])` should return `[4, 3, 2, 1]`.

<details>
<summary>💡 Hints</summary>

- Beginner: Use colors[1] for green and colors[-1] or colors[4] for purple
- Intermediate: Remember that assigning to negative indices works too (e.g., lst[-1] = new_value)
- Challenge: Loop through the original list backwards using negative indices or range with a negative step

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
colors = ["red", "green", "blue", "yellow", "purple"]
print(colors[1])   # green
print(colors[-1])  # purple

# Intermediate
numbers = [10, 20, 30, 40, 50, 60, 70, 80]
numbers[0], numbers[-1] = numbers[-1], numbers[0]
print(numbers)  # [80, 20, 30, 40, 50, 60, 70, 10]

# Challenge
def reverse_list_manual(lst):
    result = []
    for i in range(len(lst) - 1, -1, -1):
        result.append(lst[i])
    return result

# Or using negative indexing:
def reverse_list_manual(lst):
    result = []
    for i in range(1, len(lst) + 1):
        result.append(lst[-i])
    return result
```

</details>
