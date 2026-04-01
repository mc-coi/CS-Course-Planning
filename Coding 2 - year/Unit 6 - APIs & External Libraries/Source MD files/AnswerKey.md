# Unit 6: APIs & External Libraries — Complete Answer Key

---

## Problem Set 1: APIs & requests Library

---

## Problem 1: Fetch and Parse

### Solution
```python
import requests

response = requests.get("https://api.quotable.io/random")
quote = response.json()
print(f'"{quote["content"]}" — {quote["author"]}')
```

### Expected Output
```
"The way to get started is to quit talking and begin doing." — Walt Disney
(or different quote from API)
```

### Common Mistakes
- Not importing requests library
- Using `response.text` instead of `response.json()` (returns string, not dict)
- Wrong JSON field names: `quote` instead of `content`, `attr` instead of `author`
- Not handling potential API errors (connection, 404, etc.)

---

## Problem 2: Error Handling with APIs

### Solution
```python
import requests

def get_pokemon_height(name):
    """Fetch Pokemon height, handle missing Pokemon."""
    try:
        response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{name.lower()}")
        if response.status_code == 404:
            return "Pokemon not found"
        pokemon = response.json()
        return pokemon["height"]
    except Exception as e:
        return f"Error: {e}"

print(get_pokemon_height("pikachu"))          # 4
print(get_pokemon_height("invalidpokemon"))   # Pokemon not found
```

### Expected Output
```
4
Pokemon not found
```

### Common Mistakes
- Not checking status_code before accessing JSON
- Not converting name to lowercase (API expects lowercase)
- Not handling network errors/exceptions
- Catching Exception too broadly (should catch RequestException)
- Returning wrong error message

---

## Problem 3: Query Parameters

### Solution
```python
import requests

def get_city_temp(city):
    """Get current temperature for a city."""
    # Get coordinates for city
    geo_response = requests.get(
        "https://geocoding-api.open-meteo.com/v1/search",
        params={"name": city, "count": 1}
    )
    geo_data = geo_response.json()

    if not geo_data["results"]:
        return None

    lat = geo_data["results"][0]["latitude"]
    lon = geo_data["results"][0]["longitude"]

    # Get weather for coordinates
    weather_response = requests.get(
        "https://api.open-meteo.com/v1/forecast",
        params={"latitude": lat, "longitude": lon, "current_weather": True}
    )
    weather = weather_response.json()
    return weather["current_weather"]["temperature"]

cities = ["New York", "Los Angeles", "London"]
for city in cities:
    temp = get_city_temp(city)
    if temp:
        print(f"{city}: {temp}°C")
```

### Expected Output
```
New York: 5.2°C
Los Angeles: 18.5°C
London: 8.1°C
(actual values depend on current weather)
```

### Common Mistakes
- Hard-coding URL with query params instead of using `params` dictionary
- Not checking if results exist before accessing
- Wrong JSON key names (check API documentation)
- Not handling None return value
- Forgetting to pass `params` as dictionary

---

## Problem Set 2: Standard Library Modules

---

## Problem 4: Random Number Guessing Game

### Solution
```python
import random

secret = random.randint(1, 100)
attempts = 0

while True:
    guess = int(input("Guess a number (1-100): "))
    attempts += 1

    if guess == secret:
        print(f"Correct! It took {attempts} attempts.")
        break
    elif guess < secret:
        print("Too low!")
    else:
        print("Too high!")
```

### Expected Output
```
Guess a number (1-100): 50
Too high!
Guess a number (1-100): 25
Too low!
Guess a number (1-100): 37
Correct! It took 3 attempts.
```

### Common Mistakes
- Using `random.random()` instead of `random.randint()` (returns float 0-1)
- Range wrong: `randint(0, 101)` (includes 0 and 101)
- Not incrementing attempts
- Comparing string input without converting to int
- Not breaking from loop after correct guess

---

## Problem 5: Pythagorean Distance

### Solution
```python
import math

x1, y1 = 0, 0
x2, y2 = 3, 4

distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
print(f"Distance: {distance}")
```

### Expected Output
```
Distance: 5.0
```

### Common Mistakes
- Using `**0.5` instead of `math.sqrt()` (works but less clear)
- Wrong formula: `(x2-x1) + (y2-y1)` (should be squared)
- Not importing math module
- Using parentheses wrong: `math.sqrt((x2-x1)*(y2-y1))`

---

## Problem 6: Days Until Date

