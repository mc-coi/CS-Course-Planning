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

---
