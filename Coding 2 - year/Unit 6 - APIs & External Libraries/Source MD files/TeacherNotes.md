# Unit 6 - APIs & External Libraries: Teacher Misconception & Callout Guide

## Overview

Unit 6 opens the door to real-world programming: students connect to external data sources, use standard and third-party libraries, and build applications that do something meaningful. The biggest challenge is that students treat APIs as magical—they don't understand HTTP fundamentals, assume requests always succeed, and treat error codes as meaningless. They use libraries by copying code without understanding parameters, don't validate API responses, and think status codes like 404 are "errors" to ignore. This unit teaches resilience: graceful degradation, proper error handling, and defensive coding when external systems are involved.

---

## Misconceptions by Topic

### HTTP & Web APIs Basics (Days 1–3)

**⚠️ Misconception:** "API requests always work. If something fails, it's a bug in the API."

**What it looks like in code:**
```python
import requests

response = requests.get('https://api.example.com/data')
data = response.json()  # Crashes if status is not 200
process(data)
```

**Why students think this:** In development, with test APIs, requests usually work.

**How to address it:** Teach **reality**: Networks fail, servers go down, rate limits are hit. Always handle failures.

```python
import requests

try:
    response = requests.get('https://api.example.com/data', timeout=5)
    response.raise_for_status()  # Raise HTTPError if status is 4xx/5xx
    data = response.json()
except requests.exceptions.Timeout:
    print("Request timed out")
    data = None
except requests.exceptions.HTTPError as e:
    print(f"HTTP error: {e.response.status_code}")
    data = None
except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
    data = None

if data:
    process(data)
else:
    print("Could not fetch data; using default")
```

Show the flow:
1. **Check status code** → `response.raise_for_status()` or `if response.status_code != 200`
2. **Catch exceptions** → Network, timeout, JSON decode errors
3. **Handle gracefully** → Log, use defaults, retry

---

**⚠️ Misconception:** "Status codes like 404, 429, 500 are errors. I'll just use `try-except` to handle them."

**What it looks like in code:**
```python
# Student treats all status codes the same:
try:
    response = requests.get(url)
    data = response.json()
except:
    print("Error")
    data = None

# But 404 (not found) should be handled differently than 429 (rate limited)
```

**Why students think this:** Status codes are numbers; they all seem like "failures."

**How to address it:** Teach **status code semantics**:

```python
import requests
import time

response = requests.get(url)

if response.status_code == 200:
    # Success — process data
    data = response.json()
elif response.status_code == 404:
    # Not found — data doesn't exist
    print("Resource not found")
    data = None
elif response.status_code == 429:
    # Rate limited — wait and retry
    print("Rate limited; waiting...")
    time.sleep(60)
    response = requests.get(url)  # Retry
elif response.status_code == 500:
    # Server error — not your fault, but can't proceed
    print("Server error; try again later")
    data = None
elif response.status_code >= 400:
    # Other client error
    print(f"Error: {response.status_code}")
    data = None
else:
    # Other success (201, 204, etc.)
    data = response.json() if response.text else None
```

Show a decision tree:
- **2xx:** Success. Process data.
- **3xx:** Redirect. `requests` handles automatically.
- **4xx:** Client error. Check your request (URL, parameters, auth).
- **429:** Rate limit. Wait and retry.
- **5xx:** Server error. Not your fault; retry later.

---

**⚠️ Misconception:** "JSON responses are always valid. If I get a 200 status, the data is correct."

**What it looks like in code:**
```python
response = requests.get(api_url)
response.raise_for_status()  # 200 OK
data = response.json()  # Assumes valid JSON

# But the API might return:
# - Empty response (status 200, body "")
# - Malformed JSON
# - Unexpected structure

temperature = data['main']['temp']  # KeyError if structure is wrong
```

**Why students think this:** Status 200 feels like "everything is fine."

**How to address it:** Validate the response:

```python
import requests
import json

response = requests.get(api_url)
response.raise_for_status()

# Step 1: Validate response has content
if not response.text:
    print("Empty response")
    data = None
else:
    # Step 2: Validate JSON format
    try:
        data = response.json()
    except json.JSONDecodeError as e:
        print(f"Invalid JSON: {e}")
        data = None

# Step 3: Validate data structure
if data and isinstance(data, dict) and 'main' in data:
    try:
        temperature = data['main']['temp']
    except (KeyError, TypeError) as e:
        print(f"Missing field: {e}")
        temperature = None
else:
    print("Unexpected data structure")
    temperature = None
```

