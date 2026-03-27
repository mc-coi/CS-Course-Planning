# Day 3: The requests Library – GET Requests

**Learning Target:** I can use the requests library to make GET requests to an API and retrieve data.

---

## Key Concepts

**The requests Library:** A Python library that makes it easy to send HTTP requests. It's much simpler than built-in libraries like `urllib`.

**Basic GET Request:**
```
requests.get(url) → makes an HTTP GET request to the URL
```

**Response Object:** What `requests.get()` returns. It contains:
- `.status_code` — HTTP status code (200, 404, etc.)
- `.text` — Response as a string
- `.json()` — Response as a Python dictionary (if JSON)
- `.headers` — Metadata about the response

**URL Structure:**
```
https://api.example.com/endpoint?param1=value1&param2=value2
           ↑                      ↑                      ↑
       domain               endpoint            query parameters
```

---

## Code Examples

```python
import requests

# Make a GET request to a public API (no key needed)
response = requests.get("https://api.quotable.io/random")

# Check if the request was successful
print(response.status_code)  # 200 = success

# Get the response as a dictionary
data = response.json()
print(data["content"])       # Print the quote
print(data["author"])        # Print the author

# Another example: PokeAPI
response = requests.get("https://pokeapi.co/api/v2/pokemon/pikachu")
pokemon = response.json()
print(f"Name: {pokemon['name']}")
print(f"Height: {pokemon['height']}")
print(f"Weight: {pokemon['weight']}")
```

---

## Guided Practice

1. **Make a Request:** Write code to request a random quote from `https://api.quotable.io/random` and print the quote and author.

2. **Check Status:** Add a check: if the status code is 200, print "Success!" Otherwise, print the status code.

3. **Explore Data:** Request a Pokemon from the PokeAPI and print 3 different pieces of information about it.

4. **Handle the Response:** Make a request and use a try-except block to handle potential errors (we'll cover this more on Day 6).

---

## Practice Problems

**Beginner:** Write code that requests a random joke from `https://v2.jokeapi.dev/joke/Any` and prints the "setup" and "delivery" fields.

**Intermediate:** Create a function that takes a Pokemon name as input, makes an API request, and returns the Pokemon's type(s).

**Challenge:** Write a program that requests multiple Pokemon (e.g., Pikachu, Charmander, Bulbasaur) and prints a comparison of their heights and weights.

<details>
<summary>💡 Hints</summary>
- Remember to call `.json()` on the response to parse it as a dictionary
- Check `response.status_code == 200` to verify success
- Use a loop to request multiple Pokemon names
- The PokeAPI might return types as a list; access the first with `[0]`
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

response = requests.get("https://v2.jokeapi.dev/joke/Any")
joke = response.json()
print(joke["setup"])
print(joke["delivery"])
```

**Intermediate:**
```python
import requests

def get_pokemon_type(name):
    response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{name.lower()}")
    pokemon = response.json()
    types = [t["type"]["name"] for t in pokemon["types"]]
    return types

print(get_pokemon_type("Pikachu"))
```

**Challenge:**
```python
import requests

pokemon_list = ["pikachu", "charmander", "bulbasaur"]

for name in pokemon_list:
    response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{name}")
    pokemon = response.json()
    print(f"{pokemon['name']}: Height {pokemon['height']}, Weight {pokemon['weight']}")
```
</details>
