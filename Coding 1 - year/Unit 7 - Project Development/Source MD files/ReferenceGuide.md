# Unit 7 Reference Guide: Project Development Tools and Templates

## Table of Contents
1. [SDLC Framework](#sdlc-framework)
2. [Planning Templates](#planning-templates)
3. [Code Structure](#code-structure)
4. [Testing Strategies](#testing-strategies)
5. [Documentation Standards](#documentation-standards)
6. [Presentation Tips](#presentation-tips)

---

## SDLC Framework

### The Six Phases

| Phase | When | What You Do | Outputs | Success Criteria |
|-------|------|------------|---------|------------------|
| **1. Define** | Days 146-147 | Understand problem, identify users | Problem statement, audience analysis | Can describe problem in 1-2 sentences |
| **2. Plan** | Days 148-150 | Design solution, break into tasks | Pseudocode, flowcharts, task list | Detailed enough to code from |
| **3. Design** | Days 151-155 | Design architecture and MVP | UI sketches, data structures, functions | Working prototype exists |
| **4. Code** | Days 156-165 | Build incrementally, test as you go | Working features, tested functions | All features working |
| **5. Polish** | Days 166-170 | Clean code, test thoroughly, fix bugs | Professional code, comprehensive tests | Production-ready |
| **6. Present** | Days 171-180 | Document, present, reflect | Presentation, documentation, portfolio | Successfully presented |

---

## Planning Templates

### Project Proposal Template

```
PROJECT TITLE: ___________________________

PROBLEM STATEMENT (2-3 sentences):
- What problem does it solve?
- Who needs it?
- Why is it important?

TARGET AUDIENCE (1-2 sentences):
- Who are the users?
- What are their needs?

CORE FEATURES (3-5 features):
1. [Feature]
2. [Feature]
3. [Feature]

NICE-TO-HAVE FEATURES (optional):
1. [Feature]
2. [Feature]

INPUTS & OUTPUTS:
Inputs: [What data comes in?]
Outputs: [What does program produce?]

TECHNOLOGY & DATA STRUCTURES:
- Lists, dictionaries, loops, functions, file I/O, etc.

FUNCTION LIST:
Function Name          | What It Does             | Parameters | Returns
---------------------- | ----------------------- | ---------- | ----------
[name]                 | [description]           | [types]    | [types]
main()                 | Orchestrate program     | none       | none

SUCCESS CRITERIA:
[ ] Feature 1 working and tested
[ ] Feature 2 working and tested
[ ] Feature 3 working and tested
[ ] Error handling throughout
[ ] Code documented with docstrings
[ ] No crashes on bad input

TEST CASES:
- Normal case: [input] → [expected output]
- Edge case 1: [input] → [expected output]
- Error case 1: [input] → [expected output]
```

### Pseudocode Template

```
PROGRAM: [Program Name]

1. [Main step]
   a. [Sub-step]
   b. [Sub-step]
      i. [Detail]
      ii. [Detail]
2. [Main step]
   a. IF [condition]:
      - [Action 1]
      - [Action 2]
   b. ELSE:
      - [Action 3]
3. LOOP until [condition]:
   a. [Action]
   b. [Action]
4. [Calculate/process]
5. [Display/output]
6. [Save/persist if applicable]
```

### Task Breakdown Template

```
PROJECT: [Name]

MILESTONE 1: [Name] (Days X-Y)
Deadline: Day X

Tasks:
- [ ] Task 1 (estimated: 1 day)
- [ ] Task 2 (estimated: 2 days)
- [ ] Task 3 (estimated: 1 day)

Dependencies:
- Task 2 depends on Task 1

Success Criteria:
- [ ] Acceptance criteria met

---

MILESTONE 2: [Name] (Days X-Y)
[Similar structure]
```

---

## Code Structure

### Project File Organization

```python
"""
project_name.py
Brief description of what program does.

Author: [Your Name]
Date: [Date]
Version: 1.0
"""

# ════════════════════════════════════════════════════════
# IMPORTS
# ════════════════════════════════════════════════════════

import os
from datetime import datetime

# ════════════════════════════════════════════════════════
# CONSTANTS
# ════════════════════════════════════════════════════════

MAX_SCORE = 100
MIN_SCORE = 0
PASSING_GRADE = 70
DATA_FILE = "data.txt"

# ════════════════════════════════════════════════════════
# INPUT FUNCTIONS
# ════════════════════════════════════════════════════════

def get_user_input():
    """Get and validate user input."""
    pass

# ════════════════════════════════════════════════════════
# PROCESSING FUNCTIONS
# ════════════════════════════════════════════════════════

def process_data(data):
    """Process and calculate results."""
    pass

# ════════════════════════════════════════════════════════
# OUTPUT FUNCTIONS
# ════════════════════════════════════════════════════════

def display_results(results):
    """Display formatted output."""
    pass

# ════════════════════════════════════════════════════════
# FILE I/O FUNCTIONS
# ════════════════════════════════════════════════════════

def save_data(filename, data):
    """Save data to file."""
    pass

def load_data(filename):
    """Load data from file."""
    pass

# ════════════════════════════════════════════════════════
# MAIN
# ════════════════════════════════════════════════════════

def main():
    """Run the program."""
    pass

# ════════════════════════════════════════════════════════

if __name__ == "__main__":
    main()
```

### Function Docstring Template

```python
def function_name(param1, param2):
    """
    One-line description of what function does.

    Longer description if needed (can be multiple sentences).
    Explain what the function is for and any special behavior.

    Parameters:
        param1 (type): Description of param1
        param2 (type): Description of param2

    Returns:
        return_type: Description of return value

    Raises:
        ExceptionType: Description of when this is raised

    Example:
        >>> result = function_name(5, 10)
        >>> print(result)
        15
    """
    # Code here
    pass
```

---

## Testing Strategies

### Unit Test Template

```python
def test_function_name():
    """Test function_name with various inputs."""
    # Arrange (set up test data)
    input_data = [1, 2, 3]
    expected = 6

    # Act (call the function)
    result = sum_values(input_data)

    # Assert (check the result)
    assert result == expected, f"Expected {expected}, got {result}"
    print("✓ test_function_name passed")

# Run tests
test_function_name()
```

### Test Case Documentation

```
═══════════════════════════════════════════════════════════
TEST CASE #[N]: [Test Name]

Category: [Normal/Edge/Error]

Scenario: [What are we testing?]

Inputs:
- Input 1: [value]
- Input 2: [value]

Expected Output:
- Output 1: [expected value]
- Output 2: [expected value]

Actual Output:
- Output 1: [actual value]
- Output 2: [actual value]

Result: [✓ PASS / ✗ FAIL]

Notes:
[Any additional observations or bugs found]
═══════════════════════════════════════════════════════════
```

### Test Case Categories

**Normal Cases:**
- Typical usage with expected inputs
- Represents 70% of real usage

**Edge Cases:**
- Boundary values (0, 1, max, min)
- Empty inputs
- Single elements
- Very large values

**Error Cases:**
- Invalid input types
- Out-of-range values
- Missing data
- File not found
- Permission denied

---

## Documentation Standards

### README Template

```markdown
# [Project Name]

[One sentence description]

## Overview

[2-3 paragraphs explaining what the program does, who it's for, and why it's useful]

## Features

- Feature 1: Description
- Feature 2: Description
- Feature 3: Description

## Requirements

- Python 3.6 or higher
- [Any other requirements]
- No external libraries (if applicable)

## Installation

1. Clone/download the project
2. Navigate to the folder
3. Run: `python [project_name].py`

## Usage

### Basic Usage

[Describe how to use in basic way]

### Example

```
Input: [example input]
Output: [example output]
```

## File Structure

```
project_folder/
├── project_name.py      # Main program
├── README.md            # This file
├── data/                # Data folder
│   └── sample.txt
└── docs/                # Documentation
    └── user_guide.md
```

## How It Works

[Describe the main workflow/algorithm]

## Troubleshooting

### Issue: [Common issue]
Solution: [How to fix]

### Issue: [Common issue]
Solution: [How to fix]

## Future Improvements

- [ ] Feature idea 1
- [ ] Feature idea 2
- [ ] Optimization idea

## Author

[Your Name], Coding I Capstone Project, 2026

## License

Educational project
```

### Code Comments Best Practices

```python
# ✗ BAD COMMENTS (explain what the code does)
i = 0  # Set i to 0
for score in scores:  # Loop through scores
    i += 1  # Add 1 to i

# ✓ GOOD COMMENTS (explain why, not what)
# Keep track of how many scores we've processed
count = 0
for score in scores:
    # Start from 1 for user-friendly display (UI expects 1-indexed)
    count += 1

# ✓ GOOD COMMENTS (clarify tricky logic)
# Check for 89.9+ to handle floating-point rounding edge cases
if average >= 89.95:
    grade = "A"
```

---

## Presentation Tips

### Presentation Checklist

Before presenting, verify:

```
CONTENT:
[✓] Opening clearly states the problem
[✓] Demo shows core features working
[✓] Code explanation is clear (not line-by-line)
[✓] Challenges section demonstrates learning
[✓] Closing invites questions

TECHNICAL:
[✓] Demo is tested and works
[✓] Slides are visible from back of room
[✓] Audio is clear
[✓] Code editor is open and ready

DELIVERY:
[✓] Opening is confident
[✓] Eye contact with audience
[✓] Speaking clearly and slowly
[✓] Pauses for emphasis
[✓] Closes with strength
[✓] Ready for questions
```

### Question Handling

```
QUESTION: "What happens if the user types nothing?"

GOOD RESPONSE:
"Great question! We handle that with input validation.
We check if the string is empty, and if so, we ask them
to try again."

POOR RESPONSE:
"Um... I'm not sure. Maybe we just... crash? I dunno."

BEST RESPONSE (if unsure):
"That's a good question. I didn't specifically test that
case. I would need to go back and check my code."
```

---

## Quick Reference: Error Handling Patterns

```python
# Pattern 1: Input validation
while True:
    try:
        value = float(input("Enter a number: "))
        if 0 <= value <= 100:
            return value
        else:
            print("Must be 0-100")
    except ValueError:
        print("Please enter a valid number")

# Pattern 2: File operations
try:
    with open(filename, "r") as f:
        data = f.read()
except FileNotFoundError:
    print(f"File {filename} not found")
    data = ""

# Pattern 3: Safe defaults
try:
    result = risky_operation()
except SomeError:
    result = default_value
    print("Using default value")
```

---

**This guide is your reference throughout Unit 7. Bookmark it!**
