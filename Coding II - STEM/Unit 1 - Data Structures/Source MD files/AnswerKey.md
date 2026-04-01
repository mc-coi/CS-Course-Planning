# Unit 1 - Data Structures: Answer Key

## Problem 1: Create a list of 5 numbers, print the first and last elements

### Solution
```python
# Create a list of 5 numbers
numbers = [10, 25, 30, 15, 40]

# Print the first element (index 0)
print(numbers[0])

# Print the last element (index -1)
print(numbers[-1])
```

### Expected Output
```
10
40
```

### Common Mistakes
- Using index 1 instead of 0 for the first element
- Forgetting that negative indices work from the end of the list

---

## Problem 2: Create a list, use append() to add 3 items, then print the list

### Solution
```python
# Create an empty list
items = []

# Append 3 items
items.append("apple")
items.append("banana")
items.append("orange")

# Print the list
print(items)
```

### Expected Output
```
['apple', 'banana', 'orange']
```

### Common Mistakes
- Forgetting that append() modifies the list in place and returns None
- Using concatenation instead of append() (less efficient)

---

## Problem 3: Create a list of strings and print each one using a for loop

### Solution
```python
# Create a list of strings
fruits = ["apple", "banana", "cherry", "date"]

# Print each one using a for loop
for fruit in fruits:
    print(fruit)
```

### Expected Output
```
apple
banana
cherry
date
```

### Common Mistakes
- Using range(len()) when direct iteration is simpler
- Indentation errors with the for loop

---

## Problem 4: Use list slicing to extract the middle 3 elements from a list of 7 items

### Solution
```python
# Create a list of 7 items
numbers = [10, 20, 30, 40, 50, 60, 70]

# Extract the middle 3 elements (indices 2, 3, 4)
middle_three = numbers[2:5]

# Print the result
print(middle_three)
```

### Expected Output
```
[30, 40, 50]
```

### Common Mistakes
- Including the end index (forgetting that slicing is exclusive of the end point)
- Using incorrect indices (off-by-one errors)

---

## Problem 5: Create a tuple with 3 values and unpack them into separate variables

### Solution
```python
# Create a tuple with 3 values
my_tuple = (100, 200, 300)

# Unpack the tuple into separate variables
a, b, c = my_tuple

# Print the unpacked values
print(a)
print(b)
print(c)
```

### Expected Output
```
100
200
300
```

### Common Mistakes
- Wrong number of variables in unpacking (must match tuple length)
- Trying to modify tuple values after unpacking (tuples are immutable)

---

## Problem 6: Use list comprehension to create a list of squared numbers (1²-10²)

### Solution
```python
# Create a list of squared numbers from 1 to 10
squares = [x**2 for x in range(1, 11)]

# Print the result
print(squares)
```

### Expected Output
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Common Mistakes
- Using range(10) instead of range(1, 11) (off-by-one error)
- Using incorrect exponent syntax (** not ^)

---

## Problem 7: Create a 3x3 matrix and print the element at position [2][1]

### Solution
```python
# Create a 3x3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Print the element at position [2][1]
print(matrix[2][1])
```

### Expected Output
```
8
```

### Common Mistakes
- Confusing row/column order (should be [row][column])
- Using 1-based indexing instead of 0-based

---

## Problem 8: Create a dictionary with 5 key-value pairs and iterate through them with .items()

### Solution
```python
# Create a dictionary with 5 key-value pairs
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science",
    "gpa": 3.8,
    "year": 2
}

# Iterate through the dictionary using .items()
for key, value in student.items():
    print(f"{key}: {value}")
```

### Expected Output
```
name: Alice
age: 20
major: Computer Science
gpa: 3.8
year: 2
```

### Common Mistakes
- Forgetting to unpack both key and value in the for loop
- Using just student.keys() or .values() without .items()

---

## Problem 9: Create two sets and find their union, intersection, and difference

### Solution
```python
# Create two sets
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# Find union
union = set1 | set2
print("Union:", union)

# Find intersection
intersection = set1 & set2
print("Intersection:", intersection)

# Find difference (elements in set1 but not in set2)
difference = set1 - set2
print("Difference:", difference)
```

### Expected Output
```
Union: {1, 2, 3, 4, 5, 6, 7, 8}
Intersection: {4, 5}
Difference: {1, 2, 3}
```

### Common Mistakes
- Confusing the order of difference (set1 - set2 vs set2 - set1)
- Using list syntax instead of set operators

---

## Problem 10: Write a function that returns multiple values as a tuple, then unpack the result

### Solution
```python
# Function that returns multiple values as a tuple
def calculate(a, b):
    """Calculate sum, difference, and product"""
    return (a + b, a - b, a * b)

# Call the function and unpack the result
sum_val, diff_val, prod_val = calculate(10, 3)

# Print the unpacked values
print(f"Sum: {sum_val}")
print(f"Difference: {diff_val}")
print(f"Product: {prod_val}")
```

### Expected Output
```
Sum: 13
Difference: 7
Product: 30
```

### Common Mistakes
- Not using parentheses for tuple creation in return statement
- Unpacking into the wrong number of variables

---

## Problem 11: Create a nested dictionary representing a store with departments and products

### Solution
```python
# Create a nested dictionary representing a store
store = {
    "Electronics": {
        "Laptop": 999.99,
        "Phone": 599.99,
        "Headphones": 149.99
    },
    "Clothing": {
        "Shirt": 29.99,
        "Jeans": 49.99,
        "Jacket": 89.99
    },
    "Books": {
        "Fiction": 12.99,
        "Science": 15.99,
        "History": 14.99
    }
}

# Access and print a specific product
print(store["Electronics"]["Laptop"])

# Iterate through departments and products
for department, products in store.items():
    print(f"\n{department}:")
    for product, price in products.items():
        print(f"  {product}: ${price}")
```

