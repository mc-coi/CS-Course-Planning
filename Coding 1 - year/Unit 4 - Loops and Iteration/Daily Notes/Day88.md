# Day 88: List Methods — .append(), .remove(), .sort(), .reverse()

**Learning Target:** I can modify lists using methods: append, remove, sort, and reverse.

### Key Concepts

**Methods** are actions that operate on an object. Lists have built-in methods for modification.

**`.append(value)`:** Add an element to the end of the list.
```python
numbers = [1, 2, 3]
numbers.append(4)  # [1, 2, 3, 4]
```

**`.remove(value)`:** Remove the first occurrence of a value.
```python
numbers.remove(2)  # [1, 3, 4] (removes only first 2)
```

**`.pop(index)`:** Remove and return element at index (default: last element).
```python
last = numbers.pop()      # Removes and returns last element
first = numbers.pop(0)    # Removes and returns first element
```

**`.sort()`:** Sort list in place (ascending order).
```python
numbers.sort()  # [1, 3, 4] sorted ascending
```

**`.reverse()`:** Reverse list in place.
```python
numbers.reverse()  # [4, 3, 1] reversed
```

**`.index(value)`:** Return the index of first occurrence.
```python
index = numbers.index(3)  # Returns 1 (position of 3)
```

**`.count(value)`:** Count occurrences of a value.
```python
count = numbers.count(3)  # How many 3's?
```

**Important:** These methods modify the list **in place** (change the original). They don't return a new list.

### Code Examples

```python
# Example 1: Build a list with append
numbers = []
for i in range(1, 6):
    numbers.append(i * 2)
print(f"After append: {numbers}\n")  # [2, 4, 6, 8, 10]

# Example 2: Remove elements
fruits = ["apple", "banana", "cherry", "banana"]
print(f"Before remove: {fruits}")
fruits.remove("banana")  # Removes first "banana" only
print(f"After remove: {fruits}\n")  # ["apple", "cherry", "banana"]

# Example 3: Sort and reverse
scores = [85, 92, 78, 95, 88]
print(f"Original: {scores}")
scores.sort()
print(f"Sorted: {scores}")
scores.reverse()
print(f"Reversed: {scores}\n")

# Example 4: Index and count
words = ["apple", "banana", "apple", "cherry", "apple"]
print(f"Position of 'banana': {words.index('banana')}")
print(f"'apple' appears: {words.count('apple')} times\n")

# Example 5: Build list from user input
names = []
while True:
    name = input("Name ('done' to stop): ")
    if name == "done":
        break
    names.append(name)
print(f"Names: {names}")
```

### Guided Practice

Write a program that:
1. Starts with an empty list
2. Asks the user for 5 numbers, appending each to the list
3. Displays the unsorted list
4. Sorts the list
5. Displays the sorted list
6. Removes a number the user specifies
7. Displays the final list

### Practice Problems

**Problem 1 — Beginner:** Create a list, use `.append()` to add 3 numbers, then print the list.

```python
scores = [85, 92]
# Your code here
print(scores)
```

**Problem 2 — Intermediate:** Create a list of words. Ask the user for a word to remove. Remove it if it exists, otherwise print "Not found."

**Problem 3 — Challenge:** Write a program that:
- Asks the user for numbers until they enter "done"
- Appends each to a list
- Calculates and prints: sum, average, count, sorted list, highest, lowest

<details>
<summary>💡 Hints</summary>

- Problem 1: Call `append()` three times with different numbers
- Problem 2: Check `if word in list:` before removing
- Problem 3: Build list with append, then use built-in functions or sort method

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
scores = [85, 92]
scores.append(78)
scores.append(95)
scores.append(88)
print(scores)  # [85, 92, 78, 95, 88]

# Problem 2 Example
words = ["apple", "banana", "cherry", "date"]
target = input("Word to remove: ")
if target in words:
    words.remove(target)
    print(f"Removed. List: {words}")
else:
    print("Not found")

# Problem 3 Example
numbers = []
while True:
    num = int(input("Number ('done' to stop): "))
    if num == "done":
        break
    numbers.append(num)

if len(numbers) > 0:
    total = sum(numbers)
    avg = total / len(numbers)
    sorted_nums = sorted(numbers)
    print(f"Sum: {total}")
    print(f"Average: {avg:.2f}")
    print(f"Count: {len(numbers)}")
    print(f"Sorted: {sorted_nums}")
    print(f"Highest: {max(numbers)}")
    print(f"Lowest: {min(numbers)}")
```

</details>

---
