# Day 27: Project Day 3 — Add Inheritance & Polymorphism
**Learning Target:** I can enhance class hierarchies with inheritance, polymorphism, and special methods.

### Today's Objectives

1. Ensure inheritance is properly implemented
2. Add polymorphic behavior where appropriate
3. Implement special methods (__str__, __eq__, etc.)
4. Add composition relationships
5. Refactor for better design

### Enhancement Areas

**1. Special Methods**

Implement for all relevant classes:
```python
class Character:
    def __str__(self):
        return f"{self._name}: Level {self._level}"

    def __repr__(self):
        return f"{self.__class__.__name__}('{self._name}')"

    def __eq__(self, other):
        return isinstance(other, Character) and self._name == other._name

    def __lt__(self, other):
        return self._level < other._level

    def __le__(self, other):
        return self == other or self < other

    def __gt__(self, other):
        return not (self <= other)

    def __hash__(self):
        return hash(self._name)
```

**2. Polymorphic Collections**

```python
class Battle:
    def __init__(self):
        self.characters = []

    def add_character(self, character):
        self.characters.append(character)

    def sort_by_level(self):
        return sorted(self.characters)

    def display_all(self):
        for char in self.characters:
            print(char)

    def simulate_round(self):
        for character in self.characters:
            # Polymorphism: attack() works differently per type
            target = self.get_opponent(character)
            if target:
                character.attack(target)
```

**3. Abstract Methods**

Ensure all subclasses properly override abstract methods:
```python
class Character(ABC):
    @abstractmethod
    def get_damage(self):
        """Return base damage for this character type."""
        pass

    @abstractmethod
    def special_ability(self, target):
        """Execute special ability unique to this class."""
        pass

class Warrior(Character):
    def get_damage(self):
        return self.strength * 2

    def special_ability(self, target):
        """Warrior uses shield bash."""
        damage = self.strength * 3
        target.take_damage(damage)

class Mage(Character):
    def get_damage(self):
        return self.intelligence * 2

    def special_ability(self, target):
        """Mage uses fireball."""
        if self.mana >= 30:
            damage = self.intelligence * 4
            self.mana -= 30
            target.take_damage(damage)
```

**4. Composition Examples**

```python
class Team:
    """Team of characters working together."""
    def __init__(self, name):
        self.name = name
        self.members = []

    def add_member(self, character):
        self.members.append(character)

    def get_total_health(self):
        return sum(char.health for char in self.members if char.is_alive())

    def all_defeated(self):
        return all(not char.is_alive() for char in self.members)

    def __str__(self):
        return f"{self.name}: {len(self.members)} members"

class Game:
    """Game managing teams and battles."""
    def __init__(self):
        self.teams = []
        self.current_battle = None

    def create_team(self, name):
        team = Team(name)
        self.teams.append(team)
        return team

    def start_battle(self, team1, team2):
        self.current_battle = Battle(team1, team2)
        return self.current_battle

class Battle:
    """Manages a battle between two teams."""
    def __init__(self, team1, team2):
        self.team1 = team1
        self.team2 = team2
        self.round = 0

    def get_winner(self):
        if self.team1.all_defeated():
            return self.team2
        elif self.team2.all_defeated():
            return self.team1
        return None

    def simulate(self):
        while not self.get_winner():
            self.next_round()

    def next_round(self):
        self.round += 1
        # Team 1 attacks team 2
        for char in self.team1.members:
            if char.is_alive():
                target = self.get_random_target(self.team2)
                if target:
                    char.attack(target)
        # Team 2 attacks team 1
        for char in self.team2.members:
            if char.is_alive():
                target = self.get_random_target(self.team1)
                if target:
                    char.attack(target)

    def get_random_target(self, team):
        import random
        alive = [c for c in team.members if c.is_alive()]
        return random.choice(alive) if alive else None
```

**5. Multi-level Inheritance**