### Expected Output
```
999.99

Electronics:
  Laptop: $999.99
  Phone: $599.99
  Headphones: $149.99

Clothing:
  Shirt: $29.99
  Jeans: $49.99
  Jacket: $89.99

Books:
  Fiction: $12.99
  Science: $15.99
  History: $14.99
```

### Common Mistakes
- Incorrect nesting levels or bracket placement
- Forgetting to iterate through multiple levels of the dictionary

---

## Problem 12: Build a contacts book using a dictionary with nested information (phone, email, address)

### Solution
```python
# Create a contacts book with nested information
contacts = {
    "Alice": {
        "phone": "555-1001",
        "email": "alice@email.com",
        "address": "123 Main St"
    },
    "Bob": {
        "phone": "555-1002",
        "email": "bob@email.com",
        "address": "456 Oak Ave"
    },
    "Charlie": {
        "phone": "555-1003",
        "email": "charlie@email.com",
        "address": "789 Pine Rd"
    }
}

# Function to display a contact
def display_contact(name):
    if name in contacts:
        contact = contacts[name]
        print(f"Contact: {name}")
        print(f"  Phone: {contact['phone']}")
        print(f"  Email: {contact['email']}")
        print(f"  Address: {contact['address']}")
    else:
        print(f"Contact '{name}' not found")

# Display a contact
display_contact("Alice")

# List all contacts
print("\nAll Contacts:")
for name in contacts:
    print(f"  {name}")
```

### Expected Output
```
Contact: Alice
  Phone: 555-1001
  Email: alice@email.com
  Address: 123 Main St

All Contacts:
  Alice
  Bob
  Charlie
```

### Common Mistakes
- Not checking if contact exists before accessing
- Incorrect dictionary access syntax for nested data

---

## Problem 13: Given a list with duplicates, use a set to find unique items, then count each unique item

### Solution
```python
# Create a list with duplicates
items = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5]

# Find unique items using a set
unique_items = set(items)
print("Unique items:", sorted(unique_items))

# Count each unique item
print("\nItem counts:")
for item in sorted(unique_items):
    count = items.count(item)
    print(f"{item}: {count} times")

# Alternative: Using a dictionary for counts
print("\nUsing dictionary:")
count_dict = {item: items.count(item) for item in unique_items}
for item in sorted(count_dict):
    print(f"{item}: {count_dict[item]} times")
```

### Expected Output
```
Unique items: [1, 2, 3, 4, 5]

Item counts:
1: 1 times
2: 2 times
3: 3 times
4: 4 times
5: 1 times

Using dictionary:
1: 1 times
2: 2 times
3: 3 times
4: 4 times
5: 1 times
```

### Common Mistakes
- Using set without understanding it removes duplicates
- Not sorting results for consistent output

---

## Problem 14: Create a program that generates and sorts a 2D list of student records

### Solution
```python
# Create a 2D list of student records [name, grade, score]
students = [
    ["Alice", 10, 95],
    ["Bob", 11, 87],
    ["Charlie", 10, 92],
    ["Diana", 11, 89],
    ["Eve", 10, 88]
]

# Sort by grade first, then by score
students_sorted = sorted(students, key=lambda x: (x[1], x[2]))

print("Students sorted by grade, then score:")
for student in students_sorted:
    print(f"{student[0]}: Grade {student[1]}, Score {student[2]}")

# Sort by score in descending order
students_by_score = sorted(students, key=lambda x: x[2], reverse=True)

print("\nStudents sorted by score (highest first):")
for student in students_by_score:
    print(f"{student[0]}: {student[2]}")
```

### Expected Output
```
Students sorted by grade, then score:
Alice: Grade 10, Score 88
Charlie: Grade 10, Score 92
Eve: Grade 10, Score 95
Bob: Grade 11, Score 87
Diana: Grade 11, Score 89

Students sorted by score (highest first):
Alice: Grade 10, Score 95
Charlie: Grade 10, Score 92
Eve: Grade 10, Score 88
Diana: Grade 11, Score 89
Bob: Grade 11, Score 87
```

### Common Mistakes
- Incorrect sorting key syntax in lambda function
- Not understanding tuple ordering in sorting (sorts by first element, then second, etc.)

---

## Problem 15: Use list and set operations to find common elements between multiple lists

### Solution
```python
# Create multiple lists
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]
list3 = [3, 4, 5, 9, 10]

# Convert lists to sets
set1 = set(list1)
set2 = set(list2)
set3 = set(list3)

# Find common elements between all three lists (intersection)
common = set1 & set2 & set3
print("Common elements in all lists:", sorted(common))

# Find elements common between any two lists
common_1_2 = set1 & set2
common_1_3 = set1 & set3
common_2_3 = set2 & set3

print(f"Common between list1 and list2: {sorted(common_1_2)}")
print(f"Common between list1 and list3: {sorted(common_1_3)}")
print(f"Common between list2 and list3: {sorted(common_2_3)}")

# Find elements unique to list1 (not in list2 or list3)
unique_to_list1 = set1 - set2 - set3
print(f"Unique to list1: {sorted(unique_to_list1)}")

# Find all unique elements across all lists
all_unique = set1 | set2 | set3
print(f"All unique elements: {sorted(all_unique)}")
```

### Expected Output
```
Common elements in all lists: [4, 5]
Common between list1 and list2: [4, 5]
Common between list1 and list3: [3, 4, 5]
Common between list2 and list3: [4, 5]
Unique to list1: [1, 2]
All unique elements: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Common Mistakes
- Confusing union (|) with intersection (&)
- Using subtraction incorrectly for finding differences
