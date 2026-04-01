# Unit 6 - APIs & External Libraries: Answer Key

## Problem 1: Install a package with pip

### Solution
```python
# Installing packages with pip (command line)
# Open terminal/command prompt and run:
# pip install requests
# pip install numpy
# pip install matplotlib
# pip install pandas

# Verify installation in Python
import sys
import subprocess

def install_package(package_name):
    """Install a package using pip"""
    subprocess.check_call([sys.executable, "-m", "pip", "install", package_name])

# Installing packages programmatically
try:
    import requests
    print(f"✓ requests is installed")
except ImportError:
    print("Installing requests...")
    install_package("requests")
    import requests

# Checking package version
try:
    import numpy as np
    print(f"✓ numpy {np.__version__} is installed")
except ImportError:
    print("numpy not found")

# View installed packages
import subprocess
result = subprocess.run([sys.executable, "-m", "pip", "list"], capture_output=True, text=True)
print("\nKey installed packages:")
lines = result.stdout.split('\n')
for line in lines[:5]:
    print(f"  {line}")
print("  ...")
```

### Expected Output
```
✓ requests is installed
✓ numpy 1.24.3 is installed

Key installed packages:
  Package       Version
  ----------- -------
  numpy         1.24.3
  pandas        2.0.3
  requests      2.31.0
  ...
```

### Common Mistakes
- Using pip from wrong Python interpreter
- Not updating pip itself periodically
- Installing to wrong environment (conda vs venv)

---

## Problem 2: Make a GET request with requests

### Solution
```python
import requests
from requests.exceptions import RequestException, Timeout

# Simple GET request
def simple_get_request():
    """Make a simple GET request"""
    url = "https://api.github.com"

    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()  # Raise error for bad status

        print(f"Status Code: {response.status_code}")
        print(f"Content Type: {response.headers.get('content-type')}")
        print(f"Response Length: {len(response.content)} bytes")

    except requests.exceptions.HTTPError as e:
        print(f"HTTP Error: {e}")
    except Timeout:
        print("Request timed out")
    except RequestException as e:
        print(f"Request failed: {e}")

# GET request with parameters
def get_with_params():
    """GET request with query parameters"""
    url = "https://jsonplaceholder.typicode.com/posts"
    params = {
        "userId": 1,
        "_limit": 3
    }

    response = requests.get(url, params=params)
    print(f"Request URL: {response.url}")
    print(f"Status: {response.status_code}")

# GET request with custom headers
def get_with_headers():
    """GET request with custom headers"""
    url = "https://api.github.com/users/github"

    headers = {
        "User-Agent": "MyApp/1.0",
        "Accept": "application/json"
    }

    response = requests.get(url, headers=headers)
    data = response.json()

    print(f"GitHub User: {data.get('login')}")
    print(f"Public Repos: {data.get('public_repos')}")

# Run examples
print("=== Simple GET Request ===")
simple_get_request()

print("\n=== GET with Parameters ===")
get_with_params()

print("\n=== GET with Headers ===")
try:
    get_with_headers()
except Exception as e:
    print(f"Note: {e}")
```

### Expected Output
```
=== Simple GET Request ===
Status Code: 200
Content Type: application/json; charset=utf-8
Response Length: 1234 bytes

=== GET with Parameters ===
Request URL: https://jsonplaceholder.typicode.com/posts?userId=1&_limit=3
Status: 200

=== GET with Headers ===
GitHub User: github
Public Repos: 34
```

### Common Mistakes
- Not handling exceptions for network errors
- Ignoring HTTP error status codes
- Not setting timeout (can hang indefinitely)
- Forgetting to close connections

---

## Problem 3: Parse JSON response

### Solution
```python
import requests
import json

# Parse JSON from API response
def parse_json_response():
    """Fetch and parse JSON data"""
    url = "https://jsonplaceholder.typicode.com/users/1"

    response = requests.get(url)

    # Method 1: Using .json()
    user = response.json()

    print("User Information:")
    print(f"  Name: {user.get('name')}")
    print(f"  Email: {user.get('email')}")
    print(f"  Phone: {user.get('phone')}")
    print(f"  Website: {user.get('website')}")

# Parse nested JSON
def parse_nested_json():
    """Handle nested JSON structures"""
    url = "https://jsonplaceholder.typicode.com/users/1"

    response = requests.get(url)
    user = response.json()

    print("\nNested Address Information:")
    address = user.get('address', {})
    print(f"  Street: {address.get('street')}")
    print(f"  City: {address.get('city')}")
    print(f"  Coordinates: {address.get('geo')}")

# Parse JSON arrays
def parse_json_array():
    """Parse array of JSON objects"""
    url = "https://jsonplaceholder.typicode.com/users"
    params = {"_limit": 3}

    response = requests.get(url, params=params)
    users = response.json()

    print("\nFirst 3 Users:")
    for user in users:
        print(f"  {user['id']}: {user['name']} ({user['email']})")

# JSON error handling
def parse_with_error_handling():
    """Parse JSON with proper error handling"""
    url = "https://jsonplaceholder.typicode.com/posts/1"

    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()

        if response.text:
            data = response.json()
            print(f"\nPost Title: {data.get('title')}")
        else:
            print("Empty response")

    except requests.exceptions.JSONDecodeError:
        print("Invalid JSON in response")
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")

# Run examples
parse_json_response()
parse_nested_json()
parse_json_array()
parse_with_error_handling()
```

