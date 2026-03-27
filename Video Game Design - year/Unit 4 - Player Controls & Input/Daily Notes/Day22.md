# Day 22: Unit Assessment

**Learning Target:** I can demonstrate mastery of all player control and input systems from this unit.

---

## Assessment Overview

This assessment evaluates your understanding of:
- Movement systems (acceleration, velocity manipulation, speed limits)
- Jumping mechanics (coyote time, jump buffering, variable height)
- Ground detection methods (raycasting, overlap detection, layer masks)
- Animation state machines and parameter control
- Sprite flipping and directional animations
- Mouse and aim input handling
- Projectile and shooting mechanics
- Dash and special abilities with cooldowns
- Input polish and feel mechanics
- Complete player controller implementation

---

## Multiple Choice Section (10 questions, 2 points each)

**1.** Which method is called every frame and should handle input detection?
A) FixedUpdate
B) LateUpdate
C) Update
D) OnCollisionEnter

**2.** What does the Input class method GetKeyDown() do?
A) Returns true every frame the key is held
B) Returns true only on the frame the key is first pressed
C) Returns true when the key is released
D) Detects gamepad input only

**3.** How should you apply movement forces to a player Rigidbody?
A) In Update() with AddForce
B) In FixedUpdate() with velocity or AddForce
C) In LateUpdate() with position manipulation
D) In OnGUI() for immediate response

**4.** What is "coyote time" in platformer design?
A) A time delay before jumping is allowed
B) A short window after leaving ground where jumping is still possible
C) The time between two jumps
D) Air acceleration modifier

**5.** Which Animator parameter type is best for storing a speed value?
A) Bool
B) Trigger
C) Float
D) Integer

**6.** How do you flip a 2D sprite to face the opposite direction?
A) Rotate the GameObject 180 degrees
B) Negate the scale.x value
C) Use SetBool("FacingRight", false)
D) Both B and C

**7.** What does Camera.main.ScreenToWorldPoint do?
A) Converts screen pixel position to world position
B) Moves the camera to a world position
C) Calculates aiming direction
D) Detects ray-screen intersections

**8.** Which method should be used to detect if the player is touching ground?
A) OnCollisionEnter only
B) Physics.Raycast or Physics.OverlapCircle
C) Just check rb.velocity.y < 0
D) A timer that counts down from jump

**9.** What is object pooling used for?
A) Storing completed objects for deletion
B) Reusing bullet/projectile instances instead of Instantiate/Destroy
C) Managing player inventory
D) Tracking all active GameObjects

**10.** How do you prevent jump spam in a controller?
A) Check if input was received last frame
B) Use a jump cooldown timer or check grounded state
C) Freeze the Rigidbody rotation
D) Disable input during jump animation

---

## Short Answer Section (5 questions, 4 points each)

**1.** Explain how you would implement acceleration-based movement (gradual speed increase) instead of instant-speed movement. Why is this better for game feel?

**2.** What is a jump buffer, and how would you implement it in code? Why is it important for player experience?

**3.** Describe the difference between using `rb.velocity` directly and using `AddForce()` for player movement. When would you use each?

**4.** How would you create a mechanic where the player can aim a gun with the mouse and fire a bullet prefab? Include ground detection check to prevent mid-air shooting.

**5.** What is a state machine for a player controller, and what are at least 3 states you might include?

---

## Coding Challenge Section (3 challenges, 10 points each)

**Challenge 1: Polished Horizontal Movement (Beginner)**

Write a script that implements smooth acceleration-based horizontal movement:
- Input responds immediately (snappy feel)
- Acceleration gradually increases speed
- Deceleration when input stops
- Maximum speed clamping
- Print current speed to console each frame

```csharp
using UnityEngine;

public class PolishedMovement : MonoBehaviour
{
    private Rigidbody rb;
    public float maxSpeed = 10f;
    public float acceleration = 5f;
    public float deceleration = 8f;

    private float currentSpeed = 0f;

    // YOUR CODE HERE
}
```

**Challenge 2: Coyote Time Ground Detection (Intermediate)**

Implement ground detection with coyote time:
- Use Physics.OverlapCircle to detect ground
- Allow jumping for 0.2 seconds after leaving ground (coyote time)
- Only allow one jump while airborne
- Use Debug.DrawRay to visualize ground detection
- Print "Can Jump: true/false" each frame

**Challenge 3: Aim and Shoot System (Advanced)**

