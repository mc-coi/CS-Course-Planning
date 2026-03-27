# Day 15: Introduction to Matplotlib – Visualization

**Learning Target:** I can create line charts, bar charts, and customize plots to visualize data.

---

## Key Concepts

**Matplotlib:** A library for creating charts and plots. Essential for data visualization.

**Common Plot Types:**
- **Line Plot:** Show trends over time
- **Bar Chart:** Compare categories
- **Scatter Plot:** Show relationships between two variables
- **Histogram:** Show distribution of data

**Basic Workflow:**
1. Prepare data
2. Create figure and axis
3. Plot the data
4. Customize (title, labels, etc.)
5. Display with `plt.show()`

---

## Code Examples

```python
import matplotlib.pyplot as plt
import numpy as np

# LINE PLOT - Trends over time
x = np.array([1, 2, 3, 4, 5])
y = np.array([10, 15, 12, 18, 20])

plt.figure(figsize=(8, 5))
plt.plot(x, y, marker='o', color='blue', label='Sales')
plt.xlabel('Month')
plt.ylabel('Revenue ($)')
plt.title('Monthly Revenue')
plt.legend()
plt.grid(True)
plt.show()

# BAR CHART - Compare categories
categories = ['Python', 'JavaScript', 'Java', 'C++']
popularity = [35, 28, 20, 15]

plt.figure(figsize=(8, 5))
plt.bar(categories, popularity, color='green')
plt.xlabel('Programming Language')
plt.ylabel('Popularity (%)')
plt.title('Programming Language Popularity')
plt.show()

# MULTIPLE LINES
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May']
sales_2025 = [100, 120, 110, 140, 150]
sales_2026 = [150, 160, 155, 170, 180]

plt.figure(figsize=(10, 6))
plt.plot(months, sales_2025, marker='o', label='2025')
plt.plot(months, sales_2026, marker='s', label='2026')
plt.xlabel('Month')
plt.ylabel('Sales ($)')
plt.title('Year-over-Year Comparison')
plt.legend()
plt.show()

# SCATTER PLOT
x = np.random.rand(50) * 100
y = np.random.rand(50) * 100

plt.figure(figsize=(8, 6))
plt.scatter(x, y, color='red', alpha=0.6)
plt.xlabel('X Value')
plt.ylabel('Y Value')
plt.title('Scatter Plot Example')
plt.show()
```

---

## Guided Practice

1. **Line Plot:** Create a line plot of temperature over 7 days.

2. **Bar Chart:** Create a bar chart of your favorite books and their ratings.

3. **Multiple Series:** Plot sales data for two different products over months.

4. **Customization:** Add colors, markers, legend, and grid to your plot.

---

## Practice Problems

**Beginner:** Create a line plot of numbers 1-10 vs their squares (1, 4, 9, 16, ..., 100).

**Intermediate:** Create a bar chart comparing test scores across different subjects.

**Challenge:** Create a combined plot with a line chart and a bar chart (subplots).

<details>
<summary>💡 Hints</summary>
- Use `plt.plot()` for line charts
- Use `plt.bar()` for bar charts
- Use `plt.scatter()` for scatter plots
- Use `plt.xlabel()`, `plt.ylabel()`, `plt.title()` for labels
- Use `plt.legend()` to show what each line/bar represents
- Use `plt.show()` to display the plot
- `marker='o'` adds dots to line plots
- `figsize=(width, height)` controls plot size
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import matplotlib.pyplot as plt

x = list(range(1, 11))
y = [i**2 for i in x]

plt.plot(x, y, marker='o')
plt.xlabel('Number')
plt.ylabel('Square')
plt.title('Numbers vs Squares')
plt.show()
```

**Intermediate:**
```python
import matplotlib.pyplot as plt

subjects = ['Math', 'Science', 'English', 'History']
scores = [92, 88, 85, 90]

plt.bar(subjects, scores)
plt.ylabel('Score')
plt.title('Test Scores by Subject')
plt.show()
```

**Challenge:**
```python
import matplotlib.pyplot as plt
import numpy as np

months = ['Jan', 'Feb', 'Mar', 'Apr']
line_data = [100, 150, 120, 180]
bar_data = [50, 60, 55, 70]

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

ax1.plot(months, line_data, marker='o')
ax1.set_title('Line Chart')

ax2.bar(months, bar_data)
ax2.set_title('Bar Chart')

plt.show()
```
</details>
