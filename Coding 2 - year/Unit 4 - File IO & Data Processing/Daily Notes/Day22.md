# Day 22: Data Analysis — Computing Stats from Files
**Learning Target:** I can analyze file data to compute statistics and generate insights.

### Key Concepts

**Basic statistics:** Mean, median, mode, min, max, sum.

**Aggregation:** Grouping and summarizing data.

**Trends:** Identifying patterns over time or categories.

**Percentiles:** Understanding distribution of values.

**Reporting:** Presenting findings clearly.

### Code Examples

```python
# Example 1: Basic statistics
def compute_stats(numbers):
    """Compute basic statistics"""
    if not numbers:
        return {}
    
    sorted_nums = sorted(numbers)
    n = len(numbers)
    
    return {
        'count': n,
        'sum': sum(numbers),
        'mean': sum(numbers) / n,
        'min': min(numbers),
        'max': max(numbers),
        'median': sorted_nums[n // 2] if n % 2 == 1 else (sorted_nums[n//2-1] + sorted_nums[n//2]) / 2,
        'range': max(numbers) - min(numbers)
    }

scores = [85, 90, 92, 87, 88, 95, 85]
stats = compute_stats(scores)
for key, value in stats.items():
    print(f"{key}: {value:.2f}" if isinstance(value, float) else f"{key}: {value}")

# Example 2: Grouping by category
def group_and_aggregate(data, group_key, aggregate_key):
    """Group data and compute totals"""
    groups = {}
    for record in data:
        key = record.get(group_key)
        value = record.get(aggregate_key)
        if key not in groups:
            groups[key] = []
        groups[key].append(value)
    
    results = {}
    for key, values in groups.items():
        results[key] = {
            'total': sum(values),
            'count': len(values),
            'average': sum(values) / len(values)
        }
    return results

sales = [
    {'product': 'Widget', 'amount': 100},
    {'product': 'Gadget', 'amount': 150},
    {'product': 'Widget', 'amount': 120},
    {'product': 'Gadget', 'amount': 140}
]

grouped = group_and_aggregate(sales, 'product', 'amount')
for product, stats in grouped.items():
    print(f"{product}: Total=${stats['total']}, Avg=${stats['average']:.2f}")

# Example 3: Percentiles
def percentile(numbers, p):
    """Calculate percentile"""
    sorted_nums = sorted(numbers)
    n = len(sorted_nums)
    index = (p / 100) * n
    if index == int(index):
        return sorted_nums[int(index) - 1]
    return sorted_nums[int(index)]

scores = [65, 72, 78, 85, 90, 92, 95]
print(f"25th percentile: {percentile(scores, 25)}")
print(f"50th percentile (median): {percentile(scores, 50)}")
print(f"75th percentile: {percentile(scores, 75)}")

# Example 4: Frequency analysis
def frequency_analysis(data):
    """Count occurrences of each value"""
    freq = {}
    for item in data:
        freq[item] = freq.get(item, 0) + 1
    return sorted(freq.items(), key=lambda x: x[1], reverse=True)

grades = ['A', 'B', 'A', 'C', 'B', 'A', 'B']
freq = frequency_analysis(grades)
print("Grade frequency:")
for grade, count in freq:
    print(f"  {grade}: {count}")

# Example 5: Comparison across categories
def compare_categories(data, category_key, value_key):
    """Compare values across categories"""
    categories = {}
    for record in data:
        cat = record.get(category_key)
        val = record.get(value_key)
        if cat not in categories:
            categories[cat] = []
        categories[cat].append(val)
    
    comparison = {}
    for cat, values in categories.items():
        comparison[cat] = {
            'avg': sum(values) / len(values),
            'min': min(values),
            'max': max(values),
            'count': len(values)
        }
    return comparison

students = [
    {'major': 'CS', 'gpa': 3.9},
    {'major': 'Math', 'gpa': 3.7},
    {'major': 'CS', 'gpa': 3.8},
    {'major': 'Math', 'gpa': 3.6}
]

comparison = compare_categories(students, 'major', 'gpa')
for major, stats in comparison.items():
    print(f"{major}: Avg GPA {stats['avg']:.2f}")

# Example 6: Growth/trend calculation
def calculate_growth(values):
    """Calculate percentage growth"""
    if len(values) < 2 or values[0] == 0:
        return []
    growth = []
    for i in range(1, len(values)):
        pct_change = ((values[i] - values[i-1]) / values[i-1]) * 100
        growth.append(pct_change)
    return growth

sales = [100, 110, 105, 120, 135]
growth = calculate_growth(sales)
for i, g in enumerate(growth, 1):
    print(f"Month {i} to {i+1}: {g:.1f}% change")

# Example 7: Distribution analysis
def analyze_distribution(numbers, bins=5):
    """Analyze value distribution"""
    if not numbers:
        return {}
    
    min_val = min(numbers)
    max_val = max(numbers)
    bin_width = (max_val - min_val) / bins
    
    distribution = {}
    for i in range(bins):
        bin_label = f"{min_val + i*bin_width:.0f}-{min_val + (i+1)*bin_width:.0f}"
        distribution[bin_label] = 0
    
    for num in numbers:
        bin_idx = min(int((num - min_val) / bin_width), bins - 1)
        bin_label = f"{min_val + bin_idx*bin_width:.0f}-{min_val + (bin_idx+1)*bin_width:.0f}"
        distribution[bin_label] += 1
    
    return distribution

scores = [65, 70, 75, 80, 82, 85, 88, 90, 92, 95]
dist = analyze_distribution(scores)
for bin_label, count in dist.items():
    print(f"{bin_label}: {count}")

# Example 8: Outlier detection
def find_outliers(numbers, threshold=2):
    """Find values that deviate from mean"""
    mean = sum(numbers) / len(numbers)
    std_dev = (sum((x - mean) ** 2 for x in numbers) / len(numbers)) ** 0.5
    
    outliers = []
    for num in numbers:
        if abs(num - mean) > threshold * std_dev:
            outliers.append(num)
    return outliers

data = [85, 87, 90, 92, 88, 150, 86]  # 150 is outlier
outliers = find_outliers(data)
print(f"Outliers: {outliers}")

# Example 9: Correlation analysis
def correlation(x_values, y_values):
    """Calculate correlation coefficient"""
    n = len(x_values)
    mean_x = sum(x_values) / n
    mean_y = sum(y_values) / n
    
    numerator = sum((x_values[i] - mean_x) * (y_values[i] - mean_y) for i in range(n))
    denom_x = sum((x - mean_x) ** 2 for x in x_values) ** 0.5
    denom_y = sum((y - mean_y) ** 2 for y in y_values) ** 0.5
    
    return numerator / (denom_x * denom_y)

study_hours = [2, 3, 4, 5, 6, 7, 8]
test_scores = [65, 72, 78, 85, 90, 92, 95]
corr = correlation(study_hours, test_scores)
print(f"Correlation: {corr:.3f}")

# Example 10: Complete analysis report
def generate_report(data, value_key):
    """Generate comprehensive analysis report"""
    values = [r.get(value_key) for r in data if r.get(value_key) is not None]
    
    if not values:
        return "No data available"
    
    stats = compute_stats(values)
    report = []
    report.append("=== DATA ANALYSIS REPORT ===")
    report.append(f"Records analyzed: {stats['count']}")
    report.append(f"Average: {stats['mean']:.2f}")
    report.append(f"Median: {stats['median']:.2f}")
    report.append(f"Range: {stats['min']:.2f} to {stats['max']:.2f}")
    report.append(f"Total: {stats['sum']:.2f}")
    
    return '\n'.join(report)

data = [
    {'id': 1, 'value': 85},
    {'id': 2, 'value': 90},
    {'id': 3, 'value': 92},
    {'id': 4, 'value': 87}
]

print(generate_report(data, 'value'))
```

