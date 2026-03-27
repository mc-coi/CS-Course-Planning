# Unit 6 Comprehensive Assessment

**Duration:** 60 minutes  
**Total Points:** 100  
**Sections:** Multiple Choice (20 pts) | Short Answer (30 pts) | Coding (50 pts)

---

## Multiple Choice (1 point each, 20 total)

Select the best answer for each question.

**1.** What does API stand for?
- A) Advanced Programming Interface
- B) Application Programming Interface
- C) Algorithm Processing Integration
- D) Application Protocol Integration

**2.** Which HTTP method retrieves data from a server?
- A) PUT
- B) DELETE
- C) GET
- D) POST

**3.** What does JSON stand for?
- A) Java Source Object Notation
- B) JavaScript Object Notation
- C) Java Structured Object Network
- D) JavaScript Organized Notation

**4.** To make HTTP requests in Python, which library is most commonly used?
- A) network
- B) http
- C) requests
- D) urllib

**5.** An HTTP status code of 404 means:
- A) Server error
- B) Unauthorized
- C) Resource not found
- D) Bad request

**6.** How do you convert a JSON string to a Python dictionary?
- A) json.dumps()
- B) json.loads()
- C) json.decode()
- D) json.parse()

**7.** The `random.choice()` function:
- A) Generates a random float
- B) Picks one item from a sequence
- C) Shuffles a list
- D) Returns a random integer

**8.** What does `math.sqrt(25)` return?
- A) 5
- B) 5.0
- C) 625
- D) 2.5

**9.** How do you get today's date in Python?
- A) datetime.today()
- B) date.now()
- C) date.today()
- D) datetime.now()

**10.** Which collections class counts occurrences of items?
- A) defaultdict
- B) Counter
- C) deque
- D) namedtuple

**11.** NumPy arrays are preferred over Python lists for numerical computing because:
- A) They can store more data
- B) They're easier to understand
- C) They're faster and use less memory
- D) They support any data type

**12.** To create a NumPy array from a list, use:
- A) np.create([1,2,3])
- B) np.from_list([1,2,3])
- C) np.array([1,2,3])
- D) numpy.list([1,2,3])

**13.** In matplotlib, which function creates a line chart?
- A) plt.line()
- B) plt.plot()
- C) plt.draw()
- D) plt.create()

**14.** To add a title to a matplotlib plot:
- A) plt.add_title("Title")
- B) plt.set_title("Title")
- C) plt.title("Title")
- D) plt.heading("Title")

**15.** An API endpoint is:
- A) The end of an API request
- B) A specific URL that handles API requests
- C) The authentication token
- D) The response data

**16.** Which is a free public API that requires no authentication key?
- A) OpenWeatherMap
- B) NewsAPI
- C) Open-Meteo
- D) Twitter API

**17.** To make a GET request with query parameters using requests:
- A) requests.get(url + "?param=value")
- B) requests.get(url, params={"param": "value"})
- C) requests.get(url, query={"param": "value"})
- D) requests.get(url).params()

**18.** `response.raise_for_status()` does what?
- A) Displays the status code
- B) Raises an exception for unsuccessful responses
- C) Returns True/False
- D) Prints an error message

**19.** To calculate days between two dates:
- A) (date1 - date2).days
- B) date1.days_between(date2)
- C) date1.subtract(date2)
- D) (date1 - date2).total_days()

**20.** Boolean indexing in NumPy is:
- A) Using integers to select elements
- B) Using True/False conditions to filter elements
- C) Sorting by boolean values
- D) Converting to boolean type

---

## Short Answer (2 points each, 15 total)

Provide clear, concise answers.

**1.** Explain the difference between HTTP GET and POST requests.

**2.** Why is it important to use environment variables for API keys instead of hardcoding them?

**3.** What is the purpose of error handling (try-except blocks) when working with APIs?

**4.** Given this JSON: `{"user": {"name": "Alice", "age": 30}}`, how would you extract the name?

**5.** Describe one real-world application where you would use an API to fetch data and then visualize it.

**6.** What is the main advantage of NumPy arrays over Python lists for numerical operations?

**7.** When would you use the `Counter` class from collections?

**8.** Explain what `random.seed()` does and why it's useful in programming.

**9.** How would you create a 3x4 matrix using NumPy?

**10.** List the basic steps to create a bar chart using matplotlib.

**11.** How do you filter a NumPy array to get only elements greater than 10?

**12.** Explain what an HTTP status code is and provide 3 examples.

**13.** What is the difference between `requests.get()` and `response.json()`?

**14.** How would you format a date as "2026-03-25" using Python's datetime module?

**15.** Describe the typical workflow for building a data visualization project.

---

## Coding Challenges (50 points total)

### Challenge 1: API Data Fetching (15 points)

Write a Python function that:
- Takes a city name as input
- Uses the Open-Meteo Geocoding API to get latitude/longitude
- Uses the Open-Meteo Weather API to fetch current temperature
- Returns the temperature (as a float) or None if unsuccessful
- Includes proper error handling

**Requirements:**
- Handle missing cities gracefully
- Use try-except for network errors
- Check response status codes
- Return meaningful results

```python
def get_city_temperature(city_name):
    """
    Fetch current temperature for a city.
    
    Args:
        city_name (str): Name of the city
        
    Returns:
        float: Temperature in Celsius, or None if error
    """
    # Your code here
    pass

# Test your function
print(get_city_temperature("New York"))
print(get_city_temperature("InvalidCity"))
```

