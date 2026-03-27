# Day 22: Algorithm Design Patterns and Pseudocode

**Learning Target:** I can plan algorithms using pseudocode and recognize common design patterns.

---

## Key Concepts

**Pseudocode** — High-level description of an algorithm using natural language mixed with code-like structure. Language-independent, helps plan before coding.

**Algorithm Design Patterns:**
1. **Brute Force** — Try all possible solutions
2. **Divide and Conquer** — Break into smaller subproblems (merge sort, binary search)
3. **Greedy** — Make locally optimal choices (coin change, activity selection)
4. **Dynamic Programming** — Build solution from subproblems (Fibonacci with memoization)
5. **Backtracking** — Explore solutions, undo if invalid (N-Queens, sudoku)

**Benefits of Pseudocode:**
- Plan before coding
- Think about algorithm, not syntax
- Easier to refactor
- Communicate with team
- Language-independent

---

## Code Examples

```python
# Example 1: Pseudocode for binary search
"""
PSEUDOCODE for Binary Search:

FUNCTION binarySearch(array, target)
    left = 0
    right = length(array) - 1
    
    WHILE left <= right:
        mid = (left + right) / 2
        
        IF array[mid] == target:
            RETURN mid
        ELSE IF array[mid] < target:
            left = mid + 1
        ELSE:
            right = mid - 1
    
    RETURN -1  // not found
"""

# Python implementation
def binary_search(array, target):
    left, right = 0, len(array) - 1
    while left <= right:
        mid = (left + right) // 2
        if array[mid] == target:
            return mid
        elif array[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Example 2: Pseudocode for merge sort
"""
PSEUDOCODE for Merge Sort:

FUNCTION mergeSort(array)
    IF length(array) <= 1:
        RETURN array
    
    mid = length(array) / 2
    left = mergeSort(first half of array)
    right = mergeSort(second half of array)
    
    RETURN merge(left, right)

FUNCTION merge(left, right)
    result = empty array
    
    WHILE both left and right have elements:
        IF left[0] <= right[0]:
            append left[0] to result
            remove left[0] from left
        ELSE:
            append right[0] to result
            remove right[0] from right
    
    append remaining elements to result
    RETURN result
"""

# Example 3: Brute force - finding duplicates
"""
PSEUDOCODE - Brute Force Duplicates:

FUNCTION hasDuplicates(array)
    FOR i = 0 to length(array) - 1:
        FOR j = i + 1 to length(array) - 1:
            IF array[i] == array[j]:
                RETURN True
    RETURN False
"""

def has_duplicates_brute(lst):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False

# Example 4: Greedy - coin change problem
"""
PSEUDOCODE - Greedy Coin Change:

FUNCTION coinChange(amount, coins)
    // Assume coins sorted in descending order
    count = 0
    
    FOR each coin value:
        WHILE amount >= coin:
            amount = amount - coin
            count = count + 1
    
    IF amount == 0:
        RETURN count
    ELSE:
        RETURN -1  // impossible
"""

def coin_change_greedy(amount, coins):
    coins = sorted(coins, reverse=True)
    count = 0
    for coin in coins:
        while amount >= coin:
            amount -= coin
            count += 1
    return count if amount == 0 else -1

# Example 5: Dynamic Programming - climbing stairs
"""
PSEUDOCODE - Climbing Stairs (DP):

FUNCTION climbStairs(n)
    IF n <= 0:
        RETURN 0
    IF n == 1:
        RETURN 1
    
    // Can climb 1 or 2 stairs at a time
    dp = array of size n + 1
    dp[0] = 0
    dp[1] = 1
    
    FOR i = 2 to n:
        dp[i] = dp[i-1] + dp[i-2]  // ways to reach this step
    
    RETURN dp[n]
"""

def climb_stairs(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]

# Example 6: Backtracking - N-Queens (simplified pseudocode)
"""
PSEUDOCODE - N-Queens:

FUNCTION solveNQueens(n)
    solutions = empty list
    board = empty n x n grid
    
    FUNCTION backtrack(row)
        IF row == n:  // all queens placed
            SAVE copy of board to solutions
            RETURN
        
        FOR col = 0 to n - 1:
            IF isValid(board, row, col):
                place queen at (row, col)
                backtrack(row + 1)
                remove queen from (row, col)
    
    backtrack(0)
    RETURN solutions
"""

# Example 7: Two-pointer technique (pattern)
"""
PSEUDOCODE - Two Pointer Approach:

FUNCTION twoPointer(array, target)
    left = 0
    right = length(array) - 1
    
    WHILE left < right:
        sum = array[left] + array[right]
        
        IF sum == target:
            RETURN (left, right)
        ELSE IF sum < target:
            left = left + 1
        ELSE:
            right = right - 1
    
    RETURN None
"""

def two_pointer(array, target):
    left, right = 0, len(array) - 1
    while left < right:
        sum_val = array[left] + array[right]
        if sum_val == target:
            return (left, right)
        elif sum_val < target:
            left += 1
        else:
            right -= 1
    return None

# Example 8: Sliding window (pattern)
"""
PSEUDOCODE - Sliding Window:

FUNCTION slidingWindow(array, window_size)
    IF window_size > length(array):
        RETURN None
    
    max_sum = sum of first window
    current_sum = max_sum
    
    FOR i = window_size to length(array) - 1:
        // Remove leftmost, add rightmost
        current_sum = current_sum - array[i - window_size] + array[i]
        max_sum = max(max_sum, current_sum)
    
    RETURN max_sum
"""

def sliding_window(array, window_size):
    if window_size > len(array):
        return None
    
    window_sum = sum(array[:window_size])
    max_sum = window_sum
    
    for i in range(window_size, len(array)):
        window_sum = window_sum - array[i - window_size] + array[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

# Example 9: Algorithm selection guide
def algorithm_guide():
    return {
        "Need all solutions": "Backtracking",
        "Need optimal locally": "Greedy",
        "Divide into subproblems": "Divide and Conquer",
        "Build from subproblems": "Dynamic Programming",
        "Find quickly in sorted": "Binary Search",
        "Need all pairs": "Two Pointers or Nested Loops",
        "Contiguous subsequence": "Sliding Window",
        "Tree/Graph traversal": "DFS or BFS",
    }

# Example 10: Template for writing clear algorithms
"""
PSEUDOCODE - Template:

FUNCTION algorithmName(input)
    // Step 1: Initialize variables
    // Step 2: Handle edge cases
    // Step 3: Main algorithm logic
    // Step 4: Return result
"""
```

