# Day 25: Project Day 1 — Design Your System
**Learning Target:** I can plan and design a complete OOP system from requirements.

### Project Overview

This is the start of a 4-day capstone project. By Day 28, you will have a complete, working OOP system demonstrating all major concepts.

### Choose Your Project

**Option 1: Game System**
- Characters with different classes
- Combat system
- Inventory and equipment
- Experience and leveling
- Monster encounters

**Option 2: E-Commerce Platform**
- Product catalog with categories
- Shopping cart with tax
- Multiple payment methods
- Order management
- User accounts

**Option 3: Social Network**
- User profiles and relationships
- Posts and comments
- Feed generation
- Message system
- Like/unlike functionality

**Option 4: Task Management System**
- Users and projects
- Tasks with priority and status
- Team collaboration
- Due dates and reminders
- Progress tracking

### Day 25: Design Phase

#### Step 1: Define Requirements

Write clear requirements for your chosen project. Example for Game System:

```
REQUIREMENTS:
1. Create characters (Warrior, Mage, Rogue)
2. Each character has health, mana, experience
3. Combat between characters
4. Damage calculation based on character type
5. Experience and leveling system
6. Inventory for items
7. Display character status
```

#### Step 2: Identify Classes

List nouns from requirements (potential classes):
- Character
- Warrior, Mage, Rogue
- Combat system
- Item
- Inventory
- Experience/Level

#### Step 3: Define Relationships

- Character -> Has Inventory (composition)
- Warrior -> Is-A Character (inheritance)
- Mage -> Is-A Character (inheritance)
- Inventory -> Contains Items (composition)

#### Step 4: Design Class Diagram

```
Character (abstract)
  - name: str
  - health: int
  - mana: int
  - level: int
  - inventory: Inventory
  + attack(target)
  + take_damage(amount)
  + level_up()

Warrior (extends Character)
  - strength: int
  + attack(target): specialized

Mage (extends Character)
  - intelligence: int
  + attack(target): specialized

Item
  - name: str
  - damage: int
  - type: str

Inventory (composition)
  - items: List[Item]
  + add_item()
  + remove_item()
  + get_total_damage()
```

#### Step 5: Method Design

For each class, list methods and inputs/outputs:

```python
class Character:
    def __init__(self, name: str, health: int, mana: int) -> None:
        """Initialize character with starting stats."""

    def attack(self, target: 'Character') -> int:
        """Attack target and return damage dealt."""

    def take_damage(self, amount: int) -> None:
        """Reduce health by amount."""

    def gain_experience(self, amount: int) -> None:
        """Add experience, trigger level up if needed."""

    def level_up(self) -> None:
        """Increase level and boost stats."""

    def get_status(self) -> str:
        """Return string showing current status."""
```

#### Step 6: Start Implementation

Create basic class structure:

```python
from abc import ABC, abstractmethod

class Character(ABC):
    def __init__(self, name, health, mana):
        self.name = name
        self.health = health
        self.max_health = health
        self.mana = mana
        self.max_mana = mana
        self.level = 1
        self.experience = 0
        self.inventory = Inventory()

    @abstractmethod
    def attack(self, target):
        pass

    def take_damage(self, amount):
        self.health = max(0, self.health - amount)

    def gain_experience(self, amount):
        self.experience += amount
        if self.experience >= 100:
            self.level_up()

    def level_up(self):
        self.level += 1
        self.experience = 0
        self.max_health += 20
        self.health = self.max_health

    def __str__(self):
        return f"{self.name}: Level {self.level}, HP {self.health}/{self.max_health}"

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, 100, 20)
        self.strength = 10

    def attack(self, target):
        damage = self.strength * 2
        target.take_damage(damage)
        return damage

class Mage(Character):
    def __init__(self, name):
        super().__init__(name, 60, 100)
        self.intelligence = 12

    def attack(self, target):
        if self.mana >= 20:
            damage = self.intelligence * 3
            self.mana -= 20
            target.take_damage(damage)
            return damage
        return 0

class Item:
    def __init__(self, name, damage):
        self.name = name
        self.damage = damage

    def __str__(self):
        return f"{self.name} (+{self.damage} damage)"

class Inventory:
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)

    def remove_item(self, item):
        if item in self.items:
            self.items.remove(item)

    def get_total_damage_bonus(self):
        return sum(item.damage for item in self.items)

# Test basic structure
warrior = Warrior("Conan")
mage = Mage("Merlin")

print(warrior)
print(mage)

print(f"\n{warrior.name} attacks {mage.name}")
damage = warrior.attack(mage)
print(f"Damage: {damage}")
print(mage)

print(f"\n{mage.name} attacks {warrior.name}")
damage = mage.attack(warrior)
print(f"Damage: {damage}")
print(warrior)
```

### Deliverables for Day 25

1. **Design Document** (markdown or text file):
   - Project overview
   - Requirements list
   - Class diagram (text or ASCII art)
   - Key features to implement

2. **Basic Structure** (working Python code):
   - All classes defined (even if incomplete)
   - Constructor implementation
   - At least one method working in each class
   - Test/demo code showing basic functionality

3. **TODO List**:
   - List all methods that need implementation
   - List validation needed
   - List special features

### Evaluation Checklist

- [ ] Requirements are clear and specific
- [ ] All necessary classes identified
- [ ] Relationships properly designed
- [ ] Code follows OOP principles
- [ ] Basic tests demonstrate functionality
- [ ] Code is organized and readable
- [ ] Comments explain complex logic

### Tips for Success

1. **Don't overcomplicate** - Start with core features
2. **Focus on design** - Good design makes coding easier
3. **Test as you go** - Create test code early
4. **Use comments** - Document your design decisions
5. **Plan before coding** - Design time pays off in coding time

### Next Steps

Days 26-28 will involve:
- Building core classes
- Adding inheritance and polymorphism
- Implementing special methods
- Testing and debugging
- Final refinement

Come prepared with your design to build on tomorrow!