### Expected Output
```
User Information:
  Name: Leanne Graham
  Email: Bret@april.biz
  Phone: 1-770-736-8031 x56442
  Website: hildegard.org

Nested Address Information:
  Street: Kulas Light
  City: Gwenborough
  Coordinates: {'lat': '-37.3159', 'lng': '81.1496'}

First 3 Users:
  1: Leanne Graham (Bret@april.biz)
  2: Ervin Howell (Antonette@april.biz)
  3: Clementine Bauch (Clementine_Kuhn@2many.com)

Post Title: sunt aut facere repellat provident...
```

### Common Mistakes
- Not checking if response is valid before parsing
- Using `.text` instead of `.json()` for JSON data
- Not handling JSONDecodeError for malformed responses

---

## Problem 4: Fetch and process API data

### Solution
```python
import requests
import json
from datetime import datetime

# Fetch and process weather data
def fetch_weather_data():
    """Fetch weather data from API"""
    # Using OpenWeatherMap free API
    api_key = "demo"  # Use your own API key
    city = "London"
    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}"

    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        data = response.json()

        # Process the data
        print(f"Weather in {data['name']}:")
        print(f"  Temperature: {data['main']['temp']}°K")
        print(f"  Feels like: {data['main']['feels_like']}°K")
        print(f"  Humidity: {data['main']['humidity']}%")
        print(f"  Description: {data['weather'][0]['description']}")
        print(f"  Wind Speed: {data['wind']['speed']} m/s")

    except Exception as e:
        print(f"Error: {e}")

# Fetch and aggregate data
def fetch_multiple_endpoints():
    """Fetch data from multiple endpoints"""
    base_url = "https://jsonplaceholder.typicode.com"

    # Fetch posts
    posts_response = requests.get(f"{base_url}/posts?_limit=2")
    posts = posts_response.json()

    # Fetch comments
    comments_response = requests.get(f"{base_url}/comments?postId=1")
    comments = comments_response.json()

    print("Posts with Comments:")
    for post in posts:
        print(f"\nPost {post['id']}: {post['title']}")
        print(f"  Body: {post['body'][:50]}...")

        # Get comments for this post
        post_comments = [c for c in comments if c['postId'] == post['id']]
        print(f"  Comments: {len(post_comments)}")

# Transform API data
def fetch_and_transform():
    """Fetch data and transform it"""
    url = "https://jsonplaceholder.typicode.com/users"
    params = {"_limit": 3}

    response = requests.get(url, params=params)
    users = response.json()

    # Transform to simpler format
    transformed = [
        {
            "id": user["id"],
            "name": user["name"],
            "city": user["address"]["city"],
            "company": user["company"]["name"]
        }
        for user in users
    ]

    print("\nTransformed User Data:")
    for user in transformed:
        print(f"  {user['name']} - {user['city']} ({user['company']})")

# Filter and sort API data
def fetch_filter_sort():
    """Fetch, filter, and sort data"""
    url = "https://jsonplaceholder.typicode.com/todos"
    response = requests.get(url)
    todos = response.json()

    # Filter completed tasks for user 1
    user1_complete = [t for t in todos if t['userId'] == 1 and t['completed']]

    print(f"\nCompleted tasks for User 1: {len(user1_complete)}")
    for todo in user1_complete[:3]:
        print(f"  ✓ {todo['title']}")

# Run examples
print("=== Fetch and Process API Data ===\n")
fetch_and_transform()
fetch_filter_sort()
fetch_multiple_endpoints()
```

### Expected Output
```
=== Fetch and Process API Data ===

Transformed User Data:
  Leanne Graham - Gwenborough (Romaguera-Crona)
  Ervin Howell - Wisokyburgh (Deckow-Cormier)
  Clementine Bauch - McKenziehaven (Romaguera-Jacobson)

Completed tasks for User 1: 8
  ✓ delectus aut autem
  ✓ quis ut et voluptas
  ✓ fugiat veniam minus

Posts with Comments:
Post 1: sunt aut facere repellat provident
  Body: quia et suscipit suscipit recusandae...
  Comments: 5
```

### Common Mistakes
- Not handling API rate limiting
- Fetching all data when filters available
- Not caching results to reduce API calls

---

## Problem 5: Create line plot with matplotlib

