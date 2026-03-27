# Day 22: Unit 1 Assessment — Data Structures

**Learning Target:** I can demonstrate mastery of lists, tuples, dictionaries, and sets through applied problem-solving.

---

## Assessment Overview

This assessment evaluates your understanding of data structures through multiple question types:
- **Part 1:** Concept questions (multiple choice and short answer)
- **Part 2:** Code analysis and debugging
- **Part 3:** Implementation challenges (write code to solve problems)

**Time: 45-60 minutes | Total Points: 100**

---

## Part 1: Concept Questions (20 points)

**Question 1.1 (2 pts):** Which data structure is best for storing a list of student names where the list won't be modified?
- A) List
- B) Tuple
- C) Dictionary
- D) Set

**Question 1.2 (2 pts):** What does this code print?
```python
lst = [1, 2, 3, 4, 5]
print(lst[-2::-1])
```
- A) `[5, 4, 3, 2, 1]`
- B) `[4, 3, 2, 1]`
- C) `[2, 1]`
- D) `[1, 2]`

**Question 1.3 (2 pts):** What is the difference between `.remove()` and `.pop()` on a list?
- A) `.remove()` takes an index; `.pop()` takes a value
- B) `.remove()` takes a value; `.pop()` takes an index
- C) `.remove()` modifies the list; `.pop()` doesn't
- D) There is no difference

**Question 1.4 (2 pts):** Which of the following can be used as a dictionary key?
- A) List
- B) Dictionary
- C) Tuple
- D) Set

**Question 1.5 (2 pts):** What does this code output?
```python
d = {"a": 1, "b": 2}
print(d.get("c", 0))
```
- A) Error (KeyError)
- B) `None`
- C) `0`
- D) `"c"`

**Question 1.6 (2 pts):** What is the purpose of list comprehensions?
- A) To create lists in a more concise and readable way
- B) To sort lists faster
- C) To remove duplicate elements
- D) To convert lists to other data types

**Question 1.7 (2 pts):** What is the time complexity of checking if an element is in a set?
- A) O(n)
- B) O(log n)
- C) O(1)
- D) O(n²)

**Question 1.8 (2 pts):** In the tuple `(1, 2, 3)`, how would you unpack it into variables?
- A) `[a, b, c] = (1, 2, 3)`
- B) `a, b, c = (1, 2, 3)`
- C) `a = (1, 2, 3)[0]`, etc.
- D) Tuples cannot be unpacked

**Question 1.9 (2 pts):** What's the result of `{1, 1, 2, 2, 3}` in Python?
- A) `{1, 1, 2, 2, 3}`
- B) `{1, 2, 3}`
- C) Error
- D) `[1, 2, 3]`

**Question 1.10 (2 pts):** What does this code do?
```python
set_a = {1, 2, 3}
set_b = {2, 3, 4}
result = set_a & set_b
```
- A) Union of sets
- B) Intersection of sets
- C) Difference of sets
- D) Symmetric difference

---

## Part 2: Code Analysis & Debugging (20 points)

**Question 2.1 (10 pts):** Find and fix the bugs in this code.

```python
def process_data(lst):
    """Remove all negative numbers from the list."""
    for num in lst:
        if num < 0:
            lst.remove(num)
    return lst

# Test
numbers = [1, -2, 3, -4, 5]
result = process_data(numbers)
print(result)
```

**Issues to identify:**
- What's wrong with modifying a list while iterating?
- What's the correct approach?

**Question 2.2 (10 pts):** Find and fix the bug in this dictionary code.

```python
def update_student_grade(students, student_id, new_grade):
    """Update a student's grade."""
    students[student_id]["grade"] = new_grade
    return students

# Test
original = {"S001": {"name": "Alice", "grade": 85}}
updated = update_student_grade(original, "S001", 90)
print(original)  # PROBLEM: Original was modified!
```

**What's the issue, and how do you fix it?**

---

## Part 3: Implementation Challenges (60 points)

**Challenge 3.1 (15 pts):** Write a function `remove_duplicates(lst)` that removes duplicate values from a list while preserving order.

```python
# Example
input_list = [1, 2, 2, 3, 1, 4]
output = remove_duplicates(input_list)
# Expected output: [1, 2, 3, 4]

# Starter code:
def remove_duplicates(lst):
    # YOUR CODE HERE
    pass
```

**Requirements:**
- Must preserve order
- Must work with any hashable data type
- Should be efficient

---

**Challenge 3.2 (15 pts):** Write a function `word_frequency(text)` that returns a dictionary of word frequencies.

```python
# Example
text = "hello world hello python"
result = word_frequency(text)
# Expected: {"hello": 2, "world": 1, "python": 1}

# Starter code:
def word_frequency(text):
    # YOUR CODE HERE
    pass
```

