# Day 12: PlayerPrefs & Saving High Scores

**Learning Target:** I can save and load game data using PlayerPrefs.

---

## Key Concepts

**PlayerPrefs**: Simple key-value storage for game data (settings, high scores, progress).
- Persists between game sessions
- Works on all platforms (PC, Mobile, Web)
- Limited to int, float, and string types

**Keys**: Unique identifiers for each data point (e.g., "HighScore", "PlayerName").

**Initialization**: Check if key exists before reading; provide default value if not found.

---

## Code Example

```csharp
using UnityEngine;
using TMPro;

public class HighScoreManager : MonoBehaviour
{
    private const string HIGH_SCORE_KEY = "HighScore";
    private const string PLAYER_NAME_KEY = "PlayerName";
    
    public TextMeshProUGUI highScoreText;
    private int highScore = 0;

    private void Start()
    {
        LoadHighScore();
        DisplayHighScore();
    }

    public void CheckAndSaveHighScore(int newScore)
    {
        if (newScore > highScore)
        {
            highScore = newScore;
            PlayerPrefs.SetInt(HIGH_SCORE_KEY, highScore);
            PlayerPrefs.Save(); // Force save to disk
            DisplayHighScore();
            Debug.Log($"New high score: {highScore}!");
        }
    }

    private void LoadHighScore()
    {
        // GetInt with default value 0
        highScore = PlayerPrefs.GetInt(HIGH_SCORE_KEY, 0);
    }

    private void DisplayHighScore()
    {
        highScoreText.text = $"High Score: {highScore.ToString("N0")}";
    }

    public void ClearHighScore()
    {
        PlayerPrefs.DeleteKey(HIGH_SCORE_KEY);
        highScore = 0;
        DisplayHighScore();
    }
}
```

---

## Unity Setup Steps

1. **Create High Score Display**:
   - TextMeshPro text: "High Score: 0"
   - Position: Bottom-right

2. **Attach Script**:
   - Create `HighScoreManager.cs`
   - Attach to the text GameObject
   - In Inspector, assign the TextMeshPro reference

3. **Test Persistence**:
   - Play game, score 1000 points
   - Close game
   - Reopen game
   - High score should still be 1000

4. **Clear Cache** (if needed):
   - Edit → Project Settings → Editor → Clear PlayerPrefs button
   - Or call `PlayerPrefs.DeleteAll();` in code

---

## Guided Practice

1. **Save & Load High Score**:
   - Implement high score system
   - Beat the current high score
   - Close and reopen game
   - Verify it persists

2. **Multiple Values**:
   - Save high score, last level completed, player name
   - Load all at startup
   - Display them together

3. **Settings Persistence**:
   - Save volume level, graphics quality
   - Load on startup
   - Apply saved settings automatically

---

## Practice Problems

**Beginner:**
Save the player's name to PlayerPrefs when they enter it. Load and display on next game session.

**Intermediate:**
Create a leaderboard that saves the top 5 scores with player names. Display on a menu.

**Challenge:**
Implement a save game system that saves: position, health, inventory, and playtime. Load and restore game state.

<details><summary>💡 Hints</summary>
- Beginner: Use SetString/GetString for text, use a default value
- Intermediate: Use numbered keys (HighScore0, HighScore1, etc.) or serialize to JSON
- Challenge: Create a SaveData class, serialize to JSON, save to a file
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public void SavePlayerName(string name)
{
    PlayerPrefs.SetString("PlayerName", name);
}

public string LoadPlayerName()
{
    return PlayerPrefs.GetString("PlayerName", "Player");
}
```

**Intermediate:**
```csharp
public void SaveScore(string name, int score)
{
    for (int i = 0; i < 5; i++)
    {
        if (score > PlayerPrefs.GetInt($"Score{i}", 0))
        {
            PlayerPrefs.SetString($"Name{i}", name);
            PlayerPrefs.SetInt($"Score{i}", score);
            break;
        }
    }
}
```

**Challenge:**
```csharp
[System.Serializable]
public class SaveData
{
    public Vector3 playerPosition;
    public int health;
    public int[] inventory;
}

public void SaveGame()
{
    SaveData data = new SaveData { /* populate */ };
    string json = JsonUtility.ToJson(data);
    System.IO.File.WriteAllText("save.json", json);
}
```
</details>
