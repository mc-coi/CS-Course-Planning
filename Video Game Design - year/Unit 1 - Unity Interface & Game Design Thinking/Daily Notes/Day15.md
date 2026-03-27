# Day 15: Build Settings and Play Mode Workflow

**Learning Target:** I can navigate Build Settings, understand Play Mode behavior, and prepare scenes for building.

---

## Key Concepts

**Build Settings** — Configuration for compiling your game into an executable (Windows, Mac, WebGL, etc.).

**Scenes in Build** — Only scenes added here will be included in the final build. Scene 0 is loaded first.

**Play Mode** — Press Play to test the game. Changes in Play Mode are temporary and don't save.

**Edit Mode** — Normal editor state. Changes here are permanent (saved to your scene file).

**Frame Debugger** — Visualize what the GPU is rendering (Window → Analysis → Frame Debugger) — advanced topic for later.

---

## Build Settings Overview

| Setting | Purpose |
|---------|---------|
| Scenes in Build | List of scenes to include in final build |
| Platform | Target OS (PC, Mac, Web, Mobile, Console) |
| Quality | Graphics settings (shadows, reflections, LOD) |
| Resolution | Default window size |
| Fullscreen | Windowed or fullscreen mode |

---

## Unity Setup Steps

1. **Open Build Settings:** File → Build Settings
2. **Look at "Scenes in Build"** — empty by default
3. **Click "Add Open Scene"** — your current scene is added as Scene 0
4. **Create a second scene:** File → New Scene → 3D
5. **Save it as "Scene2"** (File → Save As)
6. **Return to Build Settings and click "Add Open Scene"** — Scene2 is now Scene 1
7. **Close Build Settings**
8. **In your first scene, create a UI Button** that loads Scene2 (pseudocode only for now)

---

## Guided Practice

1. **Create two scenes:** "MainLevel" and "SecondaryLevel"
2. **Add both to Build Settings** (Scene 0 and Scene 1)
3. **In MainLevel, note any changes** you make
4. **Press Play** and try to make changes (e.g., move objects, modify values)
5. **Press Stop:** Notice all Play-mode changes are reverted
6. **Confirm:** The scene is back to its saved state

---

## Practice Problems

**Beginner:** Create 3 scenes and add all to Build Settings. Verify they appear in the Scenes in Build list.

**Intermediate:** Create 2 scenes: MainMenu and GameLevel. In MainMenu, create 3 cubes. Add both to Build Settings.

**Challenge:** Create a scene with a script that logs changes. Press Play, make changes, press Stop. Document what persists and what reverts. Why is this important for game development?

<details>
<summary>💡 Hints</summary>
- Play Mode is sandboxed: prefab instances, script variable changes, and instantiated objects don't persist
- Scenes must be in Build Settings to be loaded in a final build (they can still be loaded in editor)
- You can have multiple scenes open (File → New Scene → Additive) for level editing across scenes
- Reloading a scene (SceneManager.LoadScene) resets it to its saved state
- Build Settings → Player → Resolution & Presentation to set default window size
</details>

<details>
<summary>✅ Sample: Multi-Scene Setup</summary>

Build Settings Scenes:
- Scene 0: MainScene (has level design, enemies, pickups)
- Scene 1: GameOverScene (has UI, restart button)
- Scene 2: SettingsScene (has graphics/audio sliders)

When you load Scene 1, all changes in Scene 0 are forgotten. Each scene is independent.

</details>
