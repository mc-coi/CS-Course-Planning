# Unit 5: Game Design Principles & UI

> Great games are designed, not just coded. Learn the theory behind player experience and build the UI systems that guide players through your world.

## Unit Overview

- **Duration:** 20 days / 4 weeks
- **TN Standard:** 9-12.VGD.5 — Apply game design principles and implement user interface systems
- **Prerequisite:** Units 1-4 (basic C#, GameObject basics)
- **Capstone:** Clicker/Defense game with full UI, audio, and game feel

---

## Learning Outcomes

By the end of this unit, you will be able to:

1. **Understand game design theory**
   - Apply MDA (Mechanics, Dynamics, Aesthetics) framework to analyze games
   - Design challenges that maintain player flow state
   - Structure levels using safe→challenge→reward loops
   - Understand player motivation archetypes (Achievers, Explorers, Socializers, Killers)

2. **Build professional UI systems**
   - Set up responsive Canvas with proper anchoring and scaling
   - Create dynamic text displays using TextMeshPro
   - Implement interactive buttons and menus
   - Build health bars and progress sliders

3. **Implement game systems**
   - Create score tracking and high score persistence
   - Build main menu and pause menu systems
   - Manage scene transitions
   - Use PlayerPrefs for data persistence

4. **Add professional audio**
   - Play sound effects and background music
   - Create centralized audio manager (Singleton)
   - Control volumes and implement fading

5. **Polish with game feel**
   - Add particle effects for impact
   - Create screen shake feedback
   - Implement visual effects (color flash, animations)
   - Synchronize audio-visual feedback

---

## Unit Structure

### Week 1: Game Design Theory (Days 1-4)
- **Day 1-2**: MDA Framework, Flow State, Player Motivation
- **Day 3-4**: Level Design Principles, Safe/Challenge/Reward Loop, Visual Language

### Week 2: UI Fundamentals (Days 5-10)
- **Day 5-6**: Canvas System, RectTransform, TextMeshPro
- **Day 7-8**: Button Component, Menu Navigation
- **Day 9-10**: Health Bars, Sliders, Progress Systems

### Week 3: Game Systems & Audio (Days 11-16)
- **Day 11-12**: Score Systems, PlayerPrefs, High Score Persistence
- **Day 13-14**: Main Menu, Pause Menu, Scene Management
- **Day 15-16**: Audio System, Audio Manager, Volume Control

### Week 4: Polish & Assessment (Days 17-20)
- **Day 17-18**: Game Feel (Particles, Screen Shake, Hit Flash)
- **Day 19**: UI/Audio Project Lab (Clicker or Defense Game)
- **Day 20**: Unit Assessment

---

## Key Concepts at a Glance

| Concept | What It Is | Why It Matters |
|---------|-----------|----------------|
| **MDA** | Mechanics → Dynamics → Aesthetics | Understand how game rules create player experiences |
| **Flow State** | Challenge = Skill | Keep players engaged, not bored or frustrated |
| **Level Design Loop** | Safe → Challenge → Reward | Guide players, teach mechanics, provide satisfaction |
| **Canvas** | UI drawing plane | Organize buttons, text, health bars on screen |
| **RectTransform** | UI positioning | Make layouts responsive to different screen sizes |
| **TextMeshPro** | Modern text system | Display crisp, formatted text in UI |
| **Button** | Interactive UI element | Trigger actions when clicked |
| **Slider** | Value display/control | Build health bars, progress bars, volume controls |
| **PlayerPrefs** | Key-value storage | Save scores, settings, progress between sessions |
| **Singleton** | One instance of class | Centralize audio, game state across scenes |
| **Time.timeScale** | Game speed control | Pause, slow-motion effects |
| **AudioSource** | Play sounds | Background music, sound effects |
| **Particle System** | Effect emitter | Visual feedback for hits, pickups, explosions |
| **Game Feel** | Polished feedback | Makes actions feel impactful and satisfying |

---

## Daily Note Format

Each day has:
1. **Learning Target**: Specific, measurable skill
2. **Key Concepts**: Bold terms with explanations
3. **Code Example**: Commented C# for Unity
4. **Unity Setup Steps**: Click-by-click instructions
5. **Guided Practice**: 3-5 tasks to complete
6. **Practice Problems**: Beginner, Intermediate, Challenge with hints and solutions

---

## Support Files

- **ReferenceGuide.md**: Canvas modes, TextMeshPro setup, Button onClick, Time.timeScale, PlayerPrefs, AudioSource, Particle properties
- **UnitPractice.md**: 15 problems (Beginner-Challenge) with complete solutions
- **UnitAssessment.md**: 10 MC + 5 Short Answer + 3 Coding Challenges

---

## Capstone Project: Clicker/Defense Game

Build a complete mini-game demonstrating all Unit 5 concepts:

### Requirements
- **Menus**: Main menu (Play, Quit) and pause menu (Resume, Restart, Main Menu)
- **HUD**: Score display, health bar, level indicator
- **Buttons**: All menu interactions must use Button component
- **Audio**: Background music, SFX for clicks/damage, victory/defeat sounds
- **Polish**: Particles on hit, screen shake on damage, color-coded health bar
- **Persistence**: Save high score to PlayerPrefs

### Success Criteria
- [ ] Game launches with main menu
- [ ] Can pause (ESC) and resume
- [ ] Score increases with player action
- [ ] Health bar decreases and changes color
- [ ] Audio plays on all major events
- [ ] Particles appear on hit
- [ ] Screen shakes on damage
- [ ] Can return to main menu
- [ ] No console errors

---

## Challenge Extensions

Once you've completed the basic requirements:

1. **Save Game System**: Save/load player progress mid-game
2. **Difficulty Scaling**: Increase enemy health/speed each level
3. **Combo System**: Reward consecutive hits with multiplier
4. **Achievements**: Unlock badges for milestones
5. **Settings Menu**: Audio, graphics, difficulty settings that persist
6. **Leaderboard**: Display top 5 scores with player names
7. **Animations**: Smooth transitions, button hover effects, enemy death animation
8. **VFX Variety**: Different particles for different events (heal, crit, special attack)

---

## Vocabulary

- **Anchor**: UI reference point on screen
- **Aesthetics**: Emotional experience
- **Button**: Interactive UI element
- **Canvas**: Plane where UI is drawn
- **Dynamics**: How mechanics create gameplay
- **Flow**: State of optimal challenge
- **Game Feel**: Polished feedback and responsiveness
- **Mechanic**: Game rule or system
- **Pivot**: Origin point of UI element
- **PlayerPrefs**: Persistent data storage
- **RectTransform**: UI position and size component
- **Singleton**: Design pattern for single instance
- **TextMeshPro**: Modern text rendering system
- **Time.timeScale**: Game speed multiplier
- **UI**: User interface elements

---

## Common Mistakes to Avoid

1. **Forgetting DontDestroyOnLoad()** → Audio manager resets between scenes
2. **Setting Time.timeScale = 0 without resetting** → Game stays paused when loading new scene
3. **Not using RectTransform anchors** → UI breaks on different screen sizes
4. **Forgetting `using TMPro;`** → TextMeshPro not recognized
5. **PlayOneShot with looping clip** → Sound repeats unexpectedly
6. **Not checking PlayerPrefs key exists** → Returns wrong default value
7. **Canvas Scaler not set to "Scale with Screen Size"** → UI doesn't scale responsively
8. **Button interactable = false, but onClick still fires** → Check if button is actually disabled

---

## Resources

- [Unity Canvas Documentation](https://docs.unity3d.com/Manual/UICanvas.html)
- [TextMeshPro Manual](https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.2/manual/)
- [AudioSource Reference](https://docs.unity3d.com/ScriptReference/AudioSource.html)
- [PlayerPrefs API](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html)
- [Game Feel article](https://en.wikipedia.org/wiki/Game_feel) (external)

---

## Assessment Rubric

Your capstone project will be graded on:

| Criterion | Points | Description |
|-----------|--------|------------|
| **Menus & Navigation** | 10 | Main menu, pause menu, scene transitions work correctly |
| **UI Implementation** | 10 | Buttons, text, sliders, health bar properly set up |
| **Audio System** | 10 | Music loops, SFX play, volume controls work |
| **Game Systems** | 10 | Score tracking, high score persistence, game flow |
| **Game Feel** | 10 | Particles, screen shake, visual feedback, polish |
| **Code Quality** | 10 | Well-commented, organized, no errors |
| **Bonus: Extensions** | +5 | Extra features (save system, achievements, etc.) |

**Total: 40 points**

---

## Next Steps

After Unit 5, you'll move to **Unit 6: 2D Game Development**, where you'll build complete 2D environments using sprites, tilemaps, animation, and physics. You'll apply your UI/audio knowledge to create a full 2D platformer with all the systems you've built here.

**You're building the foundation for professional game development. Great work!**
