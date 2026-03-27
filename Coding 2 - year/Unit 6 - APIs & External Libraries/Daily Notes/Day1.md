# Day 1: What is an API?

**Learning Target:** I can define what an API is and explain how it enables programs to communicate with other software and services.

---

## Key Concepts

**API (Application Programming Interface):** A set of rules and tools that allows different software programs to communicate with each other. Think of it as a restaurant menu—the menu defines what you can order, and the restaurant's kitchen is the service that fulfills your request.

**HTTP (HyperText Transfer Protocol):** The protocol used for transferring data across the web. When you visit a website or request data from an API, you're using HTTP.

**Request and Response:** An API interaction follows a simple pattern:
- **Request:** Your program asks for something (e.g., "Give me the weather for New York")
- **Response:** The API sends back data (e.g., the weather forecast)

**REST (Representational State Transfer):** A style of API design that uses standard HTTP methods (GET, POST, PUT, DELETE) to perform operations. Most modern APIs follow REST principles.

**Endpoint:** A specific URL on a server that handles requests. For example, `https://api.example.com/weather` is an endpoint.

**JSON (JavaScript Object Notation):** A lightweight format for storing and exchanging data. APIs typically return data in JSON format, which looks similar to Python dictionaries.

---

## Code Examples

```python
# APIs allow you to fetch real-world data from your Python program
# For example, you might request a random quote from an API

# Example request structure (we'll use the requests library next)
# GET https://api.quotable.io/random
# Response:
# {
#   "content": "The only way to do great work is to love what you do.",
#   "author": "Steve Jobs"
# }

# Your program can parse this JSON and use it
quote = "The only way to do great work is to love what you do."
print(f"Quote: {quote}")
```

---

## Guided Practice

1. **Discuss:** What APIs have you used without knowing it? (Social media login, Google Maps, weather apps, etc.)
2. **Define:** Write your own definition of API in one sentence.
3. **Diagram:** Draw a simple request/response cycle:
   - Your program → [HTTP request] → Remote server
   - Your program ← [HTTP response] → Remote server
4. **List:** Name 3 real-world services that probably have APIs (YouTube, Spotify, Twitter, etc.)

---

## Practice Problems

**Beginner:** What is the difference between a **request** and a **response** in an API?

**Intermediate:** Why would a programmer use an API instead of building everything from scratch?

**Challenge:** Imagine you're building a weather app. Explain how it would use an API to show today's forecast without storing its own weather data.

<details>
<summary>💡 Hints</summary>
- A request is what you *ask* for; a response is what you *get back*
- Think about specialization—some organizations are experts at one thing
- Consider: where does real-time weather data come from?
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:** A request is what your program sends to ask for data (e.g., "get the weather"). A response is what the API sends back with the data you requested (e.g., the actual weather information).

**Intermediate:** Using an API saves time and effort. Instead of building a weather service from scratch, a programmer can use an existing API that a weather service maintains. This is more reliable, more up-to-date, and requires less code.

**Challenge:** The weather app sends a request to a weather API (e.g., "get weather for New York"). The API queries its database and sends back the current forecast. The app receives the response and displays it to the user. This way, the app always has current data without needing to store and update weather information itself.
</details>
