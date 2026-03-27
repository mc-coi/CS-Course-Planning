# Unit 6: APIs & External Libraries
> Leverage external libraries and APIs to build powerful applications. Work with real data and visualization.

##  Unit Overview
- **Duration:** 6 days / 2 weeks
- **Key Concepts:** Package management (pip), requests library, JSON APIs, data visualization (matplotlib), numerical computing (numpy)
- **Big Idea:** Standing on the shoulders of giants—use existing tools rather than reinventing the wheel
- **TN Standard:** 9-12.CCI.4 — Leverage existing tools and libraries

##  Learning Targets
- I can install and manage Python packages with pip
- I can make HTTP requests and parse responses
- I can work with REST APIs and JSON data
- I can create visualizations with matplotlib
- I can perform numerical operations with numpy
- I can integrate multiple libraries in projects

---

# Day 1: Pip & Package Management
**Learning Target:** I can install and manage Python packages using pip and virtual environments.

### Key Concepts
**pip:** Package installer for Python
**Virtual environment:** Isolated Python setup for projects
**requirements.txt:** Lists project dependencies

### Code Examples
```bash
# Install package
pip install requests

# Install specific version
pip install requests==2.28.0

# Upgrade package
pip install --upgrade requests

# Uninstall package
pip uninstall requests

# List installed packages
pip list

# Create virtual environment
python -m venv my_env

# Activate (macOS/Linux)
source my_env/bin/activate

# Activate (Windows)
my_env\Scripts\activate

# Create requirements.txt
pip freeze > requirements.txt

# Install from requirements.txt
pip install -r requirements.txt
```

### Python Code Examples
```python
import requests

# Check if package is installed
try:
    import requests
    print("requests is installed")
except ImportError:
    print("requests not installed")
```

### Guided Practice
Create virtual environment, install packages, generate requirements.txt.

### Practice Problems
**Problem 1 — Beginner:** Install a package with pip.

**Problem 2 — Intermediate:** Create virtual environment and install multiple packages.

**Problem 3 — Challenge:** Create requirements.txt for a project.

<details>
<summary>✅ Sample Answers</summary>

```bash
# Problem 2
python -m venv my_project
source my_project/bin/activate
pip install requests matplotlib numpy
pip freeze > requirements.txt
```
</details>

---

# Day 2: The requests Library
**Learning Target:** I can make HTTP requests and handle responses using the requests library.

### Key Concepts
**HTTP methods:** GET (retrieve), POST (create), PUT (update), DELETE
**Status codes:** 200 (OK), 404 (not found), 500 (server error)
**Response object:** Contains status, headers, body

### Code Examples
```python
import requests

# GET request
response = requests.get("https://api.example.com/data")
print(response.status_code)  # 200, 404, etc.
print(response.text)         # Raw response
print(response.headers)      # Headers dict

# Check if successful
if response.status_code == 200:
    data = response.json()  # Parse JSON

# GET with parameters
params = {"query": "python", "limit": 10}
response = requests.get("https://api.example.com/search", params=params)

# POST request
data = {"name": "Alice", "age": 25}
response = requests.post("https://api.example.com/users", json=data)

# Error handling
try:
    response = requests.get("https://api.example.com/data", timeout=5)
    response.raise_for_status()  # Raise if error status
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```

### Guided Practice
Make requests to public API, parse response.

### Practice Problems
**Problem 1 — Beginner:** Make a GET request and print response status.

**Problem 2 — Intermediate:** Parse JSON from API response.

**Problem 3 — Challenge:** Handle errors in API requests.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import requests
response = requests.get("https://api.github.com/users/github")
user_data = response.json()
print(user_data["name"], user_data["public_repos"])

# Problem 3
try:
    response = requests.get("https://api.example.com/data")
    response.raise_for_status()
except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```
</details>

---

# Day 3: Working with JSON APIs
**Learning Target:** I can interact with REST APIs, fetch real data, and process JSON responses.

### Key Concepts
**REST API:** Web service using HTTP for CRUD operations
**JSON:** Lightweight data format
**Authentication:** API keys for access control

### Code Examples
```python
import requests
import json

# Fetch data from public API
response = requests.get("https://api.coindesk.com/v1/bpi/currentprice.json")
data = response.json()

# Navigate nested JSON
price_usd = data["bpi"]["USD"]["rate"]
print(f"Bitcoin: ${price_usd}")

# Process multiple results
response = requests.get("https://api.github.com/repos/python/cpython/issues")
issues = response.json()
for issue in issues[:3]:
    print(issue["title"], issue["state"])

