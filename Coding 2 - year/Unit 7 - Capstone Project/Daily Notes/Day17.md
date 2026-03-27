# Day 17: Sprint 3 Begins – Polish, Error Handling & Edge Cases

**Session Goal:** Focus on quality, resilience, and edge cases. Make your app bulletproof.

---

## Today's Focus

You've built features; now polish them. Sprint 3 is about making your app robust and professional. It should handle mistakes gracefully, communicate clearly, and never crash. By the time you present, users should feel confident using your software.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint 3 Overview**
- Teacher: what is "production quality"? (robust, documented, tested)
- Focus: error handling, edge cases, user experience
- Timeline: 4 days to polish, then 2 days to document and present

**Minutes 5-50:** **Systematic Error Handling & Testing**

Work through your app systematically:

1. **Every input point** — what if user enters garbage? Add validation.
2. **Every file operation** — what if file doesn't exist? Catch it.
3. **Every API call** — what if server is down? Show error.
4. **Every calculation** — what if denominator is 0? Guard it.

Test scenarios:
- Empty input (hit Enter without typing)
- Wrong type (type letters when asked for number)
- Out of range (GPA of 10, negative student ID)
- Missing files, slow networks, corrupted data

**Minutes 50-55:** **Wrap-up & Save**
- Commit improvements with messages like "Add validation for GPA input"
- Update progress

---

## Error Handling Patterns

**Pattern 1: Input Validation**
```python
def get_gpa_from_user(self):
    """Prompt user for GPA with validation."""
    while True:
        try:
            gpa = float(input("Enter GPA (0–4.0): "))
            if not 0 <= gpa <= 4.0:
                print("GPA must be between 0 and 4.0")
                continue
            return gpa
        except ValueError:
            print("Invalid number. Please try again.")
```

**Pattern 2: File Operations**
```python
def load_from_json(self, filename):
    """Load students from JSON file. Handles missing/invalid files."""
    try:
        with open(filename) as f:
            data = json.load(f)
        students = [Student(**s) for s in data]
        print(f"Loaded {len(students)} students")
        return students
    except FileNotFoundError:
        print(f"File {filename} not found. Starting with empty list.")
        return []
    except json.JSONDecodeError:
        print(f"File {filename} is corrupted. Starting fresh.")
        return []
```

**Pattern 3: API Calls**
```python
def fetch_data(self, url):
    """Fetch data from API with error handling."""
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()  # Raise error for bad status codes
        return response.json()
    except requests.exceptions.ConnectionError:
        print("No internet connection. Using cached data.")
        return self.load_cache()
    except requests.exceptions.Timeout:
        print("Request timed out. Please try again.")
        return None
    except json.JSONDecodeError:
        print("Invalid response from server.")
        return None
```

**Pattern 4: Guard Against Bad Calculations**
```python
def calculate_average_gpa(self, students):
    """Calculate average GPA, handling empty list."""
    if not students:
        print("No students to average")
        return 0
    return sum(s.gpa for s in students) / len(students)
```

---

## Edge Cases Checklist

Go through your app and handle:

- [ ] Empty lists/datasets
- [ ] Single item (not just multiple)
- [ ] Zero or negative numbers
- [ ] Very large numbers
- [ ] Special characters in text
- [ ] Whitespace (leading/trailing spaces)
- [ ] Missing files
- [ ] Corrupted data
- [ ] Slow networks / timeouts
- [ ] User hitting Ctrl+C (graceful exit)

---

## Testing Your Improvements

```python
# At bottom of a file, add quick tests:

if __name__ == "__main__":
    # Test edge cases
    system = StudentSystem()

    # Test 1: Get average of empty list
    avg = system.calculate_average_gpa([])
    assert avg == 0, "Should handle empty list"
    print("✓ Empty list test passed")

    # Test 2: Add student with invalid GPA
    try:
        system.add_student(Student("Bob", 100, 5.0))
        assert False, "Should reject GPA > 4.0"
    except ValueError:
        print("✓ Invalid GPA test passed")

    # Test 3: Search empty system
    results = system.search_by_name("Alice")
    assert results == [], "Should return empty list"
    print("✓ Empty search test passed")

    print("\nAll edge case tests passed!")
```

---

## User Experience Improvements

Make your app pleasant to use:

**Clear messages:**
```python
# BEFORE: confusing
print("Error: invalid value")

# AFTER: helpful
print("Error: GPA must be a number between 0 and 4.0. Try again.")
```

**Confirmations:**
```python
# BEFORE: dangerous
print("Deleting student...")
system.remove_student(100)

# AFTER: safe
confirm = input(f"Delete {student.name}? (yes/no): ")
if confirm.lower() == "yes":
    system.remove_student(100)
    print("Student deleted.")
```

**Progress feedback:**
```python
# BEFORE: silent
with open("students.json") as f:
    data = json.load(f)

# AFTER: user knows it's working
print("Loading students...")
with open("students.json") as f:
    data = json.load(f)
print(f"Loaded {len(data)} students.")
```

---

## Reflection / Exit Ticket

1. What edge case did you discover and fix today?
2. Did adding error handling break any features? How did you fix it?
3. How much more "professional" does your app feel now?

---

## Progress Checklist

- [ ] Input validation added to all user inputs
- [ ] File operations protected with try/except
- [ ] Edge cases identified and handled
- [ ] Error messages are helpful and clear
- [ ] App doesn't crash on bad input
- [ ] Code committed/saved
