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

---
