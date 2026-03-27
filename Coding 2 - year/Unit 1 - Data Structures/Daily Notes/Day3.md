# Day 3: List Slicing

**Learning Target:** I can use slice notation to extract subsets of a list.

---

## Key Concepts

**Slicing** creates a new list containing a subset of elements from the original list. The syntax is `list[start:stop:step]`, where:
- **start** is the beginning index (inclusive, defaults to 0)
- **stop** is the ending index (exclusive, defaults to the end)
- **step** is the interval between elements (defaults to 1)

**Key insight:** The stop index is NOT included—`list[0:3]` gets indices 0, 1, 2 (not 3).

Slicing is read-only and doesn't modify the original list. You can slice with negative indices and negative steps to work backwards.

---

## Code Examples

```python
numbers = [10, 20, 30, 40, 50, 60, 70, 80]

# Basic slicing
print(numbers[0:3])    # [10, 20, 30]
print(numbers[2:5])    # [30, 40, 50]

# Omitting start or stop
print(numbers[:3])     # [10, 20, 30] (from beginning to index 2)
print(numbers[5:])     # [60, 70, 80] (from index 5 to end)

# Using step
print(numbers[::2])    # [10, 30, 50, 70] (every 2nd element)
print(numbers[1::2])   # [20, 40, 60, 80] (every 2nd starting at index 1)

# Negative indices in slicing
print(numbers[-3:])    # [60, 70, 80] (last 3 elements)

# Reversing with step -1
print(numbers[::-1])   # [80, 70, 60, 50, 40, 30, 20, 10]
```

---

## Guided Practice

**Activity: Extract and Analyze Data**

1. Create a list of 10 grades: `grades = [85, 92, 78, 95, 88, 91, 79, 87, 93, 90]`
2. Extract the first 5 grades
3. Extract the last 3 grades
4. Extract every other grade
5. Reverse the entire list and print it
6. Explain what slice you'd use to get the middle 4 grades

---

## Practice Problems

**Beginner:** Given `letters = ["a", "b", "c", "d", "e", "f", "g"]`, use slicing to print "b", "c", "d", "e".

**Intermediate:** Given a list of 10 integers, write code to print the last half of the list, then print every third element starting from index 1.

**Challenge:** Write a function `find_middle(lst)` that returns the middle element(s) of a list. If the list has odd length, return the single middle element. If even length, return the two middle elements as a list.

<details>
<summary>💡 Hints</summary>

- Beginner: Use list[1:5] to get elements at indices 1, 2, 3, 4
- Intermediate: For the last half, consider using list[len(list)//2:] or list[-len(list)//2:]
- Challenge: Calculate the middle index using len(lst) // 2, then handle odd vs. even cases

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
letters = ["a", "b", "c", "d", "e", "f", "g"]
print(letters[1:5])  # ['b', 'c', 'd', 'e']

# Intermediate
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(numbers[5:])      # [6, 7, 8, 9, 10]
print(numbers[1::3])    # [2, 5, 8]

# Challenge
def find_middle(lst):
    mid = len(lst) // 2
    if len(lst) % 2 == 1:  # Odd length
        return lst[mid]
    else:  # Even length
        return lst[mid-1:mid+1]
```

</details>
