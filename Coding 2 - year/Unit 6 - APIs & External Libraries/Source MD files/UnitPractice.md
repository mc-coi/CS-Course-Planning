# Unit 6 Practice Problems

15 comprehensive practice problems covering all Unit 6 topics.

---

## Problem Set 1: APIs & requests Library

### Problem 1: Fetch and Parse
Fetch a random quote from `https://api.quotable.io/random` and print it in the format: `"[quote]" — [author]`

<details>
<summary>Solution</summary>

```python
import requests

response = requests.get("https://api.quotable.io/random")
quote = response.json()
print(f'"{quote["content"]}" — {quote["author"]}')
```
</details>

---

### Problem 2: Error Handling
Write a function that takes a Pokemon name and returns its height. Handle cases where the Pokemon doesn't exist.

<details>
<summary>Solution</summary>

```python
import requests

def get_pokemon_height(name):
    try:
        response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{name.lower()}")
        if response.status_code == 404:
            return "Pokemon not found"
        pokemon = response.json()
        return pokemon["height"]
    except Exception as e:
        return f"Error: {e}"

print(get_pokemon_height("pikachu"))
print(get_pokemon_height("invalidpokemon"))
```
</details>

---

### Problem 3: Query Parameters
Fetch weather data for 3 different cities using the Open-Meteo API and compare temperatures.

<details>
<summary>Solution</summary>

```python
import requests

def get_city_temp(city):
    geo_response = requests.get(
        "https://geocoding-api.open-meteo.com/v1/search",
        params={"name": city, "count": 1}
    )
    geo_data = geo_response.json()
    
    if not geo_data["results"]:
        return None
    
    lat = geo_data["results"][0]["latitude"]
    lon = geo_data["results"][0]["longitude"]
    
    weather_response = requests.get(
        "https://api.open-meteo.com/v1/forecast",
        params={"latitude": lat, "longitude": lon, "current_weather": True}
    )
    weather = weather_response.json()
    return weather["current_weather"]["temperature"]

cities = ["New York", "Los Angeles", "London"]
for city in cities:
    temp = get_city_temp(city)
    print(f"{city}: {temp}°C")
```
</details>

---

## Problem Set 2: Standard Library Modules

### Problem 4: random Module
Create a simple guessing game that picks a random number 1-100 and lets the user guess.

<details>
<summary>Solution</summary>

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
</details>

---

### Problem 5: math Module
Calculate the distance between two points (x1, y1) and (x2, y2) using the Pythagorean theorem.

<details>
<summary>Solution</summary>

```python
import math

x1, y1 = 0, 0
x2, y2 = 3, 4

distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
print(f"Distance: {distance}")
```
</details>

---

### Problem 6: datetime Module
Write a function that calculates how many days until a given date.

<details>
<summary>Solution</summary>

```python
from datetime import date

def days_until(target_date):
    """target_date should be a date object or string 'YYYY-MM-DD'"""
    if isinstance(target_date, str):
        target_date = date.fromisoformat(target_date)
    
    days = (target_date - date.today()).days
    return max(0, days)

print(days_until("2026-12-25"))
```
</details>

---

### Problem 7: collections Counter
Find the 3 most common letters in a word.

<details>
<summary>Solution</summary>

```python
from collections import Counter

word = "mississippi"
counter = Counter(word)
most_common = counter.most_common(3)

for letter, count in most_common:
    print(f"{letter}: {count}")
```
</details>

---

## Problem Set 3: NumPy & Data Processing

### Problem 8: NumPy Array Operations
Create an array of 20 random numbers (0-100) and find which ones are above the average.

<details>
<summary>Solution</summary>

```python
import numpy as np

data = np.random.randint(0, 101, 20)
avg = np.mean(data)
above_avg = data[data > avg]

print(f"Average: {avg:.1f}")
print(f"Above average: {above_avg}")
print(f"Count: {len(above_avg)}")
```
</details>

---

### Problem 9: NumPy Statistics
Given a list of test scores, use NumPy to calculate mean, median, and standard deviation.

<details>
<summary>Solution</summary>

```python
import numpy as np

scores = np.array([85, 92, 78, 95, 88, 76, 91, 84])

print(f"Mean: {np.mean(scores):.2f}")
print(f"Median: {np.median(scores):.2f}")
print(f"Std Dev: {np.std(scores):.2f}")
print(f"Min: {np.min(scores)}")
print(f"Max: {np.max(scores)}")
```
</details>

---

### Problem 10: NumPy Filtering & Sorting
Create an array of numbers, filter it for even values, and sort the result.

<details>
<summary>Solution</summary>

```python
import numpy as np

data = np.array([3, 7, 2, 9, 4, 1, 8, 5])
even = data[data % 2 == 0]
sorted_even = np.sort(even)

print(even)
print(sorted_even)
```
</details>

---

## Problem Set 4: Matplotlib Visualization

### Problem 11: Line Chart
Create a line chart showing the first 10 perfect squares (1², 2², 3², ..., 10²).

<details>
<summary>Solution</summary>

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
</details>

---

### Problem 12: Bar Chart with Categories
Create a bar chart comparing your 5 favorite books and their ratings (1-10).

<details>
<summary>Solution</summary>

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
</details>

---

### Problem 13: Subplots Visualization
Create a 2x2 subplot showing different types of charts with the same data.

<details>
<summary>Solution</summary>

```python
import matplotlib.pyplot as plt
import numpy as np

data = [10, 20, 15, 25, 20]
labels = ['A', 'B', 'C', 'D', 'E']

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Line
axes[0, 0].plot(labels, data, marker='o')
axes[0, 0].set_title('Line Chart')

# Bar
axes[0, 1].bar(labels, data)
axes[0, 1].set_title('Bar Chart')

# Scatter
axes[1, 0].scatter(range(len(data)), data)
axes[1, 0].set_title('Scatter Plot')

# Histogram
axes[1, 1].hist(data, bins=5)
axes[1, 1].set_title('Histogram')

plt.tight_layout()
plt.show()
```
</details>

---

## Problem Set 5: Integration & Projects

### Problem 14: Multi-API Integration
Fetch a random quote and a random joke, then display them side by side.

<details>
<summary>Solution</summary>

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
</details>

---

### Problem 15: Complete Data Project
Fetch weather for 3 cities, analyze the data with NumPy, and create 2 visualizations.

<details>
<summary>Solution</summary>

```python
import requests
import numpy as np
import matplotlib.pyplot as plt

def fetch_weather(cities):
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
                
                temps[city] = weather["current_weather"]["temperature"]
        except:
            pass
    
    return temps

# Fetch data
temps = fetch_weather(["New York", "Los Angeles", "Chicago"])
temps_arr = np.array(list(temps.values()))

# Create visualizations
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Bar chart
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
</details>

---

## Answer Summary

| Problem | Topic | Key Concepts |
|---------|-------|--------------|
| 1-3 | APIs | requests, JSON, error handling |
| 4-7 | Stdlib | random, math, datetime, collections |
| 8-10 | NumPy | arrays, filtering, statistics |
| 11-13 | Matplotlib | plots, charts, subplots |
| 14-15 | Integration | Multi-API, data visualization |

