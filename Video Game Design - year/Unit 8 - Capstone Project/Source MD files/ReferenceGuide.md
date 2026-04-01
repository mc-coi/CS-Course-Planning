# Unit 8 Reference Guide: Game Dev Survival Guide

This is your cheat sheet for the capstone sprint. Keep it open while you code.

---

## Build Settings & Export Steps

### Windows Standalone Build
1. **File → Build Settings**
2. **Add Open Scenes** (click button to add current scene)
3. Check all scenes you want in the build:
   - MainMenu (if you have one)
   - GameScene(s)
   - EndScreen (if you have one)
4. Select **PC, Mac & Linux Standalone** in the Scenes In Build list
5. Set **Target Platform** to Windows
6. Click **Build** → choose output folder
7. Unity generates `.exe` — done!

**Test it:** Run the .exe from outside Unity. If it crashes, check Build Settings again.

### WebGL Build
1. **File → Build Settings**
2. Make sure all scenes are in the list (same as Windows)
3. Select **WebGL** as platform
4. Click **Build**
5. Wait 2–5 minutes (first WebGL build is slow)
6. Test locally: Use a live server (e.g., Python `python -m http.server 8000`) and open `http://localhost:8000`

**Remember:** WebGL needs a web server; you can't just double-click the HTML file in your browser.

---

## Script Communication Patterns

### GetComponent: Finding Scripts on the Same Object
```csharp
// Get the Rigidbody2D on THIS gameObject
Rigidbody2D rb = GetComponent<Rigidbody2D>();

// Get a custom script on THIS gameObject
PlayerHealth health = GetComponent<PlayerHealth>();

// Safe check (returns null if not found)
if (rb != null) {
    rb.velocity = new Vector2(5, 0);
}
```

### FindObjectOfType: Finding a Script Anywhere in the Scene
```csharp
// Find the single GameManager in the entire scene
GameManager gm = FindObjectOfType<GameManager>();

if (gm != null) {
    gm.AddScore(100);
}
```

**Warning:** `FindObjectOfType` is slow if called every frame. Call it once in `Start()` and save the result.

### Singleton Pattern: The "One True Instance"
```csharp
// In your GameManager script:
public class GameManager : MonoBehaviour {
    public static GameManager instance;

    void Awake() {
        if (instance == null) {
            instance = this;
        } else {
            Destroy(gameObject);
        }
    }

    public void AddScore(int points) {
        // score logic here
    }
}

// From anywhere else:
GameManager.instance.AddScore(100);
```

**Why singletons?** Only one GameManager ever exists. No searching needed.

---

## Common Final-Stretch Bugs & Fixes

### Null Reference Exception (NRE)
**Symptom:** Game crashes with "Object reference not set to an instance of an object"

**Causes & Fixes:**
- **Missing GetComponent/FindObjectOfType call:** You assigned a variable in the Inspector, but forgot to get it from script
  ```csharp
  // WRONG:
  Rigidbody2D rb; // Never assigned in code or Inspector
  rb.velocity = Vector2.zero; // CRASH!

  // RIGHT:
  Rigidbody2D rb;
  void Start() {
      rb = GetComponent<Rigidbody2D>();
  }
  ```
- **Destroying an object then using it:**
  ```csharp
  Destroy(enemy);
  enemy.TakeDamage(10); // CRASH! enemy no longer exists
  ```
- **Forgetting to drag a reference into the Inspector:** Create a public field but never set it → NRE

**Fix:** Always debug with `Debug.Log()` before the crash line. Print the object's name to confirm it exists.

### Scene Not in Build Settings
**Symptom:** `SceneManager.LoadScene("GameScene")` doesn't work; game freezes or crashes

**Fix:** Open Build Settings and drag your scenes into the Scenes In Build list, OR type the exact scene name.

### Audio Not Playing
**Symptom:** AudioSource exists but you hear nothing

**Fixes:**
- Is **Play On Awake** checked? (If not, call `GetComponent<AudioSource>().Play()` in code)
- Is **Mute** toggled on? (Check the speaker icon in the Inspector)
- Is the volume at 0? (Drag the volume slider up)
- Is the **Audio Clip** assigned? (Empty slot = no sound)
- Is the game paused? (Check `Time.timeScale`)
- Is there even an AudioSource component? (Add one: **Add Component → Audio Source**)

### Rigidbody Not Moving
**Symptom:** You set `rb.velocity` but nothing happens

