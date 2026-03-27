# Day 1: Introduction to Lists & Creation

**Learning Target:** I can create and initialize lists in Python using multiple methods.

---

## Key Concepts

**Lists** are **ordered, mutable collections** that can store multiple values of any type. Think of a list like a numbered shopping list where you can read, modify, and reorder items.

**Mutability** means you can change the list after creating it (add, remove, or modify items). This distinguishes lists from other data structures you'll encounter later.

**Why lists matter:** Lists are one of the most fundamental data structures in programming. They let you store related data together and process it systematically. In real life, you use lists constantly: to-do lists, grade lists, inventory lists, etc.

---

## Code Examples

```python
# Creating lists with square brackets and commas
fruits = ["apple", "banana", "cherry"]
print(fruits)  # ['apple', 'banana', 'cherry']

# Lists can contain mixed types
mixed = [1, "hello", 3.14, True]
print(mixed)  # [1, 'hello', 3.14, True]

# Creating an empty list
empty_list = []
print(empty_list)  # []

# Using the list() constructor
numbers = list(range(1, 6))
print(numbers)  # [1, 2, 3, 4, 5]

# Creating a list of the same value repeated
zeros = [0] * 5
print(zeros)  # [0, 0, 0, 0, 0]
```

---

## Guided Practice

**Activity: Build a Student List**

1. Create a list called `students` with 4 classmates' names
2. Print the list to verify it was created correctly
3. Create an empty list called `attendance` that you'll fill later
4. Create a list called `test_scores` with 5 random numbers between 0-100
5. Print all three lists and describe what each one represents

---

## Practice Problems

**Beginner:** Create a list of your 5 favorite movies and print it.

```python
# Starter code:
movies = # YOUR CODE HERE
print(movies)
```

**Intermediate:** Create three separate lists (names, ages, grades) that represent data for 3 students. Then print a statement that uses data from all three lists: "Alice is 15 years old and has a B grade."

**Challenge:** Write a function `create_multiplication_table(n)` that returns a list of the first 10 multiples of `n`. For example, `create_multiplication_table(3)` should return `[3, 6, 9, 12, 15, 18, 21, 24, 27, 30]`.

<details>
<summary>💡 Hints</summary>

- Beginner: Wrap your movie titles in square brackets and separate them with commas
- Intermediate: You can access elements from each list using the same index (e.g., names[0], ages[0], grades[0])
- Challenge: Use a loop (for or while) and multiplication, or use list(range()) with a step value

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Beginner
movies = ["The Matrix", "Inception", "Dune", "Interstellar", "Avatar"]
print(movies)

# Intermediate
names = ["Alice", "Bob", "Charlie"]
ages = [15, 16, 15]
grades = ["B", "A", "C"]
print(f"{names[0]} is {ages[0]} years old and has a {grades[0]} grade.")

# Challenge
def create_multiplication_table(n):
    return [n * i for i in range(1, 11)]  # Or: [i * n for i in range(1, 11)]

# Alternative without list comprehension:
def create_multiplication_table(n):
    result = []
    for i in range(1, 11):
        result.append(n * i)
    return result
```

</details>
