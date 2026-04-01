# Unit 6 - APIs & External Libraries: Teacher Misconception & Callout Guide

## Overview
Unit 6 opens the door to real-world programming by introducing package management and external libraries. The biggest teaching challenges are: (1) students don't understand *why* external libraries matter—they think they should code everything themselves, (2) pip and virtual environments feel like unnecessary overhead, (3) HTTP requests and APIs are mysterious (why does it take time? what's a status code?), (4) JSON parsing feels redundant after Unit 4, (5) matplotlib visualization is "nice but not important," and (6) students don't handle API errors or rate limits gracefully. This unit determines whether students can leverage existing tools (a key real-world skill) or waste time reinventing wheels. Misconceptions here make the capstone project harder than it needs to be.

## Misconceptions by Topic

### Package Management & pip (Day 1)

**⚠️ Misconception:** "I don't need to install external libraries; I can code everything myself."
**What it looks like in code:**
```python
# Student avoids using libraries:
import requests  # "I'll write my own HTTP client"
# Or:
import matplotlib  # "I'll plot data using print()"

# Not installed! Program crashes.
# Or never attempted.
```
**Why students think this:** They've only used built-in libraries so far.
**How to address it:** **Show the cost-benefit.** "Every library you use saves you hundreds or thousands of lines of code. `requests` handles HTTP complexity (redirects, cookies, SSL). `matplotlib` handles graphing complexity. You *could* write these yourself, but why? Use the tools—that's how real programmers work."

Show an example:
```python
# Making an HTTP request without requests:
# You'd need to understand sockets, HTTP protocol, headers, etc.
# 50+ lines of complex code

# With requests:
import requests
response = requests.get("https://api.example.com/data")
# 1 line!
```

---

**⚠️ Misconception:** "pip must be installed globally; I shouldn't use virtual environments."
**What it looks like in code:**
```python
# Student installs everything globally:
pip install requests
pip install matplotlib
pip install numpy
# All into the system Python

# Later, conflicts arise:
# Project A needs requests==2.25.0
# Project B needs requests==2.30.0
# But globally, only one version exists!
```
**Why students think this:** They don't see the value yet.
**How to address it:** **Make virtual environments mandatory for the capstone.** "A virtual environment isolates your project's packages from other projects. Project A gets requests 2.25, Project B gets requests 2.30—no conflicts. Use `python -m venv myenv` for every project."

Show the workflow:
```bash
# Create virtual environment
python -m venv capstone_env

# Activate (macOS/Linux)
source capstone_env/bin/activate

# Install packages (isolated to this project)
pip install requests matplotlib

# See installed packages
pip list

# Create requirements.txt
pip freeze > requirements.txt

# Later, someone else can recreate the environment:
pip install -r requirements.txt
```

---

**⚠️ Misconception:** "Version numbers don't matter; any version of a library works the same."
**What it looks like in code:**
```python
# Student installs without specifying version:
pip install requests  # Installs latest (2.31.0)

# Later, code breaks because API changed in 2.30.0
# Or installs while newer version is incompatible with another library
```
**Why students think this:** They haven't hit version conflicts yet.
**How to address it:** **Show version pinning for reproducibility.** "Libraries change. Newer versions might have breaking changes. Pin versions in your `requirements.txt` to ensure consistency:
```
requests==2.28.0
matplotlib==3.5.2
numpy==1.23.0
```

This guarantees that when someone else runs your code (or you do months later), they get the same versions you tested with."

---

### HTTP Requests & APIs (Days 2–3)

**⚠️ Misconception:** "An API request is instant. Why does it take time?"
**What it looks like in code:**
```python
import requests

# Student expects this to be instant:
response = requests.get("https://api.example.com/data")  # Might take 1-5 seconds!

# Doesn't understand why
```
**Why students think this:** All their code runs locally and instantly.
**How to address it:** **Explain HTTP round-trip latency.** "An API request must:
1. Travel over the internet to the server
2. Server processes the request
3. Response travels back over the internet

Each step takes time. Network latency is real. That's why you should always add a `timeout` parameter:"

```python
import requests

# Without timeout, can hang forever
response = requests.get("https://api.example.com/data", timeout=5)  # Fail after 5 seconds

# Good practice for production code
```

---

**⚠️ Misconception:** "A successful API request always returns status code 200."
**What it looks like in code:**
```python
import requests

response = requests.get("https://api.example.com/data")

# Assumes 200
data = response.json()  # Crashes if status is not 200!

# If status is 404 or 500, response.json() fails
```
**Why students think this:** In examples, requests always succeed.
**How to address it:** **Teach status code checking.** "HTTP status codes tell you the result:
- `200-299`: Success
- `300-399`: Redirect
- `400-499`: Client error (bad request, not found, etc.)
- `500-599`: Server error

