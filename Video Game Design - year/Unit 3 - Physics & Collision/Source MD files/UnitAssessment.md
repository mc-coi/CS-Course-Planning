# Unit 3 Assessment: Physics & Collision

**Total Points: 70** | **Passing: 49+** | **Time: 90 minutes**

---

## Multiple Choice Section (10 questions, 2 points each)

**1.** Which component makes a GameObject subject to physics simulation?
A) Collider
B) Rigidbody ✓
C) PhysicsMaterial
D) Constraint

**2.** What is the difference between OnCollisionEnter and OnTriggerEnter?
A) OnCollisionEnter is for triggers, OnTriggerEnter is for collisions
B) OnCollisionEnter requires both objects to have Rigidbodies, OnTriggerEnter requires isTrigger = true ✓
C) They are identical
D) OnCollisionEnter only works in 2D

**3.** Which ForceMode applies an instant force like a punch?
A) Force
B) Impulse ✓
C) VelocityChange
D) Acceleration

**4.** What does Physics.Raycast return if it hits something?
A) The distance to the object
B) True and fills the RaycastHit parameter ✓
C) The GameObject hit
D) A Vector3 position

**5.** What property controls how sticky an object is on surfaces?
A) Drag
B) Angular Drag
C) Friction ✓
D) Bounciness

**6.** When should you use MeshCollider on a moving object?
A) Always, for accuracy
B) Never, too expensive
C) Only with Convex = true ✓
D) Only for static objects

**7.** Which method is called every frame while two objects are in contact?
A) OnCollisionEnter
B) OnCollisionExit
C) OnCollisionStay ✓
D) OnCollisionRepeat

**8.** What does the Layer Collision Matrix control?
A) Which objects can see each other
B) Which layers collide with which other layers ✓
C) How shiny objects appear
D) Animation transitions between layers

**9.** In 2D physics, what is the equivalent of Physics.Raycast?
A) Physics2D.Raycast ✓
B) Ray2D.Raycast
C) Raycast2D()
D) Physics.Raycast2D()

**10.** What constraint should most characters have frozen?
A) Position X and Y
B) Rotation X, Y, and Z ✓
C) Only Rotation Z
D) No constraints needed

**Answer Key:** 1-B, 2-B, 3-B, 4-B, 5-C, 6-C, 7-C, 8-B, 9-A, 10-B

---

## Short Answer Section (5 questions, 4 points each)

**1.** Explain the difference between static and dynamic Rigidbodies. When would you use each?

**Scoring Rubric (4 points):**
- Correct definitions (2 pts)
- Use cases explained (2 pts)

**Model Answer:**
- **Static:** No Rigidbody or Body Type = Static. Doesn't move. Used for level geometry (walls, ground, immobile platforms). Cheaper performance.
- **Dynamic:** Has Rigidbody with Body Type = Dynamic. Responds to physics forces. Used for interactive objects, enemies, projectiles. More expensive but realistic.

---

**2.** Why is it important to use FixedUpdate for physics code and Update for input code? What could go wrong if you mixed them?

**Scoring Rubric (4 points):**
- FixedUpdate called at fixed timestep (1 pt)
- Update called per frame (1 pt)
- Consequence of mixing (2 pts)

**Model Answer:**
- FixedUpdate called at fixed physics timestep (50x/sec default), Update called per frame (variable).
- Physics code in FixedUpdate ensures consistent behavior.
- Physics code in Update becomes frame-rate dependent — fast machines get more force applications, slow machines get fewer.
- Could cause erratic physics behavior, movement inconsistency, or unpredictable game feel.

---

**3.** You're building a game where objects fall through walls randomly. What are three things you should check to fix this?

**Scoring Rubric (4 points):**
- 3 valid solutions (roughly 1.3 pts each)

