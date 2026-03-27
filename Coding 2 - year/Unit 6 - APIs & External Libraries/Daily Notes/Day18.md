# Day 18: Data Visualization Project – Part 1

**Learning Target:** I can plan and start building a data visualization project that integrates APIs, data processing, and charts.

---

## Key Concepts

**Project Workflow:**
1. **Fetch Data:** Get data from an API or file
2. **Process Data:** Clean, filter, and organize data
3. **Visualize Data:** Create meaningful charts
4. **Interpret:** Draw conclusions from visualizations

**Best Practices:**
- Choose meaningful data
- Use appropriate chart types
- Label axes clearly
- Include titles and legends
- Handle errors gracefully

---

## Project: Weather Analysis Dashboard

**Objective:** Fetch weather data and create visualizations showing temperature trends, comparisons, or patterns.

### Part 1: Planning and Setup

```python
import requests
import numpy as np
import matplotlib.pyplot as plt
from datetime import date, timedelta

# STEP 1: Identify your data source
# Option A: Fetch current weather for multiple cities
# Option B: Create historical temperature data
# Option C: Use API to get forecast data

# STEP 2: Define your visualizations
# - Temperature comparison bar chart
# - Weather conditions pie chart
# - Temperature trend line chart

# STEP 3: Set up basic structure

def fetch_weather_data(cities):
    """Fetch weather data for multiple cities"""
    data = {}
    for city in cities:
        # Using geocoding + Open-Meteo
        geo_response = requests.get(
            "https://geocoding-api.open-meteo.com/v1/search",
            params={"name": city, "count": 1}
        )
        geo_data = geo_response.json()
        
        if geo_data["results"]:
            lat = geo_data["results"][0]["latitude"]
            lon = geo_data["results"][0]["longitude"]
            
            weather_response = requests.get(
                "https://api.open-meteo.com/v1/forecast",
                params={
                    "latitude": lat,
                    "longitude": lon,
                    "current_weather": True
                }
            )
            weather = weather_response.json()
            data[city] = weather["current_weather"]["temperature"]
    
    return data

def process_weather_data(raw_data):
    """Convert raw data into format for visualization"""
    cities = list(raw_data.keys())
    temperatures = list(raw_data.values())
    return cities, temperatures

def visualize_weather_data(cities, temperatures):
    """Create visualizations"""
    plt.figure(figsize=(10, 6))
    plt.bar(cities, temperatures, color='skyblue')
    plt.ylabel('Temperature (°C)')
    plt.title('Current Temperature by City')
    plt.show()

# MAIN EXECUTION
cities = ["New York", "Los Angeles", "Chicago", "London", "Tokyo"]
weather_data = fetch_weather_data(cities)
cities_list, temps = process_weather_data(weather_data)
visualize_weather_data(cities_list, temps)
```

---

## Guided Practice

1. **Plan Your Project:** Choose a data source (API or file) and define 2-3 visualizations.

2. **Set Up Structure:** Create functions for fetching, processing, and visualizing data.

3. **Test Components:** Verify each function works independently.

4. **Document:** Add comments explaining each section.

---

## Practice Problems

**Beginner:** Create a program that fetches data for 3 cities and displays a bar chart.

**Intermediate:** Create a dashboard with multiple visualizations (2+ charts) from a single data source.

**Challenge:** Create a system that fetches data, processes it with filters, and displays multiple related visualizations.

<details>
<summary>💡 Hints</summary>
- Start with a simple data source (1-2 cities, basic weather)
- Use function modularization
- Test each function separately
- Handle errors when APIs fail
- Use meaningful variable names
- Add comments for clarity
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests
import matplotlib.pyplot as plt

def get_city_temps(cities):
    temps = {}
    for city in cities:
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
    
    return temps

temps = get_city_temps(["New York", "Los Angeles", "Chicago"])
plt.bar(temps.keys(), temps.values())
plt.ylabel("Temperature (°C)")
plt.show()
```

**Intermediate/Challenge:**
```python
# Create multiple visualizations with subplots
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Chart 1: Temperature comparison
axes[0].bar(cities, temps, color='skyblue')
axes[0].set_title('Temperature by City')

# Chart 2: Statistics
stats = [min(temps.values()), max(temps.values()), np.mean(list(temps.values()))]
axes[1].bar(['Min', 'Max', 'Avg'], stats, color=['blue', 'red', 'green'])
axes[1].set_title('Temperature Statistics')

plt.tight_layout()
plt.show()
```
</details>
