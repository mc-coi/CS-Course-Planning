# Day 37: Building a Complete Interactive Program with Input Validation

**Learning Target:** I can build complete interactive programs that handle user input safely and guide users through processes.

### Key Concepts

**Input validation** checks that user input is valid before using it. This prevents errors and makes programs more robust.

**Basic validation patterns:**
1. Check if input can be converted (is it a valid number?)
2. Check if input is in a valid range (is the number positive? less than 100?)
3. Check if input meets requirements (is it long enough? does it contain required characters?)
4. Provide clear error messages and ask again

**Good program structure:**
1. Display a welcome or description
2. Get user input
3. Validate it
4. Process the input
5. Display results
6. Ask if user wants to continue or exit

### Code Examples

```python
# Example 1: Simple validation
age_str = input("How old are you? ")
try:
    age = int(age_str)
    if age < 0 or age > 150:
        print("Please enter a realistic age.")
    else:
        print(f"You are {age} years old.")
except ValueError:
    print("Please enter a valid number.")

# Example 2: Guided program flow
print("=== Welcome to Grade Calculator ===")
name = input("Enter your name: ").strip()

score1 = float(input("Test 1 score: "))
score2 = float(input("Test 2 score: "))
score3 = float(input("Test 3 score: "))

average = (score1 + score2 + score3) / 3
print(f"\n{name}, your average is {average:.1f}%")

if average >= 90:
    print("Grade: A")
elif average >= 80:
    print("Grade: B")
elif average >= 70:
    print("Grade: C")
else:
    print("Grade: F")

# Example 3: Input with range validation
while True:
    rating_str = input("Rate this program (1-5): ")
    try:
        rating = int(rating_str)
        if 1 <= rating <= 5:
            print(f"Thanks! You rated it {rating}/5.")
            break
        else:
            print("Please enter a number between 1 and 5.")
    except ValueError:
        print("Please enter a valid number.")
```

### Guided Practice

Create an **Interactive Survey Program**:
1. Display a welcome message
2. Ask the user 3 questions (with appropriate input types)
3. Validate each input
4. Display a summary of responses
5. Ask if they want to take the survey again

### Practice Problems

**Problem 1 — Beginner:**
Create a program that asks for name and age, validates that age is a positive number, then displays a message.

```python
print("=== User Information ===")
name = input("Name: ").strip()

while True:
    age_str = input("Age: ")
    try:
        age = int(age_str)
        if age > 0:
            break
        else:
            print("Please enter a positive age.")
    except ValueError:
        print("Please enter a valid number.")

print(f"Welcome, {name}! You are {age} years old.")
```

**Problem 2 — Intermediate:**
Create a program that:
- Asks for a test score (0-100)
- Validates the input
- Assigns a letter grade
- Asks if user wants to grade another test
- Repeats if yes, exits if no

**Problem 3 — Challenge:**
Create a **Menu-Driven Program**:
- Display a menu: 1) Temperature Converter, 2) Unit Converter, 3) Exit
- Validate menu choice
- Perform selected calculation
- Ask if user wants another calculation
- Loop back to menu

<details>
<summary>💡 Hints</summary>

- Problem 1: Use try/except for type conversion, check age > 0.
- Problem 2: Use a loop that asks "Again? (yes/no)" until user says no.
- Problem 3: Use a while loop with input() to get menu choice, then if/elif/else to handle choices.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example (see above)

# Problem 2 Example
while True:
    while True:
        score_str = input("Test score (0-100): ")
        try:
            score = float(score_str)
            if 0 <= score <= 100:
                break
            else:
                print("Please enter a score between 0 and 100.")
        except ValueError:
            print("Please enter a valid number.")

    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"

    print(f"Score: {score:.1f}% - Grade: {grade}")

    again = input("Grade another test? (yes/no): ").strip().lower()
    if again != "yes":
        break

print("Goodbye!")

# Problem 3 Example
while True:
    print("\n=== Calculator Menu ===")
    print("1) Temperature Converter")
    print("2) Unit Converter")
    print("3) Exit")

    choice = input("Choose (1-3): ").strip()

    if choice == "1":
        celsius = float(input("Celsius: "))
        fahrenheit = (celsius * 9/5) + 32
        print(f"{celsius}°C = {fahrenheit:.1f}°F")
    elif choice == "2":
        meters = float(input("Meters: "))
        feet = meters * 3.28084
        print(f"{meters}m = {feet:.2f} ft")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.")
```

</details>

---
