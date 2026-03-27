# Day 6: Unit 6 Project — Data Analyzer

### Project Description
Build a modular data analysis program that reads scores from a file, processes them, and produces a report. This project combines file I/O, error handling, functions, and documentation.

### Requirements
1. **Read data from a file** — handle the case where the file doesn't exist
2. **Analyze the data** — calculate stats (average, highest, lowest, passing count)
3. **Categorize results** — assign letter grades
4. **Write a report** — save results to a new file
5. **Handle errors** — use `try/except` for file operations and data conversion
6. **Documentation** — every function must have a docstring

### Starter Template

```python
"""
data_analyzer.py
Reads student score data from a CSV file, analyzes it,
and writes a summary report.
"""

def load_scores(filename):
    """Read student scores from a CSV file.

    Expected format: Name,Score (one per line, with header)

    Args:
        filename (str): Path to the CSV file.

    Returns:
        list of tuples: [(name, score), ...] or empty list on failure.
    """
    students = []
    try:
        with open(filename, "r") as f:
            next(f)  # skip header line
            for line in f:
                parts = line.strip().split(",")
                if len(parts) == 2:
                    name = parts[0]
                    score = float(parts[1])
                    students.append((name, score))
    except FileNotFoundError:
        print(f"Error: '{filename}' not found.")
    except ValueError as e:
        print(f"Error parsing file: {e}")
    return students

def calculate_stats(students):
    """Calculate summary statistics for a list of students.

    Args:
        students (list of tuples): [(name, score), ...]

    Returns:
        dict: Keys: average, highest, lowest, passing_count, total
    """
    if not students:
        return {}

    scores = [s for _, s in students]
    passing = sum(1 for s in scores if s >= 70)

    return {
        "average": sum(scores) / len(scores),
        "highest": max(scores),
        "lowest": min(scores),
        "passing_count": passing,
        "total": len(scores)
    }

def get_letter_grade(score):
    """Convert score to letter grade."""
    if score >= 90: return "A"
    if score >= 80: return "B"
    if score >= 70: return "C"
    if score >= 60: return "D"
    return "F"

def write_report(filename, students, stats):
    """Write a formatted grade report to a file.

    Args:
        filename (str): Output file path.
        students (list of tuples): [(name, score), ...]
        stats (dict): Summary statistics from calculate_stats().
    """
    try:
        with open(filename, "w") as f:
            f.write("=" * 45 + "\n")
            f.write("          STUDENT GRADE REPORT\n")
            f.write("=" * 45 + "\n\n")

            for name, score in sorted(students, key=lambda x: x[1], reverse=True):
                grade = get_letter_grade(score)
                f.write(f"  {name:<20} {score:>5.1f}  ({grade})\n")

            f.write("\n" + "-" * 45 + "\n")
            f.write(f"  Total students:  {stats['total']}\n")
            f.write(f"  Class average:   {stats['average']:.1f}\n")
            f.write(f"  Highest score:   {stats['highest']}\n")
            f.write(f"  Lowest score:    {stats['lowest']}\n")
            f.write(f"  Passing (>=70):  {stats['passing_count']}/{stats['total']}\n")
            f.write("=" * 45 + "\n")

        print(f"Report saved to '{filename}'")
    except IOError as e:
        print(f"Error writing report: {e}")

def main():
    """Run the data analyzer program."""
    input_file = "scores.csv"
    output_file = "grade_report.txt"

    print(f"Loading scores from '{input_file}'...")
    students = load_scores(input_file)

    if not students:
        print("No data to analyze.")
        return

    stats = calculate_stats(students)
    print(f"Analyzed {stats['total']} students.")

    write_report(output_file, students, stats)

main()
```

### Evaluation Checklist
- [ ] Reads data from file using `with open()`
- [ ] Handles `FileNotFoundError` with `try/except`
- [ ] Handles invalid data with `try/except`
- [ ] At least 4 functions, each with a docstring
- [ ] Writes results to an output file
- [ ] Calculates at least 3 statistics
- [ ] Main function orchestrates everything
- [ ] Program runs without crashing on valid and invalid input

---