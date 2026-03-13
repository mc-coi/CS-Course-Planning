# Unit Assessment Prep

**Review Questions:**

1. What is a lambda function? When would you use one?
2. Explain the difference between map(), filter(), and zip().
3. Write a list comprehension that squares numbers 1-5.
4. What is recursion? Give an example.
5. Explain the base case and recursive case.
6. What does Big O notation measure?
7. Compare O(n) and O(n²) complexity.
8. What is a decorator?
9. Explain what a closure is.
10. How would you optimize an O(n²) algorithm?

**Answers:**

1. A lambda is a small anonymous function. Use for simple operations with map(), filter(), sorted().
2. map() applies function to each item; filter() keeps items where function returns True; zip() combines iterables.
3. `[x**2 for x in range(1, 6)]` → `[1, 4, 9, 16, 25]`
4. Recursion is when a function calls itself. Example: factorial(n) = n * factorial(n-1)
5. Base case stops recursion; recursive case calls function with simpler input.
6. Big O measures how algorithm performance scales with input size.
7. O(n) is linear (fast); O(n²) is quadratic (slow for large inputs).
8. A decorator is a function that modifies another function's behavior.
9. A closure is a nested function that captures variables from its outer scope.
10. Use more efficient algorithm (sorting, binary search), reduce nested loops, use caching.

---
