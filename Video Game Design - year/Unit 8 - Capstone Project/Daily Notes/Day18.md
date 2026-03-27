# Day 18: Sprint 3 — Win Conditions & Completion Flow

**Session Goal:** Implement win conditions, a win screen, and the full game completion flow.

---

## Today's Focus

A game needs an ending. Today you make sure there's a satisfying conclusion: completing all levels, surviving X waves, solving all puzzles, or achieving a high score. The win screen is part of the experience.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up check-in.

**Minutes 5-40:** Implement win condition and win screen.

**Minutes 40-55:** Playtest full game: menu → level 1 → level 2 → win. Fix any breaks.

---

## Technical Tips

```csharp
// Win condition check in GameManager
public void CheckWinCondition()
{
    if (currentLevel >= totalLevels && score >= winScore)
    {
        // Load win screen
        SceneManager.LoadScene("WinScreen");
    }
}

// Win screen script
public class WinScreen : MonoBehaviour
{
    public TextMeshProUGUI finalScoreText;

    void Start()
    {
        // Display final score from GameManager
        finalScoreText.text = "Final Score: " + GameManager.instance.score;
        // Save high score
        int highScore = PlayerPrefs.GetInt("HighScore", 0);
        if (GameManager.instance.score > highScore)
            PlayerPrefs.SetInt("HighScore", GameManager.instance.score);
    }

    public void PlayAgain() { SceneManager.LoadScene("MainMenu"); }
}
```

---

## Reflection / Exit Ticket

1. Can the player WIN your game? Yes / No / Almost
2. Is the win screen satisfying? What would make it better?

---

## Progress Checklist

- [ ] Win condition clearly defined and implemented
- [ ] Win screen loads and shows final score
- [ ] High score saved to PlayerPrefs (if applicable)
- [ ] Full game: menu → levels → win → menu all working
- [ ] Scene saved and backed up
