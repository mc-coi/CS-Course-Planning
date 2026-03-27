# Day 5: Using Public APIs – Weather & More

**Learning Target:** I can use multiple public APIs to build practical applications.

---

## Key Concepts

**Free Public APIs (No Key Required):**
- **Quotable** (`api.quotable.io`) — Random quotes
- **PokeAPI** (`pokeapi.co`) — Pokemon data
- **Open-Meteo** (`api.open-meteo.com`) — Weather data (no key!)
- **Cat Facts** (`catfact.ninja`) — Random cat facts
- **Joke API** (`v2.jokeapi.dev`) — Jokes in multiple categories

**Query Parameters:** URLs can include parameters to filter or customize responses.

```
https://api.open-meteo.com/v1/forecast?latitude=40.7128&longitude=-74.0060&current_weather=true
```

In Python:
```python
params = {
    "latitude": 40.7128,
    "longitude": -74.0060,
    "current_weather": True
}
response = requests.get("https://api.open-meteo.com/v1/forecast", params=params)
```

---

## Code Examples

```python
import requests

# Example 1: Get current weather for a location (Open-Meteo)
params = {
    "latitude": 40.7128,      # New York latitude
    "longitude": -74.0060,    # New York longitude
    "current_weather": True
}
response = requests.get("https://api.open-meteo.com/v1/forecast", params=params)
weather = response.json()
print(f"Temperature: {weather['current_weather']['temperature']}°")
print(f"Wind Speed: {weather['current_weather']['windspeed']} km/h")

# Example 2: Get a random dog breed (Dog API)
response = requests.get("https://dog.ceo/api/breeds/image/random")
dog_data = response.json()
print(dog_data["message"])  # URL of random dog image

# Example 3: Multiple requests in a loop
for i in range(3):
    response = requests.get("https://api.quotable.io/random")
    quote = response.json()
    print(f"{i+1}. {quote['content']}")
```

---

## Guided Practice

1. **Weather App:** Write code that gets the current weather for your city using Open-Meteo. Print temperature, wind speed, and weather code.

2. **Quote Loop:** Create a program that fetches and prints 5 random quotes from Quotable.

3. **Parameter Practice:** Request Pokemon data for multiple Pokemon names and display their types and heights.

4. **Error Check:** Add a status code check to one of your programs. If it fails, print an error message.

---

## Practice Problems

**Beginner:** Write a program that fetches a random cat fact and prints it in uppercase.

**Intermediate:** Create a function that takes a city name and latitude/longitude, then returns the current temperature from Open-Meteo.

**Challenge:** Build a "Daily Quote Generator" that fetches a quote and saves it to a text file with the current date.

<details>
<summary>💡 Hints</summary>
- For Open-Meteo, you need latitude and longitude (Google them for your city)
- Use `params={}` to pass query parameters to `requests.get()`
- Open-Meteo returns weather in a nested structure: `data['current_weather']['temperature']`
- For file writing, use `open()` and `.write()`
- Use `.upper()` for uppercase strings
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

response = requests.get("https://catfact.ninja/fact")
fact = response.json()
print(fact["fact"].upper())
```

**Intermediate:**
```python
import requests

def get_temperature(lat, lon):
    params = {
        "latitude": lat,
        "longitude": lon,
        "current_weather": True
    }
    response = requests.get("https://api.open-meteo.com/v1/forecast", params=params)
    weather = response.json()
    return weather["current_weather"]["temperature"]

# New York coordinates
temp = get_temperature(40.7128, -74.0060)
print(f"Temperature: {temp}°C")
```

**Challenge:**
```python
import requests
from datetime import date

response = requests.get("https://api.quotable.io/random")
quote = response.json()

with open("daily_quotes.txt", "a") as file:
    file.write(f"{date.today()}: {quote['content']}\n")
    file.write(f"— {quote['author']}\n\n")

print("Quote saved!")
```
</details>
