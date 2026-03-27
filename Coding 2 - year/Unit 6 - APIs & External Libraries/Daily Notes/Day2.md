# Day 2: HTTP Methods & JSON Review

**Learning Target:** I can explain the main HTTP methods (GET, POST) and parse JSON data structures.

---

## Key Concepts

**HTTP Methods:** The action you want to perform on a resource:
- **GET:** Retrieve data from the server (safe, read-only)
- **POST:** Submit data to the server (creates new data)
- **PUT:** Update existing data
- **DELETE:** Remove data

Most beginner API work focuses on **GET** and **POST**.

**HTTP Status Codes:** Numbers the server sends back to indicate the result:
- **2xx (Success):** Request worked (e.g., 200 OK, 201 Created)
- **3xx (Redirect):** Request needs further action
- **4xx (Client Error):** Problem with your request (e.g., 404 Not Found, 403 Forbidden)
- **5xx (Server Error):** Problem on the server side

**JSON (Review):** A text format for storing data as key-value pairs, very similar to Python dictionaries.

```json
{
  "name": "Pikachu",
  "type": "electric",
  "hp": 35,
  "moves": ["thunderbolt", "quick-attack"]
}
```

In Python, you'd parse this as a dictionary:
```python
pokemon = {
    "name": "Pikachu",
    "type": "electric",
    "hp": 35,
    "moves": ["thunderbolt", "quick-attack"]
}
```

---

## Code Examples

```python
# JSON parsing in Python
import json

# JSON string (like what an API might return)
json_string = '{"name": "Pikachu", "type": "electric", "hp": 35}'

# Convert JSON string to Python dictionary
pokemon = json.loads(json_string)
print(pokemon["name"])        # Output: Pikachu
print(pokemon["type"])        # Output: electric

# Convert Python dictionary to JSON string
data = {"name": "Charmander", "type": "fire"}
json_output = json.dumps(data)
print(json_output)            # Output: {"name": "Charmander", "type": "fire"}
```

---

## Guided Practice

1. **Parse JSON:** Given the JSON string below, write Python code to extract the name and score:
   ```json
   {"name": "Alex", "score": 95, "grade": "A"}
   ```

2. **Create JSON:** Write a Python dictionary for a video game character and convert it to JSON.

3. **Predict Status Codes:** For each scenario, predict the HTTP status code:
   - User requests a valid resource → ?
   - User requests a resource that doesn't exist → ?
   - Server has an internal error → ?

4. **Method Selection:** For each action, choose GET or POST:
   - Fetch a list of books from a library API → ?
   - Submit a new book review → ?

---

## Practice Problems

**Beginner:** Convert this Python dictionary to a JSON string:
```python
student = {"name": "Jordan", "grade": 10, "gpa": 3.8}
```

**Intermediate:** Parse this JSON and calculate the total score:
```python
json_data = '{"scores": [85, 92, 78, 88]}'
```

**Challenge:** Write a function that takes a dictionary and returns a formatted JSON string (pretty-printed with indentation).

<details>
<summary>💡 Hints</summary>
- Use `json.dumps()` to convert dict to JSON string
- Use `json.loads()` to convert JSON string to dict
- `json.dumps()` has a `indent` parameter for pretty-printing
- To get total, use `sum()` on the list of scores
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import json
student = {"name": "Jordan", "grade": 10, "gpa": 3.8}
json_string = json.dumps(student)
print(json_string)  # {"name": "Jordan", "grade": 10, "gpa": 3.8}
```

**Intermediate:**
```python
import json
json_data = '{"scores": [85, 92, 78, 88]}'
data = json.loads(json_data)
total = sum(data["scores"])
print(total)  # 343
```

**Challenge:**
```python
import json

def format_json(data):
    return json.dumps(data, indent=2)

# Usage
student = {"name": "Jordan", "grade": 10}
print(format_json(student))
```
</details>
