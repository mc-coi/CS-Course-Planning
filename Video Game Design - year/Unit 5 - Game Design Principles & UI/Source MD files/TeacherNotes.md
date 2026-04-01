# Unit 5 - Game Design Principles & UI: Teacher Misconception & Callout Guide

## Overview

This unit bridges the gap between **technical skills** (Units 2-4) and **intentional design**. Students now have the ability to build mechanics but lack the framework to evaluate whether those mechanics are *fun*. The biggest challenge is that game design is **subjective**—students struggle to articulate why a game feels good or bad, and they don't understand how UI, audio, and visual feedback transform a functional mechanic into a satisfying experience. Additionally, UI implementation is deceptively complex: RectTransform scaling, Canvas layers, and button event binding confuse students who are used to working in world space. For a year-long course, students can iterate on a simple game and apply design principles repeatedly. For a semester course, you must provide clear frameworks (MDA, Flow State, Safe→Challenge→Reward) and battle-tested UI patterns.

---

## Misconceptions by Topic

### Game Design Theory & MDA Framework (Days 1–4)

**⚠️ Misconception:** "Mechanics, Dynamics, and Aesthetics all mean the same thing. Why do we need three terms?"**

**What it looks like:** A student describes a platformer as "jumping is the mechanic, dynamic, and aesthetic." They use the terms interchangeably.

**Why students think this:** The three are related—mechanics cause dynamics, which create aesthetics. Without concrete examples, the distinction is subtle.

**How to address it:** Use a repeated pattern across games. "In any game, mechanics are the **rules** (no art, no music, just math). Dynamics are what **happens** when those rules interact (players do unexpected things, strategies emerge). Aesthetics are **how the player feels** (tension, joy, boredom). Example: Chess. Mechanic: pawns move one square forward. Dynamic: players develop pawn chains for board control. Aesthetic: players feel strategic tension. Now apply this to a game they know: Minecraft. Mechanic: place blocks. Dynamic: players build elaborate structures and cooperate. Aesthetic: players feel creative and proud."

---

**⚠️ Misconception:** "Flow State means the game is always easy. If I make the game too hard, the player gets frustrated."**

**What it looks like:** A student designs a game where every level is equally easy, worried that difficulty will break flow.

**Why students think this:** They hear "flow" and think "smooth, no obstacles." Actually, flow is when **challenge matches skill**—too easy is as bad as too hard.

**How to address it:** Draw the flow diagram. Sketch a graph: Y-axis is "challenge," X-axis is "skill level." Plot "boring" (low challenge, high skill), "anxious" (high challenge, low skill), and "flow" (challenge and skill increase together). "The player starts at low skill and low challenge. As they improve, you increase challenge. If you keep challenge the same, they get bored. If you increase too fast, they get frustrated. Your job is to find the middle path—the flow channel."

---

**⚠️ Misconception:** "Player motivation—some players are Achievers, some are Explorers. I should design the game for only one type."**

**What it looks like:** A student designs a game for Achievers (competitive, score-focused) and ignores other player types.

**Why students think this:** They think player types are exclusive categories. Actually, most players have multiple motivations.

**How to address it:** Teach the spectrum. "Most players are a mix. A player might be an Achiever (likes scoring) and an Explorer (likes discovering secrets). Design for multiple types: give score systems (Achievers), hidden areas (Explorers), multiplayer options (Socializers), and challenge modes (Killers). You don't have to please everyone, but give options."

---

### UI Fundamentals & Canvas (Days 5–10)

**⚠️ Misconception:** "I created a UI button, but it's stretched across the entire screen. The Canvas must be broken."**

**What it looks like:** A student adds a button to a Canvas. The button's RectTransform is anchored to stretch (Stretch preset), so it fills the screen instead of being a small button.

**Why students think this:** They're unfamiliar with RectTransform and anchoring. The default might be stretch.

**How to address it:** Teach anchoring and sizing. "RectTransform has two parts: Anchor (where on the screen it attaches) and Size Delta (how big it is). For a button, use 'Top-Left' anchor and set fixed width/height. Watch it snap to the corner with the right size. Anchor presets are in the top-left of the Inspector—click the target icon and choose a layout."

---

**⚠️ Misconception:** "I changed a UI element's position, but it didn't move. The script must not be working."**

**What it looks like:** A student writes `rectTransform.position = new Vector3(100, 100, 0);` but the element doesn't move to the expected screen position.

**Why students think this:** RectTransform uses `anchoredPosition` for screen positioning, not `position`. `position` is world-space (useless for UI).