```python
class CombatCharacter(Character):
    """Adds combat-specific features."""
    def __init__(self, name, health, mana):
        super().__init__(name, health, mana)
        self._combat_level = 1
        self._victories = 0

    def record_victory(self):
        self._victories += 1
        self.gain_experience(50)

class Warrior(CombatCharacter):
    def __init__(self, name):
        super().__init__(name, 120, 20)
        self._strength = 10

class EliteWarrior(Warrior):
    """Advanced warrior with additional features."""
    def __init__(self, name):
        super().__init__(name)
        self._max_health += 40
        self._health = self._max_health
        self._strength += 5
        self._legendary = True

    def ultimate_attack(self, target):
        """Powerful attack only for elite warriors."""
        damage = self._strength * 5
        target.take_damage(damage)
        self.gain_experience(100)
        return damage
```

### Complete Example with All Features

```python
from abc import ABC, abstractmethod
from datetime import datetime
import random

class Character(ABC):
    def __init__(self, name, health, mana):
        self._name = name
        self._health = health
        self._max_health = health
        self._mana = mana
        self._max_mana = mana
        self._level = 1
        self._experience = 0
        self._team = None
        self._alive = True

    @property
    def name(self): return self._name
    @property
    def health(self): return self._health
    @property
    def level(self): return self._level
    @property
    def alive(self): return self._alive

    @abstractmethod
    def attack(self, target):
        pass

    def take_damage(self, damage):
        self._health = max(0, self._health - damage)
        if self._health == 0:
            self._alive = False

    def join_team(self, team):
        self._team = team

    def gain_experience(self, amount):
        self._experience += amount
        if self._experience >= 100:
            self.level_up()

    def level_up(self):
        self._level += 1
        self._experience -= 100
        self._max_health += 20
        self._health = self._max_health

    def __str__(self):
        status = "Alive" if self._alive else "Defeated"
        return f"{self._name} (Lvl {self._level}) - {status}"

    def __eq__(self, other):
        return isinstance(other, Character) and self._name == other._name

    def __lt__(self, other):
        return self._level < other._level

class Warrior(Character):
    def __init__(self, name, strength=10):
        super().__init__(name, 120, 20)
        self._strength = strength

    def attack(self, target):
        damage = self._strength * 2
        target.take_damage(damage)
        print(f"{self._name} slashes {target.name} for {damage} damage!")

class Mage(Character):
    def __init__(self, name, intelligence=12):
        super().__init__(name, 70, 120)
        self._intelligence = intelligence

    def attack(self, target):
        if self._mana >= 20:
            damage = self._intelligence * 3
            self._mana -= 20
            target.take_damage(damage)
            print(f"{self._name} casts fireball on {target.name} for {damage} damage!")
        else:
            print(f"{self._name} has no mana!")

class Team:
    def __init__(self, name):
        self.name = name
        self.members = []

    def add_member(self, character):
        self.members.append(character)
        character.join_team(self)

    def get_alive_members(self):
        return [m for m in self.members if m.alive]

    def all_defeated(self):
        return len(self.get_alive_members()) == 0

class Battle:
    def __init__(self, team1, team2):
        self.team1 = team1
        self.team2 = team2
        self.round = 0

    def next_round(self):
        self.round += 1
        print(f"\n--- Round {self.round} ---")

        for char in self.team1.get_alive_members():
            targets = self.team2.get_alive_members()
            if targets:
                target = random.choice(targets)
                char.attack(target)

        for char in self.team2.get_alive_members():
            targets = self.team1.get_alive_members()
            if targets:
                target = random.choice(targets)
                char.attack(target)

    def simulate(self):
        while not self.team1.all_defeated() and not self.team2.all_defeated():
            self.next_round()

        winner = self.team2 if self.team1.all_defeated() else self.team1
        print(f"\n{winner.name} wins!")

# Test
if __name__ == "__main__":
    team1 = Team("Red Team")
    team1.add_member(Warrior("Conan"))
    team1.add_member(Mage("Merlin"))

    team2 = Team("Blue Team")
    team2.add_member(Warrior("Aragorn"))
    team2.add_member(Mage("Gandalf"))

    battle = Battle(team1, team2)
    battle.simulate()
```

### Deliverables for Day 27

1. **Enhanced Class Hierarchy**
   - Proper inheritance structure
   - All abstract methods implemented
   - Special methods where appropriate

2. **Polymorphic System**
   - Collections of objects working polymorphically
   - Methods responding appropriately to each type

3. **Composition System**
   - Relationships properly modeled
   - Classes working together

4. **Test Cases**
   - Test inheritance
   - Test polymorphism
   - Test special methods
