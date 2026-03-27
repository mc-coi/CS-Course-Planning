# Day 4: List Methods & Iteration

**Learning Target:** I can use list methods and iterate through lists with loops.

---

## Key Concepts

**List methods** are functions that operate on lists. Key methods include:
- **`.append(x)`** - adds x to the end
- **`.insert(i, x)`** - inserts x at index i
- **`.remove(x)`** - removes the first occurrence of x
- **`.pop(i)`** - removes and returns element at index i (defaults to last element)
- **`.extend(other_list)`** - adds all elements from another list
- **`.sort()`** - sorts the list in-place
- **`.reverse()`** - reverses the list in-place
- **`.index(x)`** - returns the index of first x
- **`.count(x)`** - counts occurrences of x

**Iteration** is looping through list elements. The for loop is the most Pythonic way to do this.

---

## Code Examples

```python
# Append and extend
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)  # ['apple', 'banana', 'cherry']

fruits.extend(["date", "fig"])
print(fruits)  # ['apple', 'banana', 'cherry', 'date', 'fig']

# Insert and remove
fruits.insert(1, "blueberry")  # Insert at index 1
fruits.remove("blueberry")      # Remove by value

# Pop
last = fruits.pop()             # Remove and get last element
specific = fruits.pop(0)        # Remove and get first element

# Count and index
numbers = [1, 2, 3, 2, 4, 2, 5]
print(numbers.count(2))         # 3
print(numbers.index(3))         # 2

# Sort and reverse
nums = [5, 2, 8, 1, 9]
nums.sort()
print(nums)                     # [1, 2, 5, 8, 9]

nums.reverse()
print(nums)                     # [9, 8, 5, 2, 1]

# Iteration
for fruit in fruits:
    print(f"I like {fruit}")

# Iteration with index
for i, fruit in enumerate(fruits):
    print(f"Index {i}: {fruit}")
```

---

## Guided Practice

**Activity: Shopping List Manager**

1. Create an empty list called `shopping_list`
2. Add 5 items using `.append()`
3. Insert "milk" at position 2
4. Print the list
5. Remove one item using `.remove()`
6. Use a for loop to print each item with its position number
7. Sort the list and print it

---

## Practice Problems

**Beginner:** Create a list of 5 numbers. Use `.pop()` to remove the last number, then print the list.

**Intermediate:** Write a function `list_summary(lst)` that counts how many numbers in the list are greater than 10 and returns that count. Test it with a list of at least 6 numbers.

**Challenge:** Write a function `remove_duplicates(lst)` that removes all duplicate values from a list while preserving order. For example, `[1, 2, 2, 3, 1, 4]` becomes `[1, 2, 3, 4]`.

<details>
<summary>💡 Hints</summary>

- Beginner: Call .pop() with no arguments to remove the last element
- Intermediate: Use a for loop to iterate through the list and count elements matching a condition
- Challenge: One approach is to create a new list and only add elements you haven't seen before

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
numbers = [10, 20, 30, 40, 50]
numbers.pop()
print(numbers)  # [10, 20, 30, 40]

# Intermediate
def list_summary(lst):
    count = 0
    for num in lst:
        if num > 10:
            count += 1
    return count

# Challenge
def remove_duplicates(lst):
    result = []
    for item in lst:
        if item not in result:
            result.append(item)
    return result
```

</details>
