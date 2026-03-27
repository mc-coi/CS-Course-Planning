# Day 22: Unit Assessment

**Learning Target:** I can demonstrate mastery of all physics and collision concepts from this unit.

---

## Assessment Overview

This assessment evaluates your understanding of:
- Rigidbody properties and force application
- Colliders and collision detection
- Trigger zones and physics events
- Raycasting and overlap detection
- Joints and constraints
- Physics materials and friction
- 2D physics systems
- Physics optimization and debugging

---

## Multiple Choice Section (10 questions, 2 points each)

**1.** Which component makes a GameObject subject to physics simulation?
A) Collider  
B) Rigidbody  
C) PhysicsMaterial  
D) Constraint  

**2.** What is the difference between OnCollisionEnter and OnTriggerEnter?
A) OnCollisionEnter is for triggers, OnTriggerEnter is for collisions  
B) OnCollisionEnter requires both objects to have Rigidbodies, OnTriggerEnter requires isTrigger = true  
C) They are identical  
D) OnCollisionEnter only works in 2D  

**3.** Which ForceMode applies an instant force like a punch?
A) Force  
B) Impulse  
C) VelocityChange  
D) Acceleration  

**4.** What does Physics.Raycast return if it hits something?
A) The distance to the object  
B) True and fills the RaycastHit parameter  
C) The GameObject hit  
D) A Vector3 position  

**5.** What property controls how sticky an object is on surfaces?
A) Drag  
B) Angular Drag  
C) Friction  
D) Bounciness  

**6.** When should you use MeshCollider on a moving object?
A) Always, for accuracy  
B) Never, too expensive  
C) Only with Convex = true  
D) Only for static objects  

**7.** Which method is called every frame while two objects are in contact?
A) OnCollisionEnter  
B) OnCollisionExit  
C) OnCollisionStay  
D) OnCollisionRepeat  

**8.** What does the Layer Collision Matrix control?
A) Which objects can see each other  
B) Which layers collide with which other layers  
C) How shiny objects appear  
D) Animation transitions between layers  

**9.** In 2D physics, what is the equivalent of Physics.Raycast?
A) Physics2D.Raycast  
B) Ray2D.Raycast  
C) Raycast2D()  
D) Physics.Raycast2D()  

**10.** What constraint should most characters have frozen?
A) Position X and Y  
B) Rotation X, Y, and Z  
C) Only Rotation Z  
D) No constraints needed  

---

## Short Answer Section (5 questions, 4 points each)

**1.** Explain the difference between static and dynamic Rigidbodies. When would you use each?

**2.** Why is it important to use FixedUpdate for physics code and Update for input code? What could go wrong if you mixed them?

**3.** You're building a game where objects fall through walls randomly. What are three things you should check to fix this?

**4.** Describe how you would create a one-way platform in a 2D platformer using triggers and code.

**5.** What is bounciness in a PhysicMaterial, and why might you set it to 0, 1, or >1?

---

## Coding Challenge Section (3 challenges, 10 points each)

**Challenge 1: Ground Detection (Beginner)**

Write a script that uses raycasting to detect if a player is on the ground, and only allows jumping when grounded. Include Debug.DrawRay visualization.

```csharp
using UnityEngine;

public class GroundDetection : MonoBehaviour
{
    private Rigidbody rb;
    // YOUR CODE HERE
}
```

**Challenge 2: Pickup System (Intermediate)**

Write a complete pickup system:
- Pickup sphere with trigger collider
- Detect when player touches it
- Add 10 points to score
- Destroy the pickup
- Display score in OnGUI

**Challenge 3: Physics-Based Pusher (Advanced)**

Write a script that detects objects in a radius (Physics.OverlapSphere) and applies outward force if their mass is less than the pusher's mass. Include visual gizmo to show radius.

---

## Answer Key & Rubric

### Multiple Choice
1. B | 2. B | 3. B | 4. B | 5. C | 6. C | 7. C | 8. B | 9. A | 10. C

### Short Answer Rubric (4 points each)

**1. Static vs Dynamic:**
- Static: Doesn't move (walls, ground), no Rigidbody or Body Type = Static
- Dynamic: Moves with physics (player, enemies), has Rigidbody
- Use Static for level geometry, Dynamic for interactive objects
- Performance: Statics are cheaper

**2. FixedUpdate vs Update:**
- FixedUpdate called at fixed physics timestep (50x/sec)
- Update called per frame (variable)
- Physics code must be in FixedUpdate for consistency
- Input in Update, physics in FixedUpdate
- Mixing: Movement becomes frame-rate dependent

**3. Objects Falling Through Walls:**
- Collision Detection set to Continuous (not Discrete)
- Rigidbody moving too fast (velocity too high)
- Collider thickness too small
- Check Layer Collision Matrix

**4. One-Way Platform:**
- Use EdgeCollider2D or BoxCollider2D
- OnTriggerStay checks if object below platform
- Physics2D.IgnoreCollision() disables collision when below
- OnCollisionStay checks if above, re-enables collision
- Allows jump-through from below, standing on top

**5. Bounciness:**
- 0 = no bounce (dead, absorbs energy)
- 1 = perfect bounce (returns with same energy)
- >1 = gains energy (infinite bounce)
- Used for jump pads (>1), dead zones (0), realistic objects (0.3-0.8)

### Coding Rubric (10 points each)

**Challenge 1:**
- GetComponent<Rigidbody>() call: 2 pts
- Physics.Raycast() with down direction: 3 pts
- RaycastHit parameter and distance: 2 pts
- Debug.DrawRay visualization: 2 pts
- Correct ray offset: 1 pt

**Challenge 2:**
- Pickup: OnTriggerEnter: 3 pts
- Check Player tag: 2 pts
- Score increment: 2 pts
- Destroy pickup: 1 pt
- OnGUI display: 2 pts

**Challenge 3:**
- Physics.OverlapSphere with radius: 3 pts
- Loop through colliders: 2 pts
- Mass comparison logic: 2 pts
- AddForce with correct direction: 2 pts
- Gizmo visualization: 1 pt

---

## Study Guide

**Key Topics to Review:**
- Rigidbody properties: mass, drag, gravity
- Force application: AddForce, velocity, ForceMode
- Collider types and isTrigger
- Collision vs Trigger callbacks
- Layer masks and collision matrix
- Raycasting in 3D and 2D
- Joints (Hinge, Fixed, Spring)
- Physics materials and friction
- Physics optimization techniques

**Practice Areas:**
- Build a small game using physics
- Test different material combinations
- Implement multiple collision detection scenarios
- Debug and optimize a physics scene

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

**Build a complete game scene** demonstrating at least 5 physics concepts learned in this unit. Could be:
- Physics puzzle level
- Bouncing ball game with scoring
- 2D platformer with special mechanics
- Physics-based destruction system
- Ragdoll death system

Must include: documentation of which concepts are used.

