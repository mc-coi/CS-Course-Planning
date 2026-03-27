# Day 24: Algorithm Challenge Lab

**Learning Target:** I can apply algorithmic thinking and recursion to solve challenging problems efficiently.

---

## Challenge Set: Recursive and Algorithmic Problem Solving

**Note:** These are intentionally challenging. Focus on correctness first, optimization second.

---

## Challenge 1: Tower of Hanoi

Move all disks from rod A to rod C, following the rules:
1. Only one disk at a time
2. Larger disk can't be on smaller disk

```python
def hanoi(n, source, target, auxiliary):
    """
    Solve Tower of Hanoi recursively.
    n: number of disks
    source, target, auxiliary: rod names (strings)
    """
    # TODO: Implement recursive solution
    pass

# Test
hanoi(3, "A", "C", "B")  # Should print moves like "Move disk from A to C"
```

**Solution:**
```python
def hanoi(n, source, target, auxiliary):
    if n == 1:
        print(f"Move disk from {source} to {target}")
    else:
        hanoi(n - 1, source, auxiliary, target)
        print(f"Move disk from {source} to {target}")
        hanoi(n - 1, auxiliary, target, source)
```

---

## Challenge 2: Longest Common Subsequence

Find the longest sequence of characters that appear in the same order in both strings (not necessarily consecutive).

Example: "AGGTAB" and "GXTXAYB" → "GTAB" (length 4)

```python
def lcs(s1, s2, memo=None):
    """Find longest common subsequence using dynamic programming."""
    # TODO: Implement with memoization
    pass

# Test
print(lcs("AGGTAB", "GXTXAYB"))  # Should print 4
```

**Solution:**
```python
def lcs(s1, s2, memo=None):
    if memo is None:
        memo = {}
    
    key = (len(s1), len(s2))
    if key in memo:
        return memo[key]
    
    if not s1 or not s2:
        return 0
    
    if s1[0] == s2[0]:
        result = 1 + lcs(s1[1:], s2[1:], memo)
    else:
        result = max(lcs(s1[1:], s2, memo), lcs(s1, s2[1:], memo))
    
    memo[key] = result
    return result
```

---

## Challenge 3: N-Queens Problem (Simplified)

Find if it's possible to place N queens on an N×N chessboard such that no two queens attack each other.

```python
def can_solve_nqueens(n):
    """Return True if n-queens problem has a solution."""
    def is_safe(board, row, col):
        # Check column above
        for i in range(row):
            if board[i] == col:
                return False
        # Check diagonals
        for i in range(row):
            if abs(board[i] - col) == abs(i - row):
                return False
        return True
    
    def backtrack(row, board):
        if row == n:
            return True
        for col in range(n):
            if is_safe(board, row, col):
                board[row] = col
                if backtrack(row + 1, board):
                    return True
                board[row] = -1
        return False
    
    board = [-1] * n
    return backtrack(0, board)

# Test
print(can_solve_nqueens(4))  # True
print(can_solve_nqueens(2))  # False
```

---

## Challenge 4: Word Break Problem

Determine if a string can be segmented into words from a dictionary.

Example: "dogcatsdog" with dict ["dog", "cat", "cats", "and", "sand"] → True ("dog cat s dog"? No. "dog cats dog"? Yes!)

```python
def word_break(s, word_dict, memo=None):
    """Determine if string can be broken into dictionary words."""
    if memo is None:
        memo = {}
    
    if s in memo:
        return memo[s]
    
    if not s:
        return True
    
    for word in word_dict:
        if s.startswith(word):
            if word_break(s[len(word):], word_dict, memo):
                memo[s] = True
                return True
    
    memo[s] = False
    return False

# Test
print(word_break("dogcatsdog", ["dog", "cats"]))  # True
print(word_break("catsandog", ["cats", "dog", "sand", "and", "cat"]))  # False
```

---

## Challenge 5: Optimal Binary Search Tree (Optional)

Given keys and their frequencies, construct a BST that minimizes average search cost.

**This is advanced** - focus on understanding the problem, not necessarily implementing it today.

---

## Project Requirements

Choose 2-3 of the above challenges and implement them:

1. Write clean, well-commented code
2. Test with multiple test cases
3. Identify time and space complexity
4. Include pseudocode or algorithm explanation

---

## Submission Checklist

- [ ] At least 2 challenges attempted
- [ ] Code runs without errors
- [ ] Each solution includes test cases
- [ ] Complexity analysis provided (Big O)
- [ ] Comments explain the algorithm

---

## Extension Ideas

1. Visualize Tower of Hanoi moves
2. Find all LCS instances (not just length)
3. Return all N-Queens solutions
4. Find shortest word break segmentation

