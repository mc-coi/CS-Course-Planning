# Day 17: Matplotlib – Advanced Visualization

**Learning Target:** I can create multiple subplots, customize colors and styles, and create publication-quality charts.

---

## Key Concepts

**Subplots:** Create multiple plots in one figure for comparison.

**Customization:**
- Colors and markers
- Linestyles
- Font sizes
- Legends and annotations

**Figure Workspace:** `plt.figure()` creates a new plot area.

**Axes Object:** Direct control over plot elements.

---

## Code Examples

```python
import matplotlib.pyplot as plt
import numpy as np

# SUBPLOTS - Multiple plots side by side
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Left plot (line)
x = np.arange(0, 10, 0.1)
y = np.sin(x)
axes[0].plot(x, y, 'b-', linewidth=2)
axes[0].set_title('Sine Wave')
axes[0].set_xlabel('x')
axes[0].set_ylabel('sin(x)')

# Right plot (bar)
categories = ['A', 'B', 'C', 'D']
values = [10, 20, 15, 25]
axes[1].bar(categories, values, color='green', alpha=0.7)
axes[1].set_title('Category Comparison')
axes[1].set_ylabel('Value')

plt.tight_layout()
plt.show()

# CUSTOMIZATION - Colors, styles, fonts
plt.figure(figsize=(10, 6))
x = [1, 2, 3, 4, 5]
y1 = [1, 4, 9, 16, 25]
y2 = [1, 2, 3, 4, 5]

plt.plot(x, y1, 'r--', linewidth=2, marker='o', label='Quadratic')
plt.plot(x, y2, 'b-', linewidth=2, marker='s', label='Linear')

plt.xlabel('X Value', fontsize=12, fontweight='bold')
plt.ylabel('Y Value', fontsize=12, fontweight='bold')
plt.title('Function Comparison', fontsize=14, fontweight='bold')
plt.legend(fontsize=11)
plt.grid(True, alpha=0.3)
plt.show()

# ANNOTATIONS - Add labels to specific points
plt.figure(figsize=(10, 6))
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 6]

plt.plot(x, y, marker='o')
plt.annotate('Peak', xy=(3, 5), xytext=(3.5, 5.5),
            arrowprops=dict(arrowstyle='->', color='red'))
plt.xlabel('Time')
plt.ylabel('Value')
plt.title('Data with Annotation')
plt.show()

# HISTOGRAM - Distribution of data
data = np.random.normal(100, 15, 1000)
plt.figure(figsize=(10, 6))
plt.hist(data, bins=30, color='purple', alpha=0.7, edgecolor='black')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.title('Distribution of Data')
plt.show()
```

---

## Guided Practice

1. **Subplots:** Create a 2x2 grid of different plots (line, bar, scatter, histogram).

2. **Styling:** Create a line plot with custom colors, markers, and line styles.

3. **Annotations:** Plot a curve and annotate the highest point.

4. **Multiple Legends:** Create two line plots with different colors and a legend.

---

## Practice Problems

**Beginner:** Create two subplots: one line chart and one bar chart, side by side.

**Intermediate:** Create a styled plot with custom colors, markers, and annotated peaks/valleys.

**Challenge:** Create a dashboard with 4 subplots showing different statistics from a dataset.

<details>
<summary>💡 Hints</summary>
- Use `plt.subplots(rows, cols)` for multiple plots
- Use `axes[i].plot()`, `axes[i].bar()` etc. for individual subplots
- Color options: 'r', 'g', 'b', 'k' or full names like 'red', 'green'
- Linestyles: '-' (solid), '--' (dashed), ':' (dotted)
- Markers: 'o' (circle), 's' (square), '^' (triangle), '*' (star)
- Use `plt.annotate()` to add arrows and text to specific points
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import matplotlib.pyplot as plt

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Line plot
ax1.plot([1, 2, 3, 4], [1, 4, 9, 16])
ax1.set_title('Line Chart')

# Bar chart
ax2.bar(['A', 'B', 'C'], [10, 20, 15])
ax2.set_title('Bar Chart')

plt.show()
```

**Intermediate:**
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y, 'r-', linewidth=2, marker='o', markersize=3)
plt.annotate('Max', xy=(1.57, 1), xytext=(2.5, 0.5),
            arrowprops=dict(arrowstyle='->', color='red'))
plt.title('Sine Wave')
plt.show()
```

**Challenge:**
```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.randn(1000)

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

axes[0, 0].hist(data, bins=30)
axes[0, 0].set_title('Histogram')

axes[0, 1].boxplot(data)
axes[0, 1].set_title('Box Plot')

axes[1, 0].scatter(np.arange(100), data[:100])
axes[1, 0].set_title('Scatter Plot')

axes[1, 1].plot(data[:100])
axes[1, 1].set_title('Line Plot')

plt.tight_layout()
plt.show()
```
</details>
