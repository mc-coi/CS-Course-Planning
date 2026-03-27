# Day 17: Sprint 3 Begins — Content Depth (More Levels / More Content)

**Session Goal:** Begin Sprint 3 by adding your second level or significantly expanding game content.

---

## Today's Focus

Sprint 3 is about depth and polish. Your game loop works. Now make it worth playing from start to finish. Today: build (or block out) level 2, or add the next wave, puzzle layer, or area in your game.

---

## Work Session Agenda

**Minutes 0-5:** Sprint 3 planning: write out Must-Have for Days 17-20.

**Minutes 5-45:** Build level 2 or expand content significantly.

**Minutes 45-55:** Playtest levels 1 and 2 back to back. Does difficulty ramp feel right?

---

## Technical Tips

```csharp
// Level transition — exit triggers that load the next level
public class LevelExit : MonoBehaviour
{
    public string nextSceneName;

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            // Optional: save score/health across levels using GameManager
            SceneManager.LoadScene(nextSceneName);
        }
    }
}

// Keeping score/health when loading a new scene (GameManager must be DontDestroyOnLoad):
// Just make sure GameManager has DontDestroyOnLoad in Awake
// and track health/score as public static variables

// Scene transition with fade effect (bonus — use a Canvas Image set to black):
public IEnumerator FadeAndLoad(string sceneName)
{
    // fade to black, then load
    yield return StartCoroutine(FadeOut());
    SceneManager.LoadScene(sceneName);
}
```

---

## Reflection / Exit Ticket

1. How many levels/areas does your game have now?
2. Is the jump in difficulty between levels fair?

---

## Progress Checklist

- [ ] Second level or major content expansion in progress
- [ ] Level transition working (exit zone → load next scene)
- [ ] Content maintains consistent visual style
- [ ] Scene saved and backed up
