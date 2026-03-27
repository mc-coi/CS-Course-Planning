# Day 14: Inheritance Lab
**Learning Target:** I can design and implement complex class hierarchies using inheritance, overriding, and super().

### Lab Activities

#### Activity 1: Build a Game Character System

**Objective:** Create a comprehensive character system with multiple character types using inheritance.

**Requirements:**
- `Character` (base class): health, mana, level, experience
- `Warrior(Character)`: armor, strength
- `Mage(Character)`: spell_power, mana_regen
- `Rogue(Character)`: dodge_chance, critical_chance
- Each should override `take_damage()`, `level_up()`, and have unique methods

**Starter Code:**
```python
class Character:
    def __init__(self, name, health, mana, level=1):
        self.name = name
        self.health = health
        self.max_health = health
        self.mana = mana
        self.max_mana = mana
        self.level = level
        self.experience = 0

    def take_damage(self, damage):
        self.health = max(0, self.health - damage)

    def level_up(self):
        self.level = self.level + 1
        self.max_health = self.max_health + 20
        self.health = self.max_health
        self.max_mana = self.max_mana + 10
        self.mana = self.max_mana

    def gain_experience(self, amount):
        self.experience = self.experience + amount
        if self.experience >= 100:
            self.level_up()
            self.experience = 0

    def status(self):
        print(f"{self.name} - Level {self.level}, HP {self.health}/{self.max_health}, MP {self.mana}/{self.max_mana}")

class Warrior(Character):
    def __init__(self, name, health, mana, armor, strength):
        super().__init__(name, health, mana)
        self.armor = armor
        self.strength = strength

    def take_damage(self, damage):
        # YOUR CODE: reduce damage by armor
        pass

    def power_attack(self):
        # YOUR CODE: deal damage based on strength
        pass

class Mage(Character):
    def __init__(self, name, health, mana, spell_power, mana_regen):
        super().__init__(name, health, mana)
        self.spell_power = spell_power
        self.mana_regen = mana_regen

    def cast_spell(self, cost):
        # YOUR CODE: check if enough mana, cast if yes
        pass

    def regenerate_mana(self):
        # YOUR CODE: restore mana
        pass

class Rogue(Character):
    def __init__(self, name, health, mana, dodge_chance, critical_chance):
        super().__init__(name, health, mana)
        self.dodge_chance = dodge_chance
        self.critical_chance = critical_chance

    def take_damage(self, damage):
        # YOUR CODE: chance to dodge
        pass

    def backstab(self):
        # YOUR CODE: high damage with crit chance
        pass

# Test your code
warrior = Warrior("Conan", 100, 20, 10, 15)
mage = Mage("Merlin", 60, 100, 20, 5)
rogue = Rogue("Assassin", 70, 30, 0.3, 0.25)

warrior.status()
mage.status()
rogue.status()

warrior.take_damage(25)
warrior.status()

mage.cast_spell(30)
mage.status()
```

**Expected Output:**
```
Conan - Level 1, HP 100/100, MP 20/20
Merlin - Level 1, HP 60/60, MP 100/100
Assassin - Level 1, HP 70/70, MP 30/30

Conan - Level 1, HP 77/100, MP 20/20
Merlin cast spell!
Merlin - Level 1, HP 60/60, MP 70/100
```

**Solution:**
```python
import random

class Character:
    def __init__(self, name, health, mana, level=1):
        self.name = name
        self.health = health
        self.max_health = health
        self.mana = mana
        self.max_mana = mana
        self.level = level
        self.experience = 0

    def take_damage(self, damage):
        self.health = max(0, self.health - damage)

    def level_up(self):
        self.level = self.level + 1
        self.max_health = self.max_health + 20
        self.health = self.max_health
        self.max_mana = self.max_mana + 10
        self.mana = self.max_mana

    def gain_experience(self, amount):
        self.experience = self.experience + amount
        if self.experience >= 100:
            self.level_up()
            self.experience = 0

    def status(self):
        print(f"{self.name} - Level {self.level}, HP {self.health}/{self.max_health}, MP {self.mana}/{self.max_mana}")

class Warrior(Character):
    def __init__(self, name, health, mana, armor, strength):
        super().__init__(name, health, mana)
        self.armor = armor
        self.strength = strength

    def take_damage(self, damage):
        reduced_damage = max(1, damage - self.armor)
        super().take_damage(reduced_damage)
        print(f"{self.name} armor reduces damage to {reduced_damage}")

    def power_attack(self, target):
        damage = self.strength * 2
        target.take_damage(damage)
        print(f"{self.name} power attacks for {damage} damage!")

class Mage(Character):
    def __init__(self, name, health, mana, spell_power, mana_regen):
        super().__init__(name, health, mana)
        self.spell_power = spell_power
        self.mana_regen = mana_regen

    def cast_spell(self, cost):
        if self.mana >= cost:
            self.mana = self.mana - cost
            print(f"{self.name} cast spell!")
            return True
        else:
            print(f"{self.name} not enough mana!")
            return False

    def regenerate_mana(self):
        self.mana = min(self.max_mana, self.mana + self.mana_regen)
        print(f"{self.name} regenerated mana")

class Rogue(Character):
    def __init__(self, name, health, mana, dodge_chance, critical_chance):
        super().__init__(name, health, mana)
        self.dodge_chance = dodge_chance
        self.critical_chance = critical_chance

    def take_damage(self, damage):
        if random.random() < self.dodge_chance:
            print(f"{self.name} dodged!")
            return
        super().take_damage(damage)

    def backstab(self, target):
        damage = 25
        if random.random() < self.critical_chance:
            damage = damage * 2
            print(f"{self.name} critical backstab!")
        else:
            print(f"{self.name} backstabs!")
        target.take_damage(damage)

warrior = Warrior("Conan", 100, 20, 10, 15)
mage = Mage("Merlin", 60, 100, 20, 5)
rogue = Rogue("Assassin", 70, 30, 0.3, 0.25)

warrior.status()
mage.status()
rogue.status()

warrior.take_damage(25)
warrior.status()

mage.cast_spell(30)
mage.status()
```

