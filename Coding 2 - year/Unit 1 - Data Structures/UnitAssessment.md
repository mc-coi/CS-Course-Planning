# Unit 1: Data Structures — Formal Assessment

**Duration:** 50-60 minutes | **Total Points:** 100

---

## Part 1: Concept Questions (20 points, 2 points each)

### Question 1
Which data structure would be most appropriate for storing a set of student IDs where you frequently need to check if a particular student is present?

A) List  
B) Tuple  
C) Dictionary  
D) Set  

**Correct Answer:** D

---

### Question 2
What is the output of this code?
```python
lst = [1, 2, 3, 4, 5]
print(lst[1:4])
```

A) `[1, 2, 3, 4]`  
B) `[2, 3, 4]`  
C) `[1, 2, 3]`  
D) `[2, 3]`  

**Correct Answer:** B

---

### Question 3
What is the primary difference between `.remove()` and `.pop()` on a list?

A) `.remove()` takes an index; `.pop()` takes a value  
B) `.remove()` takes a value; `.pop()` takes an index  
C) `.remove()` modifies the list; `.pop()` doesn't  
D) Both modify the list the same way  

**Correct Answer:** B

---

### Question 4
Which of the following can be used as a dictionary key?

A) `[1, 2, 3]`  
B) `{"nested": "dict"}`  
C) `(1, 2, 3)`  
D) `{1, 2, 3}`  

**Correct Answer:** C

---

### Question 5
What does this code output?
```python
d = {"a": 1, "b": 2}
print(d.get("c", 999))
```

A) Error (KeyError)  
B) `None`  
C) `999`  
D) `"c"`  

**Correct Answer:** C

---

### Question 6
What is the output of this code?
```python
s = {1, 1, 2, 2, 3, 3}
print(s)
```

A) `{1, 1, 2, 2, 3, 3}`  
B) `[1, 1, 2, 2, 3, 3]`  
C) `{1, 2, 3}`  
D) Error  

**Correct Answer:** C

---

### Question 7
What does this set operation return?
```python
set_a = {1, 2, 3}
set_b = {2, 3, 4}
result = set_a & set_b
```

A) `{1, 2, 3, 4}`  
B) `{2, 3}`  
C) `{1, 4}`  
D) `{1}`  

**Correct Answer:** B

---

### Question 8
What is the correct way to create a single-element tuple?

A) `(1)`  
B) `(1,)`  
C) `[1]`  
D) `{1}`  

**Correct Answer:** B

---

### Question 9
What is the output of this code?
```python
words = ["a", "bb", "ccc"]
lengths = [len(w) for w in words]
print(lengths)
```

A) `["a", "bb", "ccc"]`  
B) `[1, 2, 3]`  
C) `["1", "2", "3"]`  
D) Error  

**Correct Answer:** B

---

### Question 10
What is the time complexity of checking if an element exists in a set?

A) O(n)  
B) O(log n)  
C) O(1) average  
D) O(n²)  

**Correct Answer:** C

---

## Part 2: Short Answer (15 points)

### Question 2.1 (5 points)
Explain the difference between `.append()` and `.extend()` methods on lists. Give an example of each.

**Sample Answer:**
- `.append()` adds a single element (or object) to the end of the list
- `.extend()` adds all elements from an iterable to the end of the list

Example:
```python
lst = [1, 2, 3]
lst.append([4, 5])      # Result: [1, 2, 3, [4, 5]]
lst2 = [1, 2, 3]
lst2.extend([4, 5])     # Result: [1, 2, 3, 4, 5]
```

---

### Question 2.2 (5 points)
What does it mean for a tuple to be "immutable"? Why might this be useful in programming?

**Sample Answer:**
Immutable means the tuple's contents cannot be changed after creation. You cannot add, remove, or modify elements. This is useful because:
- Prevents accidental modification of important data
- Allows tuples to be used as dictionary keys
- Provides slight performance advantages over lists
- Makes tuples safer for shared data

---

### Question 2.3 (5 points)
Write a brief explanation of what tuple unpacking is and provide a code example.

**Sample Answer:**
Tuple unpacking is extracting individual elements from a tuple and assigning them to separate variables in one statement.

Example:
```python
coordinates = (10, 20)
x, y = coordinates
print(x, y)  # 10 20

# Or with multiple values:
data = (1, 2, 3, 4, 5)
first, *middle, last = data
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5
```

---

## Part 3: Code Analysis & Debugging (20 points)

### Question 3.1 (10 points)
Find and fix the bugs in this code. Explain what's wrong.

```python
def filter_negatives(numbers):
    """Remove negative numbers from the list."""
    for num in numbers:
        if num < 0:
            numbers.remove(num)
    return numbers

# Test
data = [1, -2, 3, -4, 5]
result = filter_negatives(data)
print(result)
```

**Issues & Fixes:**
1. **Problem:** Modifying a list while iterating over it causes elements to be skipped
2. **Solution:** Create a new list or use list comprehension

**Corrected Code:**
```python
def filter_negatives(numbers):
    return [num for num in numbers if num >= 0]

# Or:
def filter_negatives(numbers):
    result = []
    for num in numbers:
        if num >= 0:
            result.append(num)
    return result
```

---

### Question 3.2 (10 points)
Find and fix the bug in this dictionary code. What's the issue and how do you fix it?