Always check status before using the response:"

```python
import requests

response = requests.get("https://api.example.com/data")

# Check status
if response.status_code == 200:
    data = response.json()
else:
    print(f"Error: {response.status_code}")
    print(response.text)  # Error message from server

# Or use raise_for_status() to raise an exception
response = requests.get("https://api.example.com/data")
response.raise_for_status()  # Raises HTTPError if status is not 2xx
data = response.json()
```

---

**⚠️ Misconception:** "I can make unlimited requests to an API."
**What it looks like in code:**
```python
# Student hammers an API in a loop:
import requests

for i in range(1000):
    response = requests.get("https://api.example.com/data")
    print(response.json())

# Hits API rate limit: "429 Too Many Requests"
# Or gets IP banned!
```
**Why students think this:** They don't know about rate limiting.
**How to address it:** **Teach rate limiting and respectful API usage.** "Most APIs limit requests—e.g., 100 per minute. If you exceed it, you get status code `429`. Check documentation and add delays between requests."

```python
import requests
import time

# Respectful API usage
for i in range(100):
    response = requests.get("https://api.example.com/data", timeout=5)

    if response.status_code == 429:
        print("Rate limited! Waiting...")
        time.sleep(60)  # Wait before retrying
        continue

    data = response.json()
    # ... process data ...

    time.sleep(0.1)  # Small delay between requests
```

---

**⚠️ Misconception:** "JSON from an API is always in the same format."
**What it looks like in code:**
```python
import requests

response = requests.get("https://api.example.com/users")
data = response.json()

# Assumes structure: {"users": [{"name": "Alice", "age": 25}, ...]}
for user in data["users"]:
    print(user["name"], user["age"])

# Breaks if API returns different structure or missing fields!
```
**Why students think this:** Documentation shows one example.
**How to address it:** **Teach defensive API parsing.** "Real APIs have edge cases:
- Different response formats
- Missing fields
- Nested differently
- Paginated results

Always validate:"

```python
import requests

response = requests.get("https://api.example.com/users")
response.raise_for_status()  # Check status first
data = response.json()

# Defensive access
users = data.get("users", [])  # Default to empty list if key missing
for user in users:
    name = user.get("name", "Unknown")
    age = user.get("age", 0)
    print(f"{name} ({age})")
```

---

### Data Visualization with matplotlib (Day 4)

**⚠️ Misconception:** "Visualization is optional. I can just print the data."
**What it looks like in code:**
```python
# Student avoids matplotlib:
import requests
import json

response = requests.get("https://api.example.com/weather")
data = response.json()

# Prints raw data
for entry in data["forecast"]:
    print(entry)

# Instead of visualizing it as a graph
```
**Why students think this:** They haven't seen the power of visualization yet.
**How to address it:** **Show how visualization reveals patterns.** "Printing 100 data points is hard to interpret. A graph shows trends at a glance. Visualization is how data scientists communicate findings."

Show an example:
```python
import matplotlib.pyplot as plt
import requests

response = requests.get("https://api.example.com/weather")
data = response.json()

# Extract temperatures
temps = [entry["temp"] for entry in data["forecast"]]
days = list(range(len(temps)))

# Visualize
plt.plot(days, temps)
plt.xlabel("Day")
plt.ylabel("Temperature (°F)")
plt.title("7-Day Forecast")
plt.show()

# You immediately see: trend up, down, peaks, valleys
# Much clearer than printed numbers!
```

---

**⚠️ Misconception:** "I need to master matplotlib syntax to use it effectively."
**What it looks like in code:**
```python
# Student over-complicates:
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(x, y, linewidth=2, color='blue', linestyle='--', marker='o')
ax.set_xlabel("X", fontsize=12, weight='bold')
ax.set_ylabel("Y", fontsize=12, weight='bold')
ax.set_title("Title", fontsize=14)
ax.grid(True, alpha=0.3)
# ... many more lines

# For basic plots, this is overkill
```
**Why students think this:** They think they need to customize everything.
**How to address it:** **Show the 80/20 rule: simple plots work for most cases.** "For 80% of plots, you need just:
```python
plt.plot(x, y)
plt.show()
```

Add labels and title when needed. Customize only when you have time. Don't spend an hour styling a graph; get it right and move on."

Keep it simple:
```python
import matplotlib.pyplot as plt

# Minimal
plt.plot(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("My Data")
plt.show()

# That's enough for most uses!
```

---