Create a complete shooting system:
- Detect mouse position with Camera.main.ScreenToWorldPoint
- Calculate direction from player to mouse
- Only allow shooting when grounded (use raycasting)
- Instantiate bullet prefab with correct velocity
- Implement 0.3-second cooldown between shots
- Update sprite rotation to face aim direction
- Visualize aim direction with Debug.DrawRay

---

## Answer Key & Rubric

### Multiple Choice
1. C | 2. B | 3. B | 4. B | 5. C | 6. D | 7. A | 8. B | 9. B | 10. B

### Short Answer Rubric (4 points each)

**1. Acceleration-Based Movement:**
- Gradual speed increase using lerp or += per frame
- currentSpeed += acceleration * Time.deltaTime
- Multiply currentSpeed by direction for movement
- Better feel: more responsive, polished, naturalistic
- Players expect gradual acceleration, not instant

**2. Jump Buffer:**
- Stores jump input for a brief window (~0.1s)
- Allows jumping if buffer is full when grounded
- Improves responsiveness: player feels heard even if timing is slightly off
- Implementation: timer that counts down, set on input, execute on ground touch

**3. rb.velocity vs AddForce:**
- velocity: direct, instant position change, good for immediate response
- AddForce: physics-based, respects mass, feels more realistic
- Use velocity for direct control (platformers)
- Use AddForce for physics objects (pushing, explosions)

**4. Mouse Aiming & Shooting:**
- Camera.main.ScreenToWorldPoint(Input.mousePosition)
- Direction = (mouseWorldPos - playerPos).normalized
- Check grounded with Raycast before allowing shoot
- Instantiate bullet with rb.velocity in direction
- Add cooldown timer between shots

**5. State Machine:**
- States: Idle, Running, Jumping, Falling, Dashing, etc.
- Transitions between states based on input and conditions
- Each state has different behavior (speed, animations, etc.)
- Allows clean, extensible controller design

### Coding Rubric (10 points each)

**Challenge 1: Polished Movement**
- GetComponent Rigidbody: 1 pt
- Input detection (GetAxis): 2 pts
- Acceleration += per frame: 2 pts
- Deceleration implementation: 2 pts
- Speed clamping: 1 pt
- Apply velocity with currentSpeed: 1 pt
- Debug output: 1 pt

**Challenge 2: Coyote Time**
- Physics.OverlapCircle for detection: 3 pts
- Coyote timer countdown: 2 pts
- Reset coyote on ground touch: 2 pts
- Jump only allowed when grounded or coyote active: 2 pts
- Debug visualization: 1 pt

**Challenge 3: Aim & Shoot**
- ScreenToWorldPoint conversion: 2 pts
- Direction calculation and normalization: 2 pts
- Grounded check before shoot: 1 pt
- Bullet Instantiate with velocity: 2 pts
- Cooldown timer: 1 pt
- Sprite rotation to aim: 1 pt
- Debug ray visualization: 1 pt

---

## Study Guide

**Key Topics to Review:**
- Input detection: GetKey, GetKeyDown, GetAxis, GetAxisRaw
- Movement patterns: direct velocity, acceleration-based, physics-based
- Ground detection: Raycast, OverlapCircle, OverlapSphere
- Coyote time and jump buffering implementation
- Animator integration and parameter management
- Sprite direction handling and flipping
- Mouse input and world space conversion
- Projectile instantiation and pooling
- Cooldown systems and timers
- State machines for clean controller logic

**Practice Areas:**
- Tweak movement values for different feels (snappy, weighty, floaty)
- Implement different ground detection methods
- Test keyboard and gamepad input
- Build different controller types (platformer, topdown, FPS)
- Debug input responsiveness and physics timing

---

## Scoring Rubric

| Section | Points | Requirements |
|---------|--------|--------------|
| Multiple Choice | 20 | 10 questions × 2 points |
| Short Answer | 20 | 5 questions × 4 points |
| Coding Challenges | 30 | 3 challenges × 10 points |
| **Total** | **70** | Passing = 49+ points |

---

## Extra Credit Opportunity (+5 points)

**Build a complete 2D platformer controller** demonstrating at least 6 concepts from this unit:
- Smooth horizontal movement with acceleration
- Jump with coyote time and jump buffer
- Ground detection visualization
- Animation state machine (Idle, Running, Jumping, Falling)
- Sprite direction flipping
- Dash ability with cooldown
- Optional: Wall sliding, double jump, air control

Must include: well-commented code, tweakable public values, debug visuals.
