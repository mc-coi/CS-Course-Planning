# Unit 6: 2D Game Development

> Most indie games are 2D — and Unity's 2D tools are incredibly powerful. Master sprites, tilemaps, animation, and 2D physics to build the kind of game you've always wanted to play.

## Unit Overview

- **Duration:** 25 days / 5 weeks
- **TN Standard:** 9-12.VGD.6 — Develop complete 2D game environments using Unity's 2D toolset
- **Prerequisites:** Units 1-5 (C#, Game Design, UI basics)
- **Capstone:** Complete 2D platformer level with animated player, tilemap environment, parallax background, working physics

---

## Learning Outcomes

1. Set up 2D projects with orthographic camera and Physics2D
2. Import and configure sprites with proper settings
3. Create sprite sheets and slice them in Sprite Editor
4. Build animation clips and state machines
5. Design levels using Tilemaps and Tile Palettes
6. Implement parallax scrolling for depth
7. Add lighting and visual polish
8. Tune 2D physics for platformers (coyote time, jump buffering, one-way platforms)
9. Optimize 2D game performance

---

## Daily Topics Overview

**Week 1: Sprites & Setup (Days 1-6)**
- Day 1: 2D vs 3D project setup
- Day 2: Sprites and SpriteRenderer basics
- Day 3: Sprite import settings and optimization
- Day 4: Sprite Editor and sprite slicing
- Day 5: Sprite sheets and frame animation
- Day 6: Animation clip management

**Week 2: Animation (Days 7-10)**
- Day 7: Animator Controller basics
- Day 8: Animation parameters and transitions
- Day 9: State machine design for player movement
- Day 10: Advanced transitions and blending

**Week 3: Tilemaps (Days 11-14)**
- Day 11: Tilemap component and Tile Palette setup
- Day 12: Painting tilemaps and TilemapCollider2D
- Day 13: Multiple tilemap layers and Rule Tiles
- Day 14: Animated tiles and auto-tiling

**Week 4: Camera & Visual (Days 15-19)**
- Day 15: 2D camera follow mechanics
- Day 16: Cinemachine Virtual Camera 2D
- Day 17: Parallax scrolling implementation
- Day 18: 2D lighting and Normal Maps
- Day 19: Visual effects for 2D games

**Week 5: Physics Tuning & Assessment (Days 20-25)**
- Day 20: 2D physics fundamentals
- Day 21: Platformer physics (coyote time, jump buffering)
- Day 22: One-way platforms and slopes
- Day 23: Complete level design
- Day 24: Level design project lab
- Day 25: Unit Assessment

---

## Support Materials

- **ReferenceGuide.md**: Sprite import settings, Animator window, Tilemap setup, Cinemachine, sorting layers, physics components
- **UnitPractice.md**: 15 problems with complete solutions
- **UnitAssessment.md**: 10 MC + 5 Short Answer + 3 Coding Challenges

---

## Key Concepts

| Concept | Importance | When Used |
|---------|-----------|-----------|
| **Orthographic Camera** | Essential | All 2D projects |
| **Sprite Rendering** | Core | Every visible 2D object |
| **Sprite Editor** | Important | Optimizing sprite sheets |
| **Animator** | Core | Character animation |
| **Tilemap** | Core | Level design, terrain |
| **Sorting Layers** | Important | Managing render order |
| **Physics2D** | Core | Movement, collisions |
| **Parallax** | Polish | Visual depth |
| **2D Lighting** | Polish | Mood, atmosphere |
| **Pixel Perfect** | Optional | Retro/pixel art style |

---

## Capstone Project Requirements

Build a **complete 2D platformer level** with:

### Level Design
- [ ] Start zone with spawn point
- [ ] Multiple platform challenges
- [ ] At least one new mechanic (slope, one-way platform, moving platform)
- [ ] Visual progression (difficulty increases)
- [ ] Clear goal/exit

### Visual Elements
- [ ] Tilemap-based terrain
- [ ] Parallax background with 2-3 layers
- [ ] Animated player (idle, walk, jump, fall states)
- [ ] Visual effects (particles on land, jump, pickup)
- [ ] Proper sorting layers (background < terrain < player < UI)

### Mechanics
- [ ] Player movement (left/right)
- [ ] Jump with proper physics
- [ ] Coyote time (extra grace period after leaving platform)
- [ ] Jump buffering (input queue for responsive jumping)
- [ ] Collectible items
- [ ] Goal/exit that transitions to next scene

### Polish
- [ ] Smooth camera follow
- [ ] Audio (footsteps, jump, pickup, victory)
- [ ] Particle effects (jump dust, pickup particles)
- [ ] Screen shake on landing (optional)
- [ ] Color-coded platforms (safe = green, hazard = red)

### Success Criteria
- [ ] Level is playable start to finish
- [ ] Physics feel responsive and fair
- [ ] No collision glitches or getting stuck
- [ ] Parallax actually feels like depth
- [ ] Animation blends smoothly
- [ ] No console errors

---

## Common Pitfalls & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| Sprites blurry | Bilinear filter | Set to Point filter |
| Sprites too small/big | Wrong Pixels Per Unit | Adjust import setting |
| Z-fighting (flickering) | Same Z position | Use Sorting Layers |
| Player glitches through platform | Physics check missed | Use FixedUpdate + continuous collision |
| Jump feels floaty | Wrong gravity scale | Increase Rigidbody2D gravity scale |
| Camera jumps | Wrong camera size | Use Orthographic size, not FOV |

---

## Learning Progression

```
Days 1-6:   Sprites & Setup (Can import & display sprites)
Days 7-10:  Animation (Can create & blend animations)
Days 11-14: Tilemaps (Can design levels with tilemaps)
Days 15-19: Camera & Visual (Can implement parallax & lighting)
Days 20-25: Physics & Polish (Can build complete level)
```

Each week builds on previous weeks. You cannot skip ahead.

---

## Assessment Rubric (40 points total)

| Category | Points | Criteria |
|----------|--------|----------|
| **Level Design** | 8 | Well-paced, clear progression, interesting challenges |
| **Visuals** | 8 | Proper tilemap, parallax, animation, sorting layers |
| **Mechanics** | 8 | Responsive movement, physics feel good, no glitches |
| **Polish** | 8 | Audio, effects, transitions, no console errors |
| **Completeness** | 5 | All required elements present |
| **Code Quality** | 5 | Well-commented, organized scripts |

---

## Next Unit

Unit 7: Game Systems & Enemies will teach you to add:
- Enemy AI (state machines)
- Spawning systems
- Health and damage
- Inventory and collectibles
- Save/load systems

You'll apply all of Unit 6's mechanics to create enemies and game systems that interact with your 2D environments.

---

**Ready to master 2D game development? Let's build something amazing!**
