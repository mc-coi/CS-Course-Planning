# Unit 5 Assessment: Game Design Principles & UI

**Name:** ________________
**Date:** ________________
**Total Points:** 100

---

## Part A: Multiple Choice (10 questions, 2 points each = 20 points)

**1.** The MDA framework stands for which three elements?
- A) Model, Design, Action
- B) Mechanics, Dynamics, Aesthetics
- C) Movement, Data, Animation
- D) Menu, Debug, Audio

**2.** What is the primary difference between Canvas Render Mode "Screen Space - Overlay" and "World Space"?
- A) Screen Space renders on top of everything; World Space is positioned in the 3D world
- B) World Space is faster and always recommended
- C) Screen Space can't handle TextMeshPro objects
- D) There is no practical difference

**3.** TextMeshPro is superior to legacy Text because:
- A) It is faster to type
- B) It allows for rich text formatting, better performance, and support for emoji
- C) It works only on mobile devices
- D) It doesn't require any component setup

**4.** A Slider component is typically used for:
- A) Only volume controls
- B) Any value that ranges from min to max (health bars, progress bars, difficulty sliders)
- C) Navigation menus
- D) Only debugging purposes

**5.** To make a Button trigger a C# method when clicked, you:
- A) Use Button.onClick and register your method in the inspector or via code
- B) Create a new script and name it "Button"
- C) Edit the Button's material color
- D) This is not possible in Unity

**6.** Setting `Time.timeScale = 0` in a pause menu script will:
- A) Exit the game immediately
- B) Freeze all physics and animations (anything depending on Time.deltaTime)
- C) Pause only animations, not physics
- D) Crash the game

**7.** PlayerPrefs is used for:
- A) Storing high scores, settings, and player data between game sessions
- B) Creating new players in multiplayer games
- C) Debugging physics issues
- D) Managing UI layouts

**8.** `AudioSource.PlayOneShot()` differs from `AudioSource.Play()` because:
- A) PlayOneShot() plays a clip without needing an AudioSource component
- B) Play() is for 3D sound; PlayOneShot() is for 2D
- C) PlayOneShot() interrupts looping audio and plays a sound immediately without stopping what's playing
- D) There is no difference

**9.** In a particle system, what does the "Emission" module control?
- A) How fast particles move
- B) When and how many particles are spawned
- C) The color of particles
- D) How particles interact with physics

**10.** Flow state (or "the zone") in game design refers to:
- A) A graphical effect that looks cool
- B) The player's mental state of focused enjoyment when difficulty matches skill level
- C) When the game crashes
- D) A specific UI design pattern

---

## Part B: Short Answer (5 questions, 4 points each = 20 points)

**11.** Explain the MDA framework (Mechanics, Dynamics, Aesthetics) using a real game example. How do these three elements work together?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**12.** Describe the steps to hook a Button's onClick event to a C# method. Can you do this in the Inspector, or must you use code? Explain both approaches.

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**13.** What is the practical difference between `AudioSource.Play()` and `AudioSource.PlayOneShot()`? Give an example of when you'd use each.

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**14.** When you set `Time.timeScale = 0` in a pause menu, what does this actually do? Why is this better than disabling objects manually? What are potential issues?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**15.** What is PlayerPrefs and what are three common uses for it? How would you save and load a player's high score using PlayerPrefs?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

---

## Part C: Coding Challenges (3 challenges, 20 points each = 60 points)

### Challenge 1: UIManager Script (20 points)

Write a UIManager script that:
- Has public references to a TextMeshPro Text component (for score) and a Slider component (for health bar)
- Includes an `UpdateScore(int score)` method that updates the score text
- Includes an `UpdateHealth(int current, int max)` method that updates the Slider's value and optionally displays health text
- Implements the Awake singleton pattern (so only one UIManager exists)
- Call both methods from Start() to demonstrate they work

```csharp
using UnityEngine;
using TMPro;
using UnityEngine.UI;

public class UIManager : MonoBehaviour
{
    // Your code here
}
```

**Grading Criteria:**
- [ ] Correct singleton pattern in Awake() (4 pts)
- [ ] Public references to TextMeshPro Text and Slider (3 pts)
- [ ] UpdateScore() method correctly updates text (4 pts)
- [ ] UpdateHealth() method correctly updates Slider.value (4 pts)
- [ ] Demonstrates both methods working in Start() (5 pts)

---

### Challenge 2: PauseMenu Script (20 points)

Write a PauseMenu script that:
- Has a public reference to a pause panel (UI Image or Panel)
- Toggles the pause panel on/off when the Escape key is pressed
- Sets `Time.timeScale = 0` when paused (freezes game)
- Sets `Time.timeScale = 1` when unpaused (resumes game)
- Logs "Game Paused" and "Game Resumed" to the console
- Handles the case where the pause panel might already be active/inactive

