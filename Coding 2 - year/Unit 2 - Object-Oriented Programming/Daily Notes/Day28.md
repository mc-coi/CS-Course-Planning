# Day 28: Project Day 4 — Testing & Refinement
**Learning Target:** I can thoroughly test, debug, and refine an OOP system for production quality.

### Testing Checklist

**Unit Tests** (test individual classes):
```python
class TestCharacter:
    def test_initialization(self):
        warrior = Warrior("Test")
        assert warrior.name == "Test"
        assert warrior.health == 120
        assert warrior.level == 1

    def test_take_damage(self):
        warrior = Warrior("Test")
        warrior.take_damage(10)
        assert warrior.health == 110

    def test_level_up(self):
        warrior = Warrior("Test")
        warrior.gain_experience(100)
        assert warrior.level == 2
        assert warrior.experience == 0

    def test_attack(self):
        attacker = Warrior("A")
        target = Mage("B")
        damage = attacker.attack(target)
        assert target.health < 70  # Original 70

class TestInventory:
    def test_add_item(self):
        inv = Inventory()
        item = Item("Sword", "Weapon", 50)
        assert inv.add_item(item)
        assert len(inv) == 1

    def test_capacity(self):
        inv = Inventory(capacity=2)
        inv.add_item(Item("Item1", "Type", 10))
        inv.add_item(Item("Item2", "Type", 20))
        assert not inv.add_item(Item("Item3", "Type", 30))

class TestBattle:
    def test_battle_outcome(self):
        team1 = Team("Red")
        team1.add_member(Warrior("Warrior1"))

        team2 = Team("Blue")
        team2.add_member(Mage("Mage1"))

        battle = Battle(team1, team2)
        # At least one team should lose
        # (simulate or test logic)
```

**Integration Tests** (test classes working together):
```python
def test_full_game_flow():
    # Create game
    game = Game()

    # Create teams
    team1 = game.create_team("Red")
    team1.add_member(Warrior("Red1"))
    team1.add_member(Mage("Red2"))

    team2 = game.create_team("Blue")
    team2.add_member(Warrior("Blue1"))
    team2.add_member(Mage("Blue2"))

    # Start battle
    battle = game.start_battle(team1, team2)
    battle.simulate()

    # Check results
    assert not team1.all_defeated() or not team2.all_defeated()
```

### Code Quality Checks

**1. Code Review Checklist:**
- [ ] All variables are meaningful
- [ ] Methods are focused (single responsibility)
- [ ] No duplicate code
- [ ] Comments explain "why" not "what"
- [ ] Error messages are helpful
- [ ] No commented-out code
- [ ] Consistent naming conventions

**2. Performance Checks:**
```python
import time

def benchmark_attack():
    warrior = Warrior("Test")
    target = Mage("Target")

    start = time.time()
    for _ in range(10000):
        warrior.attack(target)
    elapsed = time.time() - start

    print(f"10,000 attacks: {elapsed:.3f} seconds")
```

**3. Edge Case Testing:**
```python
class TestEdgeCases:
    def test_zero_health(self):
        warrior = Warrior("Test")
        warrior.take_damage(200)
        assert warrior.health == 0
        assert not warrior.alive

    def test_negative_input_validation(self):
        with pytest.raises(ValueError):
            Warrior("Test", strength=-5)

    def test_empty_team(self):
        team = Team("Empty")
        assert team.all_defeated()

    def test_max_inventory(self):
        inv = Inventory(capacity=1)
        inv.add_item(Item("Item", "Type", 10))
        inv.add_item(Item("Item2", "Type", 20))
        assert len(inv) == 1
```

### Refinement Improvements

**1. Add Better Output:**
```python
class Battle:
    def display_status(self):
        print("\n=== BATTLE STATUS ===")
        print(f"Team 1: {self.team1.name}")
        for member in self.team1.members:
            print(f"  {member}")
        print(f"\nTeam 2: {self.team2.name}")
        for member in self.team2.members:
            print(f"  {member}")

    def simulate(self, verbose=True):
        while not self.team1.all_defeated() and not self.team2.all_defeated():
            if verbose:
                self.display_status()
            self.next_round()
```

**2. Add Logging:**
```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class Character:
    def take_damage(self, damage):
        self._health = max(0, self._health - damage)
        logger.info(f"{self._name} takes {damage} damage, health now {self._health}")
        if self._health == 0:
            logger.info(f"{self._name} is defeated")
            self._alive = False
```

**3. Add Error Recovery:**
```python
def safe_attack(attacker, target):
    """Safely execute attack with error handling."""
    try:
        if not attacker.alive:
            logger.warning(f"{attacker.name} is already defeated")
            return 0
        if not target.alive:
            logger.warning(f"{target.name} is already defeated")
            return 0
        return attacker.attack(target)
    except Exception as e:
        logger.error(f"Attack failed: {e}")
        return 0
```

**4. Expand Features:**
```python
class Character:
    def __init__(self, name, health, mana):
        # ... existing code ...
        self._status_effects = []

    def apply_status(self, effect):
        """Apply temporary status effect."""
        self._status_effects.append(effect)

    def get_stats_summary(self):
        """Return detailed stat summary."""
        return {
            'name': self._name,
            'level': self._level,
            'health': self._health,
            'mana': self._mana,
            'experience': self._experience,
            'alive': self._alive
        }
```

### Final Testing Script

```python
def run_all_tests():
    """Run comprehensive test suite."""
    print("=== UNIT TESTS ===")
    test_character_creation()
    test_damage_system()
    test_leveling()
    test_inventory()
    print("✓ All unit tests passed\n")

    print("=== INTEGRATION TESTS ===")
    test_battle_system()
    test_team_coordination()
    print("✓ All integration tests passed\n")

    print("=== EDGE CASE TESTS ===")
    test_zero_health()
    test_invalid_inputs()
    test_empty_team()
    print("✓ All edge case tests passed\n")

    print("=== PERFORMANCE TESTS ===")
    benchmark_operations()
    print("✓ Performance acceptable\n")

    print("=" * 40)
    print("ALL TESTS PASSED! ✓")
    print("=" * 40)

if __name__ == "__main__":
    run_all_tests()

    print("\n=== DEMO: Full Battle ===\n")
    team1 = Team("Heroes")
    team1.add_member(Warrior("Conan"))
    team1.add_member(Mage("Merlin"))

    team2 = Team("Villains")
    team2.add_member(Warrior("Dark Knight"))
    team2.add_member(Mage("Sorcerer"))

    battle = Battle(team1, team2)
    battle.simulate(verbose=True)
```

### Deliverables for Day 28

1. **Comprehensive Tests**
   - Unit tests for each class
   - Integration tests for systems
   - Edge case coverage
   - All tests passing

2. **Quality Improvements**
   - Code review completed
   - Error handling added
   - Better documentation
   - Performance verified

3. **Enhanced Features**
   - Better output/logging
   - Error recovery
   - Additional features working
   - Feature interactions tested

4. **Documentation**
   - README explaining project
   - How to run tests
   - Usage examples
   - Design rationale

### Submission Checklist

- [ ] All tests pass
- [ ] No syntax errors
- [ ] No logical errors in testing
- [ ] Code follows conventions
- [ ] Documentation complete
- [ ] Ready for Day 29 presentations

Congratulations! You're ready for final presentations!
