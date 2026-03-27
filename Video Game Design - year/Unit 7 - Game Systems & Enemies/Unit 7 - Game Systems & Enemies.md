# Unit 7: Game Systems & Enemies

> Bring your game world to life with intelligent enemies, satisfying systems, and persistence. Learn the architecture patterns professional game developers use every day.

## Unit Overview

- **Duration:** 23 days / ~4.5 weeks
- **TN Standard:** 9-12.VGD.7 — Implement game systems including AI, spawning, saving, and game flow
- **Prerequisites:** Units 1-6 (C#, 2D development, UI basics)
- **Capstone:** Complete mini-game with enemies, spawn system, health/damage, inventory, save/load, game flow

---

## Learning Outcomes

1. Design and implement finite state machines for enemy AI
2. Create patrol, chase, and attack behaviors
3. Build spawner systems with difficulty scaling
4. Implement health and damage systems with visual feedback
5. Design inventory and collectible systems using ScriptableObjects
6. Build persistence systems with PlayerPrefs and JSON
7. Manage scene transitions and game flow
8. Create procedural generation for dynamic content
9. Implement event systems for loose coupling

---

## Daily Topics Overview

**Week 1: Enemy AI (Days 1-8)**
- Day 1-2: Finite State Machine fundamentals
- Day 3-4: Enemy patrol and waypoints
- Day 5-6: Chase and aggro mechanics
- Day 7-8: Attack behavior and cooldowns

**Week 2: Spawning & Pooling (Days 9-12)**
- Day 9-10: Object pooling for performance
- Day 11: Wave spawner systems
- Day 12: Timed spawners and difficulty scaling

**Week 3: Health & Systems (Days 13-18)**
- Day 13-14: Health and damage systems
- Day 15-16: Inventory and collectibles
- Day 17-18: Save/load systems (PlayerPrefs + JSON)

**Week 4: Game Flow & Polish (Days 19-23)**
- Day 19: Scene management and DontDestroyOnLoad
- Day 20: Game state transitions
- Day 21: Procedural generation basics
- Day 22: Game systems project lab
- Day 23: Unit Assessment

---

## Support Materials

- **ReferenceGuide.md**: FSM pattern, AI behaviors, object pool template, ScriptableObject pattern, save systems, procedural generation
- **UnitPractice.md**: 15 problems with complete solutions
- **UnitAssessment.md**: 10 MC + 5 Short Answer + 3 Coding Challenges

---

## Key Concepts

| Concept | Importance | When Used |
|---------|-----------|-----------|
| **FSM (Finite State Machine)** | Core | All enemy behavior |
| **Object Pooling** | Important | Bullets, particles, enemies |
| **Spawner Systems** | Core | Waves, difficulty scaling |
| **Health/Damage** | Core | Player/enemy interaction |
| **ScriptableObject** | Important | Item data, configuration |
| **Inventory** | Important | Loot, progression |
| **Save System** | Core | Persistence, progression |
| **Scene Management** | Core | Game flow, levels |
| **Procedural Gen** | Optional | Replayability, content |
| **Events** | Important | Loose coupling |

---

## Capstone Project Requirements

Build a **complete mini-game** demonstrating all Unit 7 systems:

### Enemy AI
- [ ] At least one enemy type with FSM
- [ ] Patrol behavior (walks back and forth)
- [ ] Chase behavior (detects and follows player)
- [ ] Attack behavior (deals damage on contact)
- [ ] Visual feedback on hit (flash, particles)

### Spawning & Difficulty
- [ ] Wave spawner or timed spawner
- [ ] Enemies spawn at designated points
- [ ] Difficulty increases each wave (more enemies, faster, stronger)
- [ ] Waves/spawning stops when goal is reached

### Health & Damage
- [ ] Player has health bar (UI)
- [ ] Enemy has health
- [ ] Damage reduces health
- [ ] Death triggers defeat condition
- [ ] Knockback or hit feedback

### Inventory & Collectibles
- [ ] At least one item type (health potion, ammo, coin)
- [ ] Collectibles spawn when enemy defeated
- [ ] Inventory tracks collected items
- [ ] Using item has effect (heal, damage boost)

### Persistence
- [ ] Save high score to PlayerPrefs
- [ ] Save game state (JSON) with complex data
- [ ] Load on startup
- [ ] Game state restored correctly

### Game Flow
- [ ] Main menu → Gameplay scene transition
- [ ] Pause menu (from Unit 5)
- [ ] Defeat condition (display game over, return to menu)
- [ ] Victory condition (defeat enough enemies, reach score)
- [ ] Smooth scene transitions

### Polish
- [ ] Audio for all major events
- [ ] Particle effects
- [ ] Screen shake on damage
- [ ] No console errors
- [ ] UI for HUD (health, score, inventory)

---

## Success Criteria Checklist

- [ ] Game launches and runs without errors
- [ ] Player can move and interact
- [ ] Enemies spawn and behave intelligently
- [ ] Combat feels satisfying (hit feedback, damage visible)
- [ ] Inventory picks up and tracks items
- [ ] Game saves/loads correctly
- [ ] Scene transitions work
- [ ] Audio plays on all major events
- [ ] Difficulty scales appropriately
- [ ] Victory/defeat conditions trigger correctly

---

## Architecture Best Practices

### Separation of Concerns
- Enemy AI in separate script
- Health in separate component (reusable)
- Spawner in separate script
- Game state in GameManager singleton

### Reusability
- Health component can be used by Player, Enemy, NPC
- Damage interface allows any object to take damage
- ScriptableObject items can be instantiated as many times needed
- Spawner can spawn any prefab

### Scalability
- Object pooling prevents memory issues
- FSM can be expanded with more states
- Spawner difficulty can scale infinitely
- Save system can handle any data size (with JSON)

---

## Common Mistakes & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| Enemy stuck in wall | Spawned inside collider | Check spawn point locations |
| Game stutters (enemies) | Creating/destroying often | Use object pooling |
| Damage not working | Missing IDamageable interface | Add interface to scripts |
| Save file lost | Only using PlayerPrefs | Use JSON for complex data |
| Scene loads but objects missing | Wrong references | Use DontDestroyOnLoad |
| Enemies don't detect player | Wrong detection radius | Increase Physics.OverlapSphere radius |
| Inventory gets full | No slot management | Implement stack limits |

---

## Learning Progression

```
Days 1-8:   Enemy AI (Can create behavioral AI)
Days 9-12:  Spawning (Can spawn enemies with difficulty)
Days 13-18: Systems (Can track health, items, save data)
Days 19-22: Game Flow (Can build complete mini-game)
Day 23:     Assessment (Demonstrate mastery)
```

---

## Assessment Rubric (40 points total)

| Category | Points | Criteria |
|----------|--------|----------|
| **Enemy AI** | 8 | FSM implemented, states work, behavior is intelligent |
| **Spawning & Difficulty** | 8 | Spawning works, difficulty scales, balanced challenge |
| **Combat System** | 8 | Damage, health, feedback all functional |
| **Persistence** | 8 | Save/load works, data persists correctly |
| **Game Flow** | 5 | Menus, transitions, win/lose conditions |
| **Code Quality** | 3 | Organization, comments, no errors |

**Total: 40 points**

---

## Beyond Unit 7

After completing this unit, you'll have:
- **Three complete units** (UI, 2D Development, Game Systems)
- **Skills to build** any 2D game from scratch
- **Professional patterns** (FSM, Singleton, Object Pooling, Serialization)
- **Portfolio projects** (multiple games with different systems)

Next units will explore:
- **Unit 8**: 3D Game Development (if continued)
- **Unit 9**: Networking & Multiplayer
- **Unit 10**: Publishing & Optimization

---

## Final Reflection

By completing Units 5-7, you've learned:
1. **Game Design**: How to create engaging experiences
2. **UI Systems**: How to guide players through your game
3. **2D Development**: How to build game worlds
4. **Game Systems**: How to add depth and replayability
5. **Architecture**: How to write scalable, professional code

You're now ready to build any 2D game concept you can imagine. The principles you've learned apply to larger games, teams, and studios.

**Congratulations on your game development journey!**
