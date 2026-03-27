# Day 19: Tree Traversal and Recursive Data Structure Traversal

**Learning Target:** I can traverse tree structures recursively and apply recursion to complex data structures.

---

## Key Concepts

**Tree** — A hierarchical data structure with a root node and child nodes. Each node has 0 or more children.

**Depth-First Traversal (DFS):**
- **Preorder:** Visit node, then traverse left, then right
- **Inorder:** Traverse left, visit node, traverse right
- **Postorder:** Traverse left, traverse right, visit node

**Breadth-First Traversal (BFS)** — Visit nodes level-by-level (typically uses queue, not recursion).

**Recursive Structure** — Trees are naturally recursive: a tree is a node with subtrees as children.

**Base Case for Trees** — When the node is None/null or a leaf node.

---

## Code Examples

```python
# Example 1: Simple TreeNode class
class TreeNode:
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

# Example 2: Preorder traversal (node, left, right)
def preorder(node):
    if node is None:
        return
    print(node.value, end=" ")  # Visit
    preorder(node.left)          # Go left
    preorder(node.right)         # Go right

# Create tree:    1
#                / \
#               2   3
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)

preorder(root)  # Output: 1 2 3

# Example 3: Inorder traversal (left, node, right)
def inorder(node):
    if node is None:
        return
    inorder(node.left)          # Go left
    print(node.value, end=" ")  # Visit
    inorder(node.right)         # Go right

inorder(root)  # Output: 2 1 3

# Example 4: Postorder traversal (left, right, node)
def postorder(node):
    if node is None:
        return
    postorder(node.left)        # Go left
    postorder(node.right)       # Go right
    print(node.value, end=" ")  # Visit

postorder(root)  # Output: 2 3 1

# Example 5: Sum all nodes in a tree
def sum_tree(node):
    if node is None:
        return 0
    return node.value + sum_tree(node.left) + sum_tree(node.right)

# More complex tree:  10
#                    /  \
#                   5    15
#                  / \
#                 3   7
root = TreeNode(10)
root.left = TreeNode(5)
root.right = TreeNode(15)
root.left.left = TreeNode(3)
root.left.right = TreeNode(7)

print(sum_tree(root))  # Output: 40 (10+5+15+3+7)

# Example 6: Find maximum in tree
def max_in_tree(node):
    if node is None:
        return float('-inf')
    
    left_max = max_in_tree(node.left)
    right_max = max_in_tree(node.right)
    
    return max(node.value, left_max, right_max)

print(max_in_tree(root))  # Output: 15

# Example 7: Tree height
def tree_height(node):
    if node is None:
        return 0
    
    left_height = tree_height(node.left)
    right_height = tree_height(node.right)
    
    return 1 + max(left_height, right_height)

print(tree_height(root))  # Output: 3

# Example 8: Count nodes
def count_nodes(node):
    if node is None:
        return 0
    return 1 + count_nodes(node.left) + count_nodes(node.right)

print(count_nodes(root))  # Output: 5

# Example 9: Traversing nested lists (non-binary tree)
def flatten_list(nested):
    """Flatten a nested list structure recursively"""
    result = []
    for item in nested:
        if isinstance(item, list):
            result.extend(flatten_list(item))  # Recurse for nested lists
        else:
            result.append(item)
    return result

nested = [1, [2, 3, [4, 5]], 6, [7]]
print(flatten_list(nested))  # Output: [1, 2, 3, 4, 5, 6, 7]

# Example 10: Depth of nested structure
def max_depth(obj):
    """Find maximum nesting depth"""
    if not isinstance(obj, list):
        return 0
    
    if not obj:
        return 1
    
    return 1 + max(max_depth(item) for item in obj)

nested = [1, [2, 3, [4, 5]], 6]
print(max_depth(nested))  # Output: 3

# Example 11: Search in tree
def search_tree(node, target):
    """Return True if target is in tree"""
    if node is None:
        return False
    
    if node.value == target:
        return True
    
    return search_tree(node.left, target) or search_tree(node.right, target)

root = TreeNode(10)
root.left = TreeNode(5)
root.right = TreeNode(15)

print(search_tree(root, 5))   # Output: True
print(search_tree(root, 20))  # Output: False

# Example 12: Building level visualization
def tree_levels(node):
    """Return list of lists, one per level"""
    if node is None:
        return []
    
    levels = []
    queue = [(node, 0)]  # (node, level)
    
    while queue:
        curr, level = queue.pop(0)
        
        if level == len(levels):
            levels.append([])
        
        levels[level].append(curr.value)
        
        if curr.left:
            queue.append((curr.left, level + 1))
        if curr.right:
            queue.append((curr.right, level + 1))
    
    return levels

root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)

print(tree_levels(root))  # Output: [[1], [2, 3], [4]]
```

---

## Guided Practice

**Step 1:** Create a tree and perform preorder traversal.
```python
class TreeNode:
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

def preorder(node):
    if node is None:
        return
    print(node.value, end=" ")
    preorder(node.left)
    preorder(node.right)

root = TreeNode(1, TreeNode(2), TreeNode(3))
preorder(root)  # Should print: 1 2 3
```

**Step 2:** Implement inorder and postorder traversals.
```python
def inorder(node):
    if node is None:
        return
    inorder(node.left)
    print(node.value, end=" ")
    inorder(node.right)

inorder(root)  # Should print: 2 1 3
```

**Step 3:** Write a function to sum all nodes in a tree.
```python
def sum_tree(node):
    if node is None:
        return 0
    return node.value + sum_tree(node.left) + sum_tree(node.right)

print(sum_tree(root))  # Should print: 6
```

---

## Practice Problems

**Beginner:** Write a function to count the total number of nodes in a tree.

**Intermediate:** Write a function to find the height of a tree (maximum distance from root to leaf).

**Challenge:** Write a function that determines if a tree is balanced (difference between left and right subtree heights is at most 1).

<details>
<summary>💡 Hints</summary>
- For Beginner: Base case is None (return 0), recursive case is 1 + left + right
- For Intermediate: Base case is None (return 0), return 1 + max of child heights
- For Challenge: Recursively check if left and right subtrees are balanced
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# Beginner
def count_nodes(node):
    if node is None:
        return 0
    return 1 + count_nodes(node.left) + count_nodes(node.right)

# Intermediate
def tree_height(node):
    if node is None:
        return 0
    left_h = tree_height(node.left)
    right_h = tree_height(node.right)
    return 1 + max(left_h, right_h)

# Challenge
def is_balanced(node):
    if node is None:
        return True
    left_h = tree_height(node.left)
    right_h = tree_height(node.right)
    return (abs(left_h - right_h) <= 1 and
            is_balanced(node.left) and
            is_balanced(node.right))
```
</details>
