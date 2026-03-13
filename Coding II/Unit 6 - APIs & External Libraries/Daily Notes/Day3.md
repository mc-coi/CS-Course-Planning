# Day 3: Working with JSON APIs
**Learning Target:** I can interact with REST APIs, fetch real data, and process JSON responses.

### Key Concepts
**REST API:** Web service using HTTP for CRUD operations
**JSON:** Lightweight data format
**Authentication:** API keys for access control

### Code Examples
```python
import requests
import json

# Fetch data from public API
response = requests.get("https://api.coindesk.com/v1/bpi/currentprice.json")
data = response.json()

# Navigate nested JSON
price_usd = data["bpi"]["USD"]["rate"]
print(f"Bitcoin: ${price_usd}")

# Process multiple results
response = requests.get("https://api.github.com/repos/python/cpython/issues")
issues = response.json()
for issue in issues[:3]:
    print(issue["title"], issue["state"])

# Using API with authentication (API key)
headers = {"Authorization": "Bearer YOUR_API_KEY"}
response = requests.get("https://api.example.com/protected", headers=headers)

# Paginated results
page = 1
all_data = []
while page <= 3:
    params = {"page": page}
    response = requests.get("https://api.example.com/data", params=params)
    all_data.extend(response.json())
    page += 1
```

### Guided Practice
Fetch weather data, stock data, or other public API information.

### Practice Problems
**Problem 1 — Beginner:** Fetch and display data from public API.

**Problem 2 — Intermediate:** Process multiple API results.

**Problem 3 — Challenge:** Handle pagination and combine data.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
import requests
response = requests.get("https://api.agify.io?name=michael")
data = response.json()
print(f"{data['name']} is approximately {data['age']} years old")

# Problem 2
response = requests.get("https://jsonplaceholder.typicode.com/posts")
posts = response.json()
for post in posts[:5]:
    print(f"ID {post['id']}: {post['title']}")
```
</details>

---

---