Or use a schema validator like `jsonschema`.

---

### GET Requests & Query Parameters (Days 3–5)

**⚠️ Misconception:** "Query parameters should be concatenated into the URL as a string."

**What it looks like in code:**
```python
# Student does:
url = 'https://api.example.com/search?q=python&limit=10'
response = requests.get(url)

# Instead of:
params = {'q': 'python', 'limit': 10}
response = requests.get('https://api.example.com/search', params=params)
```

**Why students think this:** String concatenation is straightforward.

**How to address it:** Teach the **advantages of `params` parameter**:

```python
import requests

# Problem with string concatenation:
search_term = 'python & django'
url = f'https://api.example.com/search?q={search_term}'
# Result: 'q=python & django' — BROKEN! Ampersand splits parameters!

# Solution: Use params
params = {'q': search_term}
response = requests.get('https://api.example.com/search', params=params)
# requests automatically URL-encodes: 'q=python%20%26%20django'

# Additional benefits:
# 1. Readable — params is a dict, easy to see structure
# 2. Safe — automatic URL encoding handles special characters
# 3. Composable — can build params dict programmatically

# Example:
filters = {
    'q': 'python',
    'limit': 10,
    'sort': 'stars'
}
response = requests.get('https://api.example.com/search', params=filters)
```

---

### API Authentication (Days 6–7)

**⚠️ Misconception:** "I'll put my API key in the code. It's just a key, not a password."

**What it looks like in code:**
```python
# WRONG: API key exposed in code
import requests

API_KEY = 'sk_live_abc123def456'
response = requests.get(
    'https://api.example.com/data',
    params={'key': API_KEY}
)
```

**Why students think this:** It's "just a key"; it feels less secret than a password.

**How to address it:** Teach **security**: API keys are credentials. Exposed keys = compromised account.

```python
# RIGHT: Use environment variables
import os
import requests

API_KEY = os.environ.get('API_KEY')
if not API_KEY:
    raise RuntimeError("API_KEY not set in environment variables")

response = requests.get(
    'https://api.example.com/data',
    params={'key': API_KEY}
)

# Setup:
# 1. Create .env file (add to .gitignore):
#    API_KEY=sk_live_abc123def456
# 2. Load with python-dotenv: pip install python-dotenv
#    from dotenv import load_dotenv
#    load_dotenv()
# 3. Access: os.environ.get('API_KEY')
```

Show the risk:
```python
# If you commit code with the key:
# 1. It's pushed to GitHub (public or private)
# 2. Git history remembers it forever
# 3. Anyone with repo access can use your key
# 4. Attacker can impersonate you, incur charges, steal data

# Recovery:
# 1. Delete the key from the API provider
# 2. Remove from git history (hard)
# 3. Rotate all keys
# 4. Check for abuse
```

Rule: "Never commit secrets. Use environment variables."

---

**⚠️ Misconception:** "API authentication is always the same. I'll use the API key as a query parameter."

**What it looks like in code:**
```python
# Student assumes all APIs use the same auth:
response = requests.get(url, params={'key': api_key})
```

**Why students think this:** The first API they used did this.

**How to address it:** Show **different auth methods**:

```python
import requests

api_key = 'sk_live_abc123'

# Method 1: Query parameter (rarely used, insecure)
response = requests.get(url, params={'key': api_key})

# Method 2: Header (common, more secure)
headers = {'Authorization': f'Bearer {api_key}'}
response = requests.get(url, headers=headers)

# Method 3: Header with API key naming
headers = {'X-API-Key': api_key}
response = requests.get(url, headers=headers)

# Method 4: Basic auth (username:password)
response = requests.get(url, auth=('username', 'password'))

# Method 5: OAuth2 (complex, for user delegation)
# Requires token exchange and refresh logic

# ALWAYS CHECK THE API DOCUMENTATION!
```

Emphasize: "Every API has different auth requirements. Read the docs."

---

### Error Handling & Resilience (Days 7–9)

**⚠️ Misconception:** "If an API request fails, I'll just return an error. The user can try again."

