# Day 6: Sprint 1 – Building Core Features (Part 1)

**Session Goal:** Implement the first 2–3 core features. Focus on depth over breadth.

---

## Today's Focus

Now that your structure is in place, start building real features. Pick the simplest core feature and complete it end-to-end: write the function, test it, and make sure it works. It's better to have 2 finished features than 5 half-finished ones.

---

## Work Session Agenda

**Minutes 0-5:** **Sprint Standup**
- Teacher: which features are good to code first? (typically: data setup, basic CRUD, file I/O)
- Students: identify 1–2 features for today's focus

**Minutes 5-50:** **Focused Coding**
- Pick ONE feature from your plan (e.g., "add student" or "load data from CSV")
- Write code from start to finish: function implementation, basic error handling, test it
- Run frequently to catch bugs early
- If stuck for more than 10 minutes, ask teacher or classmate

**Minutes 50-55:** **Wrap-up**
- Test your feature one more time
- Commit/save work
- Update progress tracker with what you completed

---

## Common First Features by Project

**Data Analyzer:** Load data from file (CSV/JSON)
**API App:** Fetch data from API, parse JSON response
**Student System:** Add student, save to JSON, load from JSON
**Algorithm Visualizer:** Implement one sorting algorithm, test with small array
**Custom:** Your simplest core feature

---

## Building a Feature: Step-by-Step Process

1. **Write a stub** — empty function with docstring
2. **Write pseudocode** — comment out the steps
3. **Implement line by line** — fill in real code
4. **Test immediately** — print intermediate values, verify logic
5. **Handle errors** — `try/except` for likely problems
6. **Clean up** — remove debug prints, check variable names
7. **Move to next feature** — never spend entire day polishing one thing

---

## Common Pitfalls & How to Avoid Them

**Pitfall: "I'll come back to error handling later"**
- Reality: you won't, and bugs will hide in edge cases
- Instead: add `try/except` as you code

**Pitfall: "I'll test my whole app when it's done"**
- Reality: finding bugs after building 5 features is slow
- Instead: test each feature immediately after writing it

**Pitfall: "My code is messy but it works"**
- Reality: you'll waste 2 hours debugging next week because you can't read it
- Instead: use clear variable names and add comments now

---

## Debugging Tips

**Use print statements:**
```python
def load_students(filename):
    print(f"Loading from {filename}")  # Debug point 1
    with open(filename) as f:
        data = json.load(f)
    print(f"Loaded {len(data)} records")  # Debug point 2
    return [Student(**s) for s in data]
```

**Test in isolation:**
```python
# At bottom of file, not in main loop:
if __name__ == "__main__":
    # Test load_students with a sample file
    students = load_students("data/test_students.json")
    print(students[0].get_summary())
```

**Use Python debugger (optional):**
```python
import pdb
pdb.set_trace()  # Execution pauses here; you can inspect variables
```

---

## Reflection / Exit Ticket

1. Which feature did you build today?
2. Did you run into any bugs? How did you fix them?
3. How many features are left for Sprint 1?

---

## Progress Checklist

- [ ] Picked one core feature to build
- [ ] Feature coded end-to-end
- [ ] Feature tested and working
- [ ] Code committed/saved
- [ ] Added basic error handling if applicable
