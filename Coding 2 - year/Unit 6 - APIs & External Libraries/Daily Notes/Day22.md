# Day 22: Unit Assessment

**Learning Target:** I can demonstrate mastery of APIs, external libraries, and data visualization through a comprehensive assessment.

---

## Assessment Overview

This assessment covers all Unit 6 topics: APIs, requests library, JSON parsing, authentication, error handling, standard library modules (random, math, datetime, collections), NumPy, and Matplotlib.

**Total Points:** 100
- Multiple Choice: 20 points
- Short Answer: 30 points
- Coding Challenges: 50 points

---

## Multiple Choice (1 point each, 20 total)

**1.** What does "API" stand for?
- A) Application Processing Interface
- B) Application Programming Interface
- C) Advanced Python Interface
- D) Application Protocol Interface

**2.** Which HTTP method is used to retrieve data from a server?
- A) POST
- B) GET
- C) PUT
- D) DELETE

**3.** What does JSON stand for?
- A) Java Standard Object Notation
- B) JavaScript Object Notation
- C) Java Serialized Object Notation
- D) JavaScript Ordered Notation

**4.** Which library is used to make HTTP requests in Python?
- A) http
- B) urllib
- C) requests
- D) network

**5.** What does status code 404 indicate?
- A) Server error
- B) Request successful
- C) Resource not found
- D) Unauthorized access

**6.** How do you convert a JSON string to a Python dictionary?
- A) json.dumps()
- B) json.loads()
- C) dict(json)
- D) json.parse()

**7.** Which random module function picks one item from a list?
- A) random.pick()
- B) random.choice()
- C) random.select()
- D) random.sample()

**8.** What does `math.sqrt(16)` return?
- A) 2
- B) 4
- C) 8
- D) 16

**9.** How do you get today's date in Python?
- A) datetime.now()
- B) date.now()
- C) date.today()
- D) datetime.today()

**10.** Which collections module class counts occurrences of items?
- A) Counter
- B) DefaultDict
- C) Deque
- D) OrderedDict

**11.** NumPy arrays are better than lists for numerical computing because:
- A) They store more data
- B) They're faster and use less memory
- C) They can have mixed types
- D) They're easier to understand

**12.** What is the correct way to create a NumPy array from a list?
- A) numpy.create([1,2,3])
- B) numpy.array([1,2,3])
- C) numpy.list([1,2,3])
- D) array([1,2,3])

**13.** Which matplotlib function creates a line chart?
- A) plt.line()
- B) plt.chart()
- C) plt.plot()
- D) plt.draw()

**14.** How do you add a title to a matplotlib chart?
- A) plt.add_title()
- B) plt.title()
- C) plt.set_title()
- D) plt.heading()

**15.** What is an API endpoint?
- A) The end of an API request
- B) A specific URL on a server that handles requests
- C) The final response from an API
- D) The authentication credentials

**16.** Which of these is a free public API (no key required)?
- A) OpenWeatherMap
- B) Open-Meteo
- C) NewsAPI
- D) AWS API

**17.** How do you make a GET request with parameters using requests?
- A) requests.get(url, params={})
- B) requests.get(url + "?params")
- C) requests.get(url, query={})
- D) requests.get(url).params()

**18.** What does `response.status_code == 200` indicate?
- A) Bad request
- B) Successful request
- C) Not found
- D) Server error

**19.** How many days are between two date objects?
- A) (date1 - date2).days
- B) date1.days_between(date2)
- C) date1 - date2
- D) (date1 - date2).total_seconds()

**20.** What does `datetime.strftime("%Y-%m-%d")` do?
- A) Parses a string into a date
- B) Formats a date as a string
- C) Converts timezone
- D) Calculates date difference

---

## Short Answer (2 points each, 15 total)

**1.** Explain the difference between `requests.get()` and `requests.post()`.

**2.** Why should you never hardcode API keys in your source code?

**3.** What is the purpose of error handling (try-except blocks) when working with APIs?

**4.** How would you extract the "temperature" value from this JSON response?
```json
{"weather": {"current": {"temperature": 72}}}
```

**5.** Describe one real-world application where you would use data visualization with APIs.

**6.** What is the difference between a list and a NumPy array?

**7.** Explain when you would use `Counter` from the collections module.

**8.** What does `random.seed()` do and why is it useful?

**9.** Describe how to create a 2x3 matrix using NumPy.

**10.** What are the steps to create a bar chart using matplotlib?

**11.** How would you filter a NumPy array to get only values greater than 10?

**12.** Explain what an HTTP status code is and give 3 examples.

**13.** What is the purpose of `response.raise_for_status()` in the requests library?

**14.** How would you format a date as "March 25, 2026" using strftime?

**15.** Describe the workflow for building a data visualization project.

---

## Coding Challenges (50 points total)

### Challenge 1: API Data Fetching (15 points)

Write a function that:
- Takes a city name as input
- Uses the Open-Meteo Geocoding API to get latitude and longitude
- Uses the Open-Meteo Weather API to fetch current temperature
- Returns the temperature or prints an error message if unsuccessful
- Includes proper error handling

```python
def get_city_temperature(city_name):
    """
    Fetch current temperature for a city.
    
    Args:
        city_name (str): Name of the city
        
    Returns:
        float: Temperature in Celsius or None if error
    """
    # Your code here
    pass

# Test
print(get_city_temperature("New York"))
```