**How to address it:** Use the right property. "For UI, use `rectTransform.anchoredPosition`, not `position`. `position` is for world-space objects in the scene. `anchoredPosition` is for UI screen-space positioning." Have them change one line and watch it work.

---

**⚠️ Misconception:** "I created two UI panels on different layers (Canvas with Layer UI1, another Canvas with UI Layer 2). They're both visible, but I wanted only one layer to show."**

**What it looks like:** A student creates multiple Canvas objects expecting layers to control visibility. Both render on top of each other.

**Why students think this:** Unity Layers don't control UI rendering; Canvas **sorting order** does.

**How to address it:** Use Canvas sorting. "Multiple Canvas objects stack by sorting order. Select each Canvas and set 'Sort Order' in the Inspector. Higher order = on top. One Canvas with multiple panels (children) is usually better than multiple Canvas objects, but if you need multiple, control their layering with Sort Order, not Layers."

---

**⚠️ Misconception:** "My TextMeshPro text is tiny and hard to read. I increased the font size to 100, but it's still small."**

**What it looks like:** A student sets font size to 100 but the text is still unreadable. They think there's a bug.

**Why students think this:** Font size in TextMeshPro is affected by the RectTransform size. If the text box is tiny, large font sizes won't help.

**How to address it:** Resize the text box. "Font size and text box size work together. Increase the text box's RectTransform (width/height) so the font has room. Then increase font size. Also, check text alignment (left, center, right) and the font asset—some fonts are harder to read."

---

### Buttons & Interactivity (Days 7–8)

**⚠️ Misconception:** "I created a button, but clicking it does nothing. I wrote the code, so it should work."**

**What it looks like:** A student creates a Button UI element, writes a script with a method, but the button doesn't call the method when clicked.

**Why students think this:** They wrote the code but didn't **wire** the button to the method. The Button component has an OnClick event that needs to be configured in the Inspector.

**How to address it:** Wire the event. "Buttons work in two steps: (1) Write a method:
```csharp
public void OnPlayButtonClicked()
{
    SceneManager.LoadScene("GameScene");
}
```
(2) Assign it in the Inspector. Select the button → Button component → OnClick → add a listener → drag the GameObject with the script → select the method." Walk them through the Inspector clicks step-by-step.

---

**⚠️ Misconception:** "I want to handle button clicks in code without using the OnClick event in the Inspector. Can I do that?"**

**What it looks like:** A student tries to use `Input.GetMouseButtonDown()` to check if a button is clicked.

**Why students think this:** Checking mouse input works, but it's not how buttons are meant to be used.

**How to address it:** Teach EventSystem. "Use EventSystem for robust button input:
```csharp
using UnityEngine.EventSystems;

if(EventSystem.current.IsPointerOverGameObject() && Input.GetMouseButtonDown(0))
{
    // A UI element is clicked
}
```
But really, just use the OnClick event in the Inspector. It's cleaner and handles mobile input automatically."

---

### Audio Systems & Audio Manager (Days 15–16)

**⚠️ Misconception:** "I created an AudioSource and played a sound in my script, but I don't hear anything."**

**What it looks like:** A student writes `audioSource.Play();` but no sound plays.

**Why students think this:** Common causes: (1) Volume is 0 (Audiosource or Master Volume). (2) The audio file isn't imported correctly. (3) The speaker is muted. (4) The audio clip isn't assigned.

**How to address it:** Troubleshoot systematically. "Check in order: (1) AudioSource has a clip assigned? (2) Play() is actually called (add `Debug.Log()` before it)? (3) Volume is > 0? (4) Mute is unchecked? (5) Speaker volume is on? Test by selecting the AudioSource in the Inspector and clicking the play button—if that works, the problem is your code."

---

**⚠️ Misconception:** "I have multiple AudioSources playing sounds, and they overlap loudly. I want to mix them—some sounds quieter, some louder."**

**What it looks like:** A student has many sound effects and background music all at max volume, creating a muddy mix.

**Why students think this:** They don't know about Audio Mixer or volume control.

**How to address it:** Teach mixing basics. "Create an AudioMixer (Assets → Create → Audio Mixer). Set up groups: Background, SFX, UI. Assign each AudioSource to a group. In the mixer, lower the volume of each group. Also, use lower volume for subtle sounds (footsteps) vs. loud sounds (explosions). Professional games spend time balancing audio levels."

---

### Game Feel & Polish (Days 17–18)

**⚠️ Misconception:** "I added visual effects (screen shake, particles, hit flash) but the game doesn't feel more satisfying. The effects must not be working."**

**What it looks like:** A student adds effects but they're too subtle or poorly timed.

**Why students think this:** Screen shake intensity is low, particle effect duration is short, or hit flash color isn't noticeable.

