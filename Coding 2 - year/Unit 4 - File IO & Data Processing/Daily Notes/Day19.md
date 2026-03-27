# Day 19: JSON Lab — API Data Simulation
**Learning Target:** I can apply JSON skills to process real-world API-like data structures.

### Key Concepts

**API responses:** APIs typically return nested JSON with metadata and data arrays.

**Data structure patterns:** Common patterns include lists of objects, nested objects, and mixed types.

**Parsing and transformation:** Converting API data into usable formats.

**Error handling:** Dealing with missing fields or unexpected formats.

**Data extraction:** Pulling specific information from complex responses.

### Code Examples

```python
import json
import io

# Example 1: Simple API response simulation
api_response = '''
{
  "status": "success",
  "data": [
    {"id": 1, "name": "Alice", "email": "alice@example.com"},
    {"id": 2, "name": "Bob", "email": "bob@example.com"}
  ]
}
'''

f = io.StringIO(api_response)
response = json.load(f)

if response['status'] == 'success':
    for user in response['data']:
        print(f"{user['name']}: {user['email']}")

# Example 2: Extracting specific fields
json_text = '''
{
  "results": [
    {"title": "Article 1", "author": "Alice", "views": 150},
    {"title": "Article 2", "author": "Bob", "views": 320}
  ]
}
'''

f = io.StringIO(json_text)
data = json.load(f)

articles = [(article['title'], article['views']) for article in data['results']]
for title, views in articles:
    print(f"{title}: {views} views")

# Example 3: Weather API simulation
weather_api = '''
{
  "location": "New York",
  "forecast": [
    {
      "day": "Monday",
      "temperature": 72,
      "humidity": 65,
      "conditions": "Sunny"
    },
    {
      "day": "Tuesday",
      "temperature": 68,
      "humidity": 70,
      "conditions": "Cloudy"
    }
  ]
}
'''

f = io.StringIO(weather_api)
weather = json.load(f)

print(f"Forecast for {weather['location']}:")
for day_forecast in weather['forecast']:
    print(f"  {day_forecast['day']}: {day_forecast['temperature']}°F, {day_forecast['conditions']}")

# Example 4: Filtering API results
json_text = '''
{
  "products": [
    {"name": "Widget", "price": 19.99, "stock": 50},
    {"name": "Gadget", "price": 29.99, "stock": 0},
    {"name": "Device", "price": 49.99, "stock": 15}
  ]
}
'''

f = io.StringIO(json_text)
data = json.load(f)

# Get in-stock products
in_stock = [p for p in data['products'] if p['stock'] > 0]
print(f"Available products ({len(in_stock)}):")
for product in in_stock:
    print(f"  {product['name']}: ${product['price']}")

# Example 5: Computing statistics from API data
api_response = '''
{
  "employees": [
    {"name": "Alice", "salary": 70000, "department": "Engineering"},
    {"name": "Bob", "salary": 60000, "department": "Sales"},
    {"name": "Carol", "salary": 80000, "department": "Engineering"},
    {"name": "Dave", "salary": 55000, "department": "Sales"}
  ]
}
'''

f = io.StringIO(api_response)
data = json.load(f)

# Salary stats by department
depts = {}
for emp in data['employees']:
    dept = emp['department']
    if dept not in depts:
        depts[dept] = []
    depts[dept].append(emp['salary'])

for dept, salaries in depts.items():
    avg = sum(salaries) / len(salaries)
    print(f"{dept}: Average salary ${avg:,.0f}")

# Example 6: Pagination simulation (multiple API calls)
page1 = '''
{
  "data": [
    {"id": 1, "name": "Item 1"},
    {"id": 2, "name": "Item 2"}
  ],
  "next_page": true
}
'''

page2 = '''
{
  "data": [
    {"id": 3, "name": "Item 3"},
    {"id": 4, "name": "Item 4"}
  ],
  "next_page": false
}
'''

all_items = []

for page_text in [page1, page2]:
    f = io.StringIO(page_text)
    page = json.load(f)
    all_items.extend(page['data'])
    if not page['next_page']:
        break

print(f"Total items: {len(all_items)}")
for item in all_items:
    print(f"  {item['id']}: {item['name']}")

# Example 7: Nested API response
api_response = '''
{
  "status": "ok",
  "data": {
    "user": {
      "id": 123,
      "name": "Grace",
      "posts": [
        {"id": 1, "title": "First Post", "likes": 45},
        {"id": 2, "title": "Second Post", "likes": 67}
      ]
    }
  }
}
'''

f = io.StringIO(api_response)
response = json.load(f)

user = response['data']['user']
print(f"User: {user['name']}")
total_likes = sum(p['likes'] for p in user['posts'])
print(f"Total likes: {total_likes}")

# Example 8: Transforming API response
json_text = '''
{
  "movies": [
    {"title": "Movie A", "rating": 8.5, "genre": "Action"},
    {"title": "Movie B", "rating": 7.2, "genre": "Comedy"}
  ]
}
'''

f = io.StringIO(json_text)
data = json.load(f)

# Transform to simpler format
movies_list = [f"{m['title']} ({m['genre']}): {m['rating']}/10" for m in data['movies']]

for movie_str in movies_list:
    print(movie_str)

# Example 9: Error handling with API data
api_response = '''
{
  "status": "success",
  "data": [
    {"name": "Alice", "age": 25},
    {"name": "Bob"},
    {"name": "Carol", "age": 30}
  ]
}
'''

f = io.StringIO(api_response)
data = json.load(f)

for person in data['data']:
    name = person.get('name', 'Unknown')
    age = person.get('age', 'Not provided')
    print(f"{name}: Age {age}")

# Example 10: Complete API processing pipeline
def process_user_api_response(json_text):
    """Complete pipeline for processing user API response"""
    f = io.StringIO(json_text)
    response = json.load(f)

    results = {
        'total_users': 0,
        'active_users': 0,
        'user_list': []
    }

    for user in response['data']:
        results['total_users'] += 1
        if user.get('active', False):
            results['active_users'] += 1

        results['user_list'].append({
            'name': user['name'],
            'email': user.get('email', 'N/A'),
            'status': 'Active' if user.get('active') else 'Inactive'
        })

    return results

test_api = '''
{
  "data": [
    {"name": "Alice", "email": "alice@example.com", "active": true},
    {"name": "Bob", "email": "bob@example.com", "active": false},
    {"name": "Carol", "active": true}
  ]
}
'''

result = process_user_api_response(test_api)
print(f"Total users: {result['total_users']}")
print(f"Active users: {result['active_users']}")
for user in result['user_list']:
    print(f"  {user['name']}: {user['email']} ({user['status']})")
```

