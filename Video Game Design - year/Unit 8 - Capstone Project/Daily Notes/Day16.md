# Day 16: Sprint 2 Wrap-Up — Menus & Scene Management

**Session Goal:** Build a functional main menu and game-over screen with scene transitions.

---

## Today's Focus

A game without a main menu feels like a prototype. Today you add the frame around your game: the main menu that starts the experience, and the game-over screen that closes it.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up: Sprint 2 Must-Have checklist — what's done, what's left?

**Minutes 5-40:** Build Main Menu and Game Over scenes.

**Minutes 40-55:** Test full flow: main menu → play → die → game over → back to menu. Save.

---

## Technical Tips

```csharp
// Main Menu script
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
    public void PlayGame()
    {
        SceneManager.LoadScene("Level1");
    }

    public void QuitGame()
    {
        Application.Quit();
    }
}

// IMPORTANT: Add ALL scenes to File → Build Settings → Scenes In Build

// Pause menu (Time.timeScale pauses physics and animations)
public class PauseMenu : MonoBehaviour
{
    public GameObject pausePanel;
    private bool isPaused = false;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Escape)) TogglePause();
    }

    public void TogglePause()
    {
        isPaused = !isPaused;
        Time.timeScale = isPaused ? 0f : 1f;
        pausePanel.SetActive(isPaused);
    }

    public void ResumeGame() { isPaused = false; Time.timeScale = 1f; pausePanel.SetActive(false); }
    public void GoToMainMenu() { Time.timeScale = 1f; SceneManager.LoadScene("MainMenu"); }
}
```

---

## Reflection / Exit Ticket

1. Can you complete the full game loop (menu → play → die/win → back to menu)? Y / N
2. What's the first Sprint 3 task?

---

## Progress Checklist

- [ ] Main menu scene with at least Play and Quit buttons
- [ ] Game Over scene with Retry and Main Menu buttons
- [ ] Pause menu working with Escape key
- [ ] All scenes added to Build Settings
- [ ] Full game loop playable start to finish
- [ ] Scene saved and backed up
