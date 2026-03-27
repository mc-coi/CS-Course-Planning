# Day 20: Documentation — Comments, README & Known Bugs

**Session Goal:** Write code documentation, a project README, and a known-bugs list.

---

## Today's Focus

Documentation is 15 points on the rubric — don't leave them on the table. Good documentation also makes YOU look professional. Today you write summary comments in every script, create a README file, and honestly list known bugs.

---

## Work Session Agenda

**Minutes 0-5:** Count your scripts. Write down which ones have NO comments yet.

**Minutes 5-40:** Add XML summary comments to every public method. Write README.

**Minutes 40-55:** Write the Known Bugs list. A well-documented bug is better than a hidden one.

---

## Documentation Standards

```csharp
// Every script should have a header comment:
/// <summary>
/// Manages player movement, jumping, and damage response.
/// Requires: Rigidbody2D, Collider2D, groundLayer assigned in Inspector.
/// </summary>
public class PlayerController : MonoBehaviour
{
    /// <summary>
    /// Player movement speed in units per second.
    /// </summary>
    public float moveSpeed = 8f;

    /// <summary>
    /// Applies horizontal movement and handles jump input.
    /// Called once per frame by Unity.
    /// </summary>
    void Update()
    {
        // Get horizontal input (-1 left, 0 none, 1 right)
        float h = Input.GetAxisRaw("Horizontal");
        // Apply velocity preserving existing vertical (y) velocity for gravity
        rb.velocity = new Vector2(h * moveSpeed, rb.velocity.y);
    }
}
```

---

## README Template

```
# [Game Title]
By: [Your Name]
Date: [Today's Date]
Unity Version: [e.g., 2022.3 LTS]

## Description
[2-3 sentences: what is the game? What's the core mechanic?]

## How to Play
[Controls listed simply — arrow keys or WASD, Space to jump, etc.]

## Game Features
- [Feature 1]
- [Feature 2]
- [Feature 3]

## Known Bugs / Limitations
1. [Bug description — be specific]
2. [Bug description]
3. (If none: "No known critical bugs as of submission date")

## Credits
- Game design and code: [Your name]
- Audio: [Source, e.g., freesound.org (CC0)]
- Art assets: [Kenney.nl, Unity Asset Store, original, etc.]
```

---

## Reflection / Exit Ticket

1. How many scripts did you add comments to today?
2. Is your README honest about what works and what doesn't?

---

## Progress Checklist

- [ ] Every script has a header summary comment
- [ ] Every public method has a comment
- [ ] README.md or README.txt created in project folder
- [ ] Known bugs list written and honest
- [ ] Documentation saved and backed up
