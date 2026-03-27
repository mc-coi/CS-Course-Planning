# Day 4: Planning Check-In — Teacher Review & Sprint Planning

**Session Goal:** Get teacher feedback on your GDD and plan your first sprint in detail.

---

## Today's Focus

Before you write a single line of code, today's teacher check-in ensures your scope is realistic and your plan is solid. You'll also write out your Sprint 1 task list — a specific checklist of features to build in the next 4 work days.

---

## Work Session Agenda

**Minutes 0-25:** Teacher one-on-one GDD reviews (5 min per student while others work on Sprint 1 planning below).

**Minutes 25-45:** Sprint 1 planning: write out every task you need to complete in Days 5–8.

**Minutes 45-55:** Organize tasks by priority (Must Have / Nice to Have / Future).

---

## Sprint Planning Worksheet

```
SPRINT 1 PLAN (Days 5–8, ~4 work sessions)
Goal: A PLAYABLE PROTOTYPE — player can move and interact with something

MUST HAVE (core — no game without these):
□ Unity project created and configured (correct 2D or 3D template)
□ Player GameObject with correct components (Rigidbody, Collider, Script)
□ Player can move (left/right, or 8-direction for top-down)
□ At least one basic scene with a floor/ground
□ Camera follows player (Cinemachine or manual)
□ 
□ 

SHOULD HAVE (important but not blocking):
□ Player can jump (if platformer) or aim/shoot (if shooter)
□ One enemy placeholder (doesn't need full AI yet)
□ Simple background / placeholder art
□ 
□ 

NICE TO HAVE (bonus if time allows):
□ 
□ 
□ 

By end of Sprint 1, I should be able to demo: ________________________
```

---

## Technical Tips

```csharp
// Unity project setup checklist for Day 5:
// 1. File → New Project → 2D (Core) or 3D template
// 2. Edit → Project Settings → Physics 2D → Gravity Y = -20 (snappier)
// 3. Create folder structure in Project panel:
//    _Scripts / _Sprites / _Prefabs / _Scenes / _Audio
// 4. Save Scene as "Level1" immediately (File → Save As)
// 5. Add scene to Build Settings (File → Build Settings → Add Open Scenes)

// Player setup starting point:
public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 8f;
    public float jumpForce = 15f;
    private Rigidbody2D rb;

    void Start() => rb = GetComponent<Rigidbody2D>();

    void Update()
    {
        float h = Input.GetAxisRaw("Horizontal");
        rb.velocity = new Vector2(h * moveSpeed, rb.velocity.y);

        if (Input.GetButtonDown("Jump"))
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
    }
}
```

---

## Reflection / Exit Ticket

1. What did your teacher say about your scope? Any changes made?
2. What is your Sprint 1 "definition of done" — what will you demo on Day 9?

---

## Progress Checklist

- [ ] GDD reviewed with teacher
- [ ] Any scope adjustments made to GDD
- [ ] Sprint 1 task list written with Must/Should/Nice-to-have priorities
- [ ] Definition of done written for Sprint 1
- [ ] Ready to start building tomorrow!