**How to address it:** Tune the effects. "Visual feedback needs to be **exaggerated** to feel good. Screen shake should be noticeable (0.2-0.5 units, not 0.01). Hit flash should be bright red or white. Particles should spray out. Don't worry about realism; worry about *feel*. Test by comparing to a reference game (e.g., gunplay in Fortnite has strong recoil, screen shake, and particles). Make yours that satisfying."

---

### SceneManager & Game State (Days 13–14)

**⚠️ Misconception:** "I used `SceneManager.LoadScene("GameScene")` to load a new level, but all my variables reset to default."**

**What it looks like:** A student loads a new scene and expects score or player state to persist, but it doesn't.

**Why students think this:** Loading a scene destroys all GameObjects in the current scene, including the script that holds the data.

**How to address it:** Use persistence. "To preserve data between scenes, either: (1) Store it in a static variable or Singleton. (2) Use `DontDestroyOnLoad()` to keep a GameObject across scenes. (3) Use PlayerPrefs to save to disk:
```csharp
PlayerPrefs.SetInt("score", score);
// Later, load:
int savedScore = PlayerPrefs.GetInt("score", 0);
```"

---

### PlayerPrefs & Data Persistence (Days 11–12)

**⚠️ Misconception:** "I saved a high score using `PlayerPrefs.SetInt("highScore", 1000)`, but when I restarted the game, it wasn't there."**

**What it looks like:** A student sets a PlayerPrefs value but it doesn't persist.

**Why students think this:** PlayerPrefs saves to disk, but you need to call `PlayerPrefs.Save()` to guarantee it's written (though in-editor it usually works without explicit saving).

