# Unit 6 Reference Guide: APIs & External Libraries

Quick reference for all topics covered in Unit 6.

---

## Part 1: Web APIs & Data Fetching

### HTTP Methods
```python
requests.get(url)      # Retrieve data
requests.post(url)     # Submit data
requests.put(url)      # Update data
requests.delete(url)   # Remove data
```

### Basic GET Request
```python
import requests

response = requests.get("https://api.example.com/data")

# Check status
print(response.status_code)  # 200 = success

# Get JSON data
data = response.json()
print(data["key"])

# Get response as text
print(response.text)
```

### HTTP Status Codes
| Code | Meaning | Example |
|------|---------|---------|
| 200 | OK | Request successful |
| 201 | Created | New resource created |
| 400 | Bad Request | Invalid parameters |
| 403 | Forbidden | Access denied |
| 404 | Not Found | Resource doesn't exist |
| 500 | Server Error | Server problem |

### API with Query Parameters
```python
params = {
    "city": "New York",
    "units": "metric"
}
response = requests.get(
    "https://api.example.com/weather",
    params=params
)
```

### JSON Parsing
```python
import json

# Convert JSON string to dict
data = json.loads('{"name": "Alice", "age": 30}')

# Convert dict to JSON string
json_str = json.dumps({"name": "Bob", "age": 25})

# Pretty print JSON
print(json.dumps(data, indent=2))
```

### Error Handling
```python
import requests

try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
    data = response.json()
except requests.exceptions.ConnectionError:
    print("Network error")
except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.HTTPError as e:
    print(f"HTTP error: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```

### API Authentication
```python
# Option 1: API key in URL parameters
response = requests.get(
    url,
    params={"key": api_key}
)

# Option 2: API key in headers
headers = {"Authorization": f"Bearer {api_key}"}
response = requests.get(url, headers=headers)

# Option 3: Environment variables (BEST)
import os
api_key = os.environ.get("MY_API_KEY")
```

### Popular Free APIs
```python
# Quotes
https://api.quotable.io/random

# Pokemon
https://pokeapi.co/api/v2/pokemon/{name}

# Weather (no key)
https://api.open-meteo.com/v1/forecast

# Jokes
https://v2.jokeapi.dev/joke/Any

# Cat Facts
https://catfact.ninja/fact

# Geolocation
https://geocoding-api.open-meteo.com/v1/search
```

---

## Part 2: Standard Library Modules

### The random Module
```python
import random

random.random()          # Float 0.0-1.0
random.randint(a, b)    # Integer a-b (inclusive)
random.uniform(a, b)    # Float a-b
random.choice(seq)      # Pick one item
random.shuffle(list)    # Shuffle list in place
random.sample(seq, k)   # Choose k unique items
random.seed(42)         # Set seed for reproducibility
```

### The math Module
```python
import math

# Constants
math.pi                 # 3.14159...
math.e                  # 2.71828...

# Functions
math.sqrt(x)           # Square root
math.pow(x, y)         # x to the power y
math.ceil(x)           # Round up
math.floor(x)          # Round down
math.abs(x)            # Absolute value
math.sin(x)            # Sine (radians)
math.cos(x)            # Cosine (radians)
math.tan(x)            # Tangent (radians)
math.log(x)            # Natural logarithm
```

### The datetime Module
```python
from datetime import date, time, datetime, timedelta

# Current date
today = date.today()

# Create specific date
birthday = date(2008, 5, 15)

# Current date and time
now = datetime.now()

# Date arithmetic
next_week = today + timedelta(days=7)
next_month = today + timedelta(days=30)

# Access components
print(today.year)
print(today.month)
print(today.day)

# Format as string
print(today.strftime("%Y-%m-%d"))      # 2026-03-25
print(today.strftime("%B %d, %Y"))     # March 25, 2026
print(today.strftime("%A"))            # Tuesday

# Parse string to date
date_obj = datetime.strptime("03/25/2026", "%m/%d/%Y").date()

# Calculate difference
days_diff = (date1 - date2).days

# Common format codes
# %Y - 4-digit year     %y - 2-digit year
# %m - Month number     %B - Full month name
# %d - Day of month     %A - Full weekday
# %H - Hour (0-23)      %M - Minute
# %S - Second
```

### The collections Module
```python
from collections import Counter, defaultdict, deque, OrderedDict

# COUNTER - Count occurrences
c = Counter(['a', 'b', 'a', 'c', 'a'])
print(c['a'])                    # 3
print(c.most_common(2))          # [('a', 3), ('b', 1)]

# DEFAULTDICT - Default values for missing keys
d = defaultdict(int)
d['count'] += 1
print(d['missing'])              # 0 (default)

# DEQUE - Double-ended queue
q = deque([1, 2, 3])
q.appendleft(0)                 # Add to front
q.append(4)                     # Add to back
q.popleft()                     # Remove from front
q.pop()                         # Remove from back

# ORDEREDDICT - Remember insertion order
od = OrderedDict([('a', 1), ('b', 2)])
```