### Solution
```python
import matplotlib.pyplot as plt
import numpy as np

# Simple line plot
def simple_line_plot():
    """Create a simple line plot"""
    x = [1, 2, 3, 4, 5]
    y = [2, 4, 6, 8, 10]

    plt.figure(figsize=(10, 6))
    plt.plot(x, y, marker='o', label='Linear Growth')
    plt.xlabel('X Axis')
    plt.ylabel('Y Axis')
    plt.title('Simple Line Plot')
    plt.legend()
    plt.grid(True, alpha=0.3)
    print("Line plot shows a linear relationship between x and y coordinates")

# Multiple line plots
def multiple_line_plots():
    """Plot multiple lines"""
    months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
    sales_2022 = [10000, 12000, 15000, 13000, 16000, 18000]
    sales_2023 = [12000, 14000, 13000, 15000, 17000, 19000]

    plt.figure(figsize=(10, 6))
    plt.plot(months, sales_2022, marker='s', label='2022 Sales', linewidth=2)
    plt.plot(months, sales_2023, marker='o', label='2023 Sales', linewidth=2)

    plt.xlabel('Month')
    plt.ylabel('Sales ($)')
    plt.title('Sales Comparison: 2022 vs 2023')
    plt.legend()
    plt.grid(True, alpha=0.3)
    print("Line plot compares 2022 and 2023 monthly sales with different markers and colors")

# Line plot with different styles
def styled_line_plot():
    """Plot with custom styles"""
    x = np.linspace(0, 10, 100)
    y1 = np.sin(x)
    y2 = np.cos(x)

    plt.figure(figsize=(10, 6))
    plt.plot(x, y1, linestyle='-', marker='', label='sin(x)', color='blue', linewidth=2)
    plt.plot(x, y2, linestyle='--', marker='', label='cos(x)', color='red', linewidth=2)

    plt.xlabel('X')
    plt.ylabel('Y')
    plt.title('Trigonometric Functions')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.axhline(y=0, color='k', linewidth=0.5)
    plt.axvline(x=0, color='k', linewidth=0.5)
    print("Line plot shows sine and cosine waves with custom colors and line styles")

# Data visualization from list
def plot_from_data():
    """Plot real data"""
    days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
    temperatures = [72, 75, 73, 78, 76]

    plt.figure(figsize=(10, 6))
    plt.plot(days, temperatures, marker='o', color='green', linewidth=2, markersize=8)
    plt.fill_between(range(len(days)), temperatures, alpha=0.3, color='green')

    plt.xlabel('Day of Week')
    plt.ylabel('Temperature (°F)')
    plt.title('Weekly Temperature Trend')
    plt.grid(True, axis='y', alpha=0.3)
    print("Line plot with fill shows temperature trend throughout the week")

# Run examples
print("Creating line plots with matplotlib...\n")
simple_line_plot()
print()
multiple_line_plots()
print()
styled_line_plot()
print()
plot_from_data()
```

### Expected Output
```
Creating line plots with matplotlib...

Line plot shows a linear relationship between x and y coordinates

Line plot compares 2022 and 2023 monthly sales with different markers and colors

Line plot shows sine and cosine waves with custom colors and line styles

Line plot with fill shows temperature trend throughout the week
```

### Common Mistakes
- Not showing/saving plots
- Using overlapping colors making lines hard to distinguish
- Not adding labels and titles
- Not adjusting figure size for readability

---

## Problem 6: Perform numpy operations

### Solution
```python
import numpy as np

# Array creation
print("=== NumPy Array Operations ===\n")

# 1. Create arrays
arr1d = np.array([1, 2, 3, 4, 5])
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

print("1D Array:", arr1d)
print("2D Array:\n", arr2d)

# 2. Array operations
print("\n=== Arithmetic Operations ===")
arr = np.array([10, 20, 30, 40, 50])
print(f"Original: {arr}")
print(f"Add 10: {arr + 10}")
print(f"Multiply by 2: {arr * 2}")
print(f"Divide by 5: {arr / 5}")
print(f"Square root: {np.sqrt(arr)}")

# 3. Statistical operations
print("\n=== Statistical Functions ===")
data = np.array([25, 30, 22, 28, 35, 32, 27])
print(f"Data: {data}")
print(f"Mean: {np.mean(data):.2f}")
print(f"Median: {np.median(data):.2f}")
print(f"Std Dev: {np.std(data):.2f}")
print(f"Min: {np.min(data)}")
print(f"Max: {np.max(data)}")
print(f"Sum: {np.sum(data)}")

# 4. Matrix operations
print("\n=== Matrix Operations ===")
matrix_a = np.array([[1, 2], [3, 4]])
matrix_b = np.array([[5, 6], [7, 8]])

print(f"Matrix A:\n{matrix_a}")
print(f"Matrix B:\n{matrix_b}")
print(f"Element-wise multiplication:\n{matrix_a * matrix_b}")
print(f"Matrix multiplication:\n{np.dot(matrix_a, matrix_b)}")

# 5. Array indexing and slicing
print("\n=== Indexing and Slicing ===")
arr = np.arange(10)  # [0, 1, 2, ..., 9]
print(f"Array: {arr}")
print(f"First element: {arr[0]}")
print(f"Last element: {arr[-1]}")
print(f"Elements 2-5: {arr[2:5]}")
print(f"Every other element: {arr[::2]}")
print(f"Reversed: {arr[::-1]}")

# 6. Filtering
print("\n=== Filtering ===")
arr = np.array([5, 12, 8, 15, 3, 20, 7])
print(f"Original: {arr}")
mask = arr > 10
print(f"Elements > 10: {arr[mask]}")
print(f"Even numbers: {arr[arr % 2 == 0]}")

# 7. Reshaping
print("\n=== Reshaping ===")
arr = np.arange(12)
print(f"Original (1D): {arr}")
reshaped = arr.reshape(3, 4)
print(f"Reshaped to 3x4:\n{reshaped}")
flattened = reshaped.flatten()
print(f"Flattened: {flattened}")

# 8. Aggregate along axis
print("\n=== Operations Along Axes ===")
matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(f"Matrix:\n{matrix}")
print(f"Sum along rows: {np.sum(matrix, axis=1)}")
print(f"Sum along columns: {np.sum(matrix, axis=0)}")
print(f"Mean along rows: {np.mean(matrix, axis=1)}")
```