# Using API with authentication (API key)
headers = {"Authorization": "Bearer YOUR_API_KEY"}
response = requests.get("https://api.example.com/protected", headers=headers)

# Paginated results
page = 1
all_data = []
while page <= 3:
    params = {"page": page}
    response = requests.get("https://api.example.com/data", params=params)
    all_data.extend(response.json())
    page += 1
```

### Guided Practice
Fetch weather data, stock data, or other public API information.

### Practice Problems
**Problem 1 — Beginner:** Fetch and display data from public API.

**Problem 2 — Intermediate:** Process multiple API results.

**Problem 3 — Challenge:** Handle pagination and combine data.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
import requests
response = requests.get("https://api.agify.io?name=michael")
data = response.json()
print(f"{data['name']} is approximately {data['age']} years old")

# Problem 2
response = requests.get("https://jsonplaceholder.typicode.com/posts")
posts = response.json()
for post in posts[:5]:
    print(f"ID {post['id']}: {post['title']}")
```
</details>

---

# Day 4: Data Visualization with matplotlib
**Learning Target:** I can create charts and visualizations with matplotlib.

### Key Concepts
**matplotlib:** Python plotting library
Common plots: line, bar, scatter, histogram
**pyplot:** Matplotlib's pyplot interface (easy plotting)

### Code Examples
```python
import matplotlib.pyplot as plt

# Line plot
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]
plt.plot(x, y)
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
plt.title("Line Plot")
plt.show()

# Bar chart
categories = ["A", "B", "C", "D"]
values = [10, 24, 36, 18]
plt.bar(categories, values)
plt.title("Bar Chart")
plt.show()

# Scatter plot
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 6]
plt.scatter(x, y)
plt.title("Scatter Plot")
plt.show()

# Histogram
data = [1, 1, 1, 2, 2, 3, 4, 4, 4, 4, 5]
plt.hist(data, bins=5)
plt.title("Histogram")
plt.show()

# Multiple subplots
fig, (ax1, ax2) = plt.subplots(1, 2)
ax1.plot([1, 2, 3], [1, 4, 9])
ax1.set_title("Subplot 1")
ax2.bar(["A", "B"], [10, 20])
ax2.set_title("Subplot 2")
plt.show()
```

### Guided Practice
Create visualizations from data files or APIs.

### Practice Problems
**Problem 1 — Beginner:** Create a simple line plot.

**Problem 2 — Intermediate:** Create multiple plot types.

**Problem 3 — Challenge:** Visualize API data.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 3
import requests
import matplotlib.pyplot as plt

response = requests.get("https://api.example.com/data")
data = response.json()
names = [item["name"] for item in data]
values = [item["value"] for item in data]

plt.bar(names, values)
plt.title("Data Visualization")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
</details>

---

# Day 5: numpy Basics
**Learning Target:** I can use numpy for efficient numerical operations.

### Key Concepts
**numpy:** Numerical Python library
**Arrays:** Similar to lists but optimized
**Vectorized operations:** Element-wise operations without loops

### Code Examples
```python
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
zeros = np.zeros((3, 3))
ones = np.ones((2, 4))
range_arr = np.arange(0, 10, 2)

# Array operations
arr + 10       # [11, 12, 13, 14, 15]
arr * 2        # [2, 4, 6, 8, 10]
arr ** 2       # [1, 4, 9, 16, 25]

# Statistics
np.mean([1, 2, 3, 4, 5])   # 3.0
np.median([1, 2, 3, 4, 5]) # 3.0
np.std([1, 2, 3, 4, 5])    # 1.414...

# 2D arrays
matrix = np.array([[1, 2, 3], [4, 5, 6]])
matrix[0]       # [1, 2, 3]
matrix[0, 1]    # 2

# Reshaping
arr = np.arange(12)
reshaped = arr.reshape(3, 4)

# Useful functions
np.sum([1, 2, 3, 4])
np.max([1, 2, 3, 4])
np.min([1, 2, 3, 4])
np.sort([3, 1, 4, 1, 5])
```

### Guided Practice
Perform numerical operations on arrays.

### Practice Problems
**Problem 1 — Beginner:** Create numpy arrays and perform operations.

**Problem 2 — Intermediate:** Calculate statistics with numpy.

**Problem 3 — Challenge:** Work with 2D arrays and reshaping.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import numpy as np
grades = np.array([92, 88, 95, 87, 90])
print(f"Mean: {np.mean(grades)}")
print(f"Median: {np.median(grades)}")
print(f"Std Dev: {np.std(grades)}")

