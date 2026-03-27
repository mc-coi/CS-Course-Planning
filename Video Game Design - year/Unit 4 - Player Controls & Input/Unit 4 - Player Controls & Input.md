# Unit 4: Player Controls & Input

> The player controller is the most important script in any game — it defines how the game FEELS. Learn to build polished, responsive controls that players love.

## Unit Overview

- **Duration:** 22 days / ~4.5 weeks
- **TN Standard:** 9-12.VGD.4 — Design and implement responsive player control systems
- **Prerequisites:** Unit 1 (Unity Interface), Unit 2 (C# Scripting), Unit 3 (Physics & Collision)
- **Key Skills:** Input handling, movement design, animation integration, feel polish

---

## Learning Objectives

By the end of this unit, students will be able to:

1. **Implement smooth, responsive movement** with acceleration and deceleration
2. **Design jump mechanics** with coyote time and jump buffering
3. **Detect ground state** using raycasting and overlap detection
4. **Create polished animations** using Animator state machines
5. **Handle mouse and gamepad input** for aiming and special abilities
6. **Implement shooting mechanics** with projectile spawning
7. **Build special abilities** like dash with cooldown systems
8. **Design game feel** through input polling and movement polish
9. **Create a complete, playable character controller**

---

## Unit Structure

### Week 1: Movement Foundations (Days 1–6)
- **Day 1:** Movement review and refining horizontal controls
- **Day 2:** Acceleration-based movement polish
- **Days 3–4:** Jumping fundamentals and jump variations
- **Days 5–6:** Ground detection methods and visualization

### Week 2: Animation & Direction (Days 7–12)
- **Days 7–8:** Top-down 8-directional movement
- **Days 9–10:** Animator basics and state machines
- **Days 11–12:** Sprite flipping and directional animations

### Week 3: Advanced Input (Days 13–18)
- **Days 13–14:** Mouse input and aiming
- **Days 15–16:** Projectile and shooting mechanics
- **Days 17–18:** Dash and special abilities with cooldowns

### Week 4: Polish & Assessment (Days 19–22)
- **Days 19–20:** Input polish and feel refinement
- **Day 21:** Player controller project lab
- **Day 22:** Unit assessment

---

## Daily Topics at a Glance

| Day | Topic | Key Concept |
|-----|-------|------------|
| 1 | Movement Review | Recap horizontal movement |
| 2 | Acceleration | Smooth speed ramping |
| 3 | Jump Basics | Simple jump implementation |
| 4 | Jump Variations | Variable height, double jump |
| 5 | Ground Detection (Raycasting) | Raycast downward method |
| 6 | Ground Detection (Overlap) | OverlapCircle method |
| 7 | 8-Directional Movement | Normalized diagonal input |
| 8 | Look Direction | Facing toward input direction |
| 9 | Animator Controller | Transitioning between animations |
| 10 | Animation Parameters | SetBool, SetFloat, SetTrigger |
| 11 | Sprite Flipping | Negating scale.x, facing direction |
| 12 | Direction Animations | Combining flip with states |
| 13 | Mouse Input Basics | ScreenToWorldPoint conversion |
| 14 | Aiming System | Direction calculation and visual |
| 15 | Projectile Spawning | Instantiate with velocity |
| 16 | Shooting Mechanics | Ground check, cooldown |
| 17 | Dash Ability | Coroutines, movement override |
| 18 | Cooldown Systems | Timers, ability management |
| 19 | Coyote Time & Jump Buffer | Feel improvements |
| 20 | Movement Polish | Tweaking responsiveness and feel |
| 21 | Project Lab | Build complete controller |
| 22 | Unit Assessment | Comprehensive evaluation |

---

## Essential Concepts

### Input Detection
- **Input.GetKey()** — True while key is held
- **Input.GetKeyDown()** — True only on frame key is first pressed
- **Input.GetKeyUp()** — True only on frame key is released
- **Input.GetAxis()** — Smooth value -1 to 1 (includes gamepad)
- **Input.GetAxisRaw()** — Discrete -1, 0, or 1

### Movement Patterns

**Direct Velocity Control:**
```csharp
rb.velocity = new Vector3(input * speed, rb.velocity.y, 0);
```
Best for: Platformers, pixel-perfect controls, immediate response

**Acceleration-Based:**
```csharp
currentSpeed += input * acceleration * Time.deltaTime;
rb.velocity = new Vector3(currentSpeed, rb.velocity.y, 0);
```
Best for: Smooth feel, realistic momentum, weight

**Physics-Based (AddForce):**
```csharp
rb.AddForce(new Vector3(input * force, 0, 0), ForceMode.Force);
```
Best for: Realistic physics, multiplayer, dynamic interactions

### Jumping Mechanics
- **Simple Jump** — Reset Y velocity, apply upward impulse
- **Variable Height** — Player height affects jump (hold longer = higher)
- **Coyote Time** — Allow jumping for ~0.1-0.2s after leaving ground
- **Jump Buffer** — Store jump input for ~0.05-0.1s to catch mistimed input
- **Double Jump** — Limit airborne jumps, reset on ground

### Ground Detection Methods

**Raycasting:**
```csharp
Physics.Raycast(transform.position, Vector3.down, 0.1f, groundLayer);
```

**OverlapCircle:**
```csharp
Physics.OverlapCircle(transform.position - Vector3.up * 0.5f, 0.3f, groundLayer);
```

**OverlapSphere:**
```csharp
Collider[] hits = Physics.OverlapSphere(transform.position + Vector3.down * 0.1f, radius);
```

### Animation State Machine
- **States** — Different animations (Idle, Run, Jump, Fall)
- **Parameters** — Values controlling transitions (speed, isGrounded, direction)
- **Transitions** — Rules for moving between states
- **Blend Trees** — Smooth blending between animations based on parameter

### Sprite Flipping
```csharp
// Method 1: Negate scale
spriteRenderer.flipX = moveDirection < 0;

// Method 2: Rotate
transform.rotation = moveDirection < 0 ? Quaternion.Euler(0, 180, 0) : Quaternion.identity;
```

### Mouse Input
```csharp
Vector3 mousePos = Input.mousePosition;
mousePos.z = 10f; // Distance from camera
Vector3 worldPos = Camera.main.ScreenToWorldPoint(mousePos);
Vector3 direction = (worldPos - transform.position).normalized;
```

### Projectile Shooting
```csharp
Rigidbody bullet = Instantiate(bulletPrefab, spawnPos, Quaternion.identity);
bullet.velocity = direction * bulletSpeed;
```

### Cooldown System
```csharp
private float cooldownTimer = 0f;

private void Update()
{
    cooldownTimer -= Time.deltaTime;
    if (Input.GetKeyDown(KeyCode.Space) && cooldownTimer <= 0f)
    {
        DoAbility();
        cooldownTimer = cooldownDuration;
    }
}
```

### Dash Ability (Coroutine)
```csharp
IEnumerator DashCoroutine(Vector3 direction)
{
    float elapsed = 0f;
    while (elapsed < dashDuration)
    {
        rb.velocity = direction * dashSpeed;
        elapsed += Time.deltaTime;
        yield return null;
    }
    isDashing = false;
}
```

---

## Common Feel Improvements

1. **Coyote Time** — Players forgive slightly mistimed jumps
2. **Jump Buffering** — Input registered slightly before grounding
3. **Acceleration** — Snappier input, smoother movement
4. **Deceleration** — Feels more controlled and weighty
5. **Input Polling** — Responsive immediate feedback
6. **Drag/Friction** — Prevents sliding, adds control
7. **Speed Clamping** — Prevent infinite acceleration
8. **Animation Blending** — Smooth transitions between states

---

## Tools & Components

### Input System
- **Input Manager** (Edit → Project Settings → Input)
  - Define axes (Horizontal, Vertical, Fire1, etc.)
  - Map keyboard, gamepad, mouse inputs
- **Input Class** — `UnityEngine.Input` namespace
- **Animator** — State machine and animation control
- **Rigidbody / Rigidbody2D** — Physics for movement

### Visualization & Debugging
- `Debug.DrawRay()` — Visualize raycasts
- `Debug.Log()` — Print values
- `Gizmos.DrawWireSphere()` — Show detection areas
- OnGUI display — Show real-time values

---

## Success Criteria

**By Day 22, you should:**
- [ ] Implement smooth, responsive movement with multiple styles
- [ ] Create jump mechanics with coyote time and buffering
- [ ] Build ground detection using multiple methods
- [ ] Integrate animations with state machines
- [ ] Handle mouse aiming and aim visualization
- [ ] Implement projectile shooting with cooldowns
- [ ] Build special abilities (dash) with polished feel
- [ ] Design and debug feel through iteration
- [ ] Create a complete, playable character controller
- [ ] Score 70%+ on the Unit Assessment

---

## Real-World Applications

- **Platformers** — Tight, responsive character control is essential
- **Action Games** — Dash, dodge, multi-jump mechanics
- **RPGs** — Top-down or 3rd-person character control
- **Shooters** — Smooth aiming and shooting mechanics
- **Mobile Games** — Touch-based input and gestures
- **VR Games** — Natural movement and locomotion
- **Multiplayer Games** — Consistent input across network

---

## Resources & References

### Documentation
- [Unity Input System](https://docs.unity3d.com/Manual/Input.html)
- [Animator Manual](https://docs.unity3d.com/Manual/Animator.html)
- [Physics Raycasting](https://docs.unity3d.com/Manual/RaycastingandRaycasts.html)
- [Camera.ScreenToWorldPoint](https://docs.unity3d.com/ScriptReference/Camera.ScreenToWorldPoint.html)

### Game Feel References
- *Game Feel* by Steve Swink — Comprehensive feel design reference
- *Rules of Play* by Katie Salen & Eric Zimmerman — Game design principles
- GDC Talks on game feel (search YouTube)

### Bonus: Animation Blending
- Linear Blend Trees — Blend between two animations
- 2D Blend Trees — Blend in 2D space (speed + direction)
- Motion Matching — Advanced character animation

---

## Notes for Teachers

**Pacing Suggestions:**
- Days 1–6: Movement foundations; most students familiar with concepts
- Days 7–12: Animation integration; may need extra time for Animator
- Days 13–18: Varied difficulty; let students explore
- Days 19–20: Polish phase; encourage iteration and playtesting
- Day 21: Project week; give autonomy, encourage experimentation
- Day 22: Assessment (can extend if needed)

**Common Struggles:**
- ScreenToWorldPoint z-coordinate confusion
- Mixing up GetKey vs GetKeyDown
- Animator parameter management and transitions
- Ground detection sensitivity and false positives
- Movement feeling unresponsive or sluggish

**Enrichment Ideas:**
- Advanced animation blending with blend trees
- Gamepad vibration feedback
- Networked input (multiplayer)
- Voice commands or gesture recognition
- Advanced camera systems (look-ahead, collision avoidance)

---

## Final Project Ideas

Students can apply these skills to build:
1. **Platformer Controller** — Pixel-perfect jumps, wall sliding, momentum
2. **Top-Down RPG** — 8-directional smooth movement, isometric camera
3. **FPS-Style Shooter** — Aiming, shooting, recoil, sprint
4. **Parkour Freerunner** — Wall running, vaulting, momentum preservation
5. **Action Hero Game** — Dash, combo attacks, directional awareness

---

## Mapping to TN Standards

**9-12.VGD.4** — Design and implement responsive player control systems
- Achieved through daily practice in input handling, movement design, and feel iteration
- Demonstrated by building a polished character controller by Day 21
- Assessed through the Unit Assessment (Day 22)