### Guided Practice

**Activity: Process an API-like Response**

1. Create JSON simulating a movie API response (list of movies with title, director, year, rating)
2. Read and process the data:
   - Count total movies
   - Find highest rated movie
   - Filter movies from recent years (2020+)
   - Calculate average rating
3. Display results

**Step-by-step code:**
```python
import json
import io

movies_api = '''
{
  "status": "success",
  "data": {
    "movies": [
      {"title": "Inception", "director": "Nolan", "year": 2010, "rating": 8.8},
      {"title": "Tenet", "director": "Nolan", "year": 2020, "rating": 7.3},
      {"title": "Oppenheimer", "director": "Nolan", "year": 2023, "rating": 8.5},
      {"title": "Dune", "director": "Villeneuve", "year": 2021, "rating": 8.0}
    ]
  }
}
'''

f = io.StringIO(movies_api)
response = json.load(f)
movies = response['data']['movies']

# Total movies
print(f"Total movies: {len(movies)}")

# Highest rated
highest = max(movies, key=lambda m: m['rating'])
print(f"Highest rated: {highest['title']} ({highest['rating']})")

# Recent movies (2020+)
recent = [m for m in movies if m['year'] >= 2020]
print(f"Recent movies ({len(recent)}):")
for m in recent:
    print(f"  {m['title']} ({m['year']})")

# Average rating
avg_rating = sum(m['rating'] for m in movies) / len(movies)
print(f"Average rating: {avg_rating:.2f}")
```

### Practice Problems

**Problem 1 — Beginner:** Write code that processes a simple API response (list of users) and extracts names.

**Problem 2 — Intermediate:** Write code that reads an API response with nested data, filters results, and calculates statistics.

**Problem 3 — Challenge:** Write a complete data processing system that simulates handling multiple API responses, combining data, and generating a report.

<details>
<summary>💡 Hints</summary>

**Problem 1:**
- Parse JSON with json.load().
- Extract names from user list.
- Print or return the names.

**Problem 2:**
- Access nested data structures.
- Use list comprehension to filter.
- Calculate sum/average/count.

**Problem 3:**
- Process multiple JSON inputs.
- Combine data from different sources.
- Generate formatted output.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
import json
import io

# Problem 1
api_response = '{"users": [{"name": "Alice"}, {"name": "Bob"}, {"name": "Carol"}]}'
f = io.StringIO(api_response)
data = json.load(f)
names = [u['name'] for u in data['users']]
print(names)

# Problem 2
api_response = '''
{
  "employees": [
    {"name": "Alice", "salary": 70000, "dept": "Eng"},
    {"name": "Bob", "salary": 60000, "dept": "Sales"},
    {"name": "Carol", "salary": 80000, "dept": "Eng"}
  ]
}
'''
f = io.StringIO(api_response)
data = json.load(f)

eng_salaries = [e['salary'] for e in data['employees'] if e['dept'] == 'Eng']
avg = sum(eng_salaries) / len(eng_salaries)
print(f"Engineering avg salary: ${avg}")

# Problem 3
api1 = '{"students": [{"name": "Alice", "id": 1}, {"name": "Bob", "id": 2}]}'
api2 = '{"grades": [{"id": 1, "grade": "A"}, {"id": 2, "grade": "B"}]}'

f1 = io.StringIO(api1)
f2 = io.StringIO(api2)

students = json.load(f1)['students']
grades = json.load(f2)['grades']

grades_dict = {g['id']: g['grade'] for g in grades}

for student in students:
    grade = grades_dict.get(student['id'], 'N/A')
    print(f"{student['name']}: {grade}")
```

</details>
