# Unit 1 - Data Structures: Teacher Misconception & Callout Guide

## Overview
Unit 1 is foundational but deceptively subtle. Students often understand the *syntax* of lists, dictionaries, and sets without grasping the *conceptual distinctions* between them. The biggest teaching challenges are: (1) helping students internalize that "ordered vs. unordered" and "mutable vs. immutable" are design choices, not arbitrary rules, (2) preventing shallow use of data structures—students will force a dictionary when a list would work, or vice versa, (3) catching the **nested list mutable reference bug** early (the infamous `[[0]*3]*3` problem), and (4) clarifying why tuples matter when lists seem to do the same thing. This unit builds the mental model for all of Coding II; misconceptions here will cascade through OOP and recursion.

## Misconceptions by Topic

### Lists: Indexing & Slicing (Days 1–2)

**⚠️ Misconception:** "Slicing `list[2:5]` returns elements at indices 2, 3, 4, 5."
**What it looks like in code:**
```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[2:5])  # Student expects [30, 40, 50, 60], gets [30, 40, 50]
```
**Why students think this:** They interpret the colon as "from to," mentally including both endpoints (like a math interval [a, b]). English phrase "2 to 5" includes both.
**How to address it:** Use a **fence post analogy**: "Imagine indices as fence posts between elements. `[2:5]` means 'start at post 2, stop before post 5,' so you get posts 2, 3, 4 but not 5." Draw it:
```
Index:    0    1    2    3    4    5
          [    10   20   30   40   50   60   ]
          ^    ^    ^    ^    ^    ^    ^
          post0 post1 post2 post3 post4 post5
```
`nums[2:5]` grabs elements between posts 2 and 5 (not including post 5's boundary).

---

**⚠️ Misconception:** "Negative indexing counts from the end, so `list[-1]` is confusing and I should avoid it."
**What it looks like in code:**
```python
nums = [10, 20, 30, 40, 50]
# Student avoids nums[-1] and writes nums[len(nums)-1] instead
last = nums[len(nums)-1]  # Inelegant; shows fear of negative index
```
**Why students think this:** Negative numbers feel "backwards" or non-standard. They haven't yet internalized that -1 is just "one from the end."
**How to address it:** Flip the perspective: "In Python, you're counting from **both ends**. Index 0 and -1 both point to the first element—wait, no—0 is the *first*, -1 is the *last*. Show this side-by-side:
```python
nums = [10, 20, 30, 40, 50]
#      0   1   2   3   4      (positive)
#      -5  -4  -3  -2  -1     (negative)
print(nums[0], nums[-5])   # Both: 10
print(nums[-1], nums[4])   # Both: 50
```
Normalize it: "If you want the last element, `-1` is the *only* way to say it that works for any list length. Use it freely."

---

**⚠️ Misconception:** "List slicing creates a reference to the original list, so modifying the slice changes the original."
**What it looks like in code:**
```python
nums = [1, 2, 3, 4, 5]
slice_copy = nums[1:4]
slice_copy[0] = 99
print(nums)  # Student expects [1, 99, 3, 4, 5], gets [1, 2, 3, 4, 5]
```
**Why students think this:** They've been warned about "references" in the nested list context and overgeneralize.
**How to address it:** **Clarify: slicing **always creates a NEW list**. Only assignment creates references.** Show:
```python
nums = [1, 2, 3]
slice_copy = nums[1:3]  # Creates NEW list [2, 3]
slice_copy[0] = 99      # Modifies the copy, not nums
print(nums)             # [1, 2, 3] — unchanged!

# Reference assignment (different!)
alias = nums            # alias points to SAME list
alias[0] = 99          # Modifies the original
print(nums)            # [99, 2, 3]
```

---

### List Comprehensions (Day 2)

**⚠️ Misconception:** "List comprehension is just a fancy loop; I'll stick with for loops because they're clearer."
**What it looks like in code:**
```python
# Comprehension available but avoided:
squares = [x**2 for x in range(10)]

# Student writes instead:
squares = []
for x in range(10):
    squares.append(x**2)
```
**Why students think this:** They're unfamiliar with comprehension syntax and fear it's "too clever." They don't see the cognitive benefit yet.
**How to address it:** **Teach comprehension as "declarative" vs. "imperative."** Imperative (loop) says *how*; declarative (comprehension) says *what*. For reading, comprehension is faster:
```python
# "Create a list of squares from 0 to 9"
squares = [x**2 for x in range(10)]  # What I want

# vs. the procedural "how"
squares = []
for x in range(10):
    squares.append(x**2)
```
Start small: `[x for x in list]` is just "the list itself." Then add filtering: `[x for x in list if condition]`. *Then* add transformation.

---

**⚠️ Misconception:** "The condition in a list comprehension filters before the transformation, so `[x**2 for x in nums if x > 5]` squares the numbers and then filters."
**What it looks like in code:**
```python
nums = [2, 6, 3, 8, 1]
# Student thinks: square them all, then filter to > 5
result = [x**2 for x in nums if x > 5]
# Student expects [36, 64] but might confuse the order
```
**Why students think this:** The syntax reads left-to-right, and they mentally parse it as "do the expression first, then filter."
**How to address it:** **Rewrite it as a loop to show execution order:**
```python
result = []
for x in nums:
    if x > 5:              # FILTER FIRST
        result.append(x**2)  # THEN TRANSFORM
print(result)  # [36, 64]
```
The filter (`if`) is part of the loop structure, not a post-processing step. The list comprehension is just syntactic sugar for this loop.

---

### Nested Lists & 2D Lists (Day 2)

**⚠️ Misconception (CRITICAL):** "I can create a 3x3 matrix with `matrix = [[0]*3]*3` because `[0]*3` makes one row and `*3` repeats it."
**What it looks like in code:**
```python
matrix = [[0]*3]*3
matrix[0][0] = 5
print(matrix)  # Student expects [[5, 0, 0], [0, 0, 0], [0, 0, 0]]
               # Actually prints [[5, 0, 0], [5, 0, 0], [5, 0, 0]] ← DISASTER
```
**Why students think this:** The syntax feels parallel: `[value]*n` repeats a value, so `[list]*n` should repeat a list. It *does*, but creates **three references to the same list**, not three copies.
**How to address it:** **STOP THE CLASS. This is critical misconception #1.** Show:
```python
# WRONG—all three rows point to the SAME list object
matrix_bad = [[0]*3]*3
print(id(matrix_bad[0]))  # 140234892034560
print(id(matrix_bad[1]))  # 140234892034560 (same!)
print(id(matrix_bad[2]))  # 140234892034560 (same!)

# CORRECT—each row is a new list
matrix_good = [[0 for _ in range(3)] for _ in range(3)]
print(id(matrix_good[0]))  # 140234892034560
print(id(matrix_good[1]))  # 140234892034612 (different!)
print(id(matrix_good[2]))  # 140234892034640 (different!)
```
Use an **analogy**: "Imagine copying a piece of paper 3 times. If you do `[paper]*3`, you get three pointers to the *same* paper—edit one, all three change. Use `[copy_paper() for _ in range(3)]` to get three separate copies."

---

### Tuples: Immutability & Purpose (Day 3)

**⚠️ Misconception:** "Tuples are just immutable lists. Why not always use lists? What's the point of tuples?"
**What it looks like in code:**
```python
# Student uses lists everywhere
coords = [3, 5]  # Should be (3, 5)
person = ["Alice", 25, "Engineer"]  # Could be tuple if data won't change
return [min_val, max_val, avg_val]  # Should be tuple
```
**Why students think this:** They see syntax as arbitrary and don't understand the *design intent* behind immutability.
**How to address it:** **Explain immutability as a contract**: "A tuple says 'this data is fixed.' Three benefits:
1. **Safety**: You can't accidentally modify it later.
2. **Keys**: You can use tuples as dictionary keys because they're hashable. Lists can't be keys because they could change.
3. **Semantics**: Reading `(3, 5)` signals 'this is a coordinate'—one indivisible thing. Reading `[3, 5]` signals 'this is a collection of items I might filter or rearrange.'"

Show:
```python
# Tuples as dict keys—tuples are hashable
locations = {(40.7, -74.0): "New York"}  # Works!
# cities = {[40.7, -74.0]: "New York"}  # TypeError—unhashable

# Tuple semantics
def get_stats(nums):
    return (min(nums), max(nums), sum(nums)/len(nums))
# The return type is semantically "a triple of stats," not "a list of numbers"
```

---

**⚠️ Misconception:** "I can't modify a tuple, so `point = (3, 5); point[0] = 10` fails. But I can do `point = (10, 5)` to 'reassign' the element. These are the same thing."
**What it looks like in code:**
```python
point = (3, 5)
# point[0] = 10  # TypeError
point = (10, 5)  # This works!

# Student thinks both are "modifying the tuple"
```
**Why students think this:** Both change what `point` refers to, so they seem equivalent.
**How to address it:** **Clarify rebinding vs. mutation.** Immutability means the *tuple object itself* can't change. Rebinding the variable is different:
```python
point = (3, 5)  # point refers to tuple object A
point[0] = 10   # ERROR—can't mutate tuple object A

point = (10, 5) # point now refers to a NEW tuple object B
                # Tuple object A hasn't changed; we just switched variables
```
Use an **analogy**: "A tuple is a locked box. You can't open it and swap the contents (`point[0] = 10`). But you *can* throw away the box and buy a new one (`point = (10, 5)`)."

---

**⚠️ Misconception:** "Tuple unpacking only works if I know the exact number of values."
**What it looks like in code:**
```python
# Student avoids unpacking because of fear of mismatch
coords = (3, 5, 10)
# x, y = coords  # ERROR: too many values to unpack
# Student resorts to indexing:
x = coords[0]
y = coords[1]
z = coords[2]
```
**Why students think this:** They've hit the "too many values" error once and overgeneralize.
**How to address it:** **Teach *extended unpacking* with `*`:**
```python
coords = (3, 5, 10)
x, y, *rest = coords  # x=3, y=5, rest=[10]
a, *middle, z = coords  # a=3, middle=[5], z=10

# Or swap:
a, b = 5, 10
a, b = b, a  # Pythonic swap!
```
Show that mismatches are *caught errors*, which is good—they prevent silent bugs.

---

### Dictionaries: Keys & Access (Days 4)

**⚠️ Misconception:** "Dictionary keys must be strings."
**What it looks like in code:**
```python
student = {
    0: "Alice",      # Student thinks numbers are wrong
    1: "Bob",
    "Alice": 3.9     # Converts to use string keys everywhere
}
```
**Why students think this:** Many introductory examples use string keys (e.g., `student["name"]`), and it's the most natural case.
**How to address it:** **Show diverse key types:**
```python
# Integers as keys (e.g., student IDs)
grades = {101: 92, 102: 85, 103: 88}

# Tuples as keys (e.g., coordinates)
locations = {(40.7, -74.0): "New York", (51.5, -0.1): "London"}

# The rule: keys must be HASHABLE (immutable, unique)
# Strings, numbers, tuples ✓
# Lists, dicts, sets ✗ (mutable, not hashable)
```

---

**⚠️ Misconception (CRITICAL):** "If a key doesn't exist, I should use `dict[key]` and catch the KeyError. That's the 'normal' way."
**What it looks like in code:**
```python
student = {"name": "Alice", "gpa": 3.9}

try:
    age = student["age"]
except KeyError:
    age = None

# Or worse, student checks after:
if "age" in student:
    age = student["age"]
else:
    age = None
```
**Why students think this:** They've been taught error handling and think it's the "robust" approach.
**How to address it:** **Normalize `.get()`:** "In Python, use `.get(key, default)` to safely access dictionary keys. It's the **idiomatic** way:
```python
# Best practice:
age = student.get("age", None)
# Or even simpler (None is the default):
age = student.get("age")

# Try-except is for unexpected errors, not expected missing keys.
```
Frame `.get()` as "the dictionary's safety method." It's not defensive programming; it's *normal Python*.

---

**⚠️ Misconception:** "I can modify a dictionary while iterating, so `for key in dict: del dict[key]` should work."
**What it looks like in code:**
```python
data = {"a": 1, "b": 2, "c": 3}
for key in data:
    if data[key] < 2:
        del data[key]  # RuntimeError: dictionary changed size during iteration
```
**Why students think this:** They haven't encountered the error yet or don't understand *why* it happens.
**How to address it:** **Teach the workaround:**
```python
# WRONG
for key in data:
    del data[key]  # Error!

# CORRECT—iterate over a snapshot
for key in list(data.keys()):
    del data[key]

# Or build a new dict
data = {k: v for k, v in data.items() if v >= 2}
```
Explain: "The loop is iterating over the dictionary's internal order. If you change it mid-loop, the iterator gets confused. Create a snapshot of keys first with `list(data.keys())`."

---

### Sets: Uniqueness & Operations (Day 5)

**⚠️ Misconception (VERY COMMON):** "An empty set is `{}`."
**What it looks like in code:**
```python
empty = {}
empty.add(1)  # AttributeError: 'dict' object has no attribute 'add'
```
**Why students think this:** `{}` looks like the natural empty set notation.
**How to address it:** **Explode this in the first set lesson:** "In Python, `{}` is an **empty dictionary**, not a set! To create an empty set, you **must** use `set()`. This is one of the most common mistakes. Write it on the board:
```python
empty_dict = {}           # Dictionary!
empty_set = set()         # Set!

fruits = {"apple"}        # Set with one item
fruit = {"apple": 1}      # Dictionary with one key-value pair
```
Repeat this verbally and visually until it's automatic.

---

**⚠️ Misconception:** "Sets are unordered, so I can't rely on their order. I should convert to a list and sort if I need order."
**What it looks like in code:**
```python
data = {3, 1, 4, 1, 5}
# Student converts to list:
sorted_data = sorted(list(data))  # [1, 3, 4, 5]
# Instead of just:
sorted_data = sorted(data)  # [1, 3, 4, 5]
```
**Why students think this:** They're being cautious and explicitly converting.
**How to address it:** **Clarify that `sorted()` accepts any iterable:**
```python
s = {3, 1, 4, 1, 5}
print(sorted(s))  # [1, 3, 4, 5] — works directly!

# sorted() returns a list anyway, so no need to convert first
```

---

**⚠️ Misconception:** "Set operations (`|`, `&`, `-`) are cool, but I don't understand when to use them instead of loops."
**What it looks like in code:**
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Student writes:
common = []
for item in set1:
    if item in set2:
        common.append(item)
common = list(set(common))

# Instead of:
common = set1 & set2  # {3, 4}
```
**Why students think this:** Set operations feel abstract. They don't see the readability or efficiency gain.
**How to address it:** **Show performance AND readability:**
```python
# Set intersection is O(n), loop with membership test is O(n²)
# And it's way clearer!

# What do you want?
common = set1 & set2      # Intersection—fast and obvious
only_in_1 = set1 - set2   # Difference—fast and obvious
all_in_both = set1 | set2 # Union—fast and obvious

# Teach: "Use set operations for set logic. Use loops when you need to transform or iterate."
```

---

### Choosing Data Structures (Day 5)

**⚠️ Misconception:** "Any data structure works for any problem. The choice doesn't really matter."
**What it looks like in code:**
```python
# Student uses a dictionary when a set would be clearer:
seen_ids = {id: True for id in ids}  # Wasteful!
if user_id in seen_ids: ...

# Or uses a list when a dictionary is appropriate:
student_info = [["Alice", 95], ["Bob", 87]]  # Harder to look up by name
# Instead of:
student_info = {"Alice": 95, "Bob": 87}
```
**Why students think this:** They haven't internalized the *cost* of different structures (lookup time, memory, semantic meaning).
**How to address it:** **Teach the decision tree:**
```
Question 1: Do I need to look things up by name or ID (not position)?
  → Yes: Use a DICTIONARY (fast lookup by key)
  → No: Continue to Question 2

Question 2: Is the order important?
  → Yes: Use a LIST (ordered)
  → No: Continue to Question 3

Question 3: Do I only care about unique items, or do I need duplicates?
  → Only unique: Use a SET (no duplicates, fast membership test)
  → Need duplicates: Use a LIST
```

Reinforce with examples:
```python
# Phone book: Names → Phone numbers
phonebook = {"Alice": "555-1234", "Bob": "555-5678"}  # DICT

# Grade history: [A, B+, A-, B]
grades = [90, 87, 89, 85]  # LIST (order matters, may have duplicates)

# Unique page visitors on a website
visitors = {"alice@example.com", "bob@example.com", "charlie@example.com"}  # SET
```

---

## Whole-Class Warning Signs

- Students use `[0]*n*n` without understanding the aliasing problem (check Day 2 code)
- Many students ask "when do I use tuples?" unprompted—they don't see the need yet
- Students avoiding negative indexing; they're writing `list[len(list)-1]` instead of `list[-1]`
- Widespread use of `.get()` is NOT happening; students are using `try-except` or if-checks instead
- Students creating empty sets with `{}`; lots of `AttributeError: 'dict' object has no attribute 'add'`
- Code has `{item: True for item in items}` when `set(items)` is way clearer
- List comprehensions are not being used; students are writing long for loops instead
- Students confused about whether slicing modifies the original list (it doesn't)
- Difficulty expressing set logic without loops; set operations aren't being used

---

## Questions That Reveal Understanding

1. **"You have a list `[10, 20, 30, 40, 50]`. Without running the code, what does `list[1:4]` return? Why?"**
   - Good answer: `[20, 30, 40]` because slicing is exclusive of the stop index. "It's like saying start at position 1, go up to but not including position 4."
   - Red flag: Includes the stop index, or counts from 1 instead of 0.

2. **"Why would I ever use a tuple instead of a list? Give me two real reasons."**
   - Good answer: "To use as a dictionary key (tuples are hashable, lists aren't)" AND "to protect data from accidental modification" OR "to signal that this is a fixed piece of data (like a coordinate)."
   - Red flag: "It's faster" (true but not usually the reason) or "I don't know" (suggests tuples aren't being used yet).

3. **"I want to create a 2x3 matrix with zeros. Show me the right way and explain why `[[0]*3]*2` is wrong."**
   - Good answer: `[[0 for _ in range(3)] for _ in range(2)]` or `[[0]*3 for _ in range(2)]`. Explanation: "With `[0]*3*2`, all rows point to the *same* list, so modifying one row modifies all of them."
   - Red flag: "I'm not sure" or creates the wrong code.

4. **"You have a dictionary `data = {"name": "Alice", "age": 25}`. How would you safely get the value for key 'salary' if you're not sure it exists?"**
   - Good answer: `data.get("salary")` or `data.get("salary", 0)` or `data.get("salary", "N/A")`.
   - Red flag: Tries to use `data["salary"]` directly (wrong, will error) or writes try-except when not needed.

5. **"What's the difference between `list[1:4]` and `list[1:4:2]`?"**
   - Good answer: The first gets elements at indices 1, 2, 3. The second gets every 2nd element in that range: indices 1 and 3. So `[10, 20, 30, 40, 50][1:4:2]` returns `[20, 40]`.
   - Red flag: Confusion about the third parameter (step).

6. **"Create a set with numbers 1-5, then tell me: What's `set1 & set2` for two sets? Why would you use this instead of a loop?"**
   - Good answer: Intersection—the elements that appear in both sets. "It's faster (O(n) vs. O(n²) with loops) and way more readable. If you want a Venn diagram operation, use set operations."
   - Red flag: "I'd just use a loop" (fine, but missing the elegance and performance).

7. **"If you do `[x**2 for x in range(10) if x > 5]`, what does this create? Specifically, does it square first or filter first?"**
   - Good answer: Filters first (picks x > 5), then squares. So `[36, 49, 64, 81]` (squares of 6, 7, 8, 9).
   - Red flag: Wrong order, or uncertainty.

8. **"You have `person = ("Alice", 25, "Engineer")`. Show me two ways to access the name, and explain one issue with this tuple if you later need to add a new field."**
   - Good answer: `person[0]` or `person = ("Alice", 25, "Engineer"); name, age, job = person; print(name)`. Issue: "Tuples are fixed-size; if you want to add a new field later, you'd have to create a new tuple entirely, which is awkward."
   - Red flag: Doesn't understand unpacking or the immutability constraint.

---

## Common Student Questions & How to Answer Them

**Q: "Why do we need all these data structures? Can't I just use lists for everything?"**
A: "You *could*, but it's like asking 'why do we need cars, trains, and planes if we can just walk everywhere?' Lists are great, but for specific jobs, other structures are faster and make your code clearer. If you need to look people up by name, a dictionary is way better than a list. If you need unique items, a set is cleaner than a list. We're teaching you the right tool for the right job."

**Q: "What's the difference between a list and a 2D list?"**
A: "A list is a single row of items: `[1, 2, 3]`. A 2D list is rows of rows: `[[1, 2, 3], [4, 5, 6]]`. It's like a spreadsheet: a list is one row, a 2D list is the whole grid. To access element in the 2nd row, 3rd column, you write `list[1][2]` (remember, we count from 0)."

**Q: "Is there a difference between `list.remove(item)` and `list.pop(index)`?"**
A: "Yes! `remove()` finds the *value* and deletes the first occurrence. `pop()` finds by *index* and returns what it removed. Example: `nums = [1, 2, 3, 2]; nums.remove(2)` gives `[1, 3, 2]` (removed the first 2). `nums.pop(1)` on the original gives `(2, [1, 3, 2])` (removed the element at index 1, which is 2, and returned it). If you don't know the index, use `remove()`. If you know the position, use `pop()` and you can save the value."

**Q: "Can I have a list of lists of lists? Like, three dimensions?"**
A: "Absolutely! It's called a 3D list or a 3D array. Example: `cube = [[[0 for _ in range(3)] for _ in range(3)] for _ in range(3)]`. To access element [1][2][0], you'd write `cube[1][2][0]`. But start with 2D lists first; 3D gets confusing fast. In real applications, if you need true multi-dimensional data, libraries like NumPy are better."

**Q: "What if I try to slice with a negative step like `list[5:1:-1]`? What happens?"**
A: "Great question! Negative step reverses the direction. `list[5:1:-1]` says 'start at index 5, go backward to index 1 (exclusive), stepping by -1.' So you get indices 5, 4, 3, 2. Try it: `[10, 20, 30, 40, 50][5:1:-1]` gives `[]` because there's no index 5 in a 5-element list. But `[10, 20, 30, 40, 50][::-1]` (no start/stop, just step -1) reverses the whole list: `[50, 40, 30, 20, 10]`."

---

## Analogies That Work

1. **Nested Lists & Mutable References: The Copy Machine Analogy**
   "Imagine you have a piece of paper with a drawing on it. If you do `[paper]*3`, you're making 3 pointers to the *same* paper—edit one corner, all three change. If you do `[paper.copy() for _ in range(3)]`, you actually photocopy it three times. Now each copy is separate. In Python:
   ```python
   bad = [original_list]*3  # Three pointers to the same list
   good = [original_list[:] for _ in range(3)]  # Three separate copies
   ```"

2. **Dictionary Keys & Hashing: The Mailbox Analogy**
   "Dictionaries store mail in mailboxes labeled with keys. The key must be *immutable* (never change the label) and *hashable* (you can compute a hash to find the box quickly). Tuples work: `{(1, 2): "location"}`. Lists don't: you can't label a mailbox with something that might change. Strings and numbers work fine—they're fixed."

3. **Set Operations & Venn Diagrams: The Club Analogy**
   "Imagine two clubs: Math Club and Science Club. The intersection (`set1 & set2`) is students in *both*. The union (`set1 | set2`) is students in *either*. The difference (`set1 - set2`) is students only in Math Club. Set operations are just Venn diagrams in code."

---

## Coding 1 Gaps to Watch For

**Gap: Weak understanding of loops and iteration**
- **What it looks like:** Students struggle with `for x in list:` vs. `for i in range(len(list)):` and don't understand when to use each.
- **Quick patch:** Spend 5 minutes revisiting loop patterns. Frame the first as "when you want the items," the second as "when you need the index."
  ```python
  # Iterating items
  for fruit in fruits:
      print(fruit)

  # Iterating indices
  for i in range(len(fruits)):
      print(f"Index {i}: {fruits[i]}")
  ```

**Gap: Confusion about variable assignment and aliasing**
- **What it looks like:** Students don't understand that `a = b` creates a reference, not a copy. They're surprised when modifying `b` affects `a`.
- **Quick patch:** Explicitly teach aliasing with `is` checks:
  ```python
  a = [1, 2, 3]
  b = a
  print(a is b)  # True—same object!

  c = a[:]
  print(a is c)  # False—different objects!
  ```

**Gap: Weak with function return values and multiple returns**
- **What it looks like:** Students don't naturally return tuples or understand how to unpack a returned tuple.
- **Quick patch:** Show tuple returns early:
  ```python
  def divide(a, b):
      return (a // b, a % b)

  quotient, remainder = divide(17, 5)  # Unpacking!
  ```

**Gap: Index confusion (0 vs. 1 indexing)**
- **What it looks like:** Students sometimes count from 1 in their heads, writing `list[1]` when they mean the first element.
- **Quick patch:** Anchor with a visual. Draw out indices explicitly in the first lesson. Use phrases like "zero-th element" and "first element."

---

## Critical Misconceptions to Stop for (vs. Handle 1-on-1)

**STOP for:**
- The `[[0]*3]*3` nested list aliasing bug (Day 2) — This breaks their entire mental model of lists and will surface in every subsequent unit.
- Empty set syntax (`{}` vs. `set()`) — Too many cascading errors if not fixed immediately.
- Dictionary key access without `.get()` — Students will throw unnecessary try-except blocks and write fragile code.

**Handle 1-on-1:**
- Minor slicing misconceptions (off-by-one errors on small problems)
- Students not using set operations (can use loops; not efficient, but works)
- Overly verbose list comprehensions (redundant loops) — encourage refactoring but not a blocker
- Reluctance to use tuples (they'll learn the value over time, especially in Unit 2 with OOP)

---

## Final Note for Teachers

This unit feels "easy" because it's syntax students recognize from Coding 1. **Don't be fooled.** The misconceptions are subtle and conceptual, not syntactic. A student can write `for x in list:` perfectly but still not understand *when* to use a set vs. a list. Your job is to make these design choices intuitive by:

1. **Validating the choice.** When a student uses the right structure, point it out: "Nice—you used a set there because you only care about uniqueness, not order."
2. **Questioning the wrong choice.** When you see a dictionary being forced into a list or vice versa, ask: "Why did you choose that structure?"
3. **Building mental models.** Use analogies, visuals, and code comparisons. Don't assume understanding.

By the end of Unit 1, students should be able to **defend** their data structure choices, not just explain them.
