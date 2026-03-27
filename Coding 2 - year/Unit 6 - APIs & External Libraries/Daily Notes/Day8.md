# Day 8: Weather & Data APIs Integration

**Learning Target:** I can build a practical application by integrating multiple APIs.

---

## Key Concepts

**Multi-API Applications:** Real-world apps often combine data from multiple sources:
- Get location from one API
- Get weather from another API
- Display results using a third library

**Popular Free/Freemium APIs:**
- **Open-Meteo** (weather, no key) — `/forecast`
- **OpenWeatherMap** (weather, free tier) — requires key
- **IP API** (location from IP) — `/json`
- **Geolocation** — convert city names to lat/lon

**Workflow:**
1. Make first request (e.g., get latitude/longitude from city name)
2. Extract data from response
3. Use that data in second request
4. Display results

---

## Code Examples

```python
import requests

# Example: Get weather for any city using Open-Meteo

def get_coordinates(city):
    """Get latitude and longitude for a city"""
    response = requests.get(
        "https://geocoding-api.open-meteo.com/v1/search",
        params={"name": city, "count": 1}
    )
    data = response.json()
    if data["results"]:
        result = data["results"][0]
        return result["latitude"], result["longitude"]
    return None, None

def get_weather(lat, lon):
    """Get current weather for coordinates"""
    params = {
        "latitude": lat,
        "longitude": lon,
        "current_weather": True
    }
    response = requests.get("https://api.open-meteo.com/v1/forecast", params=params)
    return response.json()

# Usage
city = "New York"
lat, lon = get_coordinates(city)
if lat and lon:
    weather = get_weather(lat, lon)
    temp = weather["current_weather"]["temperature"]
    wind = weather["current_weather"]["windspeed"]
    print(f"Weather for {city}:")
    print(f"Temperature: {temp}°C")
    print(f"Wind Speed: {wind} km/h")
```

---

## Guided Practice

1. **Build a Weather App:** Use the code above to create a program that accepts a city name and displays the weather.

2. **Error Handling:** Add try-except blocks to handle cases where a city is not found.

3. **Format Output:** Create a nicely formatted weather report with all relevant information.

4. **Multiple Cities:** Extend your program to get weather for 3 different cities in a loop.

---

## Practice Problems

**Beginner:** Write a function that takes a city name and returns the current temperature using Open-Meteo.

**Intermediate:** Create a program that gets weather for a city and determines if it's "hot" (>25°C), "warm" (15-25°C), or "cold" (<15°C).

**Challenge:** Build a weather comparison tool that gets weather for multiple cities and displays them in a table format.

<details>
<summary>💡 Hints</summary>
- Use the geocoding API to convert city names to coordinates
- Open-Meteo has a `/search` endpoint for cities and `/forecast` for weather
- Check that `response.json()["results"]` is not empty before accessing items
- Use f-strings for formatted output
- Consider using a loop for multiple cities
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

def get_temperature(city):
    # Get coordinates
    geo_response = requests.get(
        "https://geocoding-api.open-meteo.com/v1/search",
        params={"name": city, "count": 1}
    )
    geo_data = geo_response.json()
    
    if not geo_data["results"]:
        return None
    
    lat = geo_data["results"][0]["latitude"]
    lon = geo_data["results"][0]["longitude"]
    
    # Get weather
    weather_response = requests.get(
        "https://api.open-meteo.com/v1/forecast",
        params={"latitude": lat, "longitude": lon, "current_weather": True}
    )
    weather_data = weather_response.json()
    return weather_data["current_weather"]["temperature"]

print(get_temperature("New York"))
```

**Intermediate:**
```python
import requests

def describe_weather(city):
    # (same coordinate fetching as above)
    temp = get_temperature(city)
    
    if temp > 25:
        description = "hot"
    elif temp >= 15:
        description = "warm"
    else:
        description = "cold"
    
    return f"{city}: {temp}°C ({description})"

print(describe_weather("New York"))
```

**Challenge:**
```python
import requests

def get_weather_for_cities(cities):
    results = []
    for city in cities:
        # (same fetching logic)
        temp = get_temperature(city)
        results.append(f"{city:15} {temp:6.1f}°C")
    
    print("City            Temperature")
    print("-" * 30)
    for result in results:
        print(result)

get_weather_for_cities(["New York", "Los Angeles", "Chicago"])
```
</details>
