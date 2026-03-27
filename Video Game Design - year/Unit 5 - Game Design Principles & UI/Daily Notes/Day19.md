# Day 19: UI & Audio Project Lab

**Learning Target:** I can integrate UI, audio, and game feel into a complete mini-project.

---

## Project Brief

Build a **"Clicker Game"** or **"Simple Defense Game"** that demonstrates:
- Main menu and pause menu
- Health bars and score display
- Button interactions
- Sound effects and background music
- Particle effects on hit
- Screen shake on impact

---

## Required Components

**UI:**
- Main menu (Play, Quit buttons)
- In-game HUD (score, health bar, level)
- Pause menu (Resume, Restart, Main Menu)
- Game Over screen

**Audio:**
- Background music (looping)
- Click SFX
- Hit/damage SFX
- Victory/defeat SFX

**Polish:**
- Particle effects when clicking/hitting
- Screen shake on damage
- Color changes on health bar (green → yellow → red)
- Button hover effects

---

## Suggested Progression

**Phase 1: Setup**
- Create 3 scenes: MainMenu, GameScene, GameOver
- Set up Canvas with basic buttons
- Attach ButtonManager and AudioManager

**Phase 2: Gameplay**
- Simple clicker: click button to gain points
- Or simple enemy: click to deal damage
- Display score and health

**Phase 3: Polish**
- Add all effects (particles, shake, flash)
- Sound on every action
- Smooth animations

**Phase 4: Testing**
- Play from start to finish
- Verify audio loops correctly
- Check menu navigation
- Adjust difficulty/feedback

---

## Success Criteria

- [ ] Main menu loads game on button click
- [ ] Pause menu freezes time and allows resume
- [ ] Score increases with player action
- [ ] Health bar drains and changes color
- [ ] Sound effects play on all major events
- [ ] Particle effects appear on hit/pickup
- [ ] Screen shake occurs on damage
- [ ] Game can return to main menu from game over
- [ ] No errors in Console

---

## Optional Enhancements

- Save high score
- Difficulty scaling (more enemies, faster spawn)
- Combo system (consecutive hits increase multiplier)
- Visual effects (screen transition, fade effects)
- Keyboard shortcuts (ESC for pause, Space for action)

---

## Daily Standup

What did you build today? What's working? What's next?

Document your progress in a text file:
```
Day 19 Progress:
- Completed: Menu navigation, HUD setup, audio system
- In Progress: Game feel (particles, screen shake)
- Next: Bug fixes, balance testing
- Blockers: None
```