**What it looks like in code:**
```python
def fetch_data(url):
    response = requests.get(url)
    return response.json()

# If network fails, user gets nothing
```

**Why students think this:** Error handling is "done"—they returned None or raised an exception.

**How to address it:** Teach **resilience patterns**: retry logic, fallbacks, caching.

```python
import requests
import time
import json

def fetch_data_resilient(url, retries=3, timeout=5, cache_file='cache.json'):
    """
    Fetch data with retries and fallback cache.
    """
    # Step 1: Try the API
    for attempt in range(retries):
        try:
            response = requests.get(url, timeout=timeout)
            response.raise_for_status()
            data = response.json()

            # Step 2: Cache successful response
            with open(cache_file, 'w') as f:
                json.dump(data, f)

            return data
        except requests.exceptions.RequestException as e:
            print(f"Attempt {attempt + 1} failed: {e}")
            if attempt < retries - 1:
                time.sleep(2 ** attempt)  # Exponential backoff

    # Step 3: Use cache as fallback
    try:
        with open(cache_file) as f:
            data = json.load(f)
        print("Using cached data")
        return data
    except FileNotFoundError:
        print("No cache available")
        return None

# Usage:
data = fetch_data_resilient('https://api.example.com/data')
if data:
    process(data)
```

This shows: retry → cache → fallback. Production-grade resilience.

---

### Using External Libraries (Days 10–15)

**⚠️ Misconception:** "I'll use NumPy/Matplotlib the way I learned. If I need something, I'll copy code from Stack Overflow."

**What it looks like in code:**
```python
import numpy as np

# Student uses NumPy without understanding arrays:
arr = np.array([[1, 2, 3], [4, 5, 6]])
result = arr + 1  # Broadcasting — works, but why?

# When broadcasting fails, they have no idea how to debug
```

**Why students think this:** Libraries "just work" until they don't.

**How to address it:** **Teach the fundamentals**, not just syntax.

For **NumPy**, teach:
```python
import numpy as np

# 1. Arrays are not lists — different operations
arr = np.array([1, 2, 3])
lst = [1, 2, 3]

arr * 2  # [2, 4, 6] — element-wise multiplication
lst * 2  # [1, 2, 3, 1, 2, 3] — repetition!

# 2. Broadcasting — how arrays expand for operations
a = np.array([[1, 2, 3]])  # Shape: (1, 3)
b = np.array([10, 20, 30])  # Shape: (3,)
result = a + b  # Expands b to (1, 3), then adds

# 3. Dimensions matter
arr_1d = np.array([1, 2, 3])  # Shape (3,)
arr_2d = np.array([[1, 2, 3]])  # Shape (1, 3)

arr_1d.shape  # (3,)
arr_2d.shape  # (1, 3)

# If you're confused, use .shape to debug!
```

For **Matplotlib**, teach:
```python
import matplotlib.pyplot as plt

# 1. Figure and Axes structure
fig, ax = plt.subplots()  # Create figure and axes
ax.plot([1, 2, 3], [1, 4, 9])  # Plot on axes
ax.set_xlabel('X')
ax.set_ylabel('Y')
plt.show()

# 2. Different plot types
ax.plot(x, y)  # Line plot
ax.scatter(x, y)  # Scatter plot
ax.bar(x, y)  # Bar chart
ax.hist(data)  # Histogram

# 3. Customization
ax.set_title('My Plot')
ax.set_xlim(0, 10)
ax.legend()
plt.savefig('plot.png')  # Save instead of show in scripts
```

The key: **Understand the library's model. Then explore from there.**

---

**⚠️ Misconception:** "I'll import everything with `from module import *` so I don't need to type the module name."

**What it looks like in code:**
```python
from numpy import *
from pandas import *

array([1, 2, 3])  # Is this numpy.array or something else?
```

**Why students think this:** Shorter code feels simpler.

**How to address it:** Teach **clarity**: Use explicit imports.

```python
# GOOD: Clear what comes from where
import numpy as np
import matplotlib.pyplot as plt

arr = np.array([1, 2, 3])
plt.plot(arr)

# AVOID: Where does this come from?
from numpy import *
from pandas import *

array([1, 2, 3])  # Confusing!

# COMPROMISE: Import specific functions when using them once
from numpy import array, zeros, ones

arr = array([1, 2, 3])
```