```python
def add_to_scores(original_dict, name, score):
    """Add a new person and score."""
    original_dict[name] = score
    return original_dict

# Test
scores = {"Alice": 95, "Bob": 87}
updated = add_to_scores(scores, "Charlie", 92)
print("Original:", scores)
print("Updated:", updated)
# PROBLEM: Original was modified!
```

**Issue:** Assigning `original_dict[name]` directly modifies the input dictionary.

**Corrected Code:**
```python
def add_to_scores(original_dict, name, score):
    result = original_dict.copy()
    result[name] = score
    return result
```

---

## Part 4: Implementation Challenges (45 points)

### Challenge 4.1: Remove Duplicates (10 points)
Write a function `remove_duplicates(lst)` that removes duplicate values from a list while preserving the original order.

```python
def remove_duplicates(lst):
    """Remove duplicates while preserving order."""
    # TODO: Implement
    pass

# Test cases
print(remove_duplicates([1, 2, 2, 3, 1, 4]))  # [1, 2, 3, 4]
print(remove_duplicates(["a", "b", "a"]))     # ["a", "b"]
print(remove_duplicates([]))                   # []
```

**Solution:**
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

**Grading:** 5 points for correct logic, 5 points for preserving order and handling edge cases

---

### Challenge 4.2: Count Word Frequencies (10 points)
Write a function `word_frequency(text)` that returns a dictionary mapping each word to its frequency.

```python
def word_frequency(text):
    """Count frequency of each word."""
    # TODO: Implement
    pass

# Test cases
result = word_frequency("hello world hello python")
print(result)  # {"hello": 2, "world": 1, "python": 1}

result2 = word_frequency("a a a b b c")
print(result2)  # {"a": 3, "b": 2, "c": 1}
```

**Solution:**
```python
def word_frequency(text):
    words = text.split()
    freq = {}
    for word in words:
        freq[word] = freq.get(word, 0) + 1
    return freq

# Or using Counter:
from collections import Counter
def word_frequency(text):
    return dict(Counter(text.split()))
```

**Grading:** 5 points for correct frequency counting, 5 points for proper dictionary use and edge cases

---

### Challenge 4.3: Find Common Elements (10 points)
Write a function `common_elements(list1, list2)` that returns elements that appear in both lists.

```python
def common_elements(list1, list2):
    """Find elements common to both lists."""
    # TODO: Implement
    pass

# Test cases
print(common_elements([1, 2, 3, 4], [3, 4, 5, 6]))  # [3, 4] or {3, 4}
print(common_elements(["a", "b", "c"], ["b", "c", "d"]))  # ["b", "c"] or {"b", "c"}
print(common_elements([1, 2], [3, 4]))  # [] or set()
```

**Solution:**
```python
def common_elements(list1, list2):
    return list(set(list1) & set(list2))

# Or to preserve list type:
def common_elements(list1, list2):
    return [x for x in list1 if x in list2]
```

**Grading:** 5 points for correct logic, 5 points for efficient implementation and edge cases

---

### Challenge 4.4: Dictionary from Lists (10 points)
Write a function `create_phone_book(names, phone_numbers)` that combines two lists into a dictionary.

```python
def create_phone_book(names, phone_numbers):
    """Create a phone book from two parallel lists."""
    # TODO: Implement
    pass

# Test case
names = ["Alice", "Bob", "Charlie"]
phones = ["555-1234", "555-5678", "555-9012"]
book = create_phone_book(names, phones)
print(book)  # {"Alice": "555-1234", "Bob": "555-5678", ...}
```

**Solution:**
```python
def create_phone_book(names, phone_numbers):
    return dict(zip(names, phone_numbers))

# Or using dictionary comprehension:
def create_phone_book(names, phone_numbers):
    return {name: phone for name, phone in zip(names, phone_numbers)}
```

**Grading:** 5 points for correct use of zip(), 5 points for proper dictionary creation and error handling

---

### Challenge 4.5: Design a Data Structure (5 bonus points)
Design a simple library system that tracks books and borrowers. Explain your data structure choices.

```python
# Describe your design:
# 1. What data structures would you use?
# 2. Why did you choose them?
# 3. What operations would you support? (add book, borrow, return, etc.)
# 4. Show a brief code outline
```

**Sample Answer:**
```python
# Use a dictionary for fast lookup by ISBN
# Track borrow history separately
library = {
    "ISBN123": {
        "title": "Book Title",
        "author": "Author Name",
        "available": True,
        "borrower": None
    }
}

# For categories, use sets for fast membership testing
categories = {
    "Fiction": {"ISBN123", "ISBN456"},
    "Science": {"ISBN789"}
}

# Track borrowing history as list of tuples
history = [
    ("ISBN123", "Alice", "2024-01-15", "2024-01-22"),
    ...
]
```

---

## Answer Verification Checklist

- [ ] All concept questions answered
- [ ] Code analysis shows understanding of bugs
- [ ] All implementation challenges are attempted
- [ ] Code is syntactically correct
- [ ] Edge cases are handled (empty inputs, duplicates, etc.)
- [ ] Solutions match expected output

---

## Total Point Distribution

| Section | Points |
|---------|--------|
| Part 1: Concepts | 20 |
| Part 2: Short Answer | 15 |
| Part 3: Code Analysis | 20 |
| Part 4: Implementation | 45 |
| **Total** | **100** |