**Model Answer (any three):**
- Collision Detection set to Continuous (not Discrete)
- Rigidbody moving too fast — increase physics solver iterations or slow objects down
- Collider thickness — make sure colliders aren't paper-thin
- Check Layer Collision Matrix — ensure layers are set to collide
- Ensure ground has Collider component
- Check for isKinematic or isTrigger accidentally enabled

---

**4.** Describe how you would create a one-way platform in a 2D platformer using triggers and code.

**Scoring Rubric (4 points):**
- Trigger setup described (1 pt)
- Direction check logic (2 pts)
- Physics2D.IgnoreCollision usage (1 pt)

**Model Answer:**
- Create platform with BoxCollider2D (isTrigger = false, solid).
- Attach script to platform with OnCollisionEnter2D and OnCollisionStay2D.
- Check collision direction using relativeVelocity.
- If player moving downward (relativeVelocity.y > 0), use Physics2D.IgnoreCollision to disable collision temporarily.
- When player on top, re-enable collision.
- Allows jumping through from below, standing on top from above.

---

**5.** What is bounciness in a PhysicsMaterial, and why might you set it to 0, 1, or >1?

**Scoring Rubric (4 points):**
- Definition of bounciness (1 pt)
- Explanation of 0 (1 pt)
- Explanation of 1 (1 pt)
- Explanation of >1 (1 pt)

**Model Answer:**
- **Bounciness:** How much energy an object retains after collision.
- **0:** No bounce (dead, absorbs all energy). Used for dirt, heavy objects, impact zones.
- **1:** Perfect bounce (returns with same energy). Used for realistic balls or physics puzzles.
- **>1:** Gains energy (infinite bounce possible). Used for jump pads, springs, or special effects.

---

## Coding Challenge Section (3 challenges, 10 points each)

### Challenge 1: Ground Detection (Beginner)

Write a script that uses raycasting to detect if a player is on the ground, and only allows jumping when grounded. Include Debug.DrawRay visualization.

```csharp
using UnityEngine;

public class GroundDetection : MonoBehaviour
{
    private Rigidbody rb;
    public float groundCheckDistance = 0.1f;
    public LayerMask groundLayer;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && IsGrounded())
        {
            Jump();
        }
    }

    private bool IsGrounded()
    {
        // YOUR CODE HERE
        return false;
    }

    private void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(Vector3.up * 5f, ForceMode.Impulse);
    }
}
```

**Scoring Rubric (10 points):**
- GetComponent Rigidbody: 1 pt
- Physics.Raycast with correct parameters: 3 pts
- Using groundCheckDistance and groundLayer: 2 pts
- Debug.DrawRay visualization: 2 pts
- Correct ray origin (below object): 2 pts

**Model Answer:**
```csharp
private bool IsGrounded()
{
    Vector3 rayOrigin = transform.position + Vector3.down * 0.5f;
    bool grounded = Physics.Raycast(rayOrigin, Vector3.down, groundCheckDistance, groundLayer);

    Debug.DrawRay(rayOrigin, Vector3.down * groundCheckDistance, grounded ? Color.green : Color.red);

    return grounded;
}
```

---

### Challenge 2: Pickup System (Intermediate)

Write a complete pickup system:
- Pickup sphere with trigger collider
- Detect when player touches it
- Add 10 points to score
- Destroy the pickup
- Display score in OnGUI

```csharp
using UnityEngine;

public class PickupSystem : MonoBehaviour
{
    private int score = 0;

    // YOUR CODE HERE
}
```

**Scoring Rubric (10 points):**
- OnTriggerEnter setup: 2 pts
- Tag/CompareTag check: 1 pt
- Score increment logic: 2 pts
- Destroy pickup: 1 pt
- OnGUI display: 3 pts
- Code organization/clarity: 1 pt

**Model Answer:**
```csharp
using UnityEngine;

public class PickupSystem : MonoBehaviour
{
    private int score = 0;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Pickup"))
        {
            score += 10;
            Debug.Log("Score: " + score);
            Destroy(other.gameObject);
        }
    }

    private void OnGUI()
    {
        GUI.Label(new Rect(10, 10, 200, 30), "Score: " + score);
    }
}
```