Rule: "Use `import module as alias`. Be explicit."

---

### Data Visualization (Days 16–22)

**⚠️ Misconception:** "Visualization is done when the plot looks pretty."

**What it looks like in code:**
```python
import matplotlib.pyplot as plt

data = [10, 20, 15, 25, 30]
plt.plot(data)
plt.title('Data')
plt.show()

# No axis labels, no legend, no context
```

**Why students think this:** The plot displays; task done.

**How to address it:** Teach **audience-driven design**: A plot must communicate clearly.

```python
import matplotlib.pyplot as plt
import numpy as np

# Bad plot: no context
data = [10, 20, 15, 25, 30]
plt.plot(data)
plt.show()

# Good plot: tells a story
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May']
sales = [10, 20, 15, 25, 30]

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(months, sales, marker='o', linewidth=2, markersize=8)
ax.set_xlabel('Month', fontsize=12)
ax.set_ylabel('Sales (thousands)', fontsize=12)
ax.set_title('Monthly Sales Performance', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)
ax.set_ylim(0, 40)

# Add context
ax.text(2, 30, 'Sales dip in March', fontsize=10, color='red')

plt.tight_layout()
plt.savefig('sales.png', dpi=300)  # High quality
plt.show()
```

Checklist:
- Title? Yes.
- Axis labels with units? Yes.
- Legend (if multiple lines)? Yes.
- Readable font sizes? Yes.
- Appropriate scale (not misleading)? Yes.
- Grid for readability? Yes.

---

## Whole-Class Warning Signs

- **Students don't check response status codes** — show that 200 is not guaranteed. Check `response.status_code` or use `raise_for_status()`.
- **Students hardcode API keys in code** — stop immediately. Teach environment variables. Show the security risk.
- **Students assume JSON parsing will always work** — teach exception handling. Show `.json()` can fail.
- **Students use `requests.get()` without timeout** — add `timeout=5` to prevent hanging forever.
- **Students don't handle missing API response fields** — teach `.get()` with defaults and validation.
- **Students plot without titles, labels, legends** — show a good plot has context. Make visualization a design choice, not an afterthought.
- **Students use `import *`** — teach explicit imports. Clarity matters.
- **Students don't test error cases** — intentionally break APIs, show what happens, then fix it.

---

## Questions That Reveal Understanding