### Challenge 2: Data Processing with Collections (15 points)

Write a function that:
- Takes a list of words as input
- Counts frequency of each word using Counter
- Returns the 5 most common words with their counts
- Handles empty lists gracefully

```python
def find_most_common_words(words, n=5):
    """
    Find the n most common words in a list.
    
    Args:
        words (list): List of words
        n (int): Number of top words to return
        
    Returns:
        list: List of (word, count) tuples
    """
    # Your code here
    pass

# Test
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
print(find_most_common_words(words, 3))
```

### Challenge 3: Data Visualization (20 points)

Create a program that:
- Fetches weather data for at least 3 cities
- Creates at least 2 different visualizations (e.g., bar chart, line chart)
- Includes proper labels, titles, and formatting
- Handles errors gracefully
- Saves the visualization to a file

```python
def create_weather_visualization(cities):
    """
    Create a weather visualization for multiple cities.
    
    Args:
        cities (list): List of city names
    """
    # Your code here
    pass

# Test
create_weather_visualization(["New York", "Los Angeles", "Chicago"])
```

---

## Answer Key

### Multiple Choice Answers
1. B | 2. B | 3. B | 4. C | 5. C | 6. B | 7. B | 8. B | 9. C | 10. A
11. B | 12. B | 13. C | 14. B | 15. B | 16. B | 17. A | 18. B | 19. A | 20. B

### Short Answer Sample Answers

**1.** GET retrieves data from the server (safe, read-only). POST submits data to the server (creates new resources).

**2.** Hard-coded keys expose your credentials if the code is shared or leaked. Use environment variables instead.

**3.** APIs can fail due to network issues, timeouts, or server errors. Error handling makes your code robust.

**4.** `data["weather"]["current"]["temperature"]`

**5.** Example: Weather dashboard, stock market tracker, social media analytics, etc.

**6.** NumPy arrays are faster for math operations and use less memory. Lists are more flexible but slower.

**7.** When you need to count frequencies of items, like letter/word counts, voting tallies, etc.

**8.** seed() makes random results reproducible—same seed produces same sequence. Useful for testing.

**9.** `matrix = np.array([[1, 2, 3], [4, 5, 6]])` or `matrix = np.zeros((2, 3))`

**10.** Create data → plt.bar() → Add labels/title → plt.show()

**11.** `filtered = array[array > 10]` (boolean indexing)

**12.** Numbers indicating request result: 200 (OK), 404 (Not Found), 500 (Server Error)

**13.** Automatically raises an exception if the HTTP response status indicates an error.

**14.** `date.strftime("%B %d, %Y")`

**15.** 1) Define data needs 2) Fetch data (API) 3) Process/clean 4) Choose chart type 5) Visualize 6) Save/present

### Coding Challenge Sample Answers

**Challenge 1:**
```python
import requests

def get_city_temperature(city_name):
    try:
        # Get coordinates
        geo_response = requests.get(
            "https://geocoding-api.open-meteo.com/v1/search",
            params={"name": city_name, "count": 1},
            timeout=5
        )
        geo_data = geo_response.json()
        
        if not geo_data["results"]:
            print(f"City '{city_name}' not found")
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
        temp = weather_data["current_weather"]["temperature"]
        return temp
    
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None
```

**Challenge 2:**
```python
from collections import Counter

def find_most_common_words(words, n=5):
    if not words:
        return []
    
    counter = Counter(words)
    return counter.most_common(n)
```

**Challenge 3:**
```python
import requests
import numpy as np
import matplotlib.pyplot as plt

def create_weather_visualization(cities):
    temps = {}
    
    for city in cities:
        try:
            geo_resp = requests.get(
                "https://geocoding-api.open-meteo.com/v1/search",
                params={"name": city, "count": 1}
            ).json()
            
            if geo_resp["results"]:
                lat = geo_resp["results"][0]["latitude"]
                lon = geo_resp["results"][0]["longitude"]
                
                weather_resp = requests.get(
                    "https://api.open-meteo.com/v1/forecast",
                    params={"latitude": lat, "longitude": lon, "current_weather": True}
                ).json()
                
                temps[city] = weather_resp["current_weather"]["temperature"]
        except:
            pass
    
    # Create visualizations
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))
    
    # Bar chart
    ax1.bar(temps.keys(), temps.values())
    ax1.set_ylabel('Temperature (°C)')
    ax1.set_title('City Temperatures')
    
    # Line chart
    ax2.plot(list(temps.keys()), list(temps.values()), marker='o')
    ax2.set_ylabel('Temperature (°C)')
    ax2.set_title('Temperature Trend')
    
    plt.tight_layout()
    plt.savefig('weather_viz.png')
    plt.show()
```

---

## Grading Rubric

**Multiple Choice:** 1 point per correct answer (20 total)

**Short Answer:** 2 points per response
- Full credit: Correct and well-explained
- Partial credit: Mostly correct or incomplete explanation
- No credit: Incorrect or no attempt

**Coding Challenges:**
- Challenge 1 (15 pts): API interaction, error handling, returns correct data
- Challenge 2 (15 pts): Collections usage, correct logic, handles edge cases
- Challenge 3 (20 pts): Fetches data (5), creates 2+ visualizations (10), proper formatting and error handling (5)

**Total: 100 points**