**⚠️ Misconception:** "If I create many plots, I should keep calling `plt.show()` after each."
**What it looks like in code:**
```python
import matplotlib.pyplot as plt

# Wrong: blocks after first plot
plt.plot(x1, y1)
plt.show()  # Blocks; user must close to continue

plt.plot(x2, y2)  # Only runs after closing first plot
plt.show()
```
**Why students think this:** `plt.show()` displays a plot, so they think it's needed after each one.
**How to address it:** **Clarify: `plt.show()` blocks execution.** "Use `plt.show()` *once* at the end to display all plots. Or use subplots to show multiple plots in one figure:
```python
import matplotlib.pyplot as plt

# Method 1: Multiple shows
plt.figure()
plt.plot(x1, y1)

plt.figure()  # New figure
plt.plot(x2, y2)

plt.show()  # Show all at once

# Method 2: Subplots (better)
fig, (ax1, ax2) = plt.subplots(1, 2)
ax1.plot(x1, y1)
ax2.plot(x2, y2)
plt.show()
```
"

---

### NumPy Basics (Day 5)

**⚠️ Misconception:** "NumPy is just lists with different syntax."
**What it looks like in code:**
```python
import numpy as np

# Student treats arrays like lists:
arr = np.array([1, 2, 3, 4, 5])

# Doesn't see the benefit
result = [x * 2 for x in arr]  # Works, but misses numpy's power

# Instead of:
result = arr * 2  # Vectorized operation, much faster!
```
**Why students think this:** NumPy code looks similar to list code.
**How to address it:** **Show vectorization and speed.** "NumPy arrays are *fast* because operations are vectorized (done all at once, in compiled C code). Lists are slower because operations happen one-by-one in Python."

```python
import numpy as np
import time

# Large list
big_list = list(range(10000000))
arr = np.array(big_list)

# List multiplication: slow
start = time.time()
result = [x * 2 for x in big_list]
list_time = time.time() - start

# NumPy multiplication: fast
start = time.time()
result = arr * 2
numpy_time = time.time() - start

print(f"List: {list_time:.4f}s, NumPy: {numpy_time:.6f}s")
# List: ~0.5s, NumPy: ~0.002s (250x faster!)
```

---

**⚠️ Misconception:** "NumPy is only for math. I don't need it for my project."
**What it looks like in code:**
```python
# Student avoids numpy:
grades = [90, 85, 92, 88, 95]

# Calculates mean manually:
mean = sum(grades) / len(grades)

# Instead of:
import numpy as np
mean = np.mean(grades)

# Or statistics
std = sum((x - mean) ** 2 for x in grades) / len(grades)
std = (std ** 0.5)

# Instead of:
std = np.std(grades)
```
**Why students think this:** Loops and sum() are familiar.
**How to address it:** **Show NumPy makes statistics easy.** "If your project analyzes data (grades, temperatures, scores), NumPy makes it simple. Don't calculate statistics by hand—use NumPy."

```python
import numpy as np

data = [90, 85, 92, 88, 95]

print(f"Mean: {np.mean(data)}")
print(f"Median: {np.median(data)}")
print(f"Std Dev: {np.std(data)}")
print(f"Min: {np.min(data)}")
print(f"Max: {np.max(data)}")

# Much cleaner than manual loops!
```

---

## Whole-Class Warning Signs

- Students not using external libraries; they "code everything from scratch"
- No virtual environments; global pip installs with version conflicts
- Assumes all API requests return 200; doesn't check status codes
- No error handling for API requests; no timeout parameters
- Mistakes HTTP response structure; assumes one format works everywhere
- Avoids matplotlib; "print the data" mentality
- Doesn't understand rate limiting; hammers APIs
- Doesn't use NumPy for data analysis; manual loops instead
- Confused about JSON response structure; fragile parsing
- No understanding of why external libraries matter or when to use them

---

## Questions That Reveal Understanding

1. **"Explain what pip is and why virtual environments are important."**
   - Good answer: "pip installs Python packages. Virtual environments isolate project dependencies—each project gets its own packages and versions."
   - Red flag: "I don't know what pip is" or "Virtual environments are unnecessary."

2. **"Make an API request to a public API and handle the response safely."**
   - Good answer: Checks status code, handles errors, uses timeout, validates JSON structure.
   - Red flag: No error checking, assumes status is always 200, doesn't use timeout.

3. **"What do HTTP status codes mean? Give examples."**
   - Good answer: "200 = success, 404 = not found, 500 = server error. Always check status before processing."
   - Red flag: Doesn't know status codes or ignores them.

4. **"Create a simple line plot with matplotlib. What's the minimal code needed?"**
   - Good answer: Shows `plt.plot()`, labels, `plt.show()`. Keeps it simple.
   - Red flag: Over-complicates or doesn't know basic syntax.

5. **"Use NumPy to calculate mean, median, and std deviation of a list of grades."**
   - Good answer: Uses `np.mean()`, `np.median()`, `np.std()`.
   - Red flag: Manual loops or doesn't know NumPy functions.

