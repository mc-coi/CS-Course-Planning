# Day 3: GDD Completion — Controls, Tech Plan & Scenes

**Session Goal:** Finish your Game Design Document including controls, technical plan, and scene list.

---

## Today's Focus

A complete GDD includes not just the vision but the technical blueprint: what scenes exist, what scripts you'll need, and exactly how the controls work. Finishing this today means you can hit the ground running in Sprint 1.

---

## Work Session Agenda

**Minutes 0-5:** Quick partner share: what's one thing you figured out about your game design since yesterday?

**Minutes 5-40:** Complete GDD Sections 5–8 (controls, technical plan, scene list, art plan).

**Minutes 40-55:** Teacher circulates for quick GDD check-ins. Make revisions based on feedback.

---

## GDD Sections 5–8 Template

```
SECTION 5: CONTROLS
Primary action (jump / shoot / interact): [Key/Button]
Move left/right: 
Move up/down (if top-down):
Secondary action:
Pause:
Special ability (if any):

SECTION 6: TECHNICAL PLAN — SCRIPTS
List every C# script you think you'll need. Next to each, write what it does.
Example:
  - PlayerController.cs → handles movement and jumping
  - EnemyPatrol.cs → moves enemy back and forth
  - GameManager.cs → tracks score, health, scene transitions
  - UIManager.cs → updates score text and health bar
  - (your scripts here...)

SECTION 7: SCENE LIST
List every scene in your game:
  - MainMenu (buttons: Play, Quit, How to Play)
  - Level1 (first playable level)
  - Level2 ...
  - GameOver (retry / main menu buttons)
  - WinScreen (if applicable)

SECTION 8: ART & AUDIO PLAN
Will you use:
  [ ] Unity primitive shapes (cubes, spheres, planes) — easiest
  [ ] Free Unity Asset Store sprites
  [ ] Kenney.nl free assets
  [ ] Your own pixel art
Audio sources:
  [ ] Free SFX from freesound.org or mixkit.co
  [ ] Unity Asset Store audio packs
  [ ] No audio (not recommended for full points)
```

---

## Technical Tips

```csharp
// Scene management reminder (you'll need this for menus):
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
        Debug.Log("Quit (only works in build, not in editor)");
    }
}
// IMPORTANT: Add every scene to File → Build Settings → Scenes In Build
```

---

## Reflection / Exit Ticket

1. How many scripts are in your technical plan? Does that feel manageable?
2. What's the FIRST thing you'll build tomorrow in Sprint 1?

---

## Progress Checklist

- [ ] GDD Sections 5–8 completed
- [ ] Full scene list written out
- [ ] Script list drafted (at least 4–6 scripts named)
- [ ] GDD submitted or shown to teacher
- [ ] Teacher approval noted (if Custom Concept)
