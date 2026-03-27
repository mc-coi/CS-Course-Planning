# Day 15: Practice Lab — Unit Converters & Calculators
**Learning Target:** I can integrate all Unit 1 concepts to build functional, formatted programs.

### Key Concepts
This lab consolidates Weeks 2-3. You'll apply:
- Input collection and type conversion
- Variables and reassignment
- All seven arithmetic operators
- Order of operations
- Professional output formatting with f-strings
- Comments and good code organization

**Real-world programs** solve practical problems:
- Unit converters (temperature, distance, weight, currency)
- Calculators (tips, taxes, grades, loans)
- Data processors (averages, totals, percentages)

### Code Examples
```python
# Example: Temperature Converter
print("=== TEMPERATURE CONVERTER ===\n")
celsius = float(input("Temperature in Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit:.1f}°F")

# Example: Unit Converter
km = float(input("Distance in kilometers: "))
miles = km * 0.621371
print(f"{km} km = {miles:.2f} miles")
```

### Guided Practice
Create a complete program (choose one):

**Option A: Temperature Converter**
- Asks user for temperature in Celsius
- Converts to Fahrenheit using formula: F = C × 9/5 + 32
- Displays with professional formatting

**Option B: Weight Unit Converter**
- Asks for weight in pounds
- Converts to kilograms (1 lb = 0.453592 kg) and vice versa
- Shows both conversions with proper formatting

**Option C: Time Calculator**
- Asks for hours and minutes
- Calculates total seconds
- Calculates total minutes
- Displays breakdown in human-readable format

### Practice Problems

**Problem 1 — Beginner:** Create a currency converter. Ask for USD and display equivalent in EUR (use 0.92 as exchange rate).

**Problem 2 — Intermediate:** Create a distance converter. Ask for miles and display kilometers, meters, and feet.

**Problem 3 — Challenge:** Create a compound interest calculator. Ask for principal, annual rate, and years. Calculate and display the amount at the end using: A = P(1 + r/100)^n

<details>
<summary>💡 Hints</summary>

- Problem 1: Use proper decimal formatting
- Problem 2: 1 mile = 1.60934 km, 1 km = 3280.84 feet
- Problem 3: Use ** for exponentiation; remember order of operations
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
usd = float(input("Amount in USD: $"))
eur = usd * 0.92
print(f"${usd:.2f} USD = €{eur:.2f} EUR")

# Problem 2 Example
miles = float(input("Distance in miles: "))
km = miles * 1.60934
feet = miles * 5280
print(f"{miles} miles = {km:.2f} km")
print(f"{miles} miles = {feet:.0f} feet")

# Problem 3 Example
principal = float(input("Principal: $"))
rate = float(input("Annual rate (%): "))
years = int(input("Years: "))
amount = principal * (1 + rate/100) ** years
print(f"After {years} years: ${amount:.2f}")
```

</details>

---
