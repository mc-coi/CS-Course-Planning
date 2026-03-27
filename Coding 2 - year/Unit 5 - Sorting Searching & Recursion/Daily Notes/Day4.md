# Day 4: Linear Search & Big O Analysis

**Learning Target:** I can apply linear search to real problems and understand when O(n) is acceptable.

---

## Key Concepts

**Big O Notation**: A way to describe how an algorithm's runtime grows as the input size grows.

- O(1) — Constant time (always same speed, regardless of size)
- O(n) — Linear time (time grows with the list size)
- O(n²) — Quadratic time (time grows with the square of size)

**Linear Search Analysis**:
```
Input size n: [10, 100, 1000, 10000]
Max comparisons: 10, 100, 1000, 10000
Big O: O(n) — proportional to input size
```

**Trade-off:** Linear search is simple and works on unsorted data, but slow for large lists. Binary search is faster but requires sorted data.

---

## Code Examples

```python
# Practical: Search a student database
class Student:
    def __init__(self, id, name, grade):
        self.id = id
        self.name = name
        self.grade = grade

def find_student_by_name(students, name):
    """Linear search through student list by name."""
    for student in students:
        if student.name == name:
            return student
    return None

def find_students_by_grade(students, grade):
    """Find all students with a specific grade."""
    matching = []
    for student in students:
        if student.grade == grade:
            matching.append(student)
    return matching

# Test
roster = [
    Student(101, "Alice", "A"),
    Student(102, "Bob", "B"),
    Student(103, "Charlie", "A"),
    Student(104, "Diana", "A")
]

found = find_student_by_name(roster, "Bob")
if found:
    print(f"Found: {found.name} with grade {found.grade}")

honors = find_students_by_grade(roster, "A")
print(f"Number of A students: {len(honors)}")
```

---

## Guided Practice

**Activity 1: Analyze Performance**

For each scenario, decide if linear search is appropriate or if a better algorithm would be needed:
1. Searching a list of 5 items
2. Searching a list of 1,000,000 items
3. Searching a constantly-changing list
4. Searching the same sorted list of 100,000 items 10,000 times

Explain your reasoning for each.

**Activity 2: Trace and Count**

Given the list: `['apple', 'banana', 'cherry', 'date', 'elderberry']`

Trace `linear_search(list, 'cherry')` and count how many comparisons are needed.

**Activity 3: Write Linear Search for a 2D List**

Can you search a 2D list (list of lists) using linear search? Write a function that finds a value anywhere in the 2D structure.

---

## Practice Problems

**Beginner:** Write a function that searches a list of product names and returns the price if found. Return -1 if not found. Use linear search.

**Intermediate:** Write a function that counts how many times a target appears in a list AND how many comparisons were needed. Compare two different targets (e.g., one near the start, one near the end).

**Challenge:** Implement a function that searches through a list of tuples (storing both name and age). Return all people with a specific name who are older than a certain age. Estimate the Big O complexity.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Store prices in parallel lists or use a dictionary for easier access. But linear search still works.
- **Intermediate:** Use a counter variable that increments each time you compare.
- **Challenge:** You'll need to loop through the list and check TWO conditions. What's the Big O if you have nested loops?
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
names = ['apple', 'banana', 'cherry']
prices = [0.50, 0.30, 0.75]

def find_price(product):
    for i in range(len(names)):
        if names[i] == product:
            return prices[i]
    return -1

print(find_price('banana'))  # Output: 0.3

# Intermediate
def count_and_measure(arr, target):
    count = 0
    comparisons = 0
    for i in range(len(arr)):
        comparisons += 1
        if arr[i] == target:
            count += 1
    return count, comparisons

count, comps = count_and_measure([1, 2, 3, 2, 4, 2], 2)
print(f"Found {count} times in {comps} comparisons")  # Output: Found 3 times in 6 comparisons

# Challenge
def find_old_people_by_name(people, name, min_age):
    """people is list of tuples like [('Alice', 20), ('Bob', 25), ...]"""
    results = []
    for person_name, age in people:
        if person_name == name and age > min_age:
            results.append((person_name, age))
    return results

people = [('Alice', 20), ('Bob', 25), ('Alice', 30), ('Charlie', 22)]
print(find_old_people_by_name(people, 'Alice', 25))  # Output: [('Alice', 30)]

# Big O: O(n) — we loop through the list once, checking two conditions each time.
# Even though we check two conditions, it's still O(n) because constants don't matter in Big O.
```
</details>