**How to address it:** Always save explicitly. "After setting a value, call `PlayerPrefs.Save()`:
```csharp
PlayerPrefs.SetInt("highScore", score);
PlayerPrefs.Save();
```
This ensures the data is written to disk. When you load the game, use `PlayerPrefs.GetInt("highScore", 0);` (the second argument is the default if the key doesn't exist)."

---

## Whole-Class Warning Signs

- **Everyone's UI is misaligned or stretched incorrectly.** They don't understand RectTransform and anchoring. Show them the anchor presets and have them set anchors correctly on every element.

- **No one wired buttons to methods in the Inspector.** They wrote the code but didn't connect it. Show them the exact Inspector clicks: Button component → OnClick event → add listener → drag object → select method.

- **All the students' games have no audio or very quiet audio.** They either didn't add AudioSources or set volume to 0. Have a checklist: "Does your scene have an AudioSource? Is it assigned a clip? Is volume > 0?"

- **Game feel is flat—actions don't feel impactful.** They skipped polish (screen shake, particles, hit flash). Assign a "game feel" checkpoint where they add at least 3 types of feedback to one action.

- **Multiple students complain that UI looks bad at different screen resolutions.** They didn't use proper anchoring or scaling. Show them Canvas Scale Mode (Scale with Screen Size) and anchors.

---

## Questions That Reveal Understanding

1. **"Explain the MDA framework using a racing game as an example."**
   - Good answer: "Mechanics: cars have acceleration, braking, turning, collision. Dynamics: players learn to drift around corners, manage fuel, avoid obstacles. Aesthetics: players feel adrenaline, competition, satisfaction from mastering the car."
   - Red flag: "Mechanics are cars, dynamics are driving, aesthetics are graphics." (They're conflating mechanics with objects.)

2. **"Why is flow state important in game design?"**
   - Good answer: "Flow keeps players engaged. If the game is too easy, they're bored. Too hard, they're frustrated. Flow is when challenge matches skill, so players stay focused and have fun."
   - Red flag: "Because it makes the game smooth" or "Because it sounds good." (Too vague.)

3. **"You have a high score display that shows the current score, but the text is cut off. What's wrong?"**
   - Good answer: "The RectTransform is too small for the text. Increase the width/height of the text box, or decrease font size, or use Layout Group to auto-size."
   - Red flag: "The font is too big" or "The resolution is wrong." (Partially correct, but doesn't identify the RectTransform issue.)

4. **"How would you make a pause menu that shows on top of gameplay?"**
   - Good answer: "Create a Canvas for the pause menu. Set its sort order higher than the game Canvas. Disable it at start. When pause is pressed, enable it and set `Time.timeScale = 0` to freeze the game. Re-enable input for menu buttons."
   - Red flag: "Hide the game scene and show the pause scene." (They're thinking of scene loading, not overlaying UI.)

5. **"A button in your UI doesn't respond to clicks. List three things to check."**
   - Good answer: "(1) Is the button's OnClick event wired to a method? (2) Is the Canvas Raycast Target enabled? (3) Is the button blocked by another UI element (check sort order)?"
   - Red flag: "The script is broken" or "The graphics card is broken." (Not constructive troubleshooting.)

---

## Common Student Questions & How to Answer Them

**Q1: "I want to pause the game when the player clicks a button. How do I freeze everything?"**

*A:* "Set `Time.timeScale = 0` to pause physics and animations. Set it to 1 to resume. Note: UI still works at timeScale = 0, so buttons respond. Background music continues unless you pause it separately."

---

**Q2: "How do I display the score on screen?"**

*A:* "Create a Text (TextMeshPro) UI element. In your script:
```csharp
textComponent.text = "Score: " + score;
```
Call this every frame or whenever score changes. If score changes rarely, only update the text when it changes (more efficient)."

---

**Q3: "I want the game to load a new scene when the player completes a level."**

*A:* "Add `using UnityEngine.SceneManagement;` at the top. In your script:
```csharp
if(levelComplete)
{
    SceneManager.LoadScene("Level2");
}
```
Make sure the scene name matches exactly (case-sensitive) and the scene is added to Build Settings (File → Build Settings → drag the scene into the list)."

---

**Q4: "How do I save the player's high score so it persists after closing the game?"**

*A:* "Use PlayerPrefs:
```csharp
// Save:
if(score > PlayerPrefs.GetInt("highScore", 0))
{
    PlayerPrefs.SetInt("highScore", score);
    PlayerPrefs.Save();
}

// Load at game start:
int highScore = PlayerPrefs.GetInt("highScore", 0);
```
The second argument to GetInt is the default value if the key doesn't exist."

---

**Q5: "My health bar (UI Slider) doesn't move when health changes. The value updates, but the visual doesn't."**

*A:* "The Slider's value range might be wrong. Check: Slider → Min Value = 0, Max Value = 100 (or whatever max health is). Then in code:
```csharp
healthSlider.value = currentHealth;
```
If it still doesn't work, verify the Slider's graphics are set up correctly (the handle/fill images are assigned)."

---

## Analogies That Work

1. **"MDA is like cooking. Mechanics are ingredients (salt, oil, herbs). Dynamics are what happens when you mix them (flavors combine, textures change). Aesthetics are how it tastes (delicious, bland, spicy). A great game combines mechanics into satisfying dynamics that create feelings."**
   - This maps an abstract concept to a concrete process.

2. **"Flow state is like tuning a guitar. If the string is too loose (easy), it sounds flat (boring). If it's too tight (hard), it breaks (frustration). The right tension (flow) produces a perfect note (engagement)."**
   - This makes the balance intuitive.

3. **"RectTransform is like a frame on a wall. The anchor is where the frame attaches to the wall. The size is how big the frame is. If you move the anchor, the frame moves. If you change the size, the frame grows or shrinks."**
   - This demystifies RectTransform's two-part system.

---

## Unity-Specific Gotchas

- **Canvas Render Mode matters.** Screen Space - Overlay renders on top of everything (good for pause menus). Screen Space - Camera renders in front of the camera. World Space renders as if in the 3D world. Wrong mode = UI in unexpected places.

- **UI Raycast Target setting controls if elements block clicks.** If a transparent background panel has Raycast Target enabled, it blocks button clicks behind it. Disable it if the panel is just decorative.

- **Text size is affected by font size AND RectTransform size.** A large font in a tiny text box will be clipped. Both matter.

- **Buttons need an Image component and Interactable = true to respond to clicks.** A button that's grayed out (Interactable = false) won't respond.

- **Time.timeScale = 0 affects Physics.FixedUpdate() but not Update().** If you need code to run while paused (UI, menus), put it in Update(), not FixedUpdate().

- **AudioSources don't pause automatically when you set Time.timeScale = 0.** You have to pause/unpause them manually if you want background music to pause too.

- **PlayerPrefs is player-machine local, not cloud-based.** It's saved on disk but only on that specific computer/device. Don't use it for multiplayer high scores.

- **Scene names are case-sensitive in SceneManager.LoadScene().** "Game" and "game" are different. Check your scene name in Build Settings.

---

## Year-Long Differentiators

For year-long courses:
- Have students playtest each other's games regularly. Use feedback to iterate on feel and design. Encourage design documents before building.
- Introduce advanced UI (scroll views, drag-and-drop, dynamic layouts) as optional topics for students interested in polish.
- Let them discover polish opportunities organically. After building a simple game, ask: "How would you make this more satisfying?" Guide them toward screen shake, particles, audio, etc.
- Reuse UI patterns in Units 6, 7, and 8. Menus, score displays, and audio managers should be consistent across projects.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