---

#### Activity 2: Build a File Management System

**Objective:** Create a file hierarchy with different file types inheriting from a base File class.

**Requirements:**
- `File` (base): name, size, created_date
- `TextFile(File)`: encoding, line_count
- `ImageFile(File)`: resolution, format
- `VideoFile(File)`: duration, bitrate
- Each should override `get_info()` and `open()`

**Starter Code:**
```python
from datetime import datetime

class File:
    def __init__(self, name, size):
        self.name = name
        self.size = size
        self.created_date = datetime.now()

    def get_info(self):
        return f"{self.name} ({self.size} bytes)"

    def open(self):
        print(f"Opening {self.name}...")

class TextFile(File):
    def __init__(self, name, size, encoding, line_count):
        super().__init__(name, size)
        self.encoding = encoding
        self.line_count = line_count

    def get_info(self):
        base = super().get_info()
        return f"{base}, {self.line_count} lines, {self.encoding}"

    def open(self):
        super().open()
        print(f"Text editor opened {self.name}")

class ImageFile(File):
    def __init__(self, name, size, resolution, format_type):
        super().__init__(name, size)
        self.resolution = resolution
        self.format = format_type

    def get_info(self):
        base = super().get_info()
        return f"{base}, {self.resolution}, {self.format}"

    def open(self):
        super().open()
        print(f"Image viewer opened {self.name}")

class VideoFile(File):
    def __init__(self, name, size, duration, bitrate):
        super().__init__(name, size)
        self.duration = duration
        self.bitrate = bitrate

    def get_info(self):
        base = super().get_info()
        return f"{base}, {self.duration}s, {self.bitrate} kbps"

    def open(self):
        super().open()
        print(f"Video player opened {self.name}")

# Test
files = [
    TextFile("document.txt", 5000, "UTF-8", 150),
    ImageFile("photo.jpg", 2500000, "1920x1080", "JPEG"),
    VideoFile("movie.mp4", 750000000, 7200, 5000)
]

for file in files:
    print(file.get_info())
    file.open()
    print()
```

**Expected Output:**
```
document.txt (5000 bytes), 150 lines, UTF-8
Opening document.txt...
Text editor opened document.txt

photo.jpg (2500000 bytes), 1920x1080, JPEG
Opening photo.jpg...
Image viewer opened photo.jpg

movie.mp4 (750000000 bytes), 7200s, 5000 kbps
Opening movie.mp4...
Video player opened movie.mp4
```

---

#### Activity 3: Build an E-Commerce Product Hierarchy

**Objective:** Create a product system with different product types inheriting from a Product base class.

**Requirements:**
- `Product`: name, price, quantity, calculate_total()
- `PhysicalProduct(Product)`: weight, shipping_cost
- `DigitalProduct(Product)`: license_type, download_url
- `SubscriptionProduct(Product)`: billing_period, auto_renew

**Solution Structure:**
```python
class Product:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity

    def calculate_total(self):
        return self.price * self.quantity

    def display_info(self):
        print(f"{self.name}: ${self.price} x {self.quantity} = ${self.calculate_total():.2f}")

class PhysicalProduct(Product):
    def __init__(self, name, price, quantity, weight, shipping_cost):
        super().__init__(name, price, quantity)
        self.weight = weight
        self.shipping_cost = shipping_cost

    def calculate_total(self):
        base_total = super().calculate_total()
        return base_total + (self.shipping_cost * self.quantity)

    def display_info(self):
        print(f"{self.name}: ${self.price} x {self.quantity} + ${self.shipping_cost} shipping = ${self.calculate_total():.2f}")

class DigitalProduct(Product):
    def __init__(self, name, price, quantity, license_type, download_url):
        super().__init__(name, price, quantity)
        self.license_type = license_type
        self.download_url = download_url

    def display_info(self):
        print(f"{self.name}: ${self.price} ({self.license_type}) x {self.quantity} = ${self.calculate_total():.2f}")

class SubscriptionProduct(Product):
    def __init__(self, name, price, billing_period, auto_renew):
        super().__init__(name, price, 1)
        self.billing_period = billing_period
        self.auto_renew = auto_renew

    def calculate_total(self):
        # Subscription for one period
        return self.price

    def display_info(self):
        renew_status = "Auto-renews" if self.auto_renew else "No auto-renew"
        print(f"{self.name}: ${self.price}/{self.billing_period} ({renew_status})")

# Test
products = [
    PhysicalProduct("Book", 20, 2, 1.5, 5),
    DigitalProduct("eBook", 15, 1, "Single License", "https://..."),
    SubscriptionProduct("Netflix", 15.99, "month", True)
]

for product in products:
    product.display_info()
```

### Reflection Questions

1. **How did inheritance reduce code duplication in your system?**
2. **Where did you use method overriding, and why was it necessary?**
3. **Which class hierarchy was most complex, and how did you manage it?**
4. **How would you extend each system with new types?**

### Extension Challenges

**Challenge 1:** Add a `get_description()` method to Character and override appropriately.

**Challenge 2:** Create a File Manager that can filter files by type and display statistics.

**Challenge 3:** Add a cart system for e-commerce that calculates totals across different product types.
