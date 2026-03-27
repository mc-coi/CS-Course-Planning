# Vocabulary & Quick Reference

| Term | Definition |
|------|-----------|
| **Software Development Process** | The stages of planning, building, and refining a program |
| **Pseudocode** | Logic written in plain English, not code syntax |
| **Project specification** | Document describing inputs, outputs, and functions |
| **Bottom-up development** | Building helpers first, then connecting to main |
| **Unit testing** | Testing a single function in isolation |
| **Integration testing** | Testing how multiple functions work together |
| **Edge case** | Unusual input that might expose bugs (0, empty, max) |
| **Refactoring** | Improving code structure without changing behavior |
| **Single responsibility** | Each function does exactly one job |
| **Incremental development** | Building and testing small pieces at a time |
| **Bug** | An error causing incorrect behavior |
| **Debug** | The process of finding and fixing bugs |
| **Modular** | Code organized into small, reusable, single-purpose functions |
| **Code review** | Examining code for correctness, readability, and style |

### Course Concepts at a Glance

```python
# Everything you learned, in one program:

"""module docstring — what this file does"""

# Constants (Unit 2)
PASSING_SCORE = 70

def get_scores():
    """Collect valid scores from user. (Unit 5 + Unit 6)"""
    scores = []
    while True:                          # while loop (Unit 4)
        try:                             # error handling (Unit 6)
            entry = input("Score (or done): ")
            if entry.lower() == "done":  # conditionals (Unit 3)
                break                    # loop control (Unit 4)
            score = float(entry)         # type conversion (Unit 2)
            if 0 <= score <= 100:
                scores.append(score)     # list method (Unit 4)
            else:
                print("Must be 0–100")
        except ValueError:
            print("Enter a number")
    return scores                        # return value (Unit 5)

def analyze(scores):
    """Return stats dict. (Unit 5)"""
    if not scores:
        return {}
    return {                             # dictionary (Unit 4)
        "avg": sum(scores) / len(scores),
        "max": max(scores),
        "min": min(scores),
        "passing": sum(1 for s in scores if s >= PASSING_SCORE)
    }

def save_report(filename, stats):
    """Save stats to file. (Unit 6)"""
    try:                                 # file I/O (Unit 6)
        with open(filename, "w") as f:
            for key, val in stats.items():
                f.write(f"{key}: {val}\n")
    except IOError as e:
        print(f"Save failed: {e}")

def main():
    """Run the program. (Unit 7)"""
    scores = get_scores()                # function call (Unit 5)
    stats = analyze(scores)
    for k, v in stats.items():          # for loop (Unit 4)
        print(f"{k}: {v}")
    save_report("report.txt", stats)

main()
```

---