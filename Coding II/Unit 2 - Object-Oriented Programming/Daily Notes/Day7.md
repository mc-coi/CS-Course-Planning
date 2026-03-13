# Day 7: Polymorphism & Method Overriding
**Learning Target:** I can override methods and implement polymorphism.

### Key Concepts
**Polymorphism** means "many forms." Multiple classes can have the same method name with different implementations.

### Code Examples
```python
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

shapes = [Rectangle(5, 10), Circle(3)]
for shape in shapes:
    print(shape.area())  # Calls the right area() for each type
```

### Guided Practice
Create an Employee hierarchy where different employee types calculate pay differently.

### Practice Problems
**Problem 1 — Beginner:** Create a method in parent that child classes override.

**Problem 2 — Intermediate:** Create multiple shapes that override a common method.

**Problem 3 — Challenge:** Create a media player with different format classes (MP3, Video, Audio) that handle playback differently.

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 & 2 covered in code example

# Problem 3 (partial)
class MediaPlayer:
    def play(self):
        pass

class MP3Player(MediaPlayer):
    def play(self):
        print("Playing audio file...")
```
</details>

---
