# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is a list? What are the key differences between lists and tuples?
2. Explain indexing and slicing. What does `list[2:5]` return?
3. What does `list[-1]` represent? Give an example.
4. What is list comprehension? Write an example that creates squares of numbers 1-5.
5. How do you add an element to a list? How do you remove one?
6. What is a dictionary? How is it different from a list?
7. How do you access a dictionary value if you don't know if the key exists (safely)?
8. What is a set? Why would you use a set instead of a list?
9. Create a 2x2 matrix and explain how to access element at position [1][0].
10. When would you use a tuple instead of a list? Name three reasons.

**Answers:**

1. A list is an ordered, mutable collection that can hold any data type. Tuples are ordered but immutable (cannot be changed), and can be used as dictionary keys.
2. Indexing gets a single element by position: `list[0]` is first. Slicing extracts a sub-list: `list[2:5]` returns elements at indices 2, 3, 4 (stop is exclusive).
3. `list[-1]` gets the last element. Example: `nums = [1, 2, 3, 4]; nums[-1]` returns `4`.
4. List comprehension creates lists concisely. `[x**2 for x in range(1, 6)]` returns `[1, 4, 9, 16, 25]`.
5. Add with `.append(item)` or `.insert(index, item)`. Remove with `.remove(value)` or `.pop(index)`.
6. A dictionary stores key-value pairs. Lists are indexed by position; dictionaries are indexed by key (usually strings).
7. Use `.get(key, default_value)` which returns the value if the key exists, or the default if it doesn't.
8. A set is an unordered collection of unique items. Use sets when you need uniqueness, membership testing, or mathematical operations (union, intersection).
9. `matrix = [[1, 2], [3, 4]]`; element at [1][0] is `3` (second row, first column).
10. Use tuples when you need immutability (function returns, protecting data), as dictionary keys, or for slight performance improvement.