**Fixes:**
- Is **Body Type** set to **Dynamic**? (Static bodies don't move)
- Is **Gravity Scale** too high? (Try 0 first)
- Is **Constraints** blocking movement? (Check the Rigidbody2D Constraints)
- Are you setting velocity in `FixedUpdate()`? (Physics runs at a different rate than Update)

### UI Text Not Updating
**Symptom:** Text stays the same no matter what you do

**Fixes:**
```csharp
// Make sure you have a reference to the Text component
public Text scoreText;

void Start() {
    scoreText = GetComponent<Text>(); // or find it another way
}

void UpdateScore(int newScore) {
    scoreText.text = "Score: " + newScore; // Must assign .text, not the Text object
}
```

---

## Version Backup Checklist

**Before you export your final build:**

1. **File → Save Scene** (Ctrl+S)
2. **File → Save Project** (Ctrl+Shift+S)
3. **File → Save As** — save with date:
   - `GameName_v1.0_March26.unity`
4. **Zip your entire project folder:**
   - Right-click project folder → Send to → Compressed Folder (Windows)
   - Or: Drag to a .zip app (Mac)
5. **Store zip somewhere safe** (cloud storage, USB, email to yourself)

**Why?** If Unity corrupts a scene (rare but happens), you have a backup. If someone asks "what was different in version 0.8?", you have it.

---

## GDD Quick Template

When you're planning your game, fill this out:

```
Game Title: [Your Game Name]

Core Concept: [1-2 sentences. What's the game about?]

Player Goals: [What does the player try to do?]

Controls: [What buttons do what?]

Enemies/Obstacles: [What stands in the player's way?]

Win Condition: [How does the player win?]

Lose Condition: [How does the player lose?]

Art Style: [Pixel art? Hand-drawn? Geometric?]

Music/Sound: [What's the audio vibe?]

Victory Screens: [What happens when the player wins?]

Defeat Screens: [What happens when the player loses?]
```

Use this to stay focused. It's okay to change your mind mid-project — just update the GDD.

---

## Prefab Workflow Reminder

**What's a prefab?** A reusable template for a gameObject (enemy, coin, bomb, etc.)

**How to create one:**
1. Build your gameObject in the scene (model, sprite, collider, script, etc.)
2. Drag it into a folder (usually `Assets/Prefabs/`)
3. It becomes blue in the Hierarchy — it's now a prefab
4. Instantiate it with: `Instantiate(prefab, position, rotation)`

**Example:**
```csharp
public GameObject coinPrefab;

void SpawnCoin(Vector3 pos) {
    Instantiate(coinPrefab, pos, Quaternion.identity);
}
```

**Pro tip:** If you change the prefab (add a script, change the sprite), all instances update automatically.

---

## Physics Layers & Tags Quick Setup

### Tags (for identification)
1. **Hierarchy** → Select a gameObject
2. **Inspector** → Top right, **Tag** dropdown → **Add Tag**
3. Type: `Enemy`, `Coin`, `Player`, etc.
4. Use in code:
   ```csharp
   if (collision.gameObject.CompareTag("Enemy")) {
       TakeDamage();
   }
   ```

### Physics Layers (for selective collision)
1. **Edit → Project Settings → Physics2D**
2. Scroll to **Layer Collision Matrix**
3. Uncheck boxes to prevent certain layers from colliding
4. Example: Player layer won't collide with IgnoreClicks layer

**When to use:**
- Tags: Identifying what something IS
- Layers: Controlling what collides with what

---

## PlayerPrefs: Saving High Scores

PlayerPrefs stores simple data (numbers, strings) on the player's computer.

```csharp
// Save
PlayerPrefs.SetInt("HighScore", 5000);
PlayerPrefs.SetString("PlayerName", "Alex");
PlayerPrefs.Save(); // Write to disk

// Load
int highScore = PlayerPrefs.GetInt("HighScore", 0); // 0 is default if not found
string name = PlayerPrefs.GetString("PlayerName", "Player");

// Check if key exists
if (PlayerPrefs.HasKey("HighScore")) {
    Debug.Log("High score exists!");
}

// Delete
PlayerPrefs.DeleteKey("HighScore");
PlayerPrefs.DeleteAll(); // Nuclear option
```

**Use case:** When the game closes, save the high score. When it opens, load it.

```csharp
public class GameManager : MonoBehaviour {
    public int currentScore = 0;
    public int highScore;

    void Start() {
        highScore = PlayerPrefs.GetInt("HighScore", 0);
    }

    public void EndGame() {
        if (currentScore > highScore) {
            highScore = currentScore;
            PlayerPrefs.SetInt("HighScore", highScore);
            PlayerPrefs.Save();
        }
    }
}
```

---

## SceneManager Patterns

### Load a Different Scene
```csharp
using UnityEngine.SceneManagement;

// Load a scene by name
SceneManager.LoadScene("GameScene");

// Load a scene by index (based on Build Settings order)
SceneManager.LoadScene(1);

// Load additively (scene stays loaded alongside current)
SceneManager.LoadScene("UI", LoadSceneMode.Additive);
```

### Reload Current Scene
```csharp
SceneManager.LoadScene(SceneManager.GetActiveScene().name);
```

### Get Current Scene Name
```csharp
string currentScene = SceneManager.GetActiveScene().name;
if (currentScene == "GameScene") {
    // We're in the game
}
```

### Common Pattern: Scene + UI Manager
```csharp
public class UIManager : MonoBehaviour {
    public void OnPlayButtonClicked() {
        SceneManager.LoadScene("GameScene");
    }

    public void OnMainMenuButtonClicked() {
        SceneManager.LoadScene("MainMenu");
    }

    public void OnRetryButtonClicked() {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}
```

---

## Quick Debugging Checklist

Before you ask for help, check:

- [ ] Is the object active in the Hierarchy? (Grey name = inactive)
- [ ] Does the script have `using UnityEngine;` at the top?
- [ ] Are you in Play mode?
- [ ] Did you press Ctrl+S to save?
- [ ] Is the script attached to the right gameObject?
- [ ] Are all Inspector fields assigned (not empty)?
- [ ] Does Build Settings have your scenes?
- [ ] Is there a Console error? (Ctrl+Shift+C)
- [ ] Did you try restarting Unity?

---

**Good luck on your capstone! You've got this.** 🎮
