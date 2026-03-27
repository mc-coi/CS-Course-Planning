# Day 5: OOP Lab 1 — Building Simple Classes
**Learning Target:** I can design and build complete classes with constructors, instance variables, class variables, and methods.

### Key Concepts

**Class Design:** Planning a class by identifying: what data it needs (attributes), what actions it performs (methods), and what behavior is shared (class variables).

**Complete Class:** A well-structured class with `__init__`, relevant instance variables, useful methods, and proper encapsulation.

**Lab Project:** A comprehensive coding exercise that brings together multiple OOP concepts.

### Lab Activities

#### Activity 1: Build a Student Management System

**Objective:** Create a `Student` class that manages student information and grades.

**Requirements:**
- Class should have instance variables: `name`, `student_id`, `grade_level`, `grades` (list)
- Add a class variable: `total_students` (counts all students created)
- Include these methods:
  - `add_grade(grade)` — adds a grade to the list
  - `get_average()` — returns the average of all grades
  - `get_status()` — returns "Passing" if average >= 70, else "Failing"
  - `display_info()` — prints student information including average and status

**Starter Code:**
```python
class Student:
    total_students = 0

    def __init__(self, name, student_id, grade_level):
        # YOUR CODE HERE
        pass

    def add_grade(self, grade):
        # YOUR CODE HERE
        pass

    def get_average(self):
        # YOUR CODE HERE
        pass

    def get_status(self):
        # YOUR CODE HERE
        pass

    def display_info(self):
        # YOUR CODE HERE
        pass

# Test your code
alice = Student("Alice Johnson", "S001", 10)
alice.add_grade(85)
alice.add_grade(90)
alice.add_grade(88)
alice.display_info()

bob = Student("Bob Smith", "S002", 10)
bob.add_grade(65)
bob.add_grade(70)
bob.add_grade(68)
bob.display_info()

print(f"Total students created: {Student.total_students}")
```

**Expected Output:**
```
Name: Alice Johnson
ID: S001
Grade: 10
Average: 87.67
Status: Passing

Name: Bob Smith
ID: S002
Grade: 10
Average: 67.67
Status: Failing

Total students created: 2
```

**Solution:**
```python
class Student:
    total_students = 0

    def __init__(self, name, student_id, grade_level):
        self.name = name
        self.student_id = student_id
        self.grade_level = grade_level
        self.grades = []
        Student.total_students = Student.total_students + 1

    def add_grade(self, grade):
        self.grades.append(grade)

    def get_average(self):
        if len(self.grades) == 0:
            return 0
        return sum(self.grades) / len(self.grades)

    def get_status(self):
        average = self.get_average()
        if average >= 70:
            return "Passing"
        else:
            return "Failing"

    def display_info(self):
        print(f"Name: {self.name}")
        print(f"ID: {self.student_id}")
        print(f"Grade: {self.grade_level}")
        avg = self.get_average()
        print(f"Average: {avg:.2f}")
        print(f"Status: {self.get_status()}")
        print()

alice = Student("Alice Johnson", "S001", 10)
alice.add_grade(85)
alice.add_grade(90)
alice.add_grade(88)
alice.display_info()

bob = Student("Bob Smith", "S002", 10)
bob.add_grade(65)
bob.add_grade(70)
bob.add_grade(68)
bob.display_info()

print(f"Total students created: {Student.total_students}")
```

---

#### Activity 2: Build a Shopping Cart

**Objective:** Create a `ShoppingCart` class that manages products and prices.

**Requirements:**
- Class should have instance variables: `customer_name`, `items` (list of dictionaries with name and price)
- Add these methods:
  - `add_item(name, price)` — adds an item to the cart
  - `remove_item(name)` — removes the first item with that name
  - `get_total()` — returns the total cost
  - `apply_discount(percent)` — applies a percentage discount to total
  - `display_cart()` — prints all items and the total

**Starter Code:**
```python
class ShoppingCart:
    def __init__(self, customer_name):
        # YOUR CODE HERE
        pass

    def add_item(self, name, price):
        # YOUR CODE HERE
        pass

    def remove_item(self, name):
        # YOUR CODE HERE
        pass

    def get_total(self):
        # YOUR CODE HERE
        pass

    def apply_discount(self, percent):
        # YOUR CODE HERE
        pass

    def display_cart(self):
        # YOUR CODE HERE
        pass

# Test your code
cart = ShoppingCart("Alice")
cart.add_item("Laptop", 999.99)
cart.add_item("Mouse", 29.99)
cart.add_item("Keyboard", 79.99)
cart.display_cart()

print(f"Total with 10% discount: ${cart.get_total() * 0.9:.2f}")
```

**Expected Output:**
```
Shopping Cart for Alice
Laptop: $999.99
Mouse: $29.99
Keyboard: $79.99
Total: $1109.97

Total with 10% discount: $998.97
```

