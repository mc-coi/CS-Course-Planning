# Day 1: Introduction to OOP — Classes, Objects, Attributes
**Learning Target:** I can create classes, instantiate objects, and define attributes to model real-world concepts.

### Key Concepts

**Object-Oriented Programming (OOP):** A programming paradigm that organizes code around "objects" that combine data (attributes) and behavior (methods). This models real-world entities and their interactions.

**Class:** A blueprint or template for creating objects. It defines what attributes and methods objects of that class will have.

**Object (Instance):** A specific, concrete instantiation of a class. Each object has its own independent set of attribute values.

**Attribute:** A variable that belongs to an object and stores data about it. Also called a property or instance variable.

**Instantiation:** The process of creating a new object from a class using the class name followed by parentheses.

### Code Examples

```python
# Define a simple class
class Dog:
    pass

# Create an object (instantiate the class)
my_dog = Dog()

print(type(my_dog))  # <class '__main__.Dog'>
print(my_dog)  # <__main__.Dog object at 0x...>

# A more practical example: Student class
class Student:
    pass

# Create student objects
alice = Student()
bob = Student()

# Add attributes directly to objects
alice.name = "Alice"
alice.grade = 10
alice.gpa = 3.8

bob.name = "Bob"
bob.grade = 11
bob.gpa = 3.5

# Access attributes
print(alice.name)  # Alice
print(bob.gpa)     # 3.5

# Different objects have different values
print(alice.grade)  # 10
print(bob.grade)    # 11

# Real-world example: Rectangle class
class Rectangle:
    pass

rect1 = Rectangle()
rect1.width = 5
rect1.height = 3

rect2 = Rectangle()
rect2.width = 10
rect2.height = 8

# We can calculate attributes from other attributes
area1 = rect1.width * rect1.height
area2 = rect2.width * rect2.height

print(f"Rectangle 1 area: {area1}")  # Rectangle 1 area: 15
print(f"Rectangle 2 area: {area2}")  # Rectangle 2 area: 80

# Another example: Car class
class Car:
    pass

car1 = Car()
car1.brand = "Toyota"
car1.model = "Camry"
car1.year = 2022
car1.color = "silver"
car1.mileage = 45000

car2 = Car()
car2.brand = "Honda"
car2.model = "Civic"
car2.year = 2024
car2.color = "blue"
car2.mileage = 5000

print(f"{car1.year} {car1.brand} {car1.model}")  # 2022 Toyota Camry
print(f"{car2.year} {car2.brand} {car2.model}")  # 2024 Honda Civic
```

### Guided Practice

**Activity: Create a Book Class**

Follow these steps in class:

1. Define a class called `Book`
2. Create two book objects: `book1` and `book2`
3. For `book1`, add attributes: `title`, `author`, `pages`, `year_published`
4. For `book2`, add the same attributes with different values
5. Print all attributes of both books
6. Create a third book object and add attributes to it

**Expected Output:**
```
The Great Gatsby by F. Scott Fitzgerald (180 pages, published 1925)
To Kill a Mockingbird by Harper Lee (281 pages, published 1960)
1984 by George Orwell (328 pages, published 1949)
```

**Solution:**
```python
class Book:
    pass

book1 = Book()
book1.title = "The Great Gatsby"
book1.author = "F. Scott Fitzgerald"
book1.pages = 180
book1.year_published = 1925

book2 = Book()
book2.title = "To Kill a Mockingbird"
book2.author = "Harper Lee"
book2.pages = 281
book2.year_published = 1960

book3 = Book()
book3.title = "1984"
book3.author = "George Orwell"
book3.pages = 328
book3.year_published = 1949

print(f"{book1.title} by {book1.author} ({book1.pages} pages, published {book1.year_published})")
print(f"{book2.title} by {book2.author} ({book2.pages} pages, published {book2.year_published})")
print(f"{book3.title} by {book3.author} ({book3.pages} pages, published {book3.year_published})")
```

### Practice Problems

**Problem 1 — Beginner:** Create a class called `Animal`. Create two animal objects and assign these attributes to each: `name`, `species`, `age`. Print the attributes for both animals.

**Problem 2 — Intermediate:** Create a class called `BankAccount`. Create three account objects. For each, assign: `account_holder`, `account_number`, `balance`. Calculate the total balance across all three accounts and print it.

**Problem 3 — Challenge:** Create a class called `Movie`. Create a list of 5 movie objects, each with attributes: `title`, `director`, `year`, `rating`, `budget`. Find and print the movie with the highest rating and the movie with the largest budget.

<details>
<summary>💡 Hints</summary>

**Hint 1:** Remember that you can create a class with just `pass` inside if you want to add attributes later.

**Hint 2:** For Problem 2, you can add the three `balance` values together. Try storing each account object in a variable.

**Hint 3:** For Problem 3, you'll need to compare attributes using `>` and `<` operators. Try using a loop to go through all movie objects.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Animal:
    pass

animal1 = Animal()
animal1.name = "Leo"
animal1.species = "Lion"
animal1.age = 8

animal2 = Animal()
animal2.name = "Ellie"
animal2.species = "Elephant"
animal2.age = 15

print(f"{animal1.name} the {animal1.species} is {animal1.age} years old")
print(f"{animal2.name} the {animal2.species} is {animal2.age} years old")

# Problem 2
class BankAccount:
    pass

account1 = BankAccount()
account1.account_holder = "Alice"
account1.account_number = "1001"
account1.balance = 5000

account2 = BankAccount()
account2.account_holder = "Bob"
account2.account_number = "1002"
account2.balance = 7500

account3 = BankAccount()
account3.account_holder = "Charlie"
account3.account_number = "1003"
account3.balance = 3200

total = account1.balance + account2.balance + account3.balance
print(f"Total balance: ${total}")

# Problem 3
class Movie:
    pass

movie1 = Movie()
movie1.title = "Inception"
movie1.director = "Christopher Nolan"
movie1.year = 2010
movie1.rating = 8.8
movie1.budget = 160000000

movie2 = Movie()
movie2.title = "The Shawshank Redemption"
movie2.director = "Frank Darabont"
movie2.year = 1994
movie2.rating = 9.3
movie2.budget = 25000000

movie3 = Movie()
movie3.title = "Avatar"
movie3.director = "James Cameron"
movie3.year = 2009
movie3.rating = 7.8
movie3.budget = 237000000

movie4 = Movie()
movie4.title = "Interstellar"
movie4.director = "Christopher Nolan"
movie4.year = 2014
movie4.rating = 8.6
movie4.budget = 165000000

movie5 = Movie()
movie5.title = "The Dark Knight"
movie5.director = "Christopher Nolan"
movie5.year = 2008
movie5.rating = 9.0
movie5.budget = 185000000

movies = [movie1, movie2, movie3, movie4, movie5]

highest_rated = movies[0]
for movie in movies:
    if movie.rating > highest_rated.rating:
        highest_rated = movie

largest_budget = movies[0]
for movie in movies:
    if movie.budget > largest_budget.budget:
        largest_budget = movie

print(f"Highest rated: {highest_rated.title} ({highest_rated.rating})")
print(f"Largest budget: {largest_budget.title} (${largest_budget.budget:,})")
```

</details>