# Problem 3
data = np.arange(12)
matrix = data.reshape(3, 4)
print(matrix.sum(axis=1))  # Sum each row
```
</details>

---

# Day 6: Project Day — API Data Dashboard
**Learning Target:** I can integrate multiple libraries to fetch, process, and visualize real data.

### Project Overview
Build an interactive dashboard that:
- Fetches data from public APIs
- Processes and analyzes data
- Creates visualizations
- Displays results

### Requirements
- Use requests to fetch API data
- Process with numpy/lists
- Visualize with matplotlib
- Handle errors gracefully
- Provide useful insights

### Scaffold & Starter Code
```python
import requests
import matplotlib.pyplot as plt
import numpy as np

class DataDashboard:
    def __init__(self, api_url):
        self.api_url = api_url
        self.data = None
        self.fetch_data()

    def fetch_data(self):
        try:
            response = requests.get(self.api_url)
            response.raise_for_status()
            self.data = response.json()
        except requests.exceptions.RequestException as e:
            print(f"Error fetching data: {e}")

    def analyze(self):
        if not self.data:
            return
        # Process data
        return {}

    def visualize(self):
        if not self.data:
            return
        # Create plots
        plt.show()

    def display_report(self):
        if not self.data:
            print("No data available")
            return
        print("=== Data Dashboard Report ===")
        # Display stats
        self.visualize()

# Example usage
dashboard = DataDashboard("https://api.coindesk.com/v1/bpi/currentprice.json")
dashboard.display_report()
```

### Enhancement Ideas
- Real-time data updates
- Multiple data sources
- Export reports to file
- Interactive controls
- Caching to reduce API calls

---

# Unit Practice Bank

1. **Beginner:** Install a package with pip.
2. **Beginner:** Make a GET request with requests.
3. **Beginner:** Parse JSON response.
4. **Intermediate:** Fetch and process API data.
5. **Intermediate:** Create line plot with matplotlib.
6. **Intermediate:** Perform numpy operations.
7. **Challenge:** Integrate multiple libraries.
8. **Challenge:** Build data dashboard.
9. **Challenge:** Handle API pagination.
10. **Challenge:** Create visualizations from API data.
11. **Challenge:** Perform statistical analysis with numpy.
12. **Challenge:** Build real-time data fetcher.
13. **Challenge:** Create interactive visualizations.
14. **Challenge:** Integrate with multiple APIs.
15. **Challenge:** Build complete analytics application.

---

# Common Mistakes & How to Fix Them
| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to activate virtual environment | Installs to system Python | Activate venv with source/Scripts |
| API returns 401 error | Unauthorized access | Check API key or authentication |
| matplotlib shows no plot | Missing plt.show() | Call plt.show() at end |
| numpy operations on lists | Slower, unexpected results | Convert to np.array first |

---

# Unit Assessment Prep

**Review Questions:**

1. What is pip used for?
2. Why use virtual environments?
3. What's a REST API?
4. How do you handle API errors?
5. What are HTTP status codes?
6. How do you parse JSON in requests?
7. How do you create a plot in matplotlib?
8. What is vectorization in numpy?
9. How do you install from requirements.txt?
10. What's the difference between API authentication methods?

**Answers:**

1. Installing and managing Python packages
2. Isolating project dependencies and avoiding conflicts
3. Web service using HTTP methods for data operations
4. Use try/except with requests.exceptions
5. 200 (OK), 404 (not found), 500 (server error)
6. Use response.json() method
7. plt.plot(), plt.bar(), etc., then plt.show()
8. Operations apply to entire arrays without explicit loops
9. pip install -r requirements.txt
10. API keys, OAuth, basic auth, etc.

---

# Vocabulary & Quick Reference

**Key Terms:**
- **pip:** Package installer for Python
- **Virtual environment:** Isolated Python setup
- **REST API:** Web service using HTTP
- **JSON:** Data format for APIs
- **Status code:** HTTP response indicator
- **Matplotlib:** Python plotting library
- **numpy:** Numerical computing library
- **Vectorization:** Array operations without loops

**Key Syntax:**
```python
# pip
pip install package_name
pip freeze > requirements.txt

# requests
import requests
response = requests.get(url)
data = response.json()

# matplotlib
import matplotlib.pyplot as plt
plt.plot(x, y)
plt.show()

# numpy
import numpy as np
arr = np.array([1, 2, 3])
np.mean(arr)
```