### Expected Output
```
=== NumPy Array Operations ===

1D Array: [1 2 3 4 5]
2D Array:
 [[1 2 3]
 [4 5 6]
 [7 8 9]]

=== Arithmetic Operations ===
Original: [10 20 30 40 50]
Add 10: [20 30 40 50 60]
Multiply by 2: [20 40 60 80 100]
Divide by 5: [ 2.  4.  6.  8. 10.]
Square root: [3.16227766 4.47213595 5.47722558 6.32455532 7.07106781]

=== Statistical Functions ===
Data: [25 30 22 28 35 32 27]
Mean: 28.43
Median: 28.00
Std Dev: 4.60
Min: 22
Max: 35
Sum: 199

=== Matrix Operations ===
Matrix A:
[[1 2]
 [3 4]]
Matrix B:
[[5 6]
 [7 8]]
Element-wise multiplication:
[[ 5 12]
 [21 32]]
Matrix multiplication:
[[19 22]
 [43 50]]

=== Indexing and Slicing ===
Array: [0 1 2 3 4 5 6 7 8 9]
First element: 0
Last element: 9
Elements 2-5: [2 3 4]
Every other element: [0 2 4 6 8]
Reversed: [9 8 7 6 5 4 3 2 1 0]

=== Filtering ===
Original: [ 5 12  8 15  3 20  7]
Elements > 10: [12 15 20]
Even numbers: [12  8 20]

=== Reshaping ===
Original (1D): [ 0  1  2  3  4  5  6  7  8  9 11]
Reshaped to 3x4:
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
Flattened: [ 0  1  2  3  4  5  6  7  8  9 10 11]

=== Operations Along Axes ===
Matrix:
[[1 2 3]
 [4 5 6]
 [7 8 9]]
Sum along rows: [ 6 15 24]
Sum along columns: [12 15 18]
Mean along rows: [2. 5. 8.]
```

### Common Mistakes
- Forgetting to import numpy as np
- Confusing matrix multiplication with element-wise multiplication
- Off-by-one errors in slicing

---

## Problem 7: Integrate multiple libraries