---

## Guided Practice

**Step 1:** Write pseudocode for finding the maximum element in a list.
```
FUNCTION findMax(array)
    max_value = array[0]
    FOR each element in array:
        IF element > max_value:
            max_value = element
    RETURN max_value
```

**Step 2:** Write pseudocode then code for checking if a string is a palindrome.
```
FUNCTION isPalindrome(string)
    left = 0
    right = length(string) - 1
    
    WHILE left < right:
        IF string[left] != string[right]:
            RETURN False
        left = left + 1
        right = right - 1
    
    RETURN True
```

**Step 3:** Identify which design pattern fits different problems.
```
- Finding shortest path: BFS (or dynamic programming)
- Selecting non-overlapping activities: Greedy
- Calculating optimal substructure: Dynamic Programming
```

---

## Practice Problems

**Beginner:** Write pseudocode for summing an array.

**Intermediate:** Write pseudocode for the two-pointer or sliding window technique.

**Challenge:** Choose a complex problem and write both pseudocode and implementation, clearly identifying the design pattern.

<details>
<summary>💡 Hints</summary>
- For Beginner: Simple loop and accumulator
- For Intermediate: Focus on pointer movement logic
- For Challenge: Break down the problem into clear steps
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner pseudocode
"""
FUNCTION sumArray(array)
    total = 0
    FOR each element in array:
        total = total + element
    RETURN total
"""

# Implementation
def sum_array(array):
    total = 0
    for element in array:
        total += element
    return total

# Intermediate: Sliding window max
def max_sliding_window(array, k):
    if k > len(array):
        return None
    current_sum = sum(array[:k])
    max_sum = current_sum
    for i in range(k, len(array)):
        current_sum = current_sum - array[i - k] + array[i]
        max_sum = max(max_sum, current_sum)
    return max_sum
```
</details>
