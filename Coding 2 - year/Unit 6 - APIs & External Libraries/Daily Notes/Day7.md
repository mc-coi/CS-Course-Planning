# Day 7: Error Handling with APIs

**Learning Target:** I can write robust API code that handles errors gracefully using status codes and exception handling.

---

## Key Concepts

**HTTP Status Codes (Review):**
- **2xx (Success):** 200 OK, 201 Created
- **4xx (Client Error):** 400 Bad Request, 404 Not Found, 403 Forbidden
- **5xx (Server Error):** 500 Internal Server Error

**Common API Errors:**
- **Connection Error:** Network problem, API is down
- **Timeout:** API took too long to respond
- **Invalid Request:** Wrong parameters, bad URL
- **Rate Limiting:** Too many requests in short time (429)

**Exception Handling:**
```python
try:
    response = requests.get(url)
    response.raise_for_status()  # Raise exception for bad status codes
except requests.exceptions.ConnectionError:
    print("Network error")
except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.HTTPError:
    print(f"HTTP error: {response.status_code}")
```

---

## Code Examples

```python
import requests

# Method 1: Check status code
response = requests.get("https://api.quotable.io/random")
if response.status_code == 200:
    quote = response.json()
    print(quote["content"])
elif response.status_code == 404:
    print("Resource not found")
else:
    print(f"Error: {response.status_code}")

# Method 2: Use raise_for_status()
try:
    response = requests.get("https://api.quotable.io/random")
    response.raise_for_status()
    print(response.json())
except requests.exceptions.HTTPError:
    print(f"HTTP error: {response.status_code}")
except requests.exceptions.ConnectionError:
    print("Connection failed")
except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")

# Method 3: Handle with timeout
try:
    response = requests.get(
        "https://api.quotable.io/random",
        timeout=5  # 5-second timeout
    )
    data = response.json()
except requests.exceptions.Timeout:
    print("API took too long to respond")
except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```

---

## Guided Practice

1. **Status Code Check:** Write code that requests a Pokemon and checks the status code. Print different messages for 200, 404, and other codes.

2. **Exception Handling:** Add try-except blocks to protect your API requests from network errors.

3. **Timeout:** Make a request with a short timeout (e.g., 2 seconds) and catch the Timeout exception.

4. **Retry Logic:** Create a function that retries a failed request up to 3 times.

---

## Practice Problems

**Beginner:** Write code that requests data from an API, checks if status_code is 200, and prints either the data or an error message.

**Intermediate:** Create a function that makes an API request with exception handling for ConnectionError, Timeout, and HTTPError.

**Challenge:** Write a function that retries a request up to 3 times with increasing delays (1 second, 2 seconds, 3 seconds) before giving up.

<details>
<summary>💡 Hints</summary>
- Use `response.raise_for_status()` to automatically raise exceptions for bad status codes
- `response.status_code` gives you the numeric code (200, 404, etc.)
- Use `try-except` blocks to handle `requests.exceptions.*` errors
- The `timeout` parameter in `requests.get()` specifies how long to wait
- Use `time.sleep()` for delays between retries
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

response = requests.get("https://api.quotable.io/random")
if response.status_code == 200:
    print(response.json()["content"])
else:
    print(f"Error: {response.status_code}")
```

**Intermediate:**
```python
import requests

def safe_get(url):
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.ConnectionError:
        print("Connection failed")
    except requests.exceptions.Timeout:
        print("Request timed out")
    except requests.exceptions.HTTPError:
        print(f"HTTP error: {response.status_code}")
    return None

data = safe_get("https://api.quotable.io/random")
```

**Challenge:**
```python
import requests
import time

def retry_request(url, retries=3):
    for attempt in range(retries):
        try:
            response = requests.get(url, timeout=5)
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            print(f"Attempt {attempt+1} failed: {e}")
            if attempt < retries - 1:
                time.sleep(attempt + 1)
    return None

data = retry_request("https://api.quotable.io/random")
```
</details>