**Solution:**
```python
class ShoppingCart:
    def __init__(self, customer_name):
        self.customer_name = customer_name
        self.items = []

    def add_item(self, name, price):
        self.items.append({"name": name, "price": price})

    def remove_item(self, name):
        for i in range(len(self.items)):
            if self.items[i]["name"] == name:
                self.items.pop(i)
                break

    def get_total(self):
        total = 0
        for item in self.items:
            total = total + item["price"]
        return total

    def apply_discount(self, percent):
        discount_amount = self.get_total() * (percent / 100)
        return self.get_total() - discount_amount

    def display_cart(self):
        print(f"Shopping Cart for {self.customer_name}")
        for item in self.items:
            print(f"{item['name']}: ${item['price']:.2f}")
        print(f"Total: ${self.get_total():.2f}")
        print()

cart = ShoppingCart("Alice")
cart.add_item("Laptop", 999.99)
cart.add_item("Mouse", 29.99)
cart.add_item("Keyboard", 79.99)
cart.display_cart()

print(f"Total with 10% discount: ${cart.apply_discount(10):.2f}")
```

---

#### Activity 3: Build a Music Playlist

**Objective:** Create a `Song` and `Playlist` class to manage songs.

**Requirements for Song class:**
- Instance variables: `title`, `artist`, `duration` (in seconds)
- Method: `get_duration_formatted()` — returns "MM:SS" format

**Requirements for Playlist class:**
- Class variable: `total_playlists` (count all playlists)
- Instance variables: `name`, `songs` (list of Song objects)
- Methods:
  - `add_song(song)` — adds a Song to the playlist
  - `remove_song(title)` — removes a song by title
  - `get_total_duration()` — returns total time in seconds
  - `display_playlist()` — shows all songs with info

**Starter Code:**
```python
class Song:
    def __init__(self, title, artist, duration):
        # YOUR CODE HERE
        pass

    def get_duration_formatted(self):
        # YOUR CODE HERE
        pass

class Playlist:
    total_playlists = 0

    def __init__(self, name):
        # YOUR CODE HERE
        pass

    def add_song(self, song):
        # YOUR CODE HERE
        pass

    def remove_song(self, title):
        # YOUR CODE HERE
        pass

    def get_total_duration(self):
        # YOUR CODE HERE
        pass

    def display_playlist(self):
        # YOUR CODE HERE
        pass

# Test your code
song1 = Song("Imagine", "John Lennon", 183)
song2 = Song("Hey Jude", "The Beatles", 431)
song3 = Song("Bohemian Rhapsody", "Queen", 354)

playlist = Playlist("Classics")
playlist.add_song(song1)
playlist.add_song(song2)
playlist.add_song(song3)
playlist.display_playlist()
```

**Expected Output:**
```
Playlist: Classics
1. Imagine - John Lennon (3:03)
2. Hey Jude - The Beatles (7:11)
3. Bohemian Rhapsody - Queen (5:54)
Total duration: 16:08
Total playlists created: 1
```

**Solution:**
```python
class Song:
    def __init__(self, title, artist, duration):
        self.title = title
        self.artist = artist
        self.duration = duration

    def get_duration_formatted(self):
        minutes = self.duration // 60
        seconds = self.duration % 60
        return f"{minutes}:{seconds:02d}"

class Playlist:
    total_playlists = 0

    def __init__(self, name):
        self.name = name
        self.songs = []
        Playlist.total_playlists = Playlist.total_playlists + 1

    def add_song(self, song):
        self.songs.append(song)

    def remove_song(self, title):
        for i in range(len(self.songs)):
            if self.songs[i].title == title:
                self.songs.pop(i)
                break

    def get_total_duration(self):
        total = 0
        for song in self.songs:
            total = total + song.duration
        return total

    def display_playlist(self):
        print(f"Playlist: {self.name}")
        for i in range(len(self.songs)):
            song = self.songs[i]
            print(f"{i + 1}. {song.title} - {song.artist} ({song.get_duration_formatted()})")

        total_duration = self.get_total_duration()
        minutes = total_duration // 60
        seconds = total_duration % 60
        print(f"Total duration: {minutes}:{seconds:02d}")
        print(f"Total playlists created: {Playlist.total_playlists}")
        print()

song1 = Song("Imagine", "John Lennon", 183)
song2 = Song("Hey Jude", "The Beatles", 431)
song3 = Song("Bohemian Rhapsody", "Queen", 354)

playlist = Playlist("Classics")
playlist.add_song(song1)
playlist.add_song(song2)
playlist.add_song(song3)
playlist.display_playlist()
```

---

### Reflection Questions

After completing these activities, answer the following:

1. **What challenges did you face when designing the classes? How did you solve them?**
2. **How would you extend the Student class to track attendance or handle weighted grades?**
3. **What additional features might be useful in a ShoppingCart (taxes, coupons, etc.)?**
4. **How could the Playlist system be expanded to support multiple users or albums?**

### Practice Extension Problems

**Extension 1:** Add a method to the Student class that returns the letter grade (A, B, C, D, F) based on the average.

**Extension 2:** Add the ability to apply multiple discounts to ShoppingCart and track the original vs. discounted price.

**Extension 3:** Add a shuffle method to Playlist that randomizes the song order.

**Extension 4:** Create a sorted method for Playlist that sorts songs by duration or artist name.
