# Unit 5 - Game Design Principles & UI: Teacher Misconception & Callout Guide

## Overview

This unit bridges game design theory (MDA framework, flow state) with Unity's UI system (Canvas, RectTransform, TextMeshPro, buttons). In a STEM semester course, the theory portion must be tight—students grasp MDA quickly but struggle to apply it to their own games. The bigger time sink is Unity UI, where RectTransform anchoring confuses nearly everyone and button OnClick wiring trips students who think code runs automatically. Provide a working UI template (Canvas, HUD, main menu) and teach students to wire it to their game—don't have them build from scratch. Use 🚨 flags to know when to stop everything.

---

## Misconceptions by Topic

### MDA Framework & Game Design Theory (Days 1–2)

**⚠️ Misconception:** "MDA stands for Mechanics, Dynamics, Aesthetics. Mechanics are the rules. Got it."

**What it looks like:** A student recites the definition but can't apply it. They design a "shoot things" mechanic without asking what emotion (aesthetic) they want the player to feel.

**Why students think this:** Theory without application doesn't stick.

**How to address it:** Apply MDA backwards. "Design from the player's desired feeling, not the rules. Start with Aesthetics: 'I want the player to feel tense.' Then ask: what Dynamics create tension? (Scarce ammo, enemies closing in.) Then: what Mechanics create those dynamics? (Limited inventory, aggressive AI.) Work A → D → M, not M → D → A. This is how pro designers think."

🚨 **STEM Priority — STOP THE CLASS:** If students are designing by listing features rather than emotions, stop and do a 10-minute MDA reverse-design exercise. Pick a game the class knows and work backwards from feeling to mechanic.

---

**⚠️ Misconception:** "Flow state means the game should be hard. I'll make it very hard."

**What it looks like:** A student makes the game brutally difficult and calls it "flow-inducing." Players die constantly and feel frustrated, not engaged.

**Why students think this:** They confuse challenge with frustration. Flow requires that challenge scales with skill.

**How to address it:** Explain the flow channel. "Flow state occurs when challenge matches skill—neither too easy (bored) nor too hard (frustrated). Csikszentmihalyi called this the 'flow channel.' The goal is to keep players in that channel: as they improve, the game gets harder. Design a difficulty curve: easy early levels build skill, later levels test it. If playtesters are frustrated, the challenge spiked too fast."

---

### Canvas & RectTransform (Days 2–4)

**⚠️ Misconception:** "I added UI to the scene but it's not visible in the Game view—it's only in the Scene view. UI must be broken."

**What it looks like:** A student adds a Canvas and UI elements but they don't appear in the Game view.

**Why students think this:** The Canvas is set to World Space instead of Screen Space - Overlay.

**How to address it:** Check Canvas Render Mode. "The Canvas has three Render Modes: (1) Screen Space - Overlay: renders on top of everything, always visible. (2) Screen Space - Camera: attached to a camera. (3) World Space: placed in 3D world (used for in-world UI like health bars above enemies). For standard HUD/menus, use Screen Space - Overlay. Check: Canvas → Inspector → Canvas → Render Mode."

🚨 **STEM Priority — STOP THE CLASS:** Most students will hit this. Teach it before they start placing UI elements.

---

**⚠️ Misconception:** "My UI looks fine in the editor, but when I resize the window or build to a different screen size, everything is in the wrong place."

**What it looks like:** A student positions UI with fixed pixel offsets. On a 1920×1080 monitor it looks fine, but on a 1280×720 it's cut off.

**Why students think this:** They use Transform.position instead of anchoring.

**How to address it:** Set anchors correctly. "UI elements must be anchored to the correct screen region using RectTransform anchors. A score display in the top-right should be anchored to the top-right corner. A health bar in the bottom-left should anchor bottom-left. Drag the anchor handles to the correct corner. Then use the Pos X/Y offsets as relative distance from that anchor. Also: set Canvas → Canvas Scaler → UI Scale Mode = 'Scale with Screen Size' with a reference resolution (e.g., 1920×1080)."

