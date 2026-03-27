# Day 26: Project Day 2 — Build Core Classes
**Learning Target:** I can implement complete, working core classes with proper OOP structure.

### Today's Objectives

1. Implement all core classes from your design
2. Add private attributes and properties
3. Implement all methods with logic
4. Add validation and error handling
5. Create working test cases

### Implementation Checklist

For each class, ensure:
- [ ] __init__ with all attributes
- [ ] Private attributes where appropriate
- [ ] Public properties with validation
- [ ] All methods implemented with logic
- [ ] Proper error handling
- [ ] Clear docstrings

### Example: Game System Build

```python
from abc import ABC, abstractmethod
from datetime import datetime

class Character(ABC):
    """Base character class for all character types."""

    def __init__(self, name: str, health: int, mana: int):
        if not name or len(name) < 2:
            raise ValueError("Name must be at least 2 characters")
        if health <= 0 or mana < 0:
            raise ValueError("Health must be positive, mana non-negative")

        self._name = name
        self._health = health
        self._max_health = health
        self._mana = mana
        self._max_mana = mana
        self._level = 1
        self._experience = 0
        self._inventory = Inventory()
        self._created_at = datetime.now()

    @property
    def name(self):
        return self._name

    @property
    def health(self):
        return self._health

    @property
    def mana(self):
        return self._mana

    @property
    def level(self):
        return self._level

    @property
    def experience(self):
        return self._experience

    @property
    def inventory(self):
        return self._inventory

    @abstractmethod
    def attack(self, target: 'Character') -> int:
        """Attack target and return damage dealt."""
        pass

    def take_damage(self, amount: int) -> None:
        """Reduce health by amount, minimum 0."""
        if amount < 0:
            raise ValueError("Damage cannot be negative")
        self._health = max(0, self._health - amount)

    def heal(self, amount: int) -> None:
        """Heal character, maximum max_health."""
        if amount < 0:
            raise ValueError("Heal amount cannot be negative")
        self._health = min(self._max_health, self._health + amount)

    def gain_experience(self, amount: int) -> None:
        """Add experience and trigger level up if threshold reached."""
        if amount < 0:
            raise ValueError("Experience cannot be negative")
        self._experience += amount
        while self._experience >= 100:
            self.level_up()

    def level_up(self) -> None:
        """Increase level and improve stats."""
        self._level += 1
        self._experience -= 100
        self._max_health += 20
        self._health = self._max_health
        self._max_mana += 10
        self._mana = self._max_mana

    def is_alive(self) -> bool:
        """Return True if character still has health."""
        return self._health > 0

    def __str__(self):
        return f"{self._name} - Lvl {self._level} | HP {self._health}/{self._max_health} | MP {self._mana}/{self._max_mana}"

    def __repr__(self):
        return f"{self.__class__.__name__}('{self._name}', {self._health}, {self._mana})"

    def __eq__(self, other):
        return isinstance(other, Character) and self._name == other._name

    def __lt__(self, other):
        return self._level < other._level

class Warrior(Character):
    """Warrior character: high health, melee damage."""

    def __init__(self, name: str, strength: int = 10):
        super().__init__(name, 120, 20)
        if strength <= 0:
            raise ValueError("Strength must be positive")
        self._strength = strength
        self._armor = 2

    @property
    def strength(self):
        return self._strength

    def attack(self, target: Character) -> int:
        """Deal strength-based damage to target."""
        if not isinstance(target, Character):
            raise TypeError("Target must be a Character")
        damage = self._strength * 2
        target.take_damage(damage)
        return damage

    def level_up(self):
        super().level_up()
        self._strength += 2
        self._armor += 1

class Mage(Character):
    """Mage character: high mana, magic damage."""

    def __init__(self, name: str, intelligence: int = 12):
        super().__init__(name, 70, 120)
        if intelligence <= 0:
            raise ValueError("Intelligence must be positive")
        self._intelligence = intelligence

    @property
    def intelligence(self):
        return self._intelligence

    def attack(self, target: Character) -> int:
        """Cast spell dealing intelligence-based damage."""
        if not isinstance(target, Character):
            raise TypeError("Target must be a Character")

        spell_cost = 20
        if self._mana < spell_cost:
            return 0  # Not enough mana

        damage = self._intelligence * 3
        self._mana -= spell_cost
        target.take_damage(damage)
        return damage

    def level_up(self):
        super().level_up()
        self._intelligence += 2
        self._max_mana += 20

class Rogue(Character):
    """Rogue character: high speed, critical strikes."""

    def __init__(self, name: str, agility: int = 12):
        super().__init__(name, 80, 50)
        if agility <= 0:
            raise ValueError("Agility must be positive")
        self._agility = agility
        self._critical_chance = 0.25

    @property
    def agility(self):
        return self._agility

    def attack(self, target: Character) -> int:
        """Attack with chance for critical damage."""
        import random
        if not isinstance(target, Character):
            raise TypeError("Target must be a Character")

        damage = self._agility * 2
        if random.random() < self._critical_chance:
            damage *= 2

        target.take_damage(damage)
        return damage

    def level_up(self):
        super().level_up()
        self._agility += 2
        self._critical_chance += 0.05

class Item:
    """Equipment item with stats."""

    def __init__(self, name: str, item_type: str, value: int):
        if not name or not item_type or value < 0:
            raise ValueError("Invalid item parameters")
        self._name = name
        self._type = item_type
        self._value = value

    @property
    def name(self):
        return self._name

    @property
    def type(self):
        return self._type

    @property
    def value(self):
        return self._value

    def __str__(self):
        return f"{self._name} ({self._type}) +{self._value}"

    def __eq__(self, other):
        return isinstance(other, Item) and self._name == other._name

class Inventory:
    """Container for character items."""

    def __init__(self, capacity: int = 20):
        if capacity <= 0:
            raise ValueError("Capacity must be positive")
        self._items = []
        self._capacity = capacity

    def add_item(self, item: Item) -> bool:
        """Add item if capacity allows."""
        if len(self._items) >= self._capacity:
            return False
        if not isinstance(item, Item):
            raise TypeError("Must be an Item")
        self._items.append(item)
        return True

    def remove_item(self, item: Item) -> bool:
        """Remove item from inventory."""
        if item in self._items:
            self._items.remove(item)
            return True
        return False

    def get_total_value(self) -> int:
        """Return sum of all item values."""
        return sum(item.value for item in self._items)

    def __len__(self):
        return len(self._items)

    def __str__(self):
        return f"Inventory ({len(self._items)}/{self._capacity}): {', '.join(str(i) for i in self._items)}"

# Test all classes
if __name__ == "__main__":
    # Create characters
    warrior = Warrior("Conan", 12)
    mage = Mage("Merlin", 14)
    rogue = Rogue("Assassin", 13)

    print("=== Characters Created ===")
    print(warrior)
    print(mage)
    print(rogue)
    print()

    # Add items to inventory
    print("=== Adding Items ===")
    sword = Item("Excalibur", "Sword", 50)
    potion = Item("Health Potion", "Potion", 20)

    warrior.inventory.add_item(sword)
    warrior.inventory.add_item(potion)
    print(f"Warrior's {warrior.inventory}")
    print()

    # Combat test
    print("=== Combat ===")
    print(f"{warrior.name} attacks {mage.name}")
    damage = warrior.attack(mage)
    print(f"Damage dealt: {damage}")
    print(mage)
    print()

    print(f"{mage.name} attacks {warrior.name}")
    damage = mage.attack(warrior)
    print(f"Damage dealt: {damage}")
    print(warrior)
    print()

    # Experience test
    print("=== Experience ===")
    warrior.gain_experience(80)
    print(f"{warrior.name} gains 80 XP")
    print(warrior)
    warrior.gain_experience(30)
    print(f"{warrior.name} gains 30 XP (levels up!)")
    print(warrior)
```

### Deliverables for Day 26

1. **Complete Core Classes**
   - All classes with all methods implemented
   - Proper validation and error handling
   - Properties with getters/setters
   - Docstrings for all public methods

2. **Test Code**
   - Tests for each class
   - Edge cases covered
   - Example usage demonstrated

3. **Code Quality**
   - Follows PEP 8 style
   - Clear variable names
   - Comments for complex logic
   - No dead code

Continue to Day 27 for inheritance and polymorphism enhancements!
