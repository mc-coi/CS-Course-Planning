# Day 21: Project Completion & Review

**Learning Target:** I can review, test, and finalize my data visualization project.

---

## Key Concepts

**Final Checklist:**
- ✓ All functions work correctly
- ✓ Error handling in place
- ✓ Code is well-commented
- ✓ Visualizations are clear and labeled
- ✓ Project follows best practices
- ✓ Output is saved

**Testing Strategy:**
- Test with different inputs
- Verify error handling
- Check edge cases
- Validate output quality

---

## Project Review Template

```python
"""
PROJECT REVIEW CHECKLIST
========================

PROJECT: Weather Data Visualization Dashboard
STUDENT: [Your Name]
DATE: 2026-03-25

FEATURES IMPLEMENTED
====================
✓ Fetch weather data from Open-Meteo API
✓ Error handling for network issues
✓ Support for multiple cities
✓ Temperature comparison chart
✓ Wind speed visualization
✓ Statistical analysis (min, max, avg)
✓ Professional dashboard layout
✓ Save output as high-quality PNG
✓ User-friendly status messages
✓ Comprehensive documentation

CODE QUALITY
============
✓ Proper function decomposition
✓ Docstrings for all functions
✓ Meaningful variable names
✓ Consistent formatting
✓ Try-except blocks for error handling
✓ Type hints included

VISUALIZATION QUALITY
=====================
✓ Clear titles and axis labels
✓ Color scheme is meaningful
✓ Multiple chart types used
✓ Statistics displayed clearly
✓ Professional appearance

TESTING RESULTS
===============
✓ Tested with 5+ cities
✓ Verified error handling (non-existent city)
✓ Checked timeout handling
✓ Validated dashboard generation
✓ Tested file saving

AREAS FOR ENHANCEMENT (Future)
==============================
- Add 7-day forecast visualization
- Include humidity and precipitation data
- Create interactive plots with Plotly
- Add city location map visualization
- Store data in CSV for historical tracking

"""

# FINAL PROJECT CODE
import requests
import numpy as np
import matplotlib.pyplot as plt
from datetime import date
from typing import List, Dict, Optional

class WeatherDashboard:
    """
    A professional weather visualization system.
    
    This class handles fetching weather data from the Open-Meteo API
    and creating visualizations for weather analysis.
    """
    
    def __init__(self, timeout: int = 5, verbose: bool = True):
        """
        Initialize the WeatherDashboard.
        
        Args:
            timeout: Request timeout in seconds
            verbose: Print status messages
        """
        self.timeout = timeout
        self.verbose = verbose
        self.data = []
    
    def fetch_city_weather(self, city: str) -> Optional[Dict]:
        """Fetch weather for one city with full error handling"""
        try:
            if self.verbose:
                print(f"Fetching: {city}...", end=" ")
            
            # Geocoding request
            geo_resp = requests.get(
                "https://geocoding-api.open-meteo.com/v1/search",
                params={"name": city, "count": 1},
                timeout=self.timeout
            )
            geo_data = geo_resp.json()
            
            if not geo_data.get("results"):
                if self.verbose:
                    print("❌ Not found")
                return None
            
            lat = geo_data["results"][0]["latitude"]
            lon = geo_data["results"][0]["longitude"]
            
            # Weather request
            weather_resp = requests.get(
                "https://api.open-meteo.com/v1/forecast",
                params={
                    "latitude": lat,
                    "longitude": lon,
                    "current_weather": True
                },
                timeout=self.timeout
            )
            weather = weather_resp.json()["current_weather"]
            
            if self.verbose:
                print(f"✓ {weather['temperature']}°C")
            
            return {
                "city": city,
                "temperature": weather["temperature"],
                "windspeed": weather["windspeed"],
                "latitude": lat,
                "longitude": lon
            }
        
        except requests.exceptions.Timeout:
            if self.verbose:
                print("⏱️ Timeout")
            return None
        except Exception as e:
            if self.verbose:
                print(f"⚠️ Error: {e}")
            return None
    
    def fetch_all(self, cities: List[str]) -> bool:
        """Fetch weather for all cities"""
        if self.verbose:
            print(f"\n{'='*50}\nFetching weather data for {len(cities)} cities\n{'='*50}\n")
        
        self.data = []
        for city in cities:
            result = self.fetch_city_weather(city)
            if result:
                self.data.append(result)
        
        if self.verbose:
            print(f"\n{'='*50}\n✅ Success: {len(self.data)}/{len(cities)} cities\n{'='*50}\n")
        
        return len(self.data) > 0
    
    def create_dashboard(self, filename: str = "weather_dashboard.png") -> bool:
        """Create and save the dashboard"""
        if not self.data:
            if self.verbose:
                print("❌ No data to visualize")
            return False
        
        cities = [d["city"] for d in self.data]
        temps = [d["temperature"] for d in self.data]
        winds = [d["windspeed"] for d in self.data]
        
        # Create figure
        fig = plt.figure(figsize=(16, 10))
        fig.suptitle(
            f"Global Weather Dashboard — {date.today()}",
            fontsize=18,
            fontweight='bold'
        )
        
        gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)
        
        # Temperature chart
        ax1 = fig.add_subplot(gs[0:2, 0:2])
        colors = ['#e74c3c' if t > 20 else '#3498db' for t in temps]
        ax1.bar(cities, temps, color=colors, alpha=0.7, edgecolor='black', linewidth=1.5)
        ax1.set_ylabel('Temperature (°C)', fontsize=12, fontweight='bold')
        ax1.set_title('Temperature by City', fontsize=13, fontweight='bold')
        ax1.grid(axis='y', alpha=0.3, linestyle='--')
        
        # Wind speed chart
        ax2 = fig.add_subplot(gs[0, 2])
        ax2.bar(cities, winds, color='#2ecc71', alpha=0.7, edgecolor='black')
        ax2.set_ylabel('Wind (km/h)', fontsize=10, fontweight='bold')
        ax2.set_title('Wind Speed', fontsize=11, fontweight='bold')
        ax2.tick_params(axis='x', rotation=45)
        
        # Statistics
        ax3 = fig.add_subplot(gs[1, 2])
        stats = [min(temps), max(temps), np.mean(temps)]
        ax3.bar(['Min', 'Max', 'Avg'], stats, color=['#3498db', '#e74c3c', '#f39c12'], alpha=0.7)
        ax3.set_ylabel('°C', fontsize=10, fontweight='bold')
        ax3.set_title('Temperature Stats', fontsize=11, fontweight='bold')
        
        # Summary
        ax4 = fig.add_subplot(gs[2, :])
        ax4.axis('off')
        
        warmest = max(zip(cities, temps), key=lambda x: x[1])
        coldest = min(zip(cities, temps), key=lambda x: x[1])
        
        summary = f"Warmest: {warmest[0]} ({warmest[1]:.1f}°C)  |  Coldest: {coldest[0]} ({coldest[1]:.1f}°C)  |  Average: {np.mean(temps):.1f}°C"
        ax4.text(0.5, 0.5, summary, ha='center', va='center', fontsize=12,
                bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.5))
        
        # Save
        try:
            plt.savefig(filename, dpi=300, bbox_inches='tight')
            if self.verbose:
                print(f"💾 Dashboard saved: {filename}")
            plt.show()
            return True
        except Exception as e:
            if self.verbose:
                print(f"❌ Failed to save: {e}")
            return False

# TEST AND RUN
if __name__ == "__main__":
    # Test cities
    test_cities = [
        "New York", "Los Angeles", "London",
        "Tokyo", "Sydney", "Paris"
    ]
    
    # Create and run dashboard
    dashboard = WeatherDashboard(verbose=True)
    if dashboard.fetch_all(test_cities):
        dashboard.create_dashboard()
        print("✨ Project complete!")
    else:
        print("❌ Failed to fetch data")
```

---

## Guided Practice

1. **Test Edge Cases:** Try cities that don't exist, test timeout behavior.

2. **Review Code:** Check for clarity, efficiency, and best practices.

3. **Finalize Output:** Ensure dashboard is professional and saved correctly.

4. **Document:** Add final comments and docstrings.

---

## Practice Problems

**Beginner:** Create a test script that validates all functions work correctly.

**Intermediate:** Add logging to track what the program does at each step.

**Challenge:** Create a comprehensive test suite with multiple test cases.

<details>
<summary>💡 Hints</summary>
- Test with valid and invalid inputs
- Check error messages are helpful
- Verify output quality
- Ensure code is readable
- Add status messages for users
- Test file saving functionality
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
# Simple test
def test_dashboard():
    dashboard = WeatherDashboard(verbose=True)
    test_cities = ["New York", "InvalidCity", "Paris"]
    dashboard.fetch_all(test_cities)
    assert len(dashboard.data) >= 2, "Should fetch valid cities"
    print("✓ Tests passed")

test_dashboard()
```

**Intermediate:**
```python
# Add logging
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

# Use logging in your code
logging.info(f"Fetching data for {city}")
```

**Challenge:** (See full example above with comprehensive error handling and testing)
</details>
