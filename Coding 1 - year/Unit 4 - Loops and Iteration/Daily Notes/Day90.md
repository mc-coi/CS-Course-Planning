# Day 90: Mini-Project Completion, Testing, and Peer Review

**Learning Target:** I can complete, test, and refine my mini-project, and provide constructive feedback to peers.

### Key Concepts

**Testing:** Verify your program works with various inputs:
- **Normal cases:** Typical, expected inputs
- **Edge cases:** Boundary values (empty list, single item, very large/small numbers)
- **Error cases:** Invalid input, unexpected entries

**Code refinement:** Clean up, improve readability, add comments.

**Peer review:** Examine others' work for bugs, improvements, and strengths.

### Testing Your Project

**For Number Analyzer:**
- Test with 1 number (check average, min, max)
- Test with 10+ numbers
- Test with negative numbers, decimals
- Test with duplicate numbers
- Verify sorting works correctly

**For Quiz Game:**
- Test with correct answers (all right)
- Test with incorrect answers
- Test case sensitivity (if relevant)
- Test replay functionality
- Verify score calculation is accurate

### Refining Your Code

**Checklist:**
- [ ] All functions work correctly
- [ ] Variable names are clear and descriptive
- [ ] Comments explain complex sections
- [ ] Output is properly formatted with headers and labels
- [ ] No unnecessary print statements or debugging code
- [ ] Program handles invalid input gracefully
- [ ] Code is DRY (Don't Repeat Yourself)—avoid duplicate logic

### Code Review Template

When reviewing a peer's project, provide feedback on:

**Strengths:**
- What works well? What did they do cleverly?

**Functionality:**
- Do all features work correctly?
- Are there any bugs?

**Code Quality:**
- Is the code readable and well-organized?
- Are variable names clear?
- Are there comments?

**Suggestions for Improvement:**
- What could be improved?
- Any features to add?
- Any edge cases they missed?

### Sample Implementations

**Number Analyzer (Complete Example):**
```python
# Number Analyzer
print("=== NUMBER ANALYZER ===\n")

# Collect numbers
numbers = []
count = 0
while True:
    user_input = input(f"Enter number {count+1} ('done' to stop): ")
    if user_input.lower() == "done":
        break
    try:
        num = float(user_input)
        numbers.append(num)
        count += 1
    except ValueError:
        print("Invalid input. Please enter a number.")

# Analysis
if len(numbers) > 0:
    print("\n=== RESULTS ===")
    print(f"Count: {len(numbers)}")
    print(f"Sum: {sum(numbers):.2f}")
    print(f"Average: {sum(numbers)/len(numbers):.2f}")
    print(f"Highest: {max(numbers):.2f}")
    print(f"Lowest: {min(numbers):.2f}")

    numbers.sort()
    print(f"Sorted: {numbers}")
else:
    print("No numbers entered.")
```

**Quiz Game (Complete Example):**
```python
# Quiz Game
import random

questions = [
    {"q": "What is 5 + 3?", "a": "8"},
    {"q": "What is the capital of France?", "a": "Paris"},
    {"q": "What is 10 * 2?", "a": "20"},
    {"q": "What is the largest planet?", "a": "Jupiter"},
    {"q": "How many continents are there?", "a": "7"}
]

score = 0
total = len(questions)

for i, item in enumerate(questions, 1):
    print(f"\nQuestion {i} of {total}:")
    print(item["q"])
    answer = input("Your answer: ").strip()

    if answer.lower() == item["a"].lower():
        print("Correct!")
        score += 1
    else:
        print(f"Incorrect. The answer is {item['a']}")

percentage = (score / total) * 100
print(f"\n=== RESULTS ===")
print(f"Score: {score}/{total} ({percentage:.1f}%)")
```

### Reflection Questions

1. What was the most challenging part of this project?
2. Which loop concept did you use the most?
3. How did you test your program?
4. What would you do differently next time?
5. What new feature would you add if you had more time?

### Submission Checklist

- [ ] Code runs without errors
- [ ] All features work as intended
- [ ] Code is clean and well-commented
- [ ] Output is formatted nicely
- [ ] Tested with multiple inputs
- [ ] Ready to share (code and sample output)
- [ ] Peer review completed
- [ ] Feedback incorporated (if any)

---

## Week 18 Reflection

**What you've learned:**
- Lists and their methods (append, remove, sort, reverse)
- For-each loops over lists
- Building complete programs with user input, data processing, and output
- Testing and debugging
- Peer review and feedback

**Key takeaway:** Lists are game-changing. Combined with loops, they let you build real programs that collect, process, and analyze data. Your mini-project shows you can apply all Unit 4 concepts to solve real problems.

---
