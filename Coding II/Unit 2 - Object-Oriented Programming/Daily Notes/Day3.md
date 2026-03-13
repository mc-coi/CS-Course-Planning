# Day 3: Instance Methods
**Learning Target:** I can define and call instance methods that operate on object data.

### Key Concepts
Instance methods are functions defined in a class that operate on instance data. They have access to `self` and can modify the object's state.

### Code Examples
```python
class Playlist:
    def __init__(self, name):
        self.name = name
        self.songs = []

    def add_song(self, song):
        self.songs.append(song)
        print(f"Added '{song}' to {self.name}")

    def remove_song(self, song):
        if song in self.songs:
            self.songs.remove(song)

    def play(self):
        for song in self.songs:
            print(f"Playing {song}")

    def song_count(self):
        return len(self.songs)

playlist = Playlist("Rock Classics")
playlist.add_song("Bohemian Rhapsody")
playlist.add_song("Stairway to Heaven")
print(playlist.song_count())  # 2
playlist.play()
```

### Guided Practice
Create a TodoList class with methods to add tasks, complete tasks, and display all tasks.

### Practice Problems
**Problem 1 — Beginner:** Create a Stack class with push() and pop() methods.

**Problem 2 — Intermediate:** Create a Library class that tracks books and allows adding/removing/searching.

**Problem 3 — Challenge:** Create a ShoppingCart class with methods to add items, remove items, calculate total price with tax.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

# Problem 2
class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title):
        self.books.append(title)

    def search(self, title):
        return title in self.books
```
</details>

---