### Guided Practice

**Activity: Analyze Student Data**

1. Create student records with names and scores
2. Compute statistics (average, min, max)
3. Group by grade letter
4. Find top performers
5. Generate a report

**Step-by-step code:**
```python
students = [
    {'name': 'Alice', 'score': 95},
    {'name': 'Bob', 'score': 87},
    {'name': 'Charlie', 'score': 92},
    {'name': 'Diana', 'score': 78},
    {'name': 'Eve', 'score': 88}
]

scores = [s['score'] for s in students]
avg_score = sum(scores) / len(scores)

print(f"Class Statistics:")
print(f"  Average: {avg_score:.2f}")
print(f"  Highest: {max(scores)}")
print(f"  Lowest: {min(scores)}")

# Top performers (90+)
top = [s for s in students if s['score'] >= 90]
print(f"\nTop Performers:")
for student in top:
    print(f"  {student['name']}: {student['score']}")
```

### Practice Problems

**Problem 1 — Beginner:** Write a function that computes mean, min, and max from a list of numbers.

**Problem 2 — Intermediate:** Write a function that groups data by category and computes averages for each group.

**Problem 3 — Challenge:** Write a complete data analysis system that computes multiple statistics and generates a formatted report.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Use sum() and len() for mean.
- Use min() and max() functions.

**Problem 2:**
- Create a dict to group by category.
- Loop and collect values.
- Calculate average per group.

**Problem 3:**
- Compute multiple statistics.
- Format output nicely.
- Include percentiles or other advanced stats.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
def basic_stats(numbers):
    return {
        'mean': sum(numbers) / len(numbers),
        'min': min(numbers),
        'max': max(numbers)
    }

# Problem 2
def group_stats(data, group_key, value_key):
    groups = {}
    for record in data:
        g = record[group_key]
        if g not in groups:
            groups[g] = []
        groups[g].append(record[value_key])
    
    result = {}
    for g, values in groups.items():
        result[g] = sum(values) / len(values)
    return result

# Problem 3
def full_analysis(data, value_key):
    values = [r[value_key] for r in data]
    report = f"""
    === ANALYSIS REPORT ===
    Count: {len(values)}
    Average: {sum(values) / len(values):.2f}
    Min: {min(values)}
    Max: {max(values)}
    """
    return report
```

</details>