```csharp
using UnityEngine;

public class PauseMenu : MonoBehaviour
{
    // Your code here
}
```

**Grading Criteria:**
- [ ] Public reference to pause panel (3 pts)
- [ ] Detects Escape key press in Update() (3 pts)
- [ ] Toggles panel active/inactive (4 pts)
- [ ] Sets Time.timeScale correctly (5 pts)
- [ ] Logs pause/resume messages (3 pts)
- [ ] Handles edge cases properly (2 pts)

---

### Challenge 3: MainMenu Script (20 points)

Write a MainMenu script that:
- Has a `PlayGame()` method that loads the scene named "Level1"
- Has a `QuitGame()` method that quits the application
- Both methods can be called from Button onClick events
- Includes a Debug.Log message when each method is called
- Optionally, adds a UI confirmation for quit (are you sure?)

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
    // Your code here
}
```

**Grading Criteria:**
- [ ] PlayGame() loads "Level1" correctly (6 pts)
- [ ] QuitGame() quits application correctly (6 pts)
- [ ] Both methods log appropriate messages (4 pts)
- [ ] Methods can be called from Button onClick (2 pts)
- [ ] Bonus: Quit confirmation dialog (+2 pts optional)

---

## Complete Answer Key

### Part A: Multiple Choice Answer Key

1. **B** - Mechanics, Dynamics, Aesthetics
2. **A** - Screen Space renders on top of everything; World Space is positioned in the 3D world
3. **B** - It allows for rich text formatting, better performance, and support for emoji
4. **B** - Any value that ranges from min to max (health bars, progress bars, difficulty sliders)
5. **A** - Use Button.onClick and register your method in the inspector or via code
6. **B** - Freeze all physics and animations (anything depending on Time.deltaTime)
7. **A** - Storing high scores, settings, and player data between game sessions
8. **C** - PlayOneShot() interrupts looping audio and plays a sound immediately without stopping what's playing
9. **B** - When and how many particles are spawned
10. **B** - The player's mental state of focused enjoyment when difficulty matches skill level

**Score: __ / 20 points**

---

### Part B: Short Answer Answer Key

**11. MDA Framework Explanation**

The MDA framework helps designers think about games at three levels:
- **Mechanics** are the rules and systems (e.g., in Mario: jump, move left/right, collect coins)
- **Dynamics** are how mechanics interact and create gameplay (e.g., jumping over gaps, jumping on enemies to defeat them)
- **Aesthetics** are the experiences players feel (e.g., fun, challenge, excitement, satisfaction)

Example: In a health bar system—
- **Mechanic:** Health value decreases when damaged, increases when healed
- **Dynamic:** Player sees health drop during combat, must find cover or healing items
- **Aesthetic:** Creates tension, urgency, and relief when healed

All three must align for the game to feel good.

**12. Hooking Button onClick Events**

**Inspector Method:**
1. Select the Button in the Hierarchy
2. In the Inspector, find the Button component
3. Scroll to the "On Click ()" event
4. Click the "+" button to add a listener
5. Drag your script's GameObject into the object field
6. Select your script from the dropdown
7. Choose the method from the function dropdown

**Code Method:**
```csharp
Button myButton = GetComponent<Button>();
myButton.onClick.AddListener(() => MyMethod());
```

Both are valid; the Inspector method is easier for beginners, while code is more flexible for dynamic scenarios.

**13. AudioSource.Play() vs PlayOneShot()**

- **Play()** starts playing the audio clip assigned to the AudioSource. If audio is already playing, it restarts it.
- **PlayOneShot()** plays a specific audio clip once without interrupting what's currently playing. Good for overlapping sounds.

Examples:
- **Play()**: Background music, looping ambient sound
- **PlayOneShot()**: Jump sound, coin pickup sound (can happen multiple times while music plays)

**14. Time.timeScale = 0 Explanation**

When you set `Time.timeScale = 0`, all time-dependent systems freeze:
- Animations stop
- Physics simulation stops
- Anything using Time.deltaTime stops (like movement scripts)
- Update() and FixedUpdate() still run, but Time.deltaTime = 0

Why it's better than disabling objects:
- You don't have to track and re-enable every moving object
- UI can still be interacted with
- Only one line of code to freeze everything

Potential issues:
- UI animations might also freeze (solution: use unscaled delta time for UI)
- Audio continues playing (you must pause manually if desired)
- Coroutines using WaitForSeconds stop (use WaitForSecondsRealtime instead)

**15. PlayerPrefs Explanation**

PlayerPrefs is a data storage system that persists between game sessions. It stores key-value pairs (strings, ints, floats).

Common uses:
1. **High scores** - Save and load best scores
2. **Game settings** - Save volume, difficulty, graphics quality
3. **Progress** - Save which levels are unlocked

Example: Save and load high score
```csharp
// Save
PlayerPrefs.SetInt("HighScore", 1500);
PlayerPrefs.Save();

