# Day 20: Data Visualization Project – Polish & Presentations

**Learning Target:** I can refine, document, and present a complete data visualization project.

---

## Key Concepts

**Project Polish:**
- Code documentation and comments
- Error handling and edge cases
- Performance optimization
- User-friendly output
- Presentation quality

**Professional Touches:**
- Clear variable names
- Docstrings for functions
- Meaningful colors and styles
- Readable font sizes
- Consistent formatting

---

## Polished Project Template

```python
"""
Weather Data Visualization Project
==================================
Fetches current weather data for multiple cities and creates
a comprehensive dashboard with multiple visualizations.

Author: [Student Name]
Date: 2026-03-25
"""

import requests
import numpy as np
import matplotlib.pyplot as plt
from datetime import date
from typing import List, Dict, Optional

class WeatherDashboard:
    """Manages weather data fetching and visualization"""
    
    def __init__(self, timeout: int = 5):
        """Initialize the dashboard"""
        self.timeout = timeout
        self.data = []
    
    def fetch_city_weather(self, city: str) -> Optional[Dict]:
        """
        Fetch weather data for a single city.
        
        Args:
            city (str): City name
            
        Returns:
            dict: Weather data or None if error
        """
        try:
            # Get coordinates
            geo_response = requests.get(
                "https://geocoding-api.open-meteo.com/v1/search",
                params={"name": city, "count": 1},
                timeout=self.timeout
            )
            geo_data = geo_response.json()
            
            if not geo_data.get("results"):
                print(f"❌ City not found: {city}")
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
                timeout=self.timeout
            )
            weather = weather_response.json()["current_weather"]
            
            return {
                "city": city,
                "temperature": weather["temperature"],
                "windspeed": weather["windspeed"],
                "latitude": lat,
                "longitude": lon
            }
        
        except requests.exceptions.Timeout:
            print(f"⏱️  Timeout fetching data for {city}")
            return None
        except requests.exceptions.RequestException as e:
            print(f"⚠️  Error fetching {city}: {e}")
            return None
    
    def fetch_all(self, cities: List[str]) -> List[Dict]:
        """Fetch data for multiple cities"""
        print(f"Fetching data for {len(cities)} cities...")
        self.data = []
        for city in cities:
            result = self.fetch_city_weather(city)
            if result:
                self.data.append(result)
                print(f"✓ {city}: {result['temperature']}°C")
        print(f"\n✅ Successfully fetched {len(self.data)} cities\n")
        return self.data
    
    def create_dashboard(self) -> None:
        """Create a professional weather dashboard"""
        
        if not self.data:
            print("No data available for visualization")
            return
        
        cities = [d["city"] for d in self.data]
        temps = [d["temperature"] for d in self.data]
        winds = [d["windspeed"] for d in self.data]
        
        # Create professional styling
        plt.style.use('default')
        fig = plt.figure(figsize=(16, 10))
        fig.suptitle(
            f"Global Weather Dashboard — {date.today()}",
            fontsize=18,
            fontweight='bold',
            y=0.98
        )
        
        # Create gridspec for flexible layout
        gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)
        
        # 1. Main: Temperature bar chart (2x2)
        ax1 = fig.add_subplot(gs[0:2, 0:2])
        colors = ['red' if t > 20 else 'blue' for t in temps]
        ax1.bar(cities, temps, color=colors, alpha=0.7, edgecolor='black', linewidth=1.5)
        ax1.set_ylabel('Temperature (°C)', fontsize=12, fontweight='bold')
        ax1.set_title('Temperature by City', fontsize=13, fontweight='bold')
        ax1.grid(axis='y', alpha=0.3, linestyle='--')
        ax1.axhline(y=0, color='k', linestyle='-', linewidth=0.5)
        
        # 2. Wind speed (1x1)
        ax2 = fig.add_subplot(gs[0, 2])
        ax2.bar(cities, winds, color='lightblue', alpha=0.7, edgecolor='black')
        ax2.set_ylabel('Wind (km/h)', fontsize=10, fontweight='bold')
        ax2.set_title('Wind Speed', fontsize=11, fontweight='bold')
        ax2.tick_params(axis='x', rotation=45)
        
        # 3. Statistics (1x1)
        ax3 = fig.add_subplot(gs[1, 2])
        stats = [min(temps), max(temps), np.mean(temps)]
        ax3.bar(['Min', 'Max', 'Avg'], stats, color=['#3498db', '#e74c3c', '#2ecc71'], alpha=0.7)
        ax3.set_ylabel('°C', fontsize=10, fontweight='bold')
        ax3.set_title('Temperature Stats', fontsize=11, fontweight='bold')
        ax3.grid(axis='y', alpha=0.3)
        
        # 4. Summary text box (1x3)
        ax4 = fig.add_subplot(gs[2, :])
        ax4.axis('off')
        
        warmest_city = max(zip(cities, temps), key=lambda x: x[1])
        coldest_city = min(zip(cities, temps), key=lambda x: x[1])
        windiest_city = max(zip(cities, winds), key=lambda x: x[1])
        
        summary = f"""
        SUMMARY STATISTICS
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        Warmest City: {warmest_city[0]:20s} {warmest_city[1]:6.1f}°C    |    Coldest City: {coldest_city[0]:15s} {coldest_city[1]:6.1f}°C    |    Average: {np.mean(temps):6.1f}°C
        
        Windiest City: {windiest_city[0]:18s} {windiest_city[1]:6.1f} km/h    |    Cities Analyzed: {len(cities):2d}    |    Data Retrieved: {date.today()}
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        """
        ax4.text(0.05, 0.5, summary, fontsize=10, family='monospace',
                verticalalignment='center', bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.3))
        
        plt.savefig('weather_dashboard.png', dpi=300, bbox_inches='tight')
        print("💾 Dashboard saved as 'weather_dashboard.png'")
        plt.show()

# MAIN EXECUTION
if __name__ == "__main__":
    # Create dashboard instance
    dashboard = WeatherDashboard(timeout=5)
    
    # Define cities to analyze
    cities = [
        "New York", "Los Angeles", "Chicago",
        "London", "Paris", "Tokyo",
        "Sydney", "Toronto", "Dubai"
    ]
    
    # Fetch and visualize
    dashboard.fetch_all(cities)
    dashboard.create_dashboard()
    
    print("Project complete! ✨")
```

---

## Guided Practice

1. **Add Docstrings:** Document each function with purpose, parameters, and returns.

2. **Improve Styling:** Use colors, fonts, and formatting for professional appearance.

3. **Add Error Messages:** Include helpful feedback for users.

4. **Save Output:** Export dashboard as a high-quality PNG file.

---

## Practice Problems

**Beginner:** Add docstrings to all your functions.

**Intermediate:** Create a professional dashboard with styled text summary.

**Challenge:** Package your project into a reusable class with methods for fetching, processing, and visualizing.

<details>
<summary>💡 Hints</summary>
- Use docstrings with Args, Returns, and description
- Use `plt.savefig()` with high DPI for quality
- Use `gridspec` for flexible subplot layouts
- Add colors based on conditions (e.g., red for hot, blue for cold)
- Use professional fonts and sizes
- Add summary statistics clearly
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
def fetch_city_weather(city):
    """
    Fetch current weather data for a city.
    
    Args:
        city (str): Name of the city
        
    Returns:
        dict: Weather data (temperature, wind speed, coordinates)
              or None if error
    """
    # function body...
```

**Intermediate/Challenge:** See full example above.
</details>