```
Canvas Scaler settings for responsive UI:
- UI Scale Mode: Scale with Screen Size
- Reference Resolution: 1920 x 1080
- Screen Match Mode: Match Width or Height
- Match: 0.5 (compromise between width and height)
```

---

**⚠️ Misconception:** "I added a Text component to my button, but the text is too small and I can't resize it. Font size doesn't seem to work."

**What it looks like:** A student uses the legacy Text component and struggles with sizing. Or they have TextMeshPro but don't know how to install the Essential Resources.

**Why students think this:** TextMeshPro requires importing essential resources first; the legacy Text component is unpredictable.

**How to address it:** Use TextMeshPro correctly. "Always use TextMeshPro (TMP) instead of the legacy Text component. First import: Window → TextMeshPro → Import TMP Essential Resources. Then use 'TextMeshPro - Text (UI)' when adding text. TMP's font size works in points and scales with the Canvas. If text is tiny, increase font size AND make sure the RectTransform is large enough to contain it. Overflow = 'Overflow' if you need text to spill out of the bounds."

---

### Button Wiring & OnClick Events (Days 4–5)

**⚠️ Misconception:** "I added a Button component but clicking it doesn't do anything. Do I need to write an event system?"

**What it looks like:** A student creates a Button but doesn't know about the OnClick() event in the Inspector.

**Why students think this:** They expect buttons to automatically call a function named "OnClick" or similar.

**How to address it:** Wire the OnClick event. "Unity Buttons have an OnClick() event list in the Inspector. To wire it: (1) Click the + button in OnClick(). (2) Drag the GameObject with your script into the slot. (3) In the dropdown, select your script and the method you want called. The method must be public and take no parameters (or one matching type). Test: enter Play mode and click the button."

🚨 **STEM Priority — Handle 1-on-1:** This trips almost every student the first time. Demo it whole-class once, then handle individual wiring questions 1-on-1.

```csharp
// This method can be wired to a button's OnClick event
public void StartGame()
{
    SceneManager.LoadScene("GameScene");
}

public void QuitGame()
{
    Application.Quit();
    Debug.Log("Quit (only works in build, not editor)"); // for testing
}
```

---

**⚠️ Misconception:** "I wired the OnClick event but nothing happens when I click in play mode. The button is working (it clicks), but no function is called."

**What it looks like:** A student can see the button highlighting, but the wired method doesn't fire.

**Why students think this:** They wired it to the wrong object, the wrong method, or the method has the wrong signature.

**How to address it:** Debug the wiring. "Check: (1) Is the method public? Private methods don't appear in the dropdown. (2) Is the correct GameObject dragged into the OnClick slot? (3) Did you select the method from the dropdown (not just leave it on 'No Function')? (4) Is the script component enabled? Also check Console for errors—if the script has a compile error, the event won't fire."

---

### Scene Management & PlayerPrefs (Days 5–6)

**⚠️ Misconception:** "I call SceneManager.LoadScene() to go to the next level, but my score resets to 0. How do I keep it?"

**What it looks like:** A student loads a new scene and the score variable (which was on an object in the old scene) is destroyed.

**Why students think this:** They don't know that all objects are destroyed when a new scene loads.

**How to address it:** Use DontDestroyOnLoad or PlayerPrefs. "Two approaches: (1) On the object holding your score, call `DontDestroyOnLoad(gameObject);` in Awake(). The object survives the scene load. (2) Save the score to PlayerPrefs before loading: `PlayerPrefs.SetInt('Score', score);` and load it in the new scene: `int savedScore = PlayerPrefs.GetInt('Score', 0);`. For simple values like score, PlayerPrefs is easier. For complex state, use DontDestroyOnLoad."

```csharp
// Saving score across scenes with PlayerPrefs
PlayerPrefs.SetInt("Score", currentScore);
SceneManager.LoadScene("NextLevel");

// In the new scene:
int score = PlayerPrefs.GetInt("Score", 0); // 0 is default if key not found
```

---

**⚠️ Misconception:** "I called Application.Quit() in the editor but nothing happened. My game doesn't quit."

