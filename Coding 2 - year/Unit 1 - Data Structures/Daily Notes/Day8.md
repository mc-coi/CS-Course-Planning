# Day 8: Nested Lists & Complex Data

**Learning Target:** I can work with deeply nested lists and represent complex data structures.

---

## Key Concepts

**Deeply nested lists** go beyond 2D—you can have lists of lists of lists, etc. Each level adds another dimension.

**Jagged arrays** are lists where rows have different lengths. Unlike uniform 2D lists, jagged arrays are flexible but require careful indexing.

**When to nest:** Use nesting when your data naturally has hierarchical structure. For example, a school roster might be: courses → classes → students.

**Flattening** is converting nested lists into a single flat list (sometimes needed for processing).

---

## Code Examples

```python
# 2D representation (list of lists)
student_data = [
    ["Alice", [85, 92, 88]],      # Student with name and grades
    ["Bob", [78, 81, 79]],
    ["Charlie", [95, 92, 98]]
]

print(student_data[0][0])         # "Alice"
print(student_data[0][1])         # [85, 92, 88]
print(student_data[0][1][1])      # 92 (Alice's second grade)

# Jagged array (different row lengths)
irregular = [
    [1, 2, 3],
    [4, 5],
    [6, 7, 8, 9]
]

for row in irregular:
    print(row)

# Deep nesting (3D list)
cube = [
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
]

print(cube[1][0][1])  # 6

# Flattening a nested list
nested = [[1, 2], [3, 4], [5, 6]]
flat = [item for row in nested for item in row]
print(flat)  # [1, 2, 3, 4, 5, 6]

# With deeper nesting
deep_nested = [[[1, 2], [3]], [[4, 5, 6]]]
flat_deep = [item for row in deep_nested for subrow in row for item in subrow]
print(flat_deep)  # [1, 2, 3, 4, 5, 6]
```

---

## Guided Practice

**Activity: School Data Structure**

1. Create a nested list representing 2 classes, each with 2 students and their grades
2. Access and print a specific student's grades
3. Write nested loops to print all student information
4. Flatten your structure to get a single list of all grades
5. Calculate the overall average across all students

---

## Practice Problems

**Beginner:** Given a jagged array, write code to find and print the longest row.

```python
jagged = [[1, 2, 3], [4, 5], [6, 7, 8, 9, 10]]
```

**Intermediate:** Write a function `flatten(nested_list)` that flattens a 2D list into a 1D list. Then modify it to work with 3D lists.

**Challenge:** Write a function `nested_sum(nested_list)` that returns the sum of all numbers in a nested list of arbitrary depth. Test it with lists of varying nesting levels.

<details>
<summary>💡 Hints</summary>

- Beginner: Use max() with a key parameter (len) to find the longest row
- Intermediate: Use list comprehensions with multiple for clauses
- Challenge: Use recursion or a recursive list comprehension

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
jagged = [[1, 2, 3], [4, 5], [6, 7, 8, 9, 10]]
longest = max(jagged, key=len)
print(longest)  # [6, 7, 8, 9, 10]

# Intermediate
def flatten(nested_list):
    return [item for row in nested_list for item in row]

def flatten_3d(nested_list):
    return [item for row in nested_list for subrow in row for item in subrow]

# Challenge
def nested_sum(nested_list):
    total = 0
    for item in nested_list:
        if isinstance(item, list):
            total += nested_sum(item)
        else:
            total += item
    return total
```

</details>
