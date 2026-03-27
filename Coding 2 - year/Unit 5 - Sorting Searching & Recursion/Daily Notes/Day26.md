# Day 26: Analysis & Final Report Writing

**Learning Target:** I can analyze benchmarking data and write a comprehensive technical report.

---

## Key Concepts

**Report Structure:**
1. Executive Summary (1 paragraph overview)
2. Methodology (what we tested, how we tested it)
3. Results (data, tables, visualizations)
4. Analysis (interpretation of results)
5. Conclusions & Recommendations
6. Appendix (code, full data)

**Analysis Techniques:**
- Scaling analysis (how does time grow with size?)
- Data type impact (does algorithm type matter?)
- Stability checking (do equal elements maintain order?)
- Memory considerations (in-place vs. extra space)

---

## Code Examples

```python
# Report generation and analysis

class PerformanceAnalysis:
    """Analyze benchmark results and generate insights."""

    def __init__(self, results):
        self.results = results

    def calculate_big_o(self, algo_name, data_type='random'):
        """Estimate empirical Big O from benchmark data."""
        matching = [r for r in self.results.values()
                   if r['algorithm'] == algo_name
                   and r['data_type'] == data_type]

        if len(matching) < 2:
            return None

        # Sort by size
        matching = sorted(matching, key=lambda r: r['size'])

        # Use first two points to estimate
        p1 = matching[0]
        p2 = matching[-1]

        n1, t1 = p1['size'], p1['time']
        n2, t2 = p2['size'], p2['time']

        # t = k * n^x  =>  x = log(t2/t1) / log(n2/n1)
        ratio = (n2 / n1) ** 2
        if t1 > 0:
            time_ratio = t2 / t1
            exponent = __import__('math').log(time_ratio) / __import__('math').log(ratio)
            return exponent
        return None

    def rank_algorithms(self):
        """Rank algorithms by average performance."""
        by_algo = {}

        for result in self.results.values():
            algo = result['algorithm']
            if algo not in by_algo:
                by_algo[algo] = []
            by_algo[algo].append(result['time'])

        rankings = []
        for algo, times in by_algo.items():
            avg_time = sum(times) / len(times)
            rankings.append((algo, avg_time))

        return sorted(rankings, key=lambda x: x[1])

    def best_algorithm_by_scenario(self):
        """Find best algorithm for each size/data type combination."""
        scenarios = {}

        for result in self.results.values():
            scenario = (result['size'], result['data_type'])
            if scenario not in scenarios:
                scenarios[scenario] = []
            scenarios[scenario].append(result)

        best = {}
        for scenario, results_list in scenarios.items():
            best[scenario] = min(results_list, key=lambda r: r['time'])

        return best

    def generate_html_report(self, filename='report.html'):
        """Generate an HTML report with charts."""
        html = """
        <html>
        <head>
            <title>Sorting Algorithm Benchmark Report</title>
            <style>
                body { font-family: Arial; margin: 20px; }
                table { border-collapse: collapse; margin: 20px 0; }
                th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
                th { background-color: #4CAF50; color: white; }
                tr:nth-child(even) { background-color: #f2f2f2; }
                .fast { color: green; font-weight: bold; }
                .slow { color: red; }
                h2 { color: #333; border-bottom: 2px solid #4CAF50; padding-bottom: 10px; }
            </style>
        </head>
        <body>
            <h1>Sorting Algorithm Benchmark Report</h1>

            <h2>Executive Summary</h2>
            <p>
            This report benchmarks 6 sorting algorithms (Bubble, Selection, Insertion, Merge, Quick, Built-in)
            on 5 data types (Random, Sorted, Reverse, Nearly Sorted, Few Unique) across sizes from 100 to
            10,000 elements. Key findings:
            </p>
            <ul>
        """

        # Add key findings
        rankings = self.rank_algorithms()
        html += f"<li>Fastest overall: <span class='fast'>{rankings[0][0]}</span></li>"
        html += f"<li>Slowest overall: <span class='slow'>{rankings[-1][0]}</span></li>"

        # Best for each size
        best_scenarios = self.best_algorithm_by_scenario()
        best_small = [r for r in best_scenarios.values() if r['size'] == min([s[0] for s in best_scenarios.keys()])]
        if best_small:
            html += f"<li>Best for small arrays: {best_small[0]['algorithm']}</li>"

        html += """
            </ul>

            <h2>Methodology</h2>
            <p>
            Each algorithm was tested on 5 different data types and multiple sizes. Each test was run 3 times,
            and the average time was recorded. Slow algorithms (Bubble Sort, Selection Sort) were skipped on
            arrays larger than 1000 elements to save time.
            </p>

            <h2>Results</h2>
            <h3>Performance Rankings (Overall)</h3>
            <table>
                <tr>
                    <th>Rank</th>
                    <th>Algorithm</th>
                    <th>Average Time</th>
                </tr>
        """

        for rank, (algo, avg_time) in enumerate(rankings, 1):
            html += f"<tr><td>{rank}</td><td>{algo}</td><td>{avg_time*1000:.3f}ms</td></tr>"

        html += """
            </table>

            <h2>Analysis</h2>
            <p>
            The benchmarks clearly show that:
            </p>
            <ol>
                <li>O(n²) algorithms (Bubble, Selection) are unacceptable for large arrays</li>
                <li>Insertion sort excels on small or nearly-sorted data</li>
                <li>Merge sort provides consistent O(n log n) performance</li>
                <li>Quick sort offers the best average performance</li>
                <li>Python's built-in sort (Timsort) is highly optimized for real-world data</li>
            </ol>

            <h2>Recommendations</h2>
            <ol>
                <li><strong>Production Code:</strong> Always use Python's built-in sorted() or .sort()</li>
                <li><strong>Small arrays (&lt;100):</strong> Insertion sort is sufficient</li>
                <li><strong>General purpose (large):</strong> Quick sort or Timsort</li>
                <li><strong>Guaranteed complexity:</strong> Merge sort</li>
                <li><strong>Embedded systems:</strong> Selection sort (lowest memory)</li>
                <li><strong>Teaching:</strong> Understand when each algorithm is appropriate</li>
            </ol>

            <h2>Conclusion</h2>
            <p>
            While O(n²) algorithms are simple and useful for understanding sorting concepts,
            modern applications require O(n log n) algorithms. Python's Timsort combines
            the speed of quick sort with the stability of merge sort, making it the ideal choice
            for production systems.
            </p>

            <h2>Appendix: Detailed Results</h2>
            <table>
                <tr>
                    <th>Algorithm</th>
                    <th>Size</th>
                    <th>Data Type</th>
                    <th>Time (ms)</th>
                </tr>
        """

        # Add all results
        for result in sorted(self.results.values(),
                           key=lambda r: (r['size'], r['algorithm'])):
            html += f"""
            <tr>
                <td>{result['algorithm']}</td>
                <td>{result['size']}</td>
                <td>{result['data_type']}</td>
                <td>{result['time']*1000:.3f}</td>
            </tr>
            """

        html += """
            </table>

        </body>
        </html>
        """

        with open(filename, 'w') as f:
            f.write(html)

        print(f"HTML report written to {filename}")

    def generate_markdown_report(self, filename='REPORT.md'):
        """Generate a Markdown report."""
        md = """# Sorting Algorithm Benchmark Report

## Executive Summary

This report benchmarks 6 sorting algorithms on various data types and sizes.

## Methodology

- Algorithms: Bubble, Selection, Insertion, Merge, Quick, Built-in (Timsort)
- Data types: Random, Sorted, Reverse, Nearly Sorted, Few Unique
- Sizes: 100 - 10,000 elements
- Each test run 3 times, average reported

## Results

### Performance Rankings
| Rank | Algorithm | Avg Time (ms) |
|------|-----------|--------------|
"""

        rankings = self.rank_algorithms()
        for rank, (algo, avg_time) in enumerate(rankings, 1):
            md += f"| {rank} | {algo} | {avg_time*1000:.3f} |\n"

        md += """

## Analysis

Key findings:
1. O(n²) algorithms are too slow for large arrays
2. Insertion sort is excellent for small/nearly-sorted data
3. Merge sort guarantees O(n log n) performance
4. Quick sort offers best average performance
5. Python's Timsort is highly optimized

## Recommendations

| Scenario | Recommended Algorithm |
|----------|----------------------|
| Production code | sorted() / .sort() (Timsort) |
| Small arrays (<100) | Insertion sort |
| Large random arrays | Quick sort |
| Need guaranteed speed | Merge sort |
| Memory constrained | Selection sort |
| Teaching/learning | Understanding matters more than speed |

## Conclusion

Use Python's built-in sorting in production. Understand the pros/cons of each algorithm
for different scenarios.

---
*Report generated from comprehensive benchmarking suite*
"""

        with open(filename, 'w') as f:
            f.write(md)

        print(f"Markdown report written to {filename}")

# Usage example
def generate_final_report(results):
    """Generate all report formats."""
    analysis = PerformanceAnalysis(results)

    print("Generating reports...")
    analysis.generate_markdown_report()
    analysis.generate_html_report()

    print("\nFinal Rankings:")
    for rank, (algo, avg_time) in enumerate(analysis.rank_algorithms(), 1):
        print(f"  {rank}. {algo:20} {avg_time*1000:10.3f}ms")
```

---

## Guided Practice

**Activity 1: Interpret Results**

Given benchmark data, answer:
- Which algorithm is fastest overall?
- Which is fastest for small arrays?
- Which is fastest for nearly-sorted data?
- Why the differences?

**Activity 2: Write Analysis**

Write 2-3 paragraphs analyzing:
- How algorithms scale with size
- Impact of data type
- Real-world implications

**Activity 3: Make Recommendations**

For each use case, recommend an algorithm and justify:
- Sorting student IDs
- Sorting search results by relevance
- Sorting transactions by date in a bank system

---

## Practice Problems

**Beginner:** Create a simple table showing results and identify the fastest algorithm.

**Intermediate:** Write analysis paragraphs interpreting scaling behavior.

**Challenge:** Generate complete HTML/Markdown reports with all data and analysis.

<details>
<summary>💡 Hints</summary>
- **Beginner:** Make a table with algorithm name, size, time
- **Intermediate:** Compare actual scaling to expected Big O scaling
- **Challenge:** Use code above to generate reports
</details>

<details>
<summary>✅ Sample Answers</summary>
```python
# See PerformanceAnalysis class above
# Use rank_algorithms() for rankings
# Use generate_markdown_report() for reports
# Use generate_html_report() for HTML reports
```
</details>