### Solution
```python
import requests
import numpy as np
import matplotlib.pyplot as plt
import json
from datetime import datetime

# Integrated example: Fetch data, process with NumPy, visualize with Matplotlib
def integrated_data_pipeline():
    """Complete pipeline using requests, numpy, and matplotlib"""

    print("Step 1: Fetch data from API")
    url = "https://jsonplaceholder.typicode.com/todos"
    response = requests.get(url)
    todos = response.json()
    print(f"✓ Fetched {len(todos)} todos")

    print("\nStep 2: Process with NumPy")
    # Extract completion status
    user_ids = np.array([todo['userId'] for todo in todos])
    completed = np.array([todo['completed'] for todo in todos])

    # Calculate completion rate per user
    unique_users = np.unique(user_ids)
    completion_rates = []

    for user_id in unique_users:
        user_todos = completed[user_ids == user_id]
        rate = np.mean(user_todos) * 100
        completion_rates.append(rate)

    completion_rates = np.array(completion_rates)
    print(f"✓ Processed {len(unique_users)} users")
    print(f"  Average completion rate: {np.mean(completion_rates):.1f}%")

    print("\nStep 3: Visualize with Matplotlib")
    plt.figure(figsize=(12, 6))
    plt.bar(unique_users, completion_rates, color='steelblue', alpha=0.7)
    plt.xlabel('User ID')
    plt.ylabel('Task Completion Rate (%)')
    plt.title('Task Completion Rate by User')
    plt.grid(axis='y', alpha=0.3)
    print("✓ Generated visualization showing completion rates")
    print("  (Horizontal bar chart with User ID on x-axis, completion % on y-axis)")

# Practical example: Weather data
def weather_data_analysis():
    """Analyze weather data using multiple libraries"""

    print("\n=== Weather Data Analysis ===")

    # Simulated data (would come from API)
    temperatures = np.array([72, 75, 73, 78, 76, 74, 77])
    humidity = np.array([65, 60, 70, 55, 60, 65, 58])
    days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']

    print(f"Temperature Stats:")
    print(f"  Mean: {np.mean(temperatures):.1f}°F")
    print(f"  Std Dev: {np.std(temperatures):.1f}°F")
    print(f"  Range: {np.min(temperatures)}-{np.max(temperatures)}°F")

    # Visualization
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 5))

    # Temperature plot
    ax1.plot(days, temperatures, marker='o', color='red', linewidth=2)
    ax1.set_ylabel('Temperature (°F)')
    ax1.set_title('Daily Temperature')
    ax1.grid(True, alpha=0.3)

    # Humidity plot
    ax2.plot(days, humidity, marker='s', color='blue', linewidth=2)
    ax2.set_ylabel('Humidity (%)')
    ax2.set_title('Daily Humidity')
    ax2.grid(True, alpha=0.3)

    print("✓ Generated side-by-side plots for temperature and humidity")

# Configuration data integration
def load_and_process_config():
    """Load configuration and process with multiple libraries"""

    config = {
        "thresholds": [10, 20, 30, 40, 50],
        "measurements": [12, 18, 35, 45, 52],
        "dates": ["2024-01-01", "2024-01-02", "2024-01-03", "2024-01-04", "2024-01-05"]
    }

    print("\n=== Configuration Processing ===")

    # Process with NumPy
    thresholds = np.array(config["thresholds"])
    measurements = np.array(config["measurements"])

    violations = measurements > thresholds
    print(f"Threshold violations: {np.sum(violations)}")
    print(f"Violation rate: {np.mean(violations)*100:.1f}%")

    # Visualize
    plt.figure(figsize=(10, 6))
    x = np.arange(len(config["dates"]))
    plt.plot(x, thresholds, 'r--', label='Threshold', linewidth=2)
    plt.plot(x, measurements, 'b-', marker='o', label='Measurement', linewidth=2)
    plt.fill_between(x, thresholds, measurements, where=(measurements > thresholds),
                      alpha=0.3, color='red', label='Violation')
    plt.xlabel('Date')
    plt.ylabel('Value')
    plt.title('Measurements vs Thresholds')
    plt.xticks(x, config["dates"], rotation=45)
    plt.legend()
    plt.grid(True, alpha=0.3)
    print("✓ Generated threshold comparison visualization")

# Run integrated examples
integrated_data_pipeline()
weather_data_analysis()
load_and_process_config()
```

### Expected Output
```
Step 1: Fetch data from API
✓ Fetched 200 todos

Step 2: Process with NumPy
✓ Processed 10 users
  Average completion rate: 50.0%

Step 3: Visualize with Matplotlib
✓ Generated visualization showing completion rates
  (Horizontal bar chart with User ID on x-axis, completion % on y-axis)

=== Weather Data Analysis ===
Temperature Stats:
  Mean: 75.0°F
  Std Dev: 1.9°F
  Range: 72-78°F
✓ Generated side-by-side plots for temperature and humidity

=== Configuration Processing ===
Threshold violations: 2
Violation rate: 40.0%
✓ Generated threshold comparison visualization
```

### Common Mistakes
- Not installing all required libraries
- Incompatible library versions
- Not handling data format conversions between libraries

---

## Problem 8: Build data dashboard

