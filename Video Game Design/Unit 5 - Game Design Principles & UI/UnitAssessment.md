# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. Explain the MDA framework and give an example from a game.

2. What is the core game loop?

3. What is grayboxing and why is it useful?

4. How do you create a responsive UI that works on different screen sizes?

5. What is TextMeshPro and how does it differ from legacy Text?

6. How do you load a new scene and why would you use SceneManager?

7. What does PlayerPrefs do and how do you use it?

8. How do you make a button load a new scene?

9. Explain the difference between teaching through play and explicit tutorials.

10. What are Bartle Types and why do game designers care?

---

**Answers:**

1. **MDA = Mechanics (rules), Dynamics (interactions), Aesthetics (emotions). Example:** Pac-Man's mechanic of eating pellets creates the dynamic of avoiding ghosts, which creates the aesthetic of suspense and relief.

2. **Feedback (see result) → Input (make decision) → Resolution (mechanics respond) → Repeat.** Every game repeats this cycle.

3. **Using simple placeholder shapes (gray boxes) to prototype level layouts.** It's useful for testing gameplay mechanics without waiting for final art.

4. **Use Anchors to position elements relative to screen edges.** Use Layout Groups to auto-arrange child elements.

5. **TextMeshPro is modern, high-quality text rendering.** It supports rich text tags, scales beautifully, and looks professional. Legacy Text is lower quality.

6. **Use `SceneManager.LoadScene("SceneName");`.** SceneManager organizes multiple scenes (menus, levels, etc.) and manages transitions.

7. **PlayerPrefs saves small amounts of persistent data (high scores, settings).** Use `PlayerPrefs.SetInt("key", value);` to save and `PlayerPrefs.GetInt("key");` to load.

8. **Add an onClick listener to the button.** In the callback, use `SceneManager.LoadScene("SceneName");`.

9. **Teaching through play:** level design forces players to learn by doing. **Explicit tutorials:** text/narration explains mechanics. Play teaches better because players learn by experience.

10. **Four player motivations:** Achiever (challenge), Explorer (discovery), Socializer (interaction), Killer (competition). Designers create content for each type to appeal to diverse players.

---