**What it looks like:** A student adds a Quit button, wires Application.Quit(), and expects the editor to close.

**Why students think this:** Application.Quit() only works in a built application, not in Play mode in the editor.

**How to address it:** Explain editor vs. build. "Application.Quit() exits a standalone build—it has no effect in the Unity Editor. To stop Play mode in the editor, use `UnityEditor.EditorApplication.isPlaying = false;` (Editor only, surrounded by `#if UNITY_EDITOR`). Or just accept that Quit won't work in the editor and test it in a build."

---

### Time.timeScale & Pause (Days 6–7)

**⚠️ Misconception:** "I set Time.timeScale = 0 to pause, but my UI animations also stopped. I want the UI to still animate."

**What it looks like:** A student pauses with timeScale = 0 and then wonders why button animations and UI tweens also freeze.

**Why students think this:** They don't know timeScale affects everything that uses Time.deltaTime.

**How to address it:** Use unscaled time for UI. "Time.timeScale = 0 pauses everything that uses Time.deltaTime. For animations or code that should run during pause, use `Time.unscaledDeltaTime` instead of `Time.deltaTime`. Unity's Animator also has an option: Animator → Update Mode → 'Unscaled Time' (runs even when paused)."

---

## Whole-Class Warning Signs

- **Nobody can explain MDA without looking at notes.** Application is the goal, not memorization. Use a quick "design by feeling" exercise: pick a game, identify what emotion it makes you feel, and reverse-engineer the mechanics.

- **All UI is in Screen Space - World or broken.** Stop the class and show the three Canvas Render Modes. Set a class standard: use Screen Space - Overlay for all HUDs and menus.

- **Everyone's text is tiny or overflowing.** They're using legacy Text or wrong TMP settings. Show TMP import once; set a class rule: always use TextMeshPro.

- **Button OnClick events aren't wired.** Do a whole-class 5-minute demo of dragging a GameObject into OnClick, selecting a method, and testing. This is a mechanical workflow—once seen, it's easy.

- **Scores reset on scene load.** Teach PlayerPrefs as the quick fix. DontDestroyOnLoad is fine too but more complex—reserve it for the capstone.

---

## Questions That Reveal Understanding

1. **"Explain the MDA framework in one sentence."**
   - Good answer: "Mechanics are the rules, Dynamics are what players do with them, Aesthetics are the emotions that result. Design backwards from emotion."
   - Red flag: "Mechanics, Dynamics, Aesthetics—they're the parts of a game." (No design application.)

2. **"Your score text isn't updating when the player earns points. How do you debug this?"**
   - Good answer: "Check if the method updating the text is being called with Debug.Log. Then check if the TMP reference is assigned in Inspector. Then check if the text string is formatted correctly: `scoreText.text = 'Score: ' + score;`."
   - Red flag: "I'd delete the text and add a new one." (No debugging methodology.)

3. **"A player clicks your UI button but nothing happens. Walk me through your debugging process."**
   - Good answer: "Is the method public? Is the right GameObject dragged into OnClick? Did I select the method (not 'No Function')? Are there compile errors? I'd add Debug.Log inside the method to confirm it's being called."
   - Red flag: "I'd look up a tutorial." (No systematic approach.)

4. **"What's the difference between anchoring to the center vs. anchoring to a corner?"**
   - Good answer: "Anchoring to a corner means the UI element's position is relative to that corner—it stays in the same position relative to that corner regardless of screen size. Anchoring to center means it stays centered but may not stay in the right visual position if the aspect ratio changes."
   - Red flag: "I'm not sure—I just drag it where I want it." (Will break on different screens.)

5. **"Your game loads a new scene and the player's lives are reset. Name two ways to fix this."**
   - Good answer: "PlayerPrefs.SetInt/GetInt to save and load across scenes. Or DontDestroyOnLoad on the GameObject holding the lives variable."
   - Red flag: "I'd use a static variable." (Static works but is fragile—acceptable as a third option, not ideal.)

---

## Common Student Questions & How to Answer Them

