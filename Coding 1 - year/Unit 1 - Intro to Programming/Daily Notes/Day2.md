# Day 2: Pseudocode & Flowcharts
**Learning Target:** I can write and trace pseudocode and flowcharts to represent algorithms.

### Key Concepts
Before writing actual code, it's helpful to plan your solution using **pseudocode** and **flowcharts**. These tools help you think through the logic without worrying about programming syntax.

**Pseudocode** is a way of writing algorithms using English-like statements instead of actual code. It's human-readable and focuses on the logic of the solution. Unlike code, pseudocode is informal and designed for clarity. Example:
```
Ask the user for two numbers
Add the two numbers together
Display the result
```

**Flowcharts** are visual diagrams that represent the flow of an algorithm using standard shapes:
- **Ovals** = Start/End points
- **Rectangles** = Processes or actions
- **Diamonds** = Decisions (yes/no questions)
- **Arrows** = Direction of flow

A good flowchart should be:
- Clear and easy to follow
- Use standard shapes correctly
- Show decision points explicitly
- Follow a logical sequence from top to bottom

### Code Examples
```python
# Example: Average of two numbers
# Pseudocode first:
# 1. Ask user for first number
# 2. Ask user for second number
# 3. Add them together
# 4. Divide the sum by 2
# 5. Print the result

# Python code implementing the pseudocode:
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
average = (num1 + num2) / 2
print(f"Average: {average}")

# Example 2: Larger of two numbers (with decision)
# Pseudocode:
# 1. Ask user for first number
# 2. Ask user for second number
# 3. If first > second, display first
# 4. Otherwise display second
# (We'll learn if/else statements later!)
```

### Guided Practice
Write pseudocode for a simple task: "Make a cup of tea." Include at least 6 steps. Then convert your pseudocode into a flowchart (you can draw it or describe it using text).

### Practice Problems

**Problem 1 — Beginner:** Convert this algorithm into clear pseudocode:
```
Start → Ask for your name → Ask for your age → Calculate birth year (2026 - age) →
Display name and birth year → End
```

**Problem 2 — Intermediate:** Write pseudocode for ordering a pizza online (including a decision: what if they're out of your favorite topping?).

**Problem 3 — Challenge:** Create a flowchart for this scenario: "Check if a student can attend a field trip. They must be on time AND not have any failing grades."

<details>
<summary>💡 Hints</summary>

- Problem 1: Write each step as a clear English sentence; don't worry about Python syntax
- Problem 2: Include at least one "if this, then that" type of decision
- Problem 3: Use diamonds for the two decisions and think about how AND logic works
</details>

<details>
<summary>✅ Sample Answers</summary>

```
# Problem 1 Example Pseudocode:
Start
Display "Welcome"
Ask user for name, store in variable
Ask user for age, store in variable
Subtract age from 2026, store as birth_year
Display "Your name is [name] and you were born in [birth_year]"
End

# Problem 2 Example Pseudocode (first 6 steps):
Start
Open pizza website
Select restaurant
Browse menu
For each topping in the desired toppings list:
  If topping is available:
    Add topping to order
  Else:
    Show customer "out of stock message"
Continue with checkout
End
```

</details>

---
