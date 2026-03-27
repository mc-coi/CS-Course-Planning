# Day 2: The requests Library
**Learning Target:** I can make HTTP requests and handle responses using the requests library.

### Key Concepts
**HTTP methods:** GET (retrieve), POST (create), PUT (update), DELETE
**Status codes:** 200 (OK), 404 (not found), 500 (server error)
**Response object:** Contains status, headers, body

### Code Examples
```python
import requests

# GET request
response = requests.get("https://api.example.com/data")
print(response.status_code)  # 200, 404, etc.
print(response.text)         # Raw response
print(response.headers)      # Headers dict

# Check if successful
if response.status_code == 200:
    data = response.json()  # Parse JSON

# GET with parameters
params = {"query": "python", "limit": 10}
response = requests.get("https://api.example.com/search", params=params)

# POST request
data = {"name": "Alice", "age": 25}
response = requests.post("https://api.example.com/users", json=data)

# Error handling
try:
    response = requests.get("https://api.example.com/data", timeout=5)
    response.raise_for_status()  # Raise if error status
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```

### Guided Practice
Make requests to public API, parse response.

### Practice Problems
**Problem 1 — Beginner:** Make a GET request and print response status.

**Problem 2 — Intermediate:** Parse JSON from API response.

**Problem 3 — Challenge:** Handle errors in API requests.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 2
import requests
response = requests.get("https://api.github.com/users/github")
user_data = response.json()
print(user_data["name"], user_data["public_repos"])

# Problem 3
try:
    response = requests.get("https://api.example.com/data")
    response.raise_for_status()
except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```
</details>

---

---
