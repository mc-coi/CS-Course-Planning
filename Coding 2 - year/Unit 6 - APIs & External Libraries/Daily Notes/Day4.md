# Day 4: Parsing JSON Responses

**Learning Target:** I can navigate nested JSON structures and extract specific data from API responses.

---

## Key Concepts

**Nested JSON:** JSON can contain objects within objects, lists within objects, etc. You access them by chaining brackets.

```json
{
  "weather": {
    "temperature": 72,
    "condition": "sunny"
  },
  "location": "New York"
}
```

In Python:
```python
data["weather"]["temperature"]  # Access nested object
data["weather"]["condition"]     # Access another field
data["location"]                 # Access top-level field
```

**Lists in JSON:** APIs often return lists of objects. Use loops to iterate.

```json
{
  "pokemon": [
    {"name": "Pikachu", "type": "electric"},
    {"name": "Charmander", "type": "fire"}
  ]
}
```

---

## Code Examples

```python
import requests

# Get a random quote (simple structure)
response = requests.get("https://api.quotable.io/random")
quote = response.json()
print(quote["content"])         # The quote text
print(quote["author"])          # The author name

# Get a Pokemon with nested data
response = requests.get("https://pokeapi.co/api/v2/pokemon/pikachu")
pokemon = response.json()

# Access nested data
name = pokemon["name"]
stats = pokemon["stats"]  # This is a list of stat objects

# Loop through stats
for stat in stats:
    stat_name = stat["stat"]["name"]     # Nested object!
    base_value = stat["base_stat"]
    print(f"{stat_name}: {base_value}")
```

---

## Guided Practice

1. **Simple Access:** Request a cat fact from `https://catfact.ninja/fact`. Extract and print the "fact" field.

2. **Nested Access:** Request a Pokemon and access its `stats` field. Print the name and base value of the first stat.

3. **Loop Through Lists:** Request a Pokemon and iterate through its `abilities`. Print each ability name.

4. **Combine Operations:** Request a Pokemon, extract the name and first type, and print them in a formatted string.

---

## Practice Problems

**Beginner:** Request data from `https://api.quotable.io/random` and print the quote in this format: `"[quote]" — [author]`

**Intermediate:** Write a function that takes a Pokemon name and returns a list of all its abilities (names only).

**Challenge:** Request a Pokemon and create a summary string that includes the name, height, weight, and a list of its types.

<details>
<summary>💡 Hints</summary>
- Use nested brackets: `data["outer"]["inner"]`
- For lists, use a for loop: `for item in data["list"]:`
- Remember to call `.json()` on the response
- The `types` field is a list of dictionaries with structure like `{"type": {"name": "electric"}}`
</details>

<details>
<summary>✅ Sample Answers</summary>

**Beginner:**
```python
import requests

response = requests.get("https://api.quotable.io/random")
quote = response.json()
print(f'"{quote["content"]}" — {quote["author"]}')
```

**Intermediate:**
```python
import requests

def get_abilities(pokemon_name):
    response = requests.get(f"https://pokeapi.co/api/v2/pokemon/{pokemon_name.lower()}")
    pokemon = response.json()
    abilities = [ability["ability"]["name"] for ability in pokemon["abilities"]]
    return abilities

print(get_abilities("Pikachu"))
```

**Challenge:**
```python
import requests

response = requests.get("https://pokeapi.co/api/v2/pokemon/pikachu")
pokemon = response.json()

types = [t["type"]["name"] for t in pokemon["types"]]
summary = f"""
Name: {pokemon['name']}
Height: {pokemon['height']}
Weight: {pokemon['weight']}
Types: {', '.join(types)}
"""
print(summary)
```
</details>
