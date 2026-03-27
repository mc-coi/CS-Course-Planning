# Day 5: Sprint 1 Begins — Project Setup & Player Movement

**Session Goal:** Create the Unity project, set up the player, and get movement working.

---

## Today's Focus

Today is day one of building. The #1 rule: start with what you KNOW. Player movement is something you've done before (Unit 4) — get it working first. Resist the urge to add fancy features before the core works.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up: "Today I will build ___. My biggest unknown is ___."

**Minutes 5-45:** Project setup and player movement (see tasks below).

**Minutes 45-55:** Test what you built. Save EVERYTHING. Make a backup copy of your project folder.

---

## Today's Build Tasks

```
□ Create new Unity project (2D Core or 3D — match your GDD)
□ Create folder structure: _Scripts, _Sprites, _Prefabs, _Scenes, _Audio, _Prefabs
□ Create the main level scene and save it as "Level1"
□ Add scene to Build Settings
□ Create Player GameObject:
    - Add Rigidbody2D (freeze Z rotation!)
    - Add Collider2D (Capsule or Box)
    - Add PlayerController.cs script
□ Create a ground/floor with a Collider2D
□ Player moves left/right ✓
□ Player jumps ✓ (or 8-dir for top-down)
□ Camera follows player (add Cinemachine: Package Manager → Cinemachine)
□ SAVE SCENE. SAVE PROJECT.
```

---

## Technical Tips

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [Header("Movement")]
    public float moveSpeed = 8f;
    public float jumpForce = 16f;
    public LayerMask groundLayer;

    private Rigidbody2D rb;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Horizontal movement
        float h = Input.GetAxisRaw("Horizontal");
        rb.velocity = new Vector2(h * moveSpeed, rb.velocity.y);

        // Ground check using a small raycast downward
        isGrounded = Physics2D.Raycast(
            transform.position,
            Vector2.down,
            0.6f,
            groundLayer
        );

        // Jump
        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
        }

        // Flip sprite direction
        if (h > 0) transform.localScale = new Vector3(1, 1, 1);
        else if (h < 0) transform.localScale = new Vector3(-1, 1, 1);
    }
}
// REMEMBER: Set groundLayer in Inspector → create a "Ground" layer
// and assign it to your floor/platform GameObjects
```

---

## Reflection / Exit Ticket

1. Is the player moving? Yes / No — if no, what error are you getting?
2. What will you build first tomorrow?

---

## Progress Checklist

- [ ] Unity project created with folder structure
- [ ] Level1 scene created and in Build Settings
- [ ] Player moves left/right (or 8-direction)
- [ ] Player jumps (or appropriate primary action)
- [ ] Camera follows player
- [ ] Scene saved and project backed up