### Solution
```python
from datetime import date

def days_until(target_date):
    """Calculate days until target date."""
    if isinstance(target_date, str):
        target_date = date.fromisoformat(target_date)

    days = (target_date - date.today()).days
    return max(0, days)

print(days_until("2026-12-25"))  # Days until Christmas
```

### Expected Output
```
269
(or different number depending on current date)
```

### Common Mistakes
- Not handling string input (should convert)
- Using `datetime.now()` instead of `date.today()` (includes time)
- Not returning 0 for past dates (using `max()`)
- Wrong date format: "12-25-2026" instead of "2026-12-25"
- Not using `fromisoformat()`

---

## Problem 7: Collections Counter

### Solution
```python
from collections import Counter

word = "mississippi"
counter = Counter(word)
most_common = counter.most_common(3)

for letter, count in most_common:
    print(f"{letter}: {count}")
```

### Expected Output
```
s: 4
i: 4
p: 2
```

### Common Mistakes
- Not using Counter (manually counting is verbose)
- Using `counter[letter]` instead of `most_common()` (doesn't sort)
- Wrong argument: `most_common()` without argument (returns all)
- Not unpacking tuple: trying to use `most_common[0]` as dictionary

---

## Problem Set 3: NumPy & Data Processing

---

## Problem 8: NumPy Array Above Average

### Solution
```python
import numpy as np

data = np.random.randint(0, 101, 20)
avg = np.mean(data)
above_avg = data[data > avg]

print(f"Average: {avg:.1f}")
print(f"Above average: {above_avg}")
print(f"Count: {len(above_avg)}")
```

### Expected Output
```
Average: 52.3
Above average: [65 78 92 55 61]
Count: 5
```

### Common Mistakes
- Using Python list instead of NumPy array
- Using `data[data > avg]` on Python list (doesn't work)
- Not using `np.mean()` (manual sum/len works but less clear)
- Creating integers then converting (should use randint directly)

---

## Problem 9: NumPy Statistics

### Solution
```python
import numpy as np

scores = np.array([85, 92, 78, 95, 88, 76, 91, 84])

print(f"Mean: {np.mean(scores):.2f}")
print(f"Median: {np.median(scores):.2f}")
print(f"Std Dev: {np.std(scores):.2f}")
print(f"Min: {np.min(scores)}")
print(f"Max: {np.max(scores)}")
```

### Expected Output
```
Mean: 86.13
Median: 87.50
Std Dev: 6.37
Min: 76
Max: 95
```

### Common Mistakes
- Not importing numpy
- Using Python's `statistics` module instead (slow)
- Using `np.std(scores, ddof=1)` (sample vs population std dev)
- Not formatting to correct decimal places
- Using wrong function names

---

## Problem 10: NumPy Filtering and Sorting

### Solution
```python
import numpy as np

data = np.array([3, 7, 2, 9, 4, 1, 8, 5])
even = data[data % 2 == 0]
sorted_even = np.sort(even)

print(f"Even numbers: {even}")
print(f"Sorted even: {sorted_even}")
```

### Expected Output
```
Even numbers: [2 4 8]
Sorted even: [2 4 8]
```

### Common Mistakes
- Using `data[data % 2]` (returns odd numbers, 0 is falsy)
- Using `!= 0` instead of `== 0` for even
- Using `sorted(even)` (returns list, not array)
- Not using boolean indexing

---

## Problem Set 4: Matplotlib Visualization

---

## Problem 11: Line Chart of Perfect Squares

### Solution
```python
import matplotlib.pyplot as plt

x = list(range(1, 11))
y = [i**2 for i in x]

plt.figure(figsize=(10, 6))
plt.plot(x, y, marker='o', color='blue', linewidth=2)
plt.xlabel('Number')
plt.ylabel('Square')
plt.title('Perfect Squares')
plt.grid(True)
plt.show()
```

### Expected Output
```
(A line chart showing parabolic curve from (1,1) to (10,100))
```

### Common Mistakes
- Not calling `plt.show()` (chart won't display)
- Using `range(1, 11)` directly (not converting to list)
- Wrong y values: `[i*2 for i in x]` (should be `i**2`)
- Not using `marker='o'` (no points visible)
- Forgetting labels and title

---

## Problem 12: Bar Chart with Categories

### Solution
```python
import matplotlib.pyplot as plt

books = ['Book A', 'Book B', 'Book C', 'Book D', 'Book E']
ratings = [8, 9, 7, 9, 6]

plt.figure(figsize=(10, 6))
colors = ['gold' if r >= 8 else 'silver' for r in ratings]
plt.bar(books, ratings, color=colors)
plt.ylabel('Rating')
plt.title('Book Ratings')
plt.ylim(0, 10)
plt.show()
```

### Expected Output
```
(Bar chart with gold bars for 8+ ratings, silver for others)
```

### Common Mistakes
- Not setting ylim to show full scale (0-10)
- Not color-coding based on rating
- Using horizontal bars instead of vertical
- Not labeling axes
- Wrong colors or logic for conditional colors

---

## Problem 13: Subplots Visualization

### Solution
```python
import matplotlib.pyplot as plt
import numpy as np

data = [10, 20, 15, 25, 20]
labels = ['A', 'B', 'C', 'D', 'E']

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Line plot
axes[0, 0].plot(labels, data, marker='o')
axes[0, 0].set_title('Line Chart')

# Bar chart
axes[0, 1].bar(labels, data)
axes[0, 1].set_title('Bar Chart')

# Scatter plot
axes[1, 0].scatter(range(len(data)), data)
axes[1, 0].set_title('Scatter Plot')

# Histogram
axes[1, 1].hist(data, bins=5)
axes[1, 1].set_title('Histogram')

plt.tight_layout()
plt.show()
```

### Expected Output
```
(2x2 grid showing line, bar, scatter, and histogram)
```

### Common Mistakes
- Not using `subplots()` correctly (wrong syntax)
- Using `plt.subplot()` instead of `subplots()`
- Wrong indexing: `axes[0][0]` instead of `axes[0, 0]`
- Not calling `plt.tight_layout()` (overlapping labels)
- Not calling `show()`

---

## Problem Set 5: Integration & Projects

---

## Problem 14: Multi-API Integration

### Solution
```python
import requests

quote_response = requests.get("https://api.quotable.io/random")
quote = quote_response.json()

joke_response = requests.get("https://v2.jokeapi.dev/joke/Any")
joke = joke_response.json()

print("=" * 50)
print("DAILY INSPIRATION")
print("=" * 50)
print(f"\nQuote:\n{quote['content']}\n— {quote['author']}")
print(f"\nJoke:")
if joke["type"] == "single":
    print(joke["joke"])
else:
    print(f"{joke['setup']}\n{joke['delivery']}")
print("\n" + "=" * 50)
```

### Expected Output
```
==================================================
DAILY INSPIRATION
==================================================

Quote:
Innovation distinguishes between a leader and a follower.
— Steve Jobs

Joke:
Why don't scientists trust atoms? Because they make up everything!

==================================================
```

### Common Mistakes
- Not checking joke type before accessing setup/delivery
- Not handling API errors
- Wrong JSON field names
- Not formatting output nicely
- Using `f-string` without necessary escaping

---

## Problem 15: Complete Data Project

### Solution
```python
import requests
import numpy as np
import matplotlib.pyplot as plt

def fetch_weather(cities):
    """Fetch weather data for cities."""
    temps = {}
    for city in cities:
        try:
            geo = requests.get(
                "https://geocoding-api.open-meteo.com/v1/search",
                params={"name": city, "count": 1}
            ).json()

            if geo["results"]:
                lat = geo["results"][0]["latitude"]
                lon = geo["results"][0]["longitude"]

                weather = requests.get(
                    "https://api.open-meteo.com/v1/forecast",
                    params={"latitude": lat, "longitude": lon, "current_weather": True}
                ).json()

                temps[city] = weather["current_weather"]["temperature_2m"]
        except:
            pass

    return temps

# Fetch data
temps = fetch_weather(["New York", "Los Angeles", "Chicago"])
temps_arr = np.array(list(temps.values()))

# Create visualizations
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Bar chart of temperatures
ax1.bar(temps.keys(), temps.values(), color=['red' if t > 15 else 'blue' for t in temps.values()])
ax1.set_ylabel('Temperature (°C)')
ax1.set_title('City Temperatures')

# Statistics
stats = ['Min', 'Max', 'Avg']
values = [np.min(temps_arr), np.max(temps_arr), np.mean(temps_arr)]
ax2.bar(stats, values, color=['blue', 'red', 'green'])
ax2.set_ylabel('Temperature (°C)')
ax2.set_title('Temperature Statistics')

plt.tight_layout()
plt.show()
```

### Expected Output
```
(Two subplot chart: bar chart of cities and statistics)
```

### Common Mistakes
- Not handling API errors gracefully
- Not converting to NumPy array
- Wrong JSON field names
- Not extracting coordinates correctly
- Not formatting visualizations properly

---