**Requirements:**
- Split text by spaces
- Count occurrences of each word
- Return a dictionary

---

**Challenge 3.3 (15 pts):** Write a function `find_common_elements(list1, list2)` that returns elements common to both lists.

```python
# Example
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
result = find_common_elements(list1, list2)
# Expected: [3, 4, 5] or {3, 4, 5}

# Starter code:
def find_common_elements(list1, list2):
    # YOUR CODE HERE
    pass
```

**Requirements:**
- Return common elements
- Can return list or set
- Must be efficient

---

**Challenge 3.4 (15 pts):** Design and implement a simple contact book system.

```python
class ContactBook:
    def __init__(self):
        # Initialize your data structure(s)
        pass
    
    def add_contact(self, name, phone, email):
        """Add a new contact."""
        pass
    
    def get_contact(self, name):
        """Get contact info by name."""
        pass
    
    def find_by_phone(self, phone):
        """Find contact by phone number."""
        pass
    
    def list_all_contacts(self):
        """Return all contact names."""
        pass
    
    def delete_contact(self, name):
        """Delete a contact."""
        pass

# Test your implementation:
# 1. Create a contact book
# 2. Add 3-4 contacts
# 3. Retrieve and display a contact
# 4. Find a contact by phone
# 5. Delete a contact
# 6. Demonstrate all methods work
```

**Requirements:**
- Use appropriate data structures
- Must support all listed operations
- Must handle non-existent contacts gracefully
- Should be efficient

---

## Answer Key

### Part 1: Concept Questions

| Q | Answer | Explanation |
|---|--------|-------------|
| 1.1 | B | Tuple for immutable data |
| 1.2 | B | `lst[-2::-1]` = reverse from second-to-last |
| 1.3 | B | `.remove(value)` vs `.pop(index)` |
| 1.4 | C | Only tuples/immutable types can be keys |
| 1.5 | C | `.get()` returns the default value (0) |
| 1.6 | A | Concise, readable list creation |
| 1.7 | C | Sets use hash table (O(1) average) |
| 1.8 | B | Python unpacking with `a, b, c = tuple` |
| 1.9 | B | Sets automatically remove duplicates |
| 1.10 | B | `&` is intersection operator |

---

### Part 2: Code Analysis

**2.1 Fix:**
```python
def process_data(lst):
    return [num for num in lst if num >= 0]
    # Or: return [num for num in lst if num >= 0]
    # Or: for num in list(lst) to iterate over a copy
```

**Issue:** Modifying a list while iterating causes elements to be skipped.

**2.2 Fix:**
```python
def update_student_grade(students, student_id, new_grade):
    result = students.copy()  # Create a shallow copy
    result[student_id]["grade"] = new_grade
    return result
    
    # Or for deep nested dicts, use deepcopy:
    # import copy
    # result = copy.deepcopy(students)
```

**Issue:** Dictionary assignment creates a reference, modifying the original.

---

### Part 3: Implementation Challenges

**Challenge 3.1 Solution:**
```python
def remove_duplicates(lst):
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result
```

**Challenge 3.2 Solution:**
```python
def word_frequency(text):
    words = text.split()
    freq = {}
    for word in words:
        freq[word] = freq.get(word, 0) + 1
    return freq
```

**Challenge 3.3 Solution:**
```python
def find_common_elements(list1, list2):
    return list(set(list1) & set(list2))
```

**Challenge 3.4 Solution:**
```python
class ContactBook:
    def __init__(self):
        self.contacts = {}  # {name: {"phone": "...", "email": "..."}}
    
    def add_contact(self, name, phone, email):
        self.contacts[name] = {"phone": phone, "email": email}
    
    def get_contact(self, name):
        return self.contacts.get(name, None)
    
    def find_by_phone(self, phone):
        for name, info in self.contacts.items():
            if info["phone"] == phone:
                return name
        return None
    
    def list_all_contacts(self):
        return list(self.contacts.keys())
    
    def delete_contact(self, name):
        if name in self.contacts:
            del self.contacts[name]
            return True
        return False
```

---

## Grading Rubric

**Part 1 (20 pts):** 2 points per question, all or nothing

**Part 2 (20 pts):**
- Correctly identifies issues: 5 pts each
- Provides working fix: 5 pts each

**Part 3 (60 pts):**
- 3.1-3.3: 5 pts for correct solution, 5 pts for efficiency, 5 pts for handling edge cases
- 3.4: 5 pts for data structure choice, 5 pts for each method (5 methods), bonus for robustness

---

## Reflection Questions (Optional Bonus)

1. Which data structure did you find most useful in this unit and why?
2. What was the most challenging concept to master?
3. Can you think of a real-world application for nested dictionaries?
4. Why is choosing the right data structure important for solving problems efficiently?