6. **"What's the difference between a requirements.txt file and installing packages globally?"**
   - Good answer: "requirements.txt captures exact versions—reproducible. Global install risks version conflicts."
   - Red flag: "They're the same" or doesn't understand versioning.

7. **"An API returns `429 Too Many Requests`. What does this mean and how would you handle it?"**
   - Good answer: "Rate limited. Add a delay between requests or wait before retrying."
   - Red flag: Doesn't know what 429 means or would keep hammering the API.

---

## Common Student Questions & How to Answer Them

**Q: "Why should I use external libraries if I can code it myself?"**
A: "Because experts have already solved these problems better than you can in the time you have. Use `requests` instead of writing HTTP code. Use `matplotlib` instead of plotting manually. Use `numpy` instead of manual math. This frees you to focus on your logic, not the infrastructure."

**Q: "Do I have to use a virtual environment for every project?"**
A: "For serious work, yes. For simple scripts, no. But develop the habit—it's how professionals work. One command (`python -m venv myenv`) prevents hours of debugging later."

**Q: "Why do API requests take time? Can I speed them up?"**
A: "Network latency is real—data travels thousands of miles. You can't avoid it, but you can set a `timeout` and make requests in parallel (advanced). Accept that APIs are slower than local code."

**Q: "How do I know what format an API returns?"**
A: "Read the API documentation. Try a request and inspect `response.json()`. Use defensive access (`dict.get()`) to handle missing fields."

**Q: "Is matplotlib necessary for my project?"**
A: "If you're analyzing data, visualization makes insights obvious. It also looks professional in presentations. It's worth learning."

---

## Analogies That Work

1. **External Libraries as "Bought Tools"**
   "Instead of building a hammer from scratch, you buy one. External libraries are pre-built tools that solve common problems. Use them."

2. **Virtual Environments as "Isolated Workspaces"**
   "Imagine separate desks for different projects. Virtual environments are like that—each project gets its own set of packages, avoiding conflicts."

3. **HTTP Status Codes as "Traffic Lights"**
   "Green (200) = go. Red (404, 500) = stop. Yellow (3xx) = redirect. Always check the light before proceeding."

4. **APIs as "Restaurants with Menus"**
   "You make a request (order), they process it, and return a response (food). If the kitchen is busy, you wait. If they don't have what you ordered, you get an error. Handle it gracefully."

5. **NumPy as "Bulk Operations"**
   "Instead of writing one-by-one, NumPy does it all at once. Like a factory vs. manual labor—much faster."

---

## Coding 1 Gaps to Watch For

**Gap: No experience with external libraries or packages**
- **What it looks like:** Students don't understand why `import requests` is different from `import math`.
- **Quick patch:** Explain: "Built-in modules (math, json) come with Python. External packages (requests, matplotlib) must be installed with pip."

**Gap: Weak HTTP/network understanding**
- **What it looks like:** Students think the internet is "magic"; they don't understand request/response or latency.
- **Quick patch:** Show a request step-by-step: "1. Your code sends a request over the internet. 2. Server receives and processes. 3. Server sends response back. 4. Your code receives it. Each step takes time."

**Gap: No experience with error codes or exceptions**
- **What it looks like:** Students assume operations always succeed.
- **Quick patch:** Show real errors: "Status 404 means 'not found.' Status 500 means 'server error.' Always check and handle these."

---

## Critical Misconceptions to Stop for (vs. Handle 1-on-1)

**STOP for:**
- **Not checking HTTP status codes** — This leads to silent failures and confusing bugs.
- **Not understanding why external libraries matter** — If students "code from scratch," they'll waste time and produce inferior code.
- **Not using virtual environments** — This causes dependency hell and they'll lose hours debugging.

**Handle 1-on-1:**
- matplotlib customization details — they'll learn as they use it.
- NumPy advanced features — teach basics; deep features come later.
- API-specific quirks — handle as they encounter them.

---

## Final Note for Teachers

Unit 6 is where students become *practical* programmers. They learn that real code uses existing tools, not building everything from scratch. **Normalize external libraries.**

1. **Make it a habit: virtual environments first.** Every project starts with `python -m venv myenv`. Make it automatic.
2. **Show library value.** Don't just teach syntax; show why `requests` is 100x better than sockets, why `matplotlib` beats print().
3. **API error handling is essential.** Show real errors: 404, 500, 429. Teach defensive parsing and timeouts.
4. **Visualization matters.** Even basic plots reveal patterns. Encourage using them in projects.
5. **Start early with capstone.** Unit 6 is preparation for Unit 7. Using APIs and libraries in the capstone should feel natural by project start.

By the end of Unit 6, students should:
- Install and manage packages with pip
- Make HTTP requests to real APIs
- Handle API errors gracefully
- Parse JSON responses defensively
- Create basic visualizations
- Understand why external libraries are essential

This is how real programming works.
