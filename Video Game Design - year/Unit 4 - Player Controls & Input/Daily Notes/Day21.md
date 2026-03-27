# Day 21: Player Controller Mini-Project

**Learning Target:** I can design and implement a complete working character controller of my choice.

---

## Project Overview

Choose one of the following controller types and build a fully functional, polished implementation:

1. **3rd Person Action Hero** — Camera behind player, smooth rotation, combat-ready stance
2. **FPS Tactical Shooter** — Sprint, aim-down-sights, stamina, footstep audio
3. **Retro Platformer** — Pixel-perfect jumps, wall sliding, double-jump, animated sprite
4. **Top-Down RPG** — Grid-based or continuous movement, smooth isometric camera, NPC interaction detection
5. **Parkour Freerunner** — Wall running, ledge grabbing, vaulting, momentum-based movement

---

## Requirements (All Controllers)

**Must Include:**
- [x] Movement (keyboard + gamepad compatible)
- [x] Jumping/Airborne mechanics
- [x] Camera system (follow or relative)
- [x] Ground detection
- [x] At least 3 distinct player states (Idle, Moving, Airborne, etc.)
- [x] Animation blending (if using animator)
- [x] One unique mechanic (sprint, wall run, zoom, etc.)
- [x] Debug visual feedback (DrawRay, Debug.Log, on-screen text)

**Code Quality:**
- Clean, readable code with comments
- No magic numbers (use public variables for tweaking)
- Efficient (no frame-rate dependent bugs)
- Extensible (easy to add new states/features)

---

## Development Checklist

### Phase 1: Core Movement (Days 21 – Day 21 afternoon)
- [ ] Create basic movement system
- [ ] Implement jumping and ground detection
- [ ] Test with keyboard and gamepad
- [ ] Tweak speed/jump feel

### Phase 2: Camera & Feedback (Day 21 late afternoon)
- [ ] Implement chosen camera system
- [ ] Add smooth transitions and damping
- [ ] Add debug visual feedback

### Phase 3: Polish & Polish (Day 21 evening)
- [ ] Implement animations or state machine
- [ ] Add the unique mechanic
- [ ] Add audio cues (jump, land, step)
- [ ] Playtesting and feel tuning

### Phase 4: Documentation
- [ ] Comment all code
- [ ] Write a 1-page design document explaining the control scheme
- [ ] List assumptions and known limitations

---

## Example Structure: 3rd Person Action Hero

```csharp
// PlayerController.cs (main controller)
public class PlayerController : MonoBehaviour
{
    enum State { Idle, Walking, Jumping, Dashing, Attacking }
    private State currentState;

    // Movement
    public float walkSpeed = 5f;
    public float sprintSpeed = 10f;
    
    // Jumping
    public float jumpForce = 5f;
    private int jumpCount = 0;
    
    // Camera
    private CinemachineVirtualCamera virtualCam;
    
    // Components
    private CharacterController controller;
    private Animator animator;

    void Update() { /* Main loop */ }
    void HandleInput() { /* Read input */ }
    void UpdateState() { /* State machine */ }
}

// Additional supporting classes:
// - CameraFollowBehavior.cs — Camera logic
// - PlayerAnimationController.cs — Animation blending
// - AttackSystem.cs — Combat mechanics
```

---

## Design Document Template

```
PROJECT: [Chosen Controller Type]

CONTROLS:
- WASD / Left Stick: Move
- Space / A Button: Jump
- Shift / LB: Sprint
- Right-click / RB: Aim/Ability
- Mouse X/Y: Look Around

UNIQUE MECHANIC:
- Describe your main feature (dash, wall run, zoom, etc.)
- How it feels (responsive? weighty? floaty?)
- Why it's fun

CHALLENGES & SOLUTIONS:
- What was hard to implement?
- How did you solve it?

KNOWN LIMITATIONS:
- Edge cases or incomplete features
- Performance considerations
```

---

## Submission Checklist

- [ ] Playable scene with working controller
- [ ] All states transitioning correctly
- [ ] Keyboard + gamepad fully supported
- [ ] Camera follows/responds properly
- [ ] At least one unique mechanic implemented
- [ ] Code is clean and documented
- [ ] Design document (1 page, PDF or .txt)
- [ ] Test scene with ground and obstacles

---

## Playtesting Checklist

Before submitting, playtest and verify:
- [ ] Movement feels responsive (not sluggish or overly twitchy)
- [ ] Camera doesn't obscure important views
- [ ] Jump height and feel match intention
- [ ] Transitions between states are smooth
- [ ] No physics glitches or clipping
- [ ] Gamepad and keyboard both work
- [ ] Can complete basic movement challenges (jump between platforms, navigate maze, etc.)

---

## Bonus Challenges (If Time)

- **Audio Design:** Add footstep sounds, landing impacts, breathing cues
- **UI Integration:** On-screen stamina bar, health display, objective markers
- **Advanced Camera:** Collision avoidance, lead-ahead aiming, dynamic zoom
- **VFX:** Jump trails, landing dust, dash effects
- **Networking:** (Advanced) Sync controller state for multiplayer

---

## Grading Rubric (Adapted)

| Criteria | Excellent | Good | Okay | Needs Work |
|----------|-----------|------|------|-----------|
| **Core Movement** | Smooth, responsive, feels polished | Works well, minor tuning needed | Functional but feels awkward | Bugs or incomplete |
| **Camera System** | Perfect framing, no clipping, smooth | Good framing, minor issues | Works but needs tweaking | Broken or missing |
| **State Machine** | Clean, extensible, all transitions work | Mostly works, some edge cases | Works but messy | Incomplete or broken |
| **Unique Mechanic** | Well-implemented, fun, integrated | Works, adds interest | Functional but boring | Missing or broken |
| **Code Quality** | Clean, well-commented, efficient | Good structure, mostly clear | Readable but some mess | Confusing, uncommented |
| **Playtesting** | Feels great, ready for shipping | Very playable, minor tweaks | Playable but rough edges | Not fun or broken |

---

## Resources

- Previous days' code examples (Days 1–20)
- Unity Cinemachine package documentation
- Input System documentation
- Animator documentation
- Physics and CharacterController docs