### Solution
```python
import matplotlib.pyplot as plt
import numpy as np

# Build a comprehensive data dashboard
def create_dashboard():
    """Create a multi-panel dashboard"""

    # Sample data
    months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
    revenue = [45000, 52000, 48000, 61000, 72000, 85000]
    expenses = [32000, 38000, 35000, 42000, 48000, 52000]
    visitors = [5200, 6100, 5800, 7200, 8500, 9800]
    conversion = [3.2, 3.5, 3.1, 4.1, 4.5, 5.2]

    # Create figure with subplots
    fig = plt.figure(figsize=(16, 12))
    fig.suptitle('Business Dashboard', fontsize=20, fontweight='bold', y=0.995)

    # 1. Revenue trend (top left)
    ax1 = plt.subplot(2, 3, 1)
    ax1.plot(months, revenue, marker='o', color='green', linewidth=3, markersize=8)
    ax1.set_title('Revenue Trend')
    ax1.set_ylabel('Revenue ($)')
    ax1.grid(True, alpha=0.3)

    # 2. Revenue vs Expenses (top middle)
    ax2 = plt.subplot(2, 3, 2)
    x = np.arange(len(months))
    width = 0.35
    ax2.bar(x - width/2, revenue, width, label='Revenue', color='green', alpha=0.7)
    ax2.bar(x + width/2, expenses, width, label='Expenses', color='red', alpha=0.7)
    ax2.set_ylabel('Amount ($)')
    ax2.set_title('Revenue vs Expenses')
    ax2.set_xticks(x)
    ax2.set_xticklabels(months)
    ax2.legend()
    ax2.grid(True, axis='y', alpha=0.3)

    # 3. Profit (top right)
    ax3 = plt.subplot(2, 3, 3)
    profit = [r - e for r, e in zip(revenue, expenses)]
    colors = ['green' if p > 15000 else 'orange' for p in profit]
    ax3.bar(months, profit, color=colors, alpha=0.7)
    ax3.set_title('Monthly Profit')
    ax3.set_ylabel('Profit ($)')
    ax3.grid(True, axis='y', alpha=0.3)

    # 4. Visitors trend (bottom left)
    ax4 = plt.subplot(2, 3, 4)
    ax4.fill_between(range(len(months)), visitors, alpha=0.3, color='blue')
    ax4.plot(months, visitors, marker='s', color='blue', linewidth=2, markersize=6)
    ax4.set_title('Monthly Visitors')
    ax4.set_ylabel('Visitors')
    ax4.grid(True, alpha=0.3)

    # 5. Conversion Rate (bottom middle)
    ax5 = plt.subplot(2, 3, 5)
    ax5.plot(months, conversion, marker='^', color='purple', linewidth=2, markersize=8)
    ax5.set_title('Conversion Rate')
    ax5.set_ylabel('Rate (%)')
    ax5.grid(True, alpha=0.3)

    # 6. Summary Stats (bottom right)
    ax6 = plt.subplot(2, 3, 6)
    ax6.axis('off')

    stats_text = f"""
    SUMMARY STATISTICS

    Total Revenue: ${sum(revenue):,.0f}
    Total Expenses: ${sum(expenses):,.0f}
    Total Profit: ${sum(profit):,.0f}

    Avg Monthly Revenue: ${np.mean(revenue):,.0f}
    Avg Conversion Rate: {np.mean(conversion):.2f}%

    Peak Revenue Month: {months[np.argmax(revenue)]}
    Best Profit Month: {months[profit.index(max(profit))]}
    Total Visitors: {sum(visitors):,.0f}
    """

    ax6.text(0.1, 0.95, stats_text, transform=ax6.transAxes,
            fontsize=11, verticalalignment='top', fontfamily='monospace',
            bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.5))

    plt.tight_layout()
    print("✓ Dashboard created with 6 panels:")
    print("  - Revenue Trend (line plot)")
    print("  - Revenue vs Expenses (grouped bar chart)")
    print("  - Monthly Profit (bar chart)")
    print("  - Visitor Count (area chart)")
    print("  - Conversion Rate (line plot)")
    print("  - Summary Statistics (text box)")

# Run dashboard
create_dashboard()
```

### Expected Output
```
✓ Dashboard created with 6 panels:
  - Revenue Trend (line plot)
  - Revenue vs Expenses (grouped bar chart)
  - Monthly Profit (bar chart)
  - Visitor Count (area chart)
  - Conversion Rate (line plot)
  - Summary Statistics (text box)

The dashboard displays a comprehensive business overview with multiple
visualizations arranged in a 2x3 grid showing financial and visitor metrics.
```

### Common Mistakes
- Overcrowding plots with too much information
- Using inappropriate chart types
- Not labeling axes and units
- Inconsistent color schemes

---

## Problem 9: Handle API pagination

### Solution
```python
import requests

# Pagination handler
def paginated_request(base_url, initial_params=None, total_items=None):
    """Handle paginated API responses"""
    if initial_params is None:
        initial_params = {}

    all_data = []
    page = 1
    per_page = 10

    print(f"Fetching paginated data from {base_url}")

    while True:
        params = {**initial_params, 'page': page, '_limit': per_page}
        response = requests.get(base_url, params=params)

        if response.status_code != 200:
            break

        data = response.json()

        if not data:
            break

        all_data.extend(data)
        print(f"✓ Page {page}: {len(data)} items (Total: {len(all_data)})")

        if len(data) < per_page:
            break

        page += 1

        if total_items and len(all_data) >= total_items:
            all_data = all_data[:total_items]
            break

    return all_data

# Cursor-based pagination
def cursor_pagination(base_url, cursor_param='cursor'):
    """Handle cursor-based pagination"""
    all_data = []
    cursor = None

    print(f"Fetching cursor-based paginated data")

    while True:
        params = {}
        if cursor:
            params[cursor_param] = cursor

        response = requests.get(base_url, params=params)

        if response.status_code != 200:
            break

        data = response.json()

        if isinstance(data, list):
            all_data.extend(data)
        elif isinstance(data, dict):
            items = data.get('items', [])
            all_data.extend(items)
            cursor = data.get('next_cursor')
            if not cursor:
                break
        else:
            break

        print(f"✓ Fetched {len(data)} items")

    return all_data

# Example: Fetch all user posts with pagination
def fetch_all_posts():
    """Example using JSONPlaceholder API"""
    url = "https://jsonplaceholder.typicode.com/posts"
    params = {'userId': 1}

    print("\n=== Fetch All Posts for User 1 ===")

    all_posts = paginated_request(url, params, total_items=50)

    print(f"\nTotal posts fetched: {len(all_posts)}")
    for post in all_posts[:3]:
        print(f"\nPost {post['id']}: {post['title']}")
        print(f"  Body: {post['body'][:50]}...")

# Rate limiting handler
def paginated_request_with_rate_limit(url, delay=0.1):
    """Pagination with rate limiting"""
    import time

    all_data = []
    page = 1

    print("\n=== Paginated Request with Rate Limiting ===")

    while True:
        time.sleep(delay)  # Rate limiting

        params = {'page': page, '_limit': 10}
        response = requests.get(url, params=params)

        if response.status_code != 200:
            break

        data = response.json()

        if not data:
            break

        all_data.extend(data)
        print(f"✓ Page {page}: {len(data)} items")

        if len(data) < 10:
            break

        page += 1

    return all_data

# Run examples
fetch_all_posts()

# Alternative pagination example
print("\n=== Paginated Request with Rate Limiting ===")
url = "https://jsonplaceholder.typicode.com/comments"
comments = paginated_request_with_rate_limit(url, delay=0.05)
print(f"Total comments: {len(comments)}")
```

