# Day 11: The math & datetime Modules

**Learning Target:** I can use the math module for advanced calculations and the datetime module for working with dates and times.

---

## Key Concepts

**The math Module:**
- **Constants:** `math.pi`, `math.e`
- **Functions:** `math.sqrt()`, `math.ceil()`, `math.floor()`, `math.pow()`, `math.sin()`, `math.cos()`, `math.tan()`

**The datetime Module:**
- **date:** Represents a calendar date (year, month, day)
- **time:** Represents a time (hour, minute, second)
- **datetime:** Combines date and time
- **timedelta:** Represents a duration/difference

---

## Code Examples

```python
import math
from datetime import date, time, datetime, timedelta

# MATH MODULE
print(math.pi)                    # 3.14159...
print(math.sqrt(16))              # 4.0
print(math.ceil(4.2))             # 5 (round up)
print(math.floor(4.8))            # 4 (round down)
print(math.pow(2, 3))             # 8.0 (2^3)

# DATETIME MODULE
# Current date
today = date.today()
print(today)                      # 2026-03-25

# Specific date
birthday = date(1995, 7, 15)
print(birthday)                   # 1995-07-15

# Current datetime
now = datetime.now()
print(now)                        # 2026-03-25 14:30:45.123456

# Timedelta (duration)
next_week = today + timedelta(days=7)
print(next_week)                  # One week from today

# Format dates
formatted = today.strftime("%B %d, %Y")
print(formatted)                  # "March 25, 2026"

# Calculate age
birthday = date(2008, 5, 10)
age = (date.today() - birthday).days // 365
print(f"Age: {age}")
```

---

## Guided Practice

1. **Calculate Distance:** Use `math.sqrt()` to calculate the distance between two points using the Pythagorean theorem.

2. **Count Days:** Calculate how many days until your next birthday.

3. **Schedule Tasks:** Create dates for events 30 days, 60 days, and 90 days from today.

4. **Format Dates:** Convert a date to different formats using `strftime()`.

---

## Practice Problems

**Beginner:** Write code that calculates the square root of a number using `math.sqrt()` and displays it.

**Intermediate:** Create a function that takes a birth date and returns the person's age in years.

**Challenge:** Write a program that displays "Days until vacation" given a vacation date.

<details>
<summary>💡 Hints</summary>
- `math.sqrt(x)` returns the square root of x
- `(date1 - date2).days` gives the number of days between dates
- Use `strftime()` with format codes like `%B` (month name), `%d` (day), `%Y` (year)
- `timedelta(days=n)` creates a duration of n days
- `date.today()` returns today's date
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import math

number = 49
result = math.sqrt(number)
print(f"Square root of {number} is {result}")
```

**Intermediate:**
```python
from datetime import date

def calculate_age(birth_date):
    today = date.today()
    age = (today - birth_date).days // 365
    return age

birthday = date(2008, 5, 10)
print(f"Age: {calculate_age(birthday)}")
```

**Challenge:**
```python
from datetime import date, timedelta

vacation_date = date(2026, 7, 15)
days_left = (vacation_date - date.today()).days

if days_left > 0:
    print(f"Days until vacation: {days_left}")
else:
    print("Vacation is today or has passed!")
```
</details>