---

## Part 3: NumPy

### Creating Arrays
```python
import numpy as np

# From list
arr = np.array([1, 2, 3, 4, 5])

# Patterns
np.zeros(5)                     # [0. 0. 0. 0. 0.]
np.ones(5)                      # [1. 1. 1. 1. 1.]
np.arange(0, 10, 2)            # [0 2 4 6 8]
np.linspace(0, 1, 5)           # [0. 0.25 0.5 0.75 1.]

# 2D arrays
matrix = np.array([[1, 2], [3, 4]])
print(matrix.shape)             # (2, 2)
```

### Array Operations
```python
# Element-wise math (no loops!)
arr1 + arr2
arr1 * 2
arr1 + 10

# Statistical functions
np.sum(arr)
np.mean(arr)
np.median(arr)
np.std(arr)
np.min(arr)
np.max(arr)

# Reshaping
arr.reshape(3, 4)

# Slicing and indexing
arr[0]                          # First element
arr[1:3]                        # Elements 1-2
arr[-1]                         # Last element

# Boolean indexing (filtering)
filtered = arr[arr > 5]
count = np.sum(arr > 5)

# Sorting
np.sort(arr)

# Unique values
np.unique([1, 2, 2, 3, 3, 3])  # [1 2 3]

# Conditional replacement
grades = np.where(scores >= 90, 'A', 'B')
```

---

## Part 4: Matplotlib

### Basic Plot
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

plt.plot(x, y)
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Plot Title')
plt.show()
```

### Line Chart
```python
plt.figure(figsize=(10, 6))
plt.plot(x, y, marker='o', color='blue', linewidth=2, label='Line 1')
plt.plot(x, y2, marker='s', color='red', linestyle='--', label='Line 2')
plt.legend()
plt.grid(True)
plt.show()
```

### Bar Chart
```python
categories = ['A', 'B', 'C', 'D']
values = [10, 20, 15, 25]

plt.bar(categories, values, color='green', alpha=0.7)
plt.ylabel('Value')
plt.title('Bar Chart')
plt.show()
```

### Scatter Plot
```python
plt.scatter(x, y, color='red', s=50, alpha=0.6)
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot')
plt.show()
```

### Histogram
```python
data = [1, 1, 2, 3, 3, 3, 4, 5, 5, 5, 5]
plt.hist(data, bins=5, edgecolor='black')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

### Subplots
```python
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

axes[0, 0].plot(x, y)
axes[0, 0].set_title('Plot 1')

axes[0, 1].bar(x, y)
axes[0, 1].set_title('Plot 2')

axes[1, 0].scatter(x, y)
axes[1, 0].set_title('Plot 3')

axes[1, 1].hist(data)
axes[1, 1].set_title('Plot 4')

plt.tight_layout()
plt.show()
```

### Customization
```python
# Colors: 'r', 'g', 'b', 'k', 'y', etc. or full names
# Markers: 'o' (circle), 's' (square), '^' (triangle), '*' (star)
# Linestyles: '-' (solid), '--' (dashed), ':' (dotted), '-.' (dash-dot)

plt.plot(x, y, color='blue', marker='o', linestyle='--', linewidth=2)
plt.title('Title', fontsize=14, fontweight='bold')
plt.xlabel('X Label', fontsize=12)
plt.ylabel('Y Label', fontsize=12)

# Save figure
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
```

### Annotations
```python
plt.plot(x, y)
plt.annotate('Peak', xy=(3, 9), xytext=(3.5, 10),
            arrowprops=dict(arrowstyle='->', color='red'))
plt.show()
```

---

## Common Patterns

### Complete API + Visualization Example
```python
import requests
import numpy as np
import matplotlib.pyplot as plt

# Fetch data
response = requests.get("https://api.example.com/data")
data = response.json()

# Process data
values = np.array(data["values"])

# Visualize
plt.bar(range(len(values)), values)
plt.title("Data Visualization")
plt.show()
```

### Error-Handling Pattern
```python
import requests

try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
    return response.json()
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None
```

### Data Processing Pattern
```python
import numpy as np
from collections import Counter

# Get data
data = [1, 2, 2, 3, 3, 3, 4]

# Analyze
arr = np.array(data)
counter = Counter(data)

# Display results
print(f"Mean: {np.mean(arr)}")
print(f"Most common: {counter.most_common(1)}")
```