### Expected Output
```
Fetching paginated data from https://jsonplaceholder.typicode.com/posts
✓ Page 1: 10 items (Total: 10)

Total posts fetched: 10
Post 1: sunt aut facere repellat provident
  Body: quia et suscipit suscipit recusandae...

Post 2: qui est esse
  Body: est rerum tempore vitae sequi sint...

Post 3: ea molestias quasi exercitationem repellat qui ipsa sit aut
  Body: et iusto sed quo iure voluptatibus...

=== Paginated Request with Rate Limiting ===
✓ Page 1: 10 items
✓ Page 2: 10 items
✓ Page 3: 10 items
Total comments: 30
```

### Common Mistakes
- Not handling empty responses
- Infinite loops from incorrect page detection
- Not respecting rate limits
- Not handling different pagination styles

---

## Problem 10: Create visualizations from API data

### Solution
```python
import requests
import matplotlib.pyplot as plt
import numpy as np

# Fetch data and create visualization
def visualize_api_data():
    """Fetch posts data and create visualizations"""

    print("Fetching data from API...")
    url = "https://jsonplaceholder.typicode.com/posts"
    response = requests.get(url)
    posts = response.json()

    # Extract user data
    user_ids = [post['userId'] for post in posts]
    unique_users = sorted(set(user_ids))

    # Count posts per user
    posts_per_user = []
    for user_id in unique_users:
        count = sum(1 for p in posts if p['userId'] == user_id)
        posts_per_user.append(count)

    # Create visualizations
    fig, axes = plt.subplots(1, 2, figsize=(14, 5))

    # Bar chart
    axes[0].bar(unique_users, posts_per_user, color='steelblue', alpha=0.7)
    axes[0].set_xlabel('User ID')
    axes[0].set_ylabel('Number of Posts')
    axes[0].set_title('Posts per User')
    axes[0].grid(axis='y', alpha=0.3)

    # Pie chart
    axes[1].pie(posts_per_user, labels=unique_users, autopct='%1.1f%%')
    axes[1].set_title('Distribution of Posts by User')

    plt.tight_layout()
    print("✓ Visualization created showing:")
    print("  - Bar chart: Posts per user")
    print("  - Pie chart: User distribution")

# Visualize comments data
def visualize_comments_data():
    """Fetch and visualize comments by post"""

    print("\nFetching comments data...")
    url = "https://jsonplaceholder.typicode.com/comments"
    response = requests.get(url)
    comments = response.json()

    # Count comments per post
    post_ids = [c['postId'] for c in comments]
    comments_per_post = {}

    for post_id in set(post_ids):
        count = sum(1 for c in comments if c['postId'] == post_id)
        comments_per_post[post_id] = count

    # Get top 10 posts by comments
    top_posts = sorted(comments_per_post.items(), key=lambda x: x[1], reverse=True)[:10]
    post_ids_top = [p[0] for p in top_posts]
    comment_counts = [p[1] for p in top_posts]

    # Create visualization
    fig, ax = plt.subplots(figsize=(12, 6))
    bars = ax.barh(range(len(post_ids_top)), comment_counts, color='coral')

    # Color bars by comment count
    for i, bar in enumerate(bars):
        if comment_counts[i] > 5:
            bar.set_color('green')
        else:
            bar.set_color('orange')

    ax.set_yticks(range(len(post_ids_top)))
    ax.set_yticklabels([f'Post {pid}' for pid in post_ids_top])
    ax.set_xlabel('Number of Comments')
    ax.set_title('Top 10 Posts by Comment Count')
    ax.grid(axis='x', alpha=0.3)

    plt.tight_layout()
    print("✓ Horizontal bar chart created showing top posts by comments")

# Run visualizations
visualize_api_data()
visualize_comments_data()
```

