# Day 6: API Keys & Authentication

**Learning Target:** I can work with APIs that require authentication using API keys.

---

## Key Concepts

**API Keys:** A unique token that identifies your application and allows the API provider to track usage. Many APIs require keys for security and rate limiting.

**Where to Get Keys:**
- Sign up for a free account on the API provider's website
- Generate an API key from your account settings
- Some APIs offer free tier limits (e.g., 100 requests per day)

**Common APIs Requiring Keys (Free Tiers Available):**
- OpenWeatherMap (weather)
- NewsAPI (news articles)
- OMDB (movie data)
- NASA (space data)

**Best Practice: Environment Variables** Keep your key secret by storing it in an environment variable or a config file (never hardcode it in your code).

```python
import os

# Read API key from environment
api_key = os.environ.get("OPENWEATHER_KEY")
```

**For School:** Typically, pre-installed libraries mean keys are already configured. Discuss how keys would be used in production.

---

## Code Examples

```python
import requests
import os

# Option 1: API key in URL parameter
api_key = "your_api_key_here"  # Usually read from environment
response = requests.get(
    "https://api.openweathermap.org/data/2.5/weather",
    params={
        "q": "New York",
        "appid": api_key,
        "units": "metric"
    }
)
weather = response.json()
print(f"Temperature: {weather['main']['temp']}°C")

# Option 2: API key in headers
headers = {
    "Authorization": f"Bearer {api_key}"
}
response = requests.get(
    "https://api.example.com/endpoint",
    headers=headers
)

# Option 3: Using environment variables (BEST PRACTICE)
api_key = os.environ.get("MY_API_KEY")
if api_key is None:
    print("Error: API key not found in environment")
else:
    response = requests.get("https://api.example.com/data", params={"key": api_key})
```

---

## Guided Practice

1. **Research Keys:** Find an API that requires a key (e.g., OpenWeatherMap, NewsAPI). Research their documentation.

2. **Sign Up (Optional):** If allowed, sign up for a free account and generate a test key.

3. **URL Parameters vs Headers:** Discuss when each method is used and why.

4. **Security:** Why should you never hardcode your API key in your source code?

---

## Practice Problems

**Beginner:** Write code that stores an API key in a variable and uses it in a requests.get() call (use a dummy key for now).

**Intermediate:** Write a function that reads an API key from an environment variable and makes a request. Include error handling if the key is missing.

**Challenge:** Create a system where API keys are stored in a separate config file (not in version control) and loaded into your program.

<details>
<summary>💡 Hints</summary>
- Use `os.environ.get("KEY_NAME")` to read environment variables
- Check if the key is `None` to handle missing keys
- In production, use `.gitignore` to prevent pushing sensitive files
- Some APIs allow keys in the URL; others require headers
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

api_key = "demo_key_12345"
response = requests.get(
    "https://api.example.com/data",
    params={"key": api_key}
)
print(response.json())
```

**Intermediate:**
```python
import requests
import os

def fetch_weather(city):
    api_key = os.environ.get("OPENWEATHER_KEY")
    if not api_key:
        raise ValueError("API key not found in environment")
    
    response = requests.get(
        "https://api.openweathermap.org/data/2.5/weather",
        params={"q": city, "appid": api_key}
    )
    return response.json()

# Usage
weather = fetch_weather("New York")
```

**Challenge:**
```python
import json
import os

# config.json (NOT in git):
# {"api_key": "your_key_here"}

with open("config.json") as f:
    config = json.load(f)
    api_key = config["api_key"]

# Use api_key in requests
```
</details>
