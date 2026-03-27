# Day 19: Data Visualization Project – Part 2

**Learning Target:** I can complete a data visualization project with multiple charts, error handling, and polished output.

---

## Key Concepts

**Project Completion Checklist:**
- Data fetching (with error handling)
- Data processing and cleaning
- Multiple visualizations
- Clear labels and titles
- Responsive error messages
- Well-organized code

**Enhancement Ideas:**
- Add more API calls
- Create more chart types
- Add user interaction
- Display statistics
- Save output to file

---

## Extended Project Example

```python
import requests
import numpy as np
import matplotlib.pyplot as plt
from datetime import date

# COMPLETE WEATHER VISUALIZATION PROJECT

def fetch_city_weather(city):
    """Fetch weather data for a single city with error handling"""
    try:
        # Get coordinates
        geo_response = requests.get(
            "https://geocoding-api.open-meteo.com/v1/search",
            params={"name": city, "count": 1},
            timeout=5
        )
        geo_data = geo_response.json()
        
        if not geo_data["results"]:
            print(f"Warning: City '{city}' not found")
            return None
        
        lat = geo_data["results"][0]["latitude"]
        lon = geo_data["results"][0]["longitude"]
        
        # Get weather
        weather_response = requests.get(
            "https://api.open-meteo.com/v1/forecast",
            params={
                "latitude": lat,
                "longitude": lon,
                "current_weather": True
            },
            timeout=5
        )
        weather_data = weather_response.json()
        
        return {
            "city": city,
            "temperature": weather_data["current_weather"]["temperature"],
            "windspeed": weather_data["current_weather"]["windspeed"],
            "latitude": lat,
            "longitude": lon
        }
    
    except requests.exceptions.RequestException as e:
        print(f"Error fetching data for {city}: {e}")
        return None

def fetch_multiple_cities(cities):
    """Fetch data for multiple cities"""
    data = []
    for city in cities:
        result = fetch_city_weather(city)
        if result:
            data.append(result)
    return data

def create_dashboard(weather_data):
    """Create a comprehensive weather dashboard"""
    
    if not weather_data:
        print("No data to visualize")
        return
    
    cities = [d["city"] for d in weather_data]
    temps = [d["temperature"] for d in weather_data]
    winds = [d["windspeed"] for d in weather_data]
    
    # Create 2x2 subplot dashboard
    fig, axes = plt.subplots(2, 2, figsize=(14, 10))
    fig.suptitle(f"Weather Dashboard - {date.today()}", fontsize=16, fontweight='bold')
    
    # 1. Temperature comparison
    axes[0, 0].bar(cities, temps, color='coral', edgecolor='black')
    axes[0, 0].set_ylabel('Temperature (°C)')
    axes[0, 0].set_title('Temperature by City')
    axes[0, 0].grid(axis='y', alpha=0.3)
    
    # 2. Wind speed comparison
    axes[0, 1].bar(cities, winds, color='lightblue', edgecolor='black')
    axes[0, 1].set_ylabel('Wind Speed (km/h)')
    axes[0, 1].set_title('Wind Speed by City')
    axes[0, 1].grid(axis='y', alpha=0.3)
    
    # 3. Temperature statistics
    stats_labels = ['Min', 'Max', 'Avg']
    stats_values = [min(temps), max(temps), np.mean(temps)]
    axes[1, 0].bar(stats_labels, stats_values, color=['blue', 'red', 'green'], alpha=0.7)
    axes[1, 0].set_ylabel('Temperature (°C)')
    axes[1, 0].set_title('Temperature Statistics')
    axes[1, 0].grid(axis='y', alpha=0.3)
    
    # 4. Summary text
    axes[1, 1].axis('off')
    summary_text = f"""
    WEATHER SUMMARY
    ================
    
    Warmest: {max(zip(cities, temps), key=lambda x: x[1])[0]} ({max(temps)}°C)
    Coldest: {min(zip(cities, temps), key=lambda x: x[1])[0]} ({min(temps)}°C)
    
    Windiest: {max(zip(cities, winds), key=lambda x: x[1])[0]} ({max(winds)} km/h)
    Calmest: {min(zip(cities, winds), key=lambda x: x[1])[0]} ({min(winds)} km/h)
    
    Cities Analyzed: {len(cities)}
    Average Temp: {np.mean(temps):.1f}°C
    """
    axes[1, 1].text(0.1, 0.5, summary_text, fontsize=11, family='monospace',
                    verticalalignment='center')
    
    plt.tight_layout()
    plt.show()

# MAIN PROGRAM
if __name__ == "__main__":
    cities_to_check = ["New York", "Los Angeles", "Chicago", "Paris", "Tokyo"]
    
    print("Fetching weather data...")
    weather_data = fetch_multiple_cities(cities_to_check)
    
    print(f"Successfully fetched data for {len(weather_data)} cities")
    
    print("Creating dashboard...")
    create_dashboard(weather_data)
```

---

## Guided Practice

1. **Enhance Data:** Add more data points or different APIs.

2. **Add Statistics:** Calculate and display min, max, average.

3. **Create Dashboard:** Combine multiple visualizations in subplots.

4. **Polish Output:** Add titles, legends, formatting, and colors.

---

## Practice Problems

**Beginner:** Add summary statistics to your visualization (min, max, average).

**Intermediate:** Create a multi-subplot dashboard (2x2) with different visualizations.

**Challenge:** Add user input to choose cities and customize the dashboard display.

<details>
<summary>💡 Hints</summary>
- Use `np.min()`, `np.max()`, `np.mean()` for statistics
- Use `plt.subplots(rows, cols)` for dashboards
- Add `tight_layout()` to prevent overlapping
- Use `suptitle()` for overall title
- Test with try-except blocks
- Save your work with `plt.savefig()`
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
# Add to your visualization function
temps = [d["temperature"] for d in weather_data]
stats = {
    "Min": min(temps),
    "Max": max(temps),
    "Avg": sum(temps) / len(temps)
}

print("Temperature Statistics:")
for stat, value in stats.items():
    print(f"  {stat}: {value:.1f}°C")
```

**Intermediate:** (See full example above)

**Challenge:**
```python
# Add user input
cities = input("Enter cities (comma-separated): ").split(",")
cities = [c.strip() for c in cities]

data = fetch_multiple_cities(cities)
create_dashboard(data)

# Save output
plt.savefig("weather_dashboard.png", dpi=300, bbox_inches='tight')
```
</details>