**Grading (15 pts):**
- Correct API calls (5 pts)
- Error handling (5 pts)
- Returns correct data (5 pts)

---

### Challenge 2: Data Processing (15 points)

Write a function that:
- Takes a list of words as input
- Uses collections.Counter to count frequency
- Returns the N most common words with their counts
- Handles edge cases (empty list, N larger than list size)

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

# Test your function
words = ["apple", "banana", "apple", "cherry", "banana", "apple", "date"]
print(find_most_common_words(words, 3))
# Expected: [('apple', 3), ('banana', 2), ('cherry', 1)]
```

**Grading (15 pts):**
- Correct use of Counter (5 pts)
- Correct return format (5 pts)
- Handles edge cases (5 pts)

---

### Challenge 3: Data Visualization (20 points)

Create a complete program that:
- Fetches weather data for **at least 3 cities** using the Open-Meteo API
- Creates **at least 2 different visualizations** (e.g., bar chart + line chart)
- Includes proper labels, titles, and formatting
- Handles errors gracefully
- Saves the visualization to a file

**Requirements:**
- Fetch data from API (not hardcoded)
- Use matplotlib with multiple charts
- Clean, readable code with comments
- Error handling throughout
- Output saved to file

```python
import requests
import numpy as np
import matplotlib.pyplot as plt

def create_weather_dashboard(cities):
    """
    Create a weather visualization for multiple cities.
    
    Args:
        cities (list): List of city names
    """
    # Step 1: Fetch data from API
    # Step 2: Process data
    # Step 3: Create visualizations
    # Step 4: Save output
    
    pass

# Test your function
create_weather_dashboard(["New York", "Los Angeles", "Chicago"])
```

**Grading (20 pts):**
- Data fetching from API (5 pts)
- Multiple visualizations (5 pts)
- Proper labels and formatting (5 pts)
- Error handling and code quality (5 pts)

---

## Answer Key

### Multiple Choice
1. B | 2. C | 3. B | 4. C | 5. C | 6. B | 7. B | 8. B | 9. C | 10. B
11. C | 12. C | 13. B | 14. C | 15. B | 16. C | 17. B | 18. B | 19. A | 20. B

### Short Answer (Sample Answers)

**1.** GET retrieves data from the server (read-only, safe). POST submits data to the server (creates/modifies resources).

**2.** Hard-coded keys can be exposed if code is shared or compromised. Environment variables keep secrets secure.

**3.** APIs can fail due to network issues, timeouts, or server errors. Error handling makes code robust and user-friendly.

**4.** `data["user"]["name"]`

**5.** Examples: Weather dashboard, stock tracker, COVID-19 statistics visualization, social media analytics, etc.

**6.** NumPy arrays are faster for math (100x+), use less memory, and support vectorized operations without loops.

**7.** When counting frequencies: word counts, letter frequencies, voting tallies, survey responses, etc.

**8.** `seed()` makes random values reproducible—same seed always produces same sequence. Useful for testing and debugging.

**9.** `matrix = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])` or `matrix = np.zeros((3,4))`

**10.** 1) Prepare data | 2) Create figure | 3) Use plt.bar() | 4) Add labels/title | 5) Display with plt.show()

**11.** `filtered = array[array > 10]` (Boolean indexing)

**12.** HTTP status codes indicate request results: 200 (Success), 404 (Not Found), 500 (Server Error), 403 (Forbidden), 201 (Created)

**13.** `requests.get()` makes the HTTP request; `response.json()` parses the response body as JSON.

**14.** `date.strftime("%Y-%m-%d")` formats as "2026-03-25"

**15.** 1) Define data source | 2) Fetch data (API) | 3) Process/clean data | 4) Choose visualization type | 5) Create charts | 6) Save/present results

### Coding Challenge Samples

**Challenge 1 Sample Answer:**
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
        
        if not geo_data.get("results"):
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
        return weather_data["current_weather"]["temperature"]
    
    except:
        return None
```

**Challenge 2 Sample Answer:**
```python
from collections import Counter

def find_most_common_words(words, n=5):
    if not words:
        return []
    
    counter = Counter(words)
    return counter.most_common(n)
```

**Challenge 3 Sample Answer:**
```python
import requests
import numpy as np
import matplotlib.pyplot as plt

def create_weather_dashboard(cities):
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
    
    # Create visualizations
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))
    
    # Bar chart
    ax1.bar(temps.keys(), temps.values())
    ax1.set_ylabel("Temperature (°C)")
    ax1.set_title("Temperature by City")
    
    # Line chart
    ax2.plot(list(temps.keys()), list(temps.values()), marker='o')
    ax2.set_ylabel("Temperature (°C)")
    ax2.set_title("Temperature Trend")
    
    plt.tight_layout()
    plt.savefig("weather_dashboard.png", dpi=150)
    plt.show()
```

---

## Grading Rubric

| Section | Points | Breakdown |
|---------|--------|-----------|
| Multiple Choice | 20 | 1 pt each |
| Short Answer | 30 | 2 pts each |
| Challenge 1 | 15 | API + Error + Data |
| Challenge 2 | 15 | Collections + Logic + Edges |
| Challenge 3 | 20 | Fetch + Visualize + Format |
| **Total** | **100** | |

**Scale:**  
90-100: A | 80-89: B | 70-79: C | 60-69: D | Below 60: F

