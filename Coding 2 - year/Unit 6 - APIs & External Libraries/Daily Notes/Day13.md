# Day 13: The collections Module

**Learning Target:** I can use advanced data structures like Counter, defaultdict, and deque to solve real-world problems.

---

## Key Concepts

**Counter:** Counts occurrences of items in a sequence. Useful for frequency analysis.

```python
from collections import Counter
data = ['apple', 'banana', 'apple', 'cherry', 'banana', 'apple']
counts = Counter(data)
# Counter({'apple': 3, 'banana': 2, 'cherry': 1})
```

**defaultdict:** A dictionary that provides default values for missing keys (no KeyError).

```python
from collections import defaultdict
counts = defaultdict(int)  # Missing keys default to 0
counts['apple'] += 1
```

**OrderedDict:** A dictionary that remembers insertion order (Python 3.7+ dicts do this by default, but OrderedDict is still useful).

**deque:** Double-ended queue for efficient insertion/removal at both ends.

```python
from collections import deque
queue = deque(['first', 'second', 'third'])
queue.appendleft('new_first')  # Add to front
queue.pop()                     # Remove from back
```

---

## Code Examples

```python
from collections import Counter, defaultdict, deque

# COUNTER - Count occurrences
text = "hello world hello"
char_count = Counter(text)
print(char_count)              # Counter({'l': 3, 'o': 2, 'h': 1, ...})
print(char_count.most_common(3))  # Top 3: [('l', 3), ('o', 2), ('h', 1)]

# Counting words
words = "the quick brown fox jumps over the lazy dog".split()
word_count = Counter(words)
print(word_count['the'])       # 2
print(word_count.most_common(1))  # [('the', 2)]

# DEFAULTDICT - Default values for missing keys
scores = defaultdict(int)
scores['Alice'] += 10
scores['Bob'] += 5
scores['Alice'] += 15
print(scores['Alice'])         # 25
print(scores['Charlie'])       # 0 (default)

# DEQUE - Double-ended queue
queue = deque()
queue.append('first')
queue.append('second')
queue.appendleft('priority')
print(queue.popleft())         # 'priority'
print(queue.pop())             # 'second'

# Practical: Last N items
from collections import deque
recent = deque(maxlen=3)  # Keep only last 3
for item in [1, 2, 3, 4, 5]:
    recent.append(item)
print(list(recent))        # [3, 4, 5]
```

---

## Guided Practice

1. **Word Frequency:** Count the frequency of words in a sentence using Counter.

2. **Grade Tracker:** Use defaultdict to track scores for multiple students without KeyError.

3. **Undo Stack:** Use deque to implement an undo feature (store last 5 actions).

4. **Most Common:** Find the 5 most common letters in a text using Counter.

---

## Practice Problems

**Beginner:** Count the frequency of each letter in the word "mississippi" using Counter.

**Intermediate:** Create a system to track student grades using defaultdict. Add grades and calculate averages.

**Challenge:** Implement a simple browser history using deque that stores the last 10 URLs visited.

<details>
<summary>💡 Hints</summary>
- Counter counts items automatically
- `.most_common(n)` returns the n most frequent items
- defaultdict avoids KeyError for missing keys
- deque is efficient for queue operations (FIFO)
- `maxlen` parameter in deque automatically removes old items
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
from collections import Counter

word = "mississippi"
letter_count = Counter(word)
print(letter_count)
# Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```

**Intermediate:**
```python
from collections import defaultdict

grades = defaultdict(list)

grades['Alice'].append(95)
grades['Alice'].append(87)
grades['Bob'].append(92)

for student, scores in grades.items():
    avg = sum(scores) / len(scores)
    print(f"{student}: {avg:.1f}")
```

**Challenge:**
```python
from collections import deque

history = deque(maxlen=10)

def visit(url):
    history.append(url)
    print(f"Visited: {url}")

def show_history():
    print("Recent visits:")
    for url in history:
        print(f"  {url}")

visit("google.com")
visit("github.com")
visit("stackoverflow.com")
show_history()
```
</details>