---

### Challenge 3: Physics-Based Pusher (Advanced)

Write a script that detects objects in a radius (Physics.OverlapSphere) and applies outward force if their mass is less than the pusher's mass. Include visual gizmo to show radius.

```csharp
using UnityEngine;

public class PhysicsPusher : MonoBehaviour
{
    private Rigidbody rb;
    public float pushRadius = 5f;
    public float pushForce = 10f;
    public LayerMask targetLayer;

    // YOUR CODE HERE
}
```

**Scoring Rubric (10 points):**
- GetComponent Rigidbody: 1 pt
- Physics.OverlapSphere with radius: 2 pts
- Loop through colliders: 1 pt
- Mass comparison logic: 2 pts
- AddForce with correct direction: 2 pts
- Gizmo visualization (OnDrawGizmosSelected): 2 pts

**Model Answer:**
```csharp
using UnityEngine;

public class PhysicsPusher : MonoBehaviour
{
    private Rigidbody rb;
    public float pushRadius = 5f;
    public float pushForce = 10f;
    public LayerMask targetLayer;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    public void DoPush()
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, pushRadius, targetLayer);

        foreach (Collider hit in hits)
        {
            Rigidbody otherRb = hit.GetComponent<Rigidbody>();
            if (otherRb != null && otherRb.mass < rb.mass)
            {
                Vector3 direction = (hit.transform.position - transform.position).normalized;
                otherRb.AddForce(direction * pushForce, ForceMode.Impulse);
            }
        }
    }

    private void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.cyan;
        Gizmos.DrawWireSphere(transform.position, pushRadius);
    }
}
```

---

## Study Guide for Review

**Key Topics:**
- Rigidbody properties: mass, drag, gravity, isKinematic
- Force application: AddForce with ForceMode options
- Colliders: types, components, isTrigger vs solid
- Collision callbacks: OnCollisionEnter/Stay/Exit
- Trigger callbacks: OnTriggerEnter/Stay/Exit
- Layer system and collision matrix
- Raycasting: Physics.Raycast, RaycastHit, hit detection
- Overlap detection: OverlapSphere, OverlapBox
- Joints: HingeJoint, FixedJoint, SpringJoint
- Physics materials: friction, bounciness, restitution
- 2D physics: Rigidbody2D, Collider2D, Physics2D
- Physics debugging: visualizers, gizmos, Debug.DrawRay

**Practice Focus Areas:**
- Build simple jump mechanics from scratch
- Test different material combinations
- Implement multiple collision scenarios
- Debug and optimize physics scenes
- Create physics-based game mechanics

---

## Scoring Rubric Summary

| Section | Points | Passing |
|---------|--------|---------|
| Multiple Choice | 20 | 70% = 14 pts |
| Short Answer | 20 | 70% = 14 pts |
| Coding Challenges | 30 | 70% = 21 pts |
| **TOTAL** | **70** | **49+** |

**Grade Scale:**
- A: 63-70 (90-100%)
- B: 56-62 (80-89%)
- C: 49-55 (70-79%)
- Below C: Needs remediation

---

## Extra Credit (+5 points max)

Build a complete game scene demonstrating at least 5 physics concepts from this unit. Examples:
- Physics puzzle level with moving platforms
- Bouncing ball game with scoring system
- 2D platformer with varied materials
- Physics-based destruction system
- Ragdoll or ragdoll-like system

**Requirements:**
- At least 5 concepts clearly demonstrated
- Code should be well-commented
- Include a brief document explaining which concepts are used where

---

## Notes for Remediation

If a student scores below 49 (not passing):
1. Review Unit Overview and Daily Notes for Days 1-22
2. Work through at least 5 practice problems from UnitPractice.md
3. Focus on weak areas identified in assessment
4. Schedule a retake (must pass with 70%+ to credit)