// Load
int highScore = PlayerPrefs.GetInt("HighScore", 0); // 0 is default if not found
```

**Score: __ / 20 points**

---

### Part C: Coding Challenges Answer Key

#### Challenge 1: UIManager Script Solution

```csharp
using UnityEngine;
using TMPro;
using UnityEngine.UI;

public class UIManager : MonoBehaviour
{
    public TextMeshProUGUI scoreText;
    public Slider healthSlider;

    private static UIManager instance;

    private void Awake()
    {
        if (instance == null)
        {
            instance = this;
        }
        else
        {
            Destroy(gameObject);
        }
    }

    private void Start()
    {
        UpdateScore(0);
        UpdateHealth(100, 100);
    }

    public void UpdateScore(int score)
    {
        scoreText.text = "Score: " + score;
    }

    public void UpdateHealth(int current, int max)
    {
        healthSlider.value = (float)current / max;
        // Optional: also display health text
        Debug.Log($"Health: {current}/{max}");
    }
}
```

**Grading:**
- Singleton pattern correct (checks if instance exists, destroys duplicate) - 4 pts
- Public references properly typed (TextMeshProUGUI, Slider) - 3 pts
- UpdateScore updates text correctly - 4 pts
- UpdateHealth calculates ratio and sets slider value - 4 pts
- Both methods called and work in Start() - 5 pts

---

#### Challenge 2: PauseMenu Script Solution

```csharp
using UnityEngine;

public class PauseMenu : MonoBehaviour
{
    public GameObject pausePanel;

    private bool isPaused = false;

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape))
        {
            TogglePause();
        }
    }

    private void TogglePause()
    {
        isPaused = !isPaused;

        if (isPaused)
        {
            pausePanel.SetActive(true);
            Time.timeScale = 0f;
            Debug.Log("Game Paused");
        }
        else
        {
            pausePanel.SetActive(false);
            Time.timeScale = 1f;
            Debug.Log("Game Resumed");
        }
    }
}
```

**Grading:**
- Public reference to pause panel - 3 pts
- Detects Escape key with GetKeyDown() - 3 pts
- Toggles panel active/inactive correctly - 4 pts
- Time.timeScale set correctly for pause and resume - 5 pts
- Logs "Game Paused" and "Game Resumed" - 3 pts
- Handles toggle state properly - 2 pts

---

#### Challenge 3: MainMenu Script Solution

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
    public void PlayGame()
    {
        Debug.Log("Loading Level1...");
        SceneManager.LoadScene("Level1");
    }

    public void QuitGame()
    {
        Debug.Log("Quitting game...");
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }
}
```

**Alternative with Quit Confirmation:**

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
    public GameObject quitConfirmPanel;

    public void PlayGame()
    {
        Debug.Log("Loading Level1...");
        SceneManager.LoadScene("Level1");
    }

    public void ShowQuitConfirmation()
    {
        if (quitConfirmPanel != null)
        {
            quitConfirmPanel.SetActive(true);
        }
    }

    public void ConfirmQuit()
    {
        Debug.Log("Quitting game...");
        #if UNITY_EDITOR
            UnityEditor.EditorApplication.isPlaying = false;
        #else
            Application.Quit();
        #endif
    }

    public void CancelQuit()
    {
        if (quitConfirmPanel != null)
        {
            quitConfirmPanel.SetActive(false);
        }
    }
}
```

**Grading:**
- PlayGame() loads "Level1" - 6 pts
- QuitGame() quits correctly - 6 pts
- Both methods log appropriate messages - 4 pts
- Methods accessible from Button onClick - 2 pts
- Bonus: Quit confirmation dialog - +2 pts

---

## Grading Scale

- **A (90–100):** Excellent. Strong understanding of UI systems, game design principles, and C# scripting.
- **B (80–89):** Very good. Solid grasp of concepts with minor gaps.
- **C (70–79):** Good. Understands key concepts but some gaps in application.
- **D (60–69):** Meets minimum standards. Needs more practice.
- **F (Below 60):** Does not meet standards. Significant gaps in understanding.

---

## Submission Checklist

Before submitting:
- [ ] All 10 multiple choice questions answered
- [ ] All 5 short answer questions answered thoroughly
- [ ] Challenge 1: UIManager script compiles and runs
- [ ] Challenge 2: PauseMenu script compiles and runs
- [ ] Challenge 3: MainMenu script compiles and runs
- [ ] Answer key reviewed (for self-grading)
- [ ] Assignment submitted on time

---
