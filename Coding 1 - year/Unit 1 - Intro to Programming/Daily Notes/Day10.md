# Day 10: Practice Lab — Interactive Programs with Input/Output
**Learning Target:** I can create interactive programs that collect input, process it, and produce formatted output.

### Key Concepts
This day consolidates Week 2 learning. You'll create programs that:
- Ask users for information using `input()`
- Store it in variables with proper data types
- Process it (possibly with calculations or conversions)
- Display results in a user-friendly way

A good interactive program:
- Has clear prompts that tell users what to enter
- Processes input properly (converts to correct types)
- Shows results with labels and formatting
- Uses comments to explain the logic
- Makes it easy for users to understand what's happening

### Code Examples
```python
# Example: Personal Profile
print("=== PERSONAL PROFILE ===\n")
first_name = input("First name: ")
last_name = input("Last name: ")
age = int(input("Age: "))
gpa = float(input("GPA: "))

print("\n=== YOUR PROFILE ===")
print("Name: " + first_name + " " + last_name)
print(f"Age: {age}")
print(f"GPA: {gpa}")
print(f"Birth year (approximately): {2026 - age}")
```

### Guided Practice
Create a complete interactive program (choose one):

**Option A: Student Information Program**
- Collect: name, grade, age, favorite subject, GPA
- Calculate: approximate birth year
- Display everything in a formatted profile with clear labels

**Option B: Simple Currency Converter**
- Collect: an amount in USD
- Collect: which currency to convert to (EUR, JPY, GBP)
- Calculate: the converted amount using appropriate exchange rates
- Display with proper formatting

**Option C: Personal Statistics**
- Collect: name, height (in inches), weight (in lbs), age
- Calculate: BMI if desired (BMI = weight(lbs) / height(in)² × 703)
- Display in a formatted card or report

### Practice Problems

**Problem 1 — Beginner:** Create a program that asks for a student's name and three test scores, then calculates and displays the average.

**Problem 2 — Intermediate:** Create a program that asks for hours worked and hourly rate, then calculates gross pay, tax (15%), and net pay.

**Problem 3 — Challenge:** Create a program that builds a "character sheet" for a game. Ask for name, health, mana, strength, and level, then display everything formatted nicely in a box.

<details>
<summary>💡 Hints</summary>

- Problem 1: Ask for three separate scores, add them, divide by 3
- Problem 2: Use proper formatting for money output (dollar signs, 2 decimals)
- Problem 3: Use decorative characters to make a nice border around the card
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = input("Student name: ")
score1 = float(input("Test 1 score: "))
score2 = float(input("Test 2 score: "))
score3 = float(input("Test 3 score: "))
average = (score1 + score2 + score3) / 3
print(f"{name}'s average: {average:.2f}")

# Problem 2 Example
hours = float(input("Hours worked: "))
rate = float(input("Hourly rate: $"))
gross = hours * rate
tax = gross * 0.15
net = gross - tax
print(f"Gross: ${gross:.2f}")
print(f"Tax (15%): ${tax:.2f}")
print(f"Net: ${net:.2f}")

# Problem 3 Example
name = input("Character name: ")
health = int(input("Health: "))
mana = int(input("Mana: "))
strength = int(input("Strength: "))
level = int(input("Level: "))

print("\n" + "="*25)
print(f"  {name}")
print("="*25)
print(f"Health:    {health}")
print(f"Mana:      {mana}")
print(f"Strength:  {strength}")
print(f"Level:     {level}")
print("="*25)
```

</details>

---
