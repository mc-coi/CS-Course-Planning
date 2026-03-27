# Day 12: The datetime Module – Dates & Formatting

**Learning Target:** I can work with dates, times, and create formatted date strings for real-world applications.

---

## Key Concepts

**Creating Dates:**
```python
date(year, month, day)
```

**Common Methods:**
- `.today()` — Current date
- `.year`, `.month`, `.day` — Access parts
- `strftime(format)` — Format as string
- `strptime(string, format)` — Parse string to date

**Format Codes:**
- `%Y` — 4-digit year (2026)
- `%y` — 2-digit year (26)
- `%m` — Month number (03)
- `%B` — Full month name (March)
- `%b` — Abbreviated month (Mar)
- `%d` — Day of month (25)
- `%A` — Full weekday (Tuesday)
- `%a` — Abbreviated weekday (Tue)
- `%H` — Hour (00-23)
- `%M` — Minute (00-59)
- `%S` — Second (00-59)

---

## Code Examples

```python
from datetime import date, datetime

# Create dates
today = date.today()
christmas = date(2026, 12, 25)
new_years = date(2027, 1, 1)

# Access components
print(today.year)      # 2026
print(today.month)     # 3
print(today.day)       # 25

# Format as strings
print(today.strftime("%B %d, %Y"))           # "March 25, 2026"
print(today.strftime("%A, %B %d"))           # "Tuesday, March 25"
print(today.strftime("%m/%d/%Y"))            # "03/25/2026"
print(today.strftime("%Y-%m-%d"))            # "2026-03-25" (ISO format)

# Parse string to date
date_string = "12/25/2026"
christmas = datetime.strptime(date_string, "%m/%d/%Y").date()
print(christmas)       # 2026-12-25

# Working with datetime (includes time)
now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))    # "2026-03-25 14:30:45"
```

---

## Guided Practice

1. **Format Today's Date:** Display today's date in three different formats (e.g., "March 25, 2026" and "2026-03-25").

2. **Parse User Input:** Ask the user for a date in MM/DD/YYYY format and convert it to a date object.

3. **Get Day of Week:** Determine what day of the week your birthday falls on.

4. **Log with Timestamps:** Create a simple log file entry with current date and time.

---

## Practice Problems

**Beginner:** Write code that displays today's date in the format "Tuesday, March 25, 2026".

**Intermediate:** Create a function that takes a date string (e.g., "12/25/2026") and returns the day of the week.

**Challenge:** Build a simple event logger that logs events with formatted timestamps (e.g., "[2026-03-25 14:30:45] Event description").

<details>
<summary>💡 Hints</summary>
- Use `date.today()` for today's date
- Use `.strftime()` with format codes to create formatted strings
- Use `.strptime()` to parse a string into a date
- `.weekday()` returns 0-6 (Mon-Sun); use `calendar` module for names
- `datetime.now()` includes time; `date.today()` is date-only
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
from datetime import date

today = date.today()
print(today.strftime("%A, %B %d, %Y"))
```

**Intermediate:**
```python
from datetime import datetime

def get_day_of_week(date_string):
    date_obj = datetime.strptime(date_string, "%m/%d/%Y")
    return date_obj.strftime("%A")

print(get_day_of_week("12/25/2026"))
```

**Challenge:**
```python
from datetime import datetime

events = []

def log_event(description):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    event = f"[{timestamp}] {description}"
    events.append(event)
    print(event)

log_event("User logged in")
log_event("File saved")
```
</details>
