# Day 9: Building a Multi-API Application

**Learning Target:** I can design and build a complete application that uses multiple APIs and handles data processing.

---

## Key Concepts

**Application Design:**
1. **Planning:** Decide what data you need and which APIs provide it
2. **Fetching:** Get data from each API
3. **Processing:** Clean and combine data
4. **Displaying:** Present results to the user

**Data Combination:** You can merge data from multiple APIs by matching keys:
- Get location from one API
- Use location in another API
- Combine results

**Code Organization:** Use functions to separate concerns:
- One function per API call
- One function for processing
- One function for display

---

## Code Examples

```python
import requests

# Complete Joke + Quote Application

def get_random_joke():
    """Fetch a random joke"""
    response = requests.get("https://v2.jokeapi.dev/joke/Any")
    if response.status_code == 200:
        joke = response.json()
        if "type" in joke and joke["type"] == "single":
            return joke["joke"]
        else:
            return f"{joke['setup']} {joke['delivery']}"
    return None

def get_random_quote():
    """Fetch a random quote"""
    response = requests.get("https://api.quotable.io/random")
    if response.status_code == 200:
        quote = response.json()
        return quote["content"], quote["author"]
    return None, None

def get_pokemon_name():
    """Fetch a random Pokemon"""
    # Random ID between 1 and 151
    import random
    pokemon_id = random.randint(1, 151)
    response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{pokemon_id}")
    if response.status_code == 200:
        pokemon = response.json()
        return pokemon["name"].capitalize()
    return None

def display_daily_summary():
    """Display a daily summary mixing all APIs"""
    print("=" * 50)
    print("DAILY SUMMARY")
    print("=" * 50)
    
    joke = get_random_joke()
    print(f"\nJoke: {joke}\n")
    
    quote, author = get_random_quote()
    print(f"Quote: \"{quote}\"")
    print(f"— {author}\n")
    
    pokemon = get_pokemon_name()
    print(f"Random Pokemon: {pokemon}\n")
    print("=" * 50)

# Run the application
display_daily_summary()
```

---

## Guided Practice

1. **Combine APIs:** Create a program that fetches a quote, a joke, and a Pokemon fact in one summary display.

2. **Data Processing:** Fetch weather for 3 cities and determine which is warmest.

3. **User Input:** Ask the user for input (e.g., a city name) and use it to fetch weather data.

4. **Error Handling:** Add try-except blocks throughout to handle API failures gracefully.

---

## Practice Problems

**Beginner:** Create a function that fetches and displays a quote and a joke together.

**Intermediate:** Build a "Daily Briefing" program that gets weather for your city and displays it with a random inspirational quote.

**Challenge:** Create an interactive program that accepts user input for a city name and displays weather, relevant facts, and a motivational quote.

<details>
<summary>💡 Hints</summary>
- Wrap each API call in its own function for reusability
- Always check `response.status_code` or use try-except
- Use `input()` to get user input
- Format output nicely with print statements and separators
- Use `random.randint()` for variety
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

def get_quote():
    response = requests.get("https://api.quotable.io/random")
    data = response.json()
    return f'"{data["content"]}" — {data["author"]}'

def get_joke():
    response = requests.get("https://v2.jokeapi.dev/joke/Any")
    data = response.json()
    if data["type"] == "single":
        return data["joke"]
    return f"{data['setup']} {data['delivery']}"

print(get_quote())
print(get_joke())
```

**Intermediate:**
```python
import requests
from datetime import date

# (Weather function from Day 8)

def display_briefing(city):
    temp = get_temperature(city)
    response = requests.get("https://api.quotable.io/random")
    quote = response.json()
    
    print(f"\n=== Daily Briefing for {date.today()} ===")
    print(f"Weather in {city}: {temp}°C")
    print(f"\nQuote of the day:")
    print(f'"{quote["content"]}"')
    print(f"— {quote["author"]}\n")

display_briefing("New York")
```

**Challenge:**
```python
import requests

def interactive_briefing():
    city = input("Enter your city: ")
    
    # Get weather
    temp = get_temperature(city)
    
    # Get quote
    response = requests.get("https://api.quotable.io/random")
    quote = response.json()
    
    # Display
    print(f"\n=== Your Daily Briefing ===")
    print(f"City: {city}")
    print(f"Temperature: {temp}°C")
    print(f"Quote: \"{quote['content']}\"")
    print(f"— {quote['author']}\n")

interactive_briefing()
```
</details>
