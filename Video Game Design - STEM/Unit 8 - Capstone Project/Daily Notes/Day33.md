# Day 33: Playtesting & Feedback

**Learning Target:** Conduct playtesting with real players and use feedback to iterate on your game design.

### Key Concepts

- **Playtesting:** Having actual players test your game
- **Feedback Collection:** Structured questions to gather data
- **Quantitative Data:** Measurable metrics (time to win, deaths, score)
- **Qualitative Feedback:** Opinions and feelings
- **A/B Testing:** Testing two versions to see which is better
- **Iteration:** Using feedback to improve the game
- **Bug Reporting:** Documenting issues for fixing
- **Design Validation:** Proving your design choices are correct

### Content

Playtesting is where you learn if your game is actually fun. You can't know until real players play it.

**Playtesting Questions:**
1. Is the core mechanic fun?
2. Is the difficulty appropriate?
3. Is the goal clear?
4. Is the control responsive?
5. Did you enjoy the experience? (1-10 rating)
6. What was most fun?
7. What was frustrating?
8. Would you recommend this game?

**Playtesting Session:**
1. Brief player on the goal (1 minute)
2. Player plays (5-10 minutes)
3. Observe (don't help or talk)
4. Ask questions
5. Take notes
6. Repeat with 3-5 players

**Data Analysis:**
- Average fun rating
- Common complaints
- Most praised feature
- Difficulty sweet spot

### Code Examples

```csharp
using UnityEngine;
using System.Collections.Generic;

public class PlaytestingManager : MonoBehaviour
{
    // PLAYTESTING: Collect data and feedback

    [System.Serializable]
    public class PlaytestSession
    {
        public string playerName;
        public float sessionTime;
        public int finalScore;
        public int deathCount;
        public float funRating;  // 1-10
        public string feedback;
        public bool wouldRecommend;
    }

    private List<PlaytestSession> sessions = new List<PlaytestSession>();
    private PlaytestSession currentSession;
    private float sessionStartTime;
    private int deathCount = 0;

    void Start()
    {
        StartNewSession("Player 1");
    }

    void Update()
    {
        // Track session time
        if (currentSession != null)
        {
            currentSession.sessionTime = Time.time - sessionStartTime;
        }
    }

    public void StartNewSession(string playerName)
    {
        currentSession = new PlaytestSession();
        currentSession.playerName = playerName;
        sessionStartTime = Time.time;
        deathCount = 0;

        Debug.Log("Playtesting session started: " + playerName);
    }

    public void RecordDeath()
    {
        deathCount++;
        if (currentSession != null)
        {
            currentSession.deathCount = deathCount;
        }
    }

    public void EndSession(int finalScore)
    {
        if (currentSession == null)
            return;

        currentSession.finalScore = finalScore;
        sessions.Add(currentSession);

        Debug.Log("Session ended for: " + currentSession.playerName);
        AnalyzeSessions();
    }

    public void RecordFeedback(string playerName, float funRating, string feedback, bool wouldRecommend)
    {
        PlaytestSession session = sessions.Find(s => s.playerName == playerName);
        if (session != null)
        {
            session.funRating = funRating;
            session.feedback = feedback;
            session.wouldRecommend = wouldRecommend;

            Debug.Log($"Feedback recorded for {playerName}: {funRating}/10");
        }
    }

    void AnalyzeSessions()
    {
        if (sessions.Count == 0)
            return;

        // Calculate averages
        float avgTime = 0;
        float avgScore = 0;
        float avgDeaths = 0;
        float avgFunRating = 0;
        int recommendCount = 0;

        foreach (PlaytestSession session in sessions)
        {
            avgTime += session.sessionTime;
            avgScore += session.finalScore;
            avgDeaths += session.deathCount;
            avgFunRating += session.funRating;
            if (session.wouldRecommend)
                recommendCount++;
        }

        avgTime /= sessions.Count;
        avgScore /= sessions.Count;
        avgDeaths /= sessions.Count;
        avgFunRating /= sessions.Count;

        // Report results
        Debug.Log("=== PLAYTESTING ANALYSIS ===");
        Debug.Log("Sessions: " + sessions.Count);
        Debug.Log("Avg Time: " + avgTime.ToString("F1") + "s");
        Debug.Log("Avg Score: " + avgScore.ToString("F0"));
        Debug.Log("Avg Deaths: " + avgDeaths.ToString("F1"));
        Debug.Log("Avg Fun Rating: " + avgFunRating.ToString("F1") + "/10");
        Debug.Log("Would Recommend: " + recommendCount + "/" + sessions.Count);

        // Iteration recommendations
        if (avgFunRating < 5)
            Debug.LogWarning("Core mechanic may not be fun. Iterate!");
        if (avgDeaths > 10)
            Debug.LogWarning("Game is too hard. Reduce difficulty.");
        if (avgTime < 60)
            Debug.LogWarning("Game is too short. Add more content.");
    }

    public List<PlaytestSession> GetSessions()
    {
        return sessions;
    }
}

// Playtesting UI for gathering feedback
public class PlaytestingUI : MonoBehaviour
{
    public void SubmitFeedback(string playerName, float funRating, string feedback, bool wouldRecommend)
    {
        PlaytestingManager manager = FindObjectOfType<PlaytestingManager>();
        if (manager != null)
        {
            manager.RecordFeedback(playerName, funRating, feedback, wouldRecommend);
        }
    }
}
```

### Guided Practice

1. Create a playtesting plan (how many players, what questions)
2. Set up a simple feedback form
3. Recruit 3-5 playtesters (friends, classmates, etc.)
4. Run each playtesting session
5. Record metrics: time, score, deaths, fun rating
6. Collect qualitative feedback
7. Analyze results and identify patterns
8. Plan iterations based on feedback

### Practice Problems

**Problem 1 — Beginner:** Create a playtesting feedback form with at least 5 questions.

**Problem 2 — Intermediate:** Conduct playtesting with 3 players and document their responses.

**Problem 3 — Challenge:** Analyze playtesting data, identify 3 specific changes, and implement them based on feedback.

<details>
<summary>Hints</summary>

**Problem 1:** Ask: fun rating (1-10), most fun part, frustrating part, difficulty level, would recommend (yes/no).

**Problem 2:** Track: session time, deaths, final score, and responses to questions. Keep notes on behaviors you observe.

**Problem 3:** Look for patterns: If multiple players say something is too hard, reduce difficulty. If they all loved a feature, emphasize it more.

</details>

<details>
<summary>Sample Answers</summary>

**Sample Feedback Form:**
- On a scale of 1-10, how fun was the game? ___
- What part did you enjoy most? _______
- What was most frustrating? _______
- How difficult was the game? (Too easy / Just right / Too hard)
- Would you recommend this game to a friend? (Yes / No)

**Sample Data Analysis:**
- Avg fun rating: 6.7/10 (decent)
- Common feedback: "Too hard early on"
- Most praised: "Core mechanic feels good"
- Iteration: Reduce enemy health in first level

</details>