**Q1: "My health bar is a slider. How do I connect it to the player's health?"**

*A:* "Get a reference to the Slider component in your health script: `public Slider healthSlider;`. In the Inspector, drag the Slider GameObject into the slot. Then when health changes: `healthSlider.value = (float)currentHealth / maxHealth;`. Set Slider Min = 0, Max = 1. The fill will update automatically."

---

**Q2: "How do I make a timer that counts down and shows on screen?"**

*A:* "Track time in a float: `timeRemaining -= Time.deltaTime;`. Display it: `timerText.text = Mathf.CeilToInt(timeRemaining).ToString();` to show whole numbers rounding up. Or formatted: `timerText.text = string.Format('{0:00}:{1:00}', minutes, seconds);`. When it hits 0, trigger game over."

---

**Q3: "How do I make my main menu buttons lead to the game scene?"**

*A:* "Create a method in a script on the Canvas (or a separate MenuManager): `public void StartGame() { SceneManager.LoadScene('GameScene'); }`. Wire it to the button's OnClick event. Make sure the scene is in File → Build Settings → Scenes In Build, or it won't load."

---

**Q4: "My pause menu appears but the game keeps running. How do I actually pause?"**

*A:* "Set `Time.timeScale = 0f;` to freeze all physics and animations. Show your pause Canvas: `pausePanel.SetActive(true);`. To unpause: `Time.timeScale = 1f;` and hide the panel. For UI elements that need to animate during pause (like buttons), set their Animator to 'Unscaled Time'."

---

**Q5: "How do I display 'Game Over' or 'You Win' based on a condition?"**

*A:* "Create two UI panels (GameOverPanel, WinPanel) and set both to inactive by default: `gameObject.SetActive(false);`. When the condition is met (health == 0 or level complete), activate the right panel: `gameOverPanel.SetActive(true);` and pause: `Time.timeScale = 0f;`. Wire the 'Restart' button to a method that sets timeScale back to 1 and reloads the scene."

---

## Analogies That Work

1. **"MDA is like designing a restaurant. The menu items (Mechanics) determine what the chef cooks (Dynamics), which creates the dining experience (Aesthetics). You don't design the menu first—you decide what experience you want guests to have, then design the menu to create it."**
   - Makes the backwards design approach intuitive.

2. **"RectTransform anchors are like pinning a note to a bulletin board. If you pin to the center, the note stays centered. If you pin to the top-right corner, the note stays in the top-right even when the board gets bigger or smaller. Always pin to the corner where your UI element belongs."**
   - Makes anchoring immediately visual.

3. **"PlayerPrefs is like a sticky note on the refrigerator. When you leave the kitchen (scene), the note stays. When you come back, you can read it. Time.timeScale = 0 is like hitting pause on a video—everything freezes, including you, unless you set something to 'unscaled.'"**
   - Quick practical mental models.

---

## Unity-Specific Gotchas

- **Scenes must be added to Build Settings to be loaded by name.** File → Build Settings → Scenes In Build → drag scenes in. SceneManager.LoadScene("GameScene") will throw an error if "GameScene" isn't listed.

- **Canvas Scaler Reference Resolution matters.** Without it, UI scales based on actual pixel size. Add Canvas Scaler → Scale with Screen Size → set 1920×1080 as reference. All UI will scale proportionally on other resolutions.

- **Button's Interactable checkbox.** If a button doesn't respond to clicks, check Interactable = true in the Inspector. It can be inadvertently unchecked.

- **TextMeshPro text isn't updated from code until you import Essential Resources.** If TMP text shows "TMP" as a placeholder or throws namespace errors, run Window → TextMeshPro → Import TMP Essential Resources.

- **Application.Quit() has no effect in Play mode.** Always remind students this is expected. Test quit in a standalone build, or use `#if UNITY_EDITOR` to stop play mode during development.

- **FindObjectOfType() is slow when called every frame.** Cache references in Start(): `scoreDisplay = FindObjectOfType<ScoreDisplay>();`. Calling it in Update() causes performance problems in complex scenes.

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