1. **"What should you do if an API request gets a 429 status code (rate limited)?"** (Answer: Wait before retrying. Exponential backoff is common. If they say "just retry immediately," they'll hammer the API and get banned.)

2. **"Where should you store your API key?"** (Answer: Environment variables, not in code. If they say "in a config file committed to git," they're a security risk.)

3. **"You get a 200 status but the JSON parsing fails. What's the issue?"** (Answer: Response body might be empty, malformed, or unexpected format. Shows they understand status ≠ data validity.)

4. **"Write code to fetch data with a fallback cache."** (Answer: Try fetch → save cache → on fail, load cache. Shows understanding of resilience patterns.)

5. **"Explain what `params` does in `requests.get(url, params=...)`."** (Answer: URL-encodes and appends query parameters safely. If they say "just concatenate the URL," they'll break on special characters.)

6. **"Design a visualization for a dataset. What must it include?"** (Answer: Title, axis labels, scale, legend (if needed). If they say "just plot it," they don't understand communication.)

7. **"How would you handle an API that requires different authentication than you've seen before?"** (Answer: Read the documentation. Different APIs have different auth schemes. If they try to apply a one-size-fits-all approach, they're not thinking critically.)

---

## Common Student Questions & How to Answer Them

**Q: "Should I use `response.json()` or `json.loads(response.text)`?"**
A: "Use `response.json()` — it's simpler and handles encoding automatically. Use `json.loads()` only if you need to parse a JSON string directly (not from an HTTP response)."

---

**Q: "My API calls are slow. How do I speed them up?"**
A: "Options: (1) Check if the API has pagination and you're fetching unnecessary data. (2) Use connection pooling (requests.Session). (3) Implement caching—save results locally. (4) Profile the API response time vs. your code. If the API is slow, there's not much you can do except use a faster API."

---

**Q: "What's the difference between headers and params?"**
A: "Params go in the URL (query string): `?key=value`. Headers go in the HTTP request header. Auth often uses headers (more secure). Data filtering often uses params. Check the API docs—each API has conventions."

---

**Q: "How do I know what to pass to a library function?"**
A: "Read the documentation! But start with the function signature: `help(function)` or `function?` in Jupyter. Then check examples. Most libraries have good docs and Stack Overflow answers."

---

**Q: "My plot looks bad. How do I make it better?"**
A: "Add: (1) title, (2) axis labels, (3) appropriate scale, (4) grid, (5) legend. Use larger fonts. Check that colors are distinct. Look at professional plots for inspiration. Design matters."

---

## Analogies That Work

**1. APIs and Contracts:**
"An API is a contract. You request something (GET /data), the server promises a response. But contracts can be broken—server is down, you hit rate limits, you're not authenticated. Always handle the cases where the contract breaks."

---

**2. Status Codes:**
"Status codes tell a story: 200 = 'I have what you want,' 404 = 'it doesn't exist,' 429 = 'you're asking too much, wait,' 500 = 'I'm broken, try later.' Each tells you how to respond."

---

**3. API Keys as Credentials:**
"An API key is like a credit card number. You wouldn't post your credit card in a public forum. Don't commit API keys to GitHub. Use environment variables like you'd use a wallet—carry it, don't broadcast it."

---

**4. Libraries as Tools:**
"A library is a pre-built tool. NumPy is a calculator for arrays; Matplotlib is a paintbrush for graphs. Understanding how the tool works (NumPy's broadcasting, Matplotlib's figure/axes structure) is key to using it well."

---

**5. Visualization and Communication:**
"A plot without labels is like a conversation without context. The other person doesn't know what you're talking about. Add titles, labels, and legends so your data tells a story."

---

## Coding 1 Gaps to Watch For

Students enter Unit 6 with function and exception handling basics. Watch for:

**Gap 1: Dictionary Access**
- **What to watch for:** Students use `data['key']` and crash on missing keys.
- **Quick fix:** Teach `.get(key, default)`. Show the difference: `data['key']` crashes; `data.get('key', None)` is safe.

**Gap 2: Exception Specificity**
- **What to watch for:** Students use broad `except Exception:` instead of specific `requests.exceptions.Timeout`.
- **Quick fix:** Show each exception type and when it occurs. Practice catching different errors specifically.

**Gap 3: List vs. NumPy Operations**
- **What to watch for:** Students expect `[1, 2, 3] * 2` to multiply elements (it repeats instead).
- **Quick fix:** Show NumPy arrays do element-wise operations. Lists don't. Always check the type.

**Gap 4: Understanding JSON Structure**
- **What to watch for:** Students parse JSON but don't understand nested structure.
- **Quick fix:** Have them print `data` with indentation: `json.dumps(data, indent=2)`. Visualizing structure helps.

**Gap 5: String Formatting in URLs**
- **What to watch for:** Students concatenate URLs with f-strings and break on special characters.
- **Quick fix:** Use `params={}` dict. Let requests handle encoding. Always safer.

---

## Quick Troubleshooting Guide

| Problem | Most Likely Cause | Fix |
|---------|------------------|-----|
| `requests.exceptions.Timeout` | No timeout specified; request hangs | Add `timeout=5` parameter |
| `json.JSONDecodeError` | Response is not valid JSON | Check `response.text` first; validate format |
| `KeyError` accessing response data | Expected field is missing | Use `.get(key, default)` instead of `[key]` |
| API key exposed in code | Hardcoded in script | Move to environment variable; use `.env` file |
| Rate limited (429) repeatedly | Retrying immediately without delay | Add exponential backoff: `time.sleep(2**attempt)` |
| Plot has no labels | Forgot to add them | Add `ax.set_xlabel()`, `ax.set_ylabel()`, `ax.set_title()` |
| NumPy broadcasting error | Shape mismatch | Check array shapes with `.shape`; reshape if needed |
| Matplotlib plot not displaying | Not calling `plt.show()` | Add `plt.show()` or save with `plt.savefig()` |
| API returns unexpected structure | Not validating response | Validate keys exist and types are correct |
| HTTP 401 error | Authentication missing or wrong | Check API docs; use correct auth method and headers |