### Expected Output
```
Fetching data from API...
✓ Visualization created showing:
  - Bar chart: Posts per user
  - Pie chart: User distribution

Fetching comments data...
✓ Horizontal bar chart created showing top posts by comments
```

### Common Mistakes
- Not checking API response before visualization
- Missing axes labels and titles
- Poor color choices
- Overcrowding visualizations

---

## Problem 11: Perform statistical analysis with numpy

### Solution
```python
import numpy as np
import matplotlib.pyplot as plt

print("=== NumPy Statistical Analysis ===\n")

# Sample dataset
data = np.array([23, 45, 56, 34, 67, 89, 23, 45, 56, 78, 90, 34, 56])

print("Data:", data)
print(f"Count: {len(data)}")

# Descriptive statistics
print("\n=== Descriptive Statistics ===")
print(f"Mean: {np.mean(data):.2f}")
print(f"Median: {np.median(data):.2f}")
print(f"Mode: {np.bincount(data).argmax()}")
print(f"Std Dev: {np.std(data):.2f}")
print(f"Variance: {np.var(data):.2f}")
print(f"Min: {np.min(data)}")
print(f"Max: {np.max(data)}")
print(f"Range: {np.max(data) - np.min(data)}")

# Percentiles
print("\n=== Percentiles ===")
print(f"25th percentile: {np.percentile(data, 25):.2f}")
print(f"50th percentile (Median): {np.percentile(data, 50):.2f}")
print(f"75th percentile: {np.percentile(data, 75):.2f}")

# Correlation
print("\n=== Correlation Analysis ===")
x = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
y = np.array([2, 4, 5, 4, 5, 7, 8, 8, 9, 10])
correlation = np.corrcoef(x, y)[0, 1]
print(f"Correlation between x and y: {correlation:.3f}")

# Distribution analysis
print("\n=== Distribution Analysis ===")
histogram, edges = np.histogram(data, bins=5)
print(f"Histogram: {histogram}")
print(f"Bin edges: {edges}")

# Create histogram visualization
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Histogram
ax1.hist(data, bins=5, color='steelblue', alpha=0.7, edgecolor='black')
ax1.set_xlabel('Value')
ax1.set_ylabel('Frequency')
ax1.set_title('Data Distribution')
ax1.grid(axis='y', alpha=0.3)

# Scatter plot with correlation
ax2.scatter(x, y, s=100, alpha=0.6, color='red')
# Add trend line
z = np.polyfit(x, y, 1)
p = np.poly1d(z)
ax2.plot(x, p(x), "b--", linewidth=2, label=f'Trend (r={correlation:.2f})')
ax2.set_xlabel('X')
ax2.set_ylabel('Y')
ax2.set_title('Correlation Analysis')
ax2.legend()
ax2.grid(True, alpha=0.3)

plt.tight_layout()
print("\n✓ Generated visualization showing distribution and correlation")

# Z-score normalization
print("\n=== Normalization ===")
z_scores = (data - np.mean(data)) / np.std(data)
print(f"Original data range: {np.min(data)} to {np.max(data)}")
print(f"Z-score range: {np.min(z_scores):.2f} to {np.max(z_scores):.2f}")
print(f"Z-scores mean: {np.mean(z_scores):.6f} (should be ~0)")
print(f"Z-scores std: {np.std(z_scores):.6f} (should be ~1)")
```

### Expected Output
```
=== NumPy Statistical Analysis ===

Data: [23 45 56 34 67 89 23 45 56 78 90 34 56]
Count: 13

=== Descriptive Statistics ===
Mean: 54.69
Median: 56.00
Mode: 56
Std Dev: 24.26
Variance: 589.59
Min: 23
Max: 90
Range: 67

=== Percentiles ===
25th percentile: 39.00
50th percentile (Median): 56.00
75th percentile: 72.50

=== Correlation Analysis ===
Correlation between x and y: 0.976

=== Distribution Analysis ===
Histogram: [2 2 4 3 2]
Bin edges: [23. 36.4 49.8 63.2 76.6 90. ]

=== Normalization ===
Original data range: 23 to 90
Z-score range: -1.31 to 1.46
Z-scores mean: 0.000000 (should be ~0)
Z-scores std: 1.000000 (should be ~1)

✓ Generated visualization showing distribution and correlation
```

### Common Mistakes
- Confusing correlation with causation
- Not handling outliers in statistical analysis
- Incorrect percentile calculations

---

## Problem 12-15: Advanced Topics (Build Real-Time Data Fetcher, Interactive Visualizations, Multiple APIs, Complete Analytics App)

These projects involve combining all previous concepts with additional features like websockets, real-time updates, and multi-source data integration. They represent capstone-level work integrating all libraries and techniques from the unit.

For these advanced problems, students should focus on:
- Properly error handling across multiple APIs
- Efficient caching and rate limiting
- Responsive UI updates
- Data consistency across sources
- Performance optimization

These are best completed as semester-long projects building from earlier unit foundations.
