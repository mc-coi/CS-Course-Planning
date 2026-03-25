# Unit 3: Physics & Collision

## Unit Overview

**Duration:** Days 9-12 (4 days)
**Key Concepts:** Rigidbody component, gravity and forces, collision detection, trigger volumes, physics-based movement
**Big Idea:** Unity's physics engine simulates real-world forces. Understanding Rigidbody, colliders, and collision callbacks lets you create interactive, dynamic gameplay with proper physical behavior.

---

## Learning Targets

By the end of this unit, you will be able to:

- [ ] Attach a Rigidbody component and understand its properties (mass, drag, gravity)
- [ ] Apply forces to objects using AddForce() and AddTorque()
- [ ] Distinguish between FixedUpdate() and Update() for physics code
- [ ] Use Box, Sphere, and Capsule colliders appropriately
- [ ] Detect collisions using OnCollisionEnter(), OnCollisionStay(), and OnCollisionExit()
- [ ] Use tags to identify GameObjects and CompareTag() to check them
- [ ] Implement trigger colliders with OnTriggerEnter() and OnTriggerExit()
- [ ] Use SetActive() to enable/disable GameObjects
- [ ] Implement jumping mechanics with ground detection
- [ ] Use Raycasting to detect floors and other surfaces

---

## Day-by-Day Content

### Day 9: Rigidbody & Gravity

#### Key Concepts
- **Rigidbody:** A component that simulates physics (gravity, forces, collisions)
- **Mass:** How heavy an object is; affects acceleration from forces
- **Gravity:** Constant downward acceleration (default: -9.81 m/s²)
- **Drag:** Air resistance; opposes movement
- **Angular Drag:** Air resistance for rotation
- **AddForce():** Applies a force to the Rigidbody
- **Velocity:** The current speed and direction of movement
- **FixedUpdate():** Called at a fixed time step for physics calculations (default: 50 times per second)
- **Physics Timestep:** The rate at which Unity calculates physics (independent of frame rate)

#### Content
The Rigidbody component is essential for physics-based games. Without a Rigidbody, an object doesn't fall or respond to forces. With a Rigidbody, gravity and forces work automatically.

**Adding a Rigidbody:**
1. Select a GameObject
2. In the Inspector, click "Add Component"
3. Search for "Rigidbody" and add it
4. Properties appear: Mass, Drag, Angular Drag, gravity enabled, etc.

**Key Properties:**
- **Mass:** Higher mass = harder to push around (default: 1)
- **Drag:** Friction from air (0 = no drag, higher = more resistance to movement)
- **Gravity Scale:** Multiplier for gravity (1 = normal, 2 = twice as strong)
- **Constraints:** Lock axes to prevent unwanted movement/rotation

**FixedUpdate vs Update:**
- **Update():** Called once per frame (variable frame rate)
- **FixedUpdate():** Called at fixed physics timestep (50 times/sec by default)

Physics code should go in FixedUpdate(). If you use Update() for forces, the frame rate will affect physics. FixedUpdate() ensures consistent physics regardless of frame rate.

#### Annotated Code Example

```csharp
using UnityEngine;

public class PhysicsBasics : MonoBehaviour
{
    public float jumpForce = 5f;
    public float moveForce = 10f;
    private Rigidbody rb;

    void Start()
    {
        // Cache the Rigidbody component for efficiency
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Jump input detection (use Update for input)
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }
    }

    void FixedUpdate()
    {
        // Apply forces in FixedUpdate for consistent physics
        if (Input.GetKey(KeyCode.D))
        {
            // Add force in the right direction
            rb.AddForce(moveForce, 0, 0, ForceMode.Force);
        }

        if (Input.GetKey(KeyCode.A))
        {
            rb.AddForce(-moveForce, 0, 0, ForceMode.Force);
        }
    }

    void Jump()
    {
        // Apply upward force
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z); // Reset Y velocity
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
        Debug.Log("Jumped!");
    }
}
```

---

### Day 10: Colliders & Collision Detection

#### Key Concepts
- **Collider:** A shape that defines an object's physical boundaries
- **Box Collider:** Rectangular collision shape (good for cubes, blocks)
- **Sphere Collider:** Circular collision shape (good for balls, spheres)
- **Capsule Collider:** Elongated rounded shape (good for characters)
- **OnCollisionEnter():** Called when two colliders first touch
- **OnCollisionStay():** Called every frame while colliders are touching
- **OnCollisionExit():** Called when colliders stop touching
- **Tag:** A label for identifying GameObjects
- **CompareTag():** Efficiently checks if an object has a specific tag
- **Rigidbody Requirement:** OnCollision methods require a Rigidbody on at least one object

#### Content
Colliders define the physical shape of objects. Most GameObjects need a collider to interact with physics and detect collisions.

**Collider Types:**
- **Box Collider:** Perfect for rectangular objects. Set Size to match the GameObject's visual dimensions.
- **Sphere Collider:** Perfect for round objects. Set Radius to match visual size.
- **Capsule Collider:** Good for character bodies. Typically oriented along the Y axis.

**Collision Detection Callbacks:**
These methods are called automatically by Unity when collisions happen:

```csharp
void OnCollisionEnter(Collision collision)
{
    // Called once when collision begins
    // collision contains info about the other object
}

void OnCollisionStay(Collision collision)
{
    // Called every frame while colliding
}

void OnCollisionExit(Collision collision)
{
    // Called once when collision ends
}
```

**Tags:**
Tags are string labels for GameObjects. Create tags in Tags & Layers (top right of Inspector):
1. Click "Add Tag"
2. Create a new tag name (e.g., "Enemy", "Coin", "Platform")
3. Assign tags to GameObjects
4. Check tags with CompareTag() (more efficient than == comparison)

#### Annotated Code Example

```csharp
using UnityEngine;

public class CollisionDetector : MonoBehaviour
{
    public int damageOnImpact = 10;
    private int timesCollided = 0;

    void Start()
    {
        // Add a tag "Hazard" in the Tags & Layers menu first
        gameObject.tag = "Hazard";
    }

    // Called when this object collides with another
    void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Collided with: " + collision.gameObject.name);
        timesCollided++;

        // Check if the colliding object is an enemy
        if (collision.gameObject.CompareTag("Enemy"))
        {
            Debug.Log("Hit an enemy!");
            // Could damage the enemy here

            // Get a component from the collided object
            Health enemyHealth = collision.gameObject.GetComponent<Health>();
            if (enemyHealth != null)
            {
                enemyHealth.TakeDamage(damageOnImpact);
            }
        }

        // Get collision information
        Vector3 collisionPoint = collision.contacts[0].point;
        Vector3 collisionNormal = collision.contacts[0].normal;
        Debug.Log("Collision point: " + collisionPoint);
    }

    void OnCollisionStay(Collision collision)
    {
        // This object is touching another every frame
        // Could be used for sliding friction effects
    }

    void OnCollisionExit(Collision collision)
    {
        Debug.Log("Stopped colliding with: " + collision.gameObject.name);
    }
}

// Example Health component
public class Health : MonoBehaviour
{
    public int maxHealth = 100;
    private int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        Debug.Log("Health: " + currentHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log(gameObject.name + " died!");
        Destroy(gameObject);
    }
}
```

---

### Day 11: Triggers & Object Management

#### Key Concepts
- **Trigger Collider:** A collider that doesn't physically collide; instead, it detects when objects enter/exit it
- **Is Trigger:** A checkbox on colliders that makes them triggers instead of solid colliders
- **OnTriggerEnter():** Called when an object enters a trigger
- **OnTriggerStay():** Called every frame while inside a trigger
- **OnTriggerExit():** Called when an object leaves a trigger
- **Rigidbody Requirement:** At least one object must have a Rigidbody for trigger detection
- **SetActive():** Enables or disables a GameObject and its components
- **GameObject.Find():** Finds an object by name (slow; use sparingly)
- **Instantiate():** Creates a copy of a GameObject at runtime
- **Destroy():** Removes a GameObject from the scene

#### Content
Triggers are useful for area-based events: entering a door, collecting an item, entering a hazard zone, etc.

**Setting Up Triggers:**
1. Add a collider to a GameObject
2. Check the "Is Trigger" checkbox
3. Add a Rigidbody to the same object (set it to Kinematic if you don't want it affected by gravity)
4. In a script, implement OnTriggerEnter() to detect when something enters

**Key Difference from Collision:**
- **Collision:** OnCollisionEnter requires both objects to have Rigidbodies. Physical collision happens.
- **Trigger:** OnTriggerEnter works if at least one has a Rigidbody. No physical collision.

**SetActive() for Object Management:**
```csharp
gameObject.SetActive(false);  // Disable and hide
gameObject.SetActive(true);   // Enable and show
```

#### Annotated Code Example

```csharp
using UnityEngine;

public class TriggerDetector : MonoBehaviour
{
    public int coinValue = 10;
    public ParticleSystem collectEffect;
    private int coinsCollected = 0;

    void Start()
    {
        gameObject.tag = "Collectible";
    }

    // Called when an object enters this trigger
    void OnTriggerEnter(Collider other)
    {
        Debug.Log("Something entered the trigger: " + other.name);

        // Check if it's the player
        if (other.CompareTag("Player"))
        {
            CollectCoin(other.gameObject);
        }
    }

    void OnTriggerStay(Collider other)
    {
        // Could apply effects while inside (e.g., slow player down)
    }

    void OnTriggerExit(Collider other)
    {
        Debug.Log("Something left the trigger: " + other.name);
    }

    void CollectCoin(GameObject collector)
    {
        Debug.Log("Coin collected!");
        coinsCollected++;

        // Play particle effect at coin position
        if (collectEffect != null)
        {
            Instantiate(collectEffect, transform.position, Quaternion.identity);
        }

        // Add score to player (if they have a score component)
        ScoreManager scoreManager = collector.GetComponent<ScoreManager>();
        if (scoreManager != null)
        {
            scoreManager.AddScore(coinValue);
        }

        // Disable or destroy the coin
        gameObject.SetActive(false);  // Just disable it
        // Or: Destroy(gameObject);  // Completely remove it
    }
}

// Simple score manager for the player
public class ScoreManager : MonoBehaviour
{
    private int score = 0;

    public void AddScore(int points)
    {
        score += points;
        Debug.Log("Score: " + score);
    }

    public int GetScore()
    {
        return score;
    }
}
```

---

### Day 12: Physics-Based Movement & Ground Detection

#### Key Concepts
- **Raycasting:** Casting a line from a point to detect what it hits
- **Physics.Raycast():** Casts a ray and returns true if it hits something
- **Grounded Check:** Detecting if the player is on the ground using raycasts
- **Jump Mechanics:** Preventing jumping while in the air
- **Falling Velocity:** Acceleration due to gravity accumulates over time
- **Slope Detection:** Using raycasts to determine if the ground is flat or angled
- **Character Controller:** Simplified alternative to Rigidbody for character movement

#### Content
Ground detection is crucial for platformer games. You need to know if the player is on the ground to allow jumping. Raycasting is the most reliable method.

**Raycast Basics:**
```csharp
RaycastHit hit;
bool didHit = Physics.Raycast(startPosition, direction, out hit, maxDistance);

if (didHit)
{
    Debug.Log("Ray hit: " + hit.collider.gameObject.name);
    Debug.Log("Distance: " + hit.distance);
    Debug.Log("Hit point: " + hit.point);
}
```

**Ground Detection:**
Cast a ray downward from the player. If it hits something, the player is grounded.

```csharp
RaycastHit hit;
float groundDistance = 0.1f;  // Small distance below the player
bool isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);
```

This works by sending a ray from the player's position straight down. If something is within `groundDistance` below, the player is grounded.

#### Annotated Code Example

```csharp
using UnityEngine;

public class PhysicsCharacterController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float groundDrag = 5f;
    public float airDrag = 1f;
    public float groundDistance = 0.2f;

    private Rigidbody rb;
    private bool isGrounded = false;
    private float verticalVelocity = 0f;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Check if grounded using raycast
        RaycastHit hit;
        isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

        Debug.Log("Grounded: " + isGrounded);

        // Input for movement
        float horizontalInput = 0f;
        if (Input.GetKey(KeyCode.D))
            horizontalInput += 1f;
        if (Input.GetKey(KeyCode.A))
            horizontalInput -= 1f;

        // Jump input
        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }
    }

    void FixedUpdate()
    {
        // Apply movement
        float horizontalInput = 0f;
        if (Input.GetKey(KeyCode.D))
            horizontalInput += 1f;
        if (Input.GetKey(KeyCode.A))
            horizontalInput -= 1f;

        // Apply horizontal movement
        rb.velocity = new Vector3(horizontalInput * moveSpeed, rb.velocity.y, 0);

        // Apply drag
        if (isGrounded)
        {
            rb.drag = groundDrag;
        }
        else
        {
            rb.drag = airDrag;
        }
    }

    void Jump()
    {
        Debug.Log("Jump!");
        // Reset vertical velocity and apply upward impulse
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
    }
}
```

---

## Practice Problems

### Beginner Tier

**Problem 1:** Create a Cube, add a Rigidbody to it, and let gravity pull it down. What happens when you run the scene?

<details>
<summary>Hint</summary>
Select the Cube. Add Component > Rigidbody. The Rigidbody should have "Use Gravity" checked by default. Play the scene.
</details>

<details>
<summary>Answer</summary>
The Cube falls down due to gravity. The Rigidbody component simulates gravity by default. If there's a Plane below, the Cube collides with it and stops.
</details>

---

**Problem 2:** Add a Box Collider to a Cube and a Plane. Create a simple collision detection script that prints "Collision!" when they touch.

<details>
<summary>Hint</summary>
Use OnCollisionEnter() in a MonoBehaviour script. Both objects need colliders; at least one needs a Rigidbody.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class SimpleCollision : MonoBehaviour
{
    void OnCollisionEnter(Collision collision)
    {
        Debug.Log("Collision!");
    }
}
```
Attach this to the Cube. The Cube needs a Rigidbody; the Plane needs a Box Collider.
</details>

---

**Problem 3:** Create a trigger zone that prints "Entered!" when the player walks through it.

<details>
<summary>Hint</summary>
Create a new Cube with a Box Collider set to "Is Trigger". Create a sphere with a Rigidbody as the player. Implement OnTriggerEnter().
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class TriggerZone : MonoBehaviour
{
    void OnTriggerEnter(Collider other)
    {
        Debug.Log("Entered!");
    }
}
```
Attach to a trigger collider. When any object with a Rigidbody enters, "Entered!" prints to the Console.
</details>

---

### Intermediate Tier

**Problem 4:** Create a script that makes a Cube jump when you press Space, but only if it's grounded (use raycast for ground detection).

<details>
<summary>Hint</summary>
Use Physics.Raycast() to check if the Cube is above ground. Only allow jumping if isGrounded is true.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class RaycastJump : MonoBehaviour
{
    public float jumpForce = 5f;
    public float groundDistance = 0.2f;
    private Rigidbody rb;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Check if grounded
        RaycastHit hit;
        isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
            rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
            Debug.Log("Jumped!");
        }
    }
}
```
</details>

---

**Problem 5:** Create a coin collectible that disappears when the player touches it and adds 10 points to a score.

<details>
<summary>Hint</summary>
Use a trigger collider for the coin. In OnTriggerEnter(), check if the object is the player. Call a score method, then disable/destroy the coin.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class CoinPickup : MonoBehaviour
{
    public int coinValue = 10;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            ScoreManager scoreManager = other.GetComponent<ScoreManager>();
            if (scoreManager != null)
            {
                scoreManager.AddScore(coinValue);
            }
            Destroy(gameObject);
        }
    }
}
```
</details>

---

**Problem 6:** Create a script that applies force to a Rigidbody when you press a direction key (A/D). Movement should feel smooth and respond to input.

<details>
<summary>Hint</summary>
Use Input.GetKey() in FixedUpdate(). Apply force with rb.AddForce() in the direction the player wants to move.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class ForceMovement : MonoBehaviour
{
    public float moveForce = 10f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        if (Input.GetKey(KeyCode.D))
        {
            rb.AddForce(moveForce, 0, 0);
        }

        if (Input.GetKey(KeyCode.A))
        {
            rb.AddForce(-moveForce, 0, 0);
        }
    }
}
```
</details>

---

### Challenge Tier

**Problem 7:** Create a complete platformer controller: move left/right, jump when grounded, and prevent double-jumping. Use raycasts for ground detection and Rigidbody for physics.

<details>
<summary>Hint</summary>
Track isGrounded with a raycast each frame. Only allow jumping if isGrounded is true. Use a Rigidbody with appropriate drag values.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class PlatformerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 5f;
    public float groundDistance = 0.2f;
    public float groundDrag = 5f;
    public float airDrag = 1f;

    private Rigidbody rb;
    private bool isGrounded = false;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // Check if grounded
        RaycastHit hit;
        isGrounded = Physics.Raycast(transform.position, Vector3.down, out hit, groundDistance);

        if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            Jump();
        }
    }

    void FixedUpdate()
    {
        float moveInput = 0f;
        if (Input.GetKey(KeyCode.D))
            moveInput += 1f;
        if (Input.GetKey(KeyCode.A))
            moveInput -= 1f;

        // Apply movement
        rb.velocity = new Vector3(moveInput * moveSpeed, rb.velocity.y, 0);

        // Apply drag based on ground state
        rb.drag = isGrounded ? groundDrag : airDrag;
    }

    void Jump()
    {
        rb.velocity = new Vector3(rb.velocity.x, 0, rb.velocity.z);
        rb.AddForce(0, jumpForce, 0, ForceMode.Impulse);
    }
}
```
</details>

---

**Problem 8:** Create a damage system where the player takes damage on collision with hazards, and loses health. Display the current health in the Console.

<details>
<summary>Hint</summary>
Use OnCollisionEnter() to detect collision with hazards. Check the tag, then call a damage method. Track health and prevent it from going below 0.
</details>

<details>
<summary>Answer</summary>
```csharp
using UnityEngine;

public class HealthSystem : MonoBehaviour
{
    public int maxHealth = 100;
    private int currentHealth;

    void Start()
    {
        currentHealth = maxHealth;
        Debug.Log("Health: " + currentHealth + "/" + maxHealth);
    }

    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Hazard"))
        {
            TakeDamage(10);
        }
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;
        if (currentHealth < 0)
            currentHealth = 0;

        Debug.Log("Health: " + currentHealth + "/" + maxHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    void Die()
    {
        Debug.Log("Player died!");
        Destroy(gameObject);
    }
}
```
</details>

---

## Practice Bank (15 Problems)

1. **Rigidbody Exploration:** Create three objects with different masses. Apply the same force to all three. Which accelerates fastest? Explain why.

2. **Collision Tags:** Create a scene with multiple GameObjects of different types. Tag them appropriately (Enemy, Coin, Wall, etc.). Use OnCollisionEnter() to detect each type.

3. **Trigger Volume:** Create a large trigger zone that counts how many objects are inside it. Print the count to the Console.

4. **Raycast Visualization:** Write a script that casts raycasts in multiple directions and uses Debug.DrawRay() to visualize them in the Scene view.

5. **Mass and Gravity:** Create two objects with the same size but different mass values. Drop them from the same height. Time how long they take to fall. What do you observe?

6. **Friction Simulation:** Without using the Rigidbody's drag, implement friction manually in FixedUpdate() by reducing velocity each frame.

7. **Bouncing Ball:** Create a ball that bounces realistically using Rigidbody physics. Adjust mass, drag, and material properties until it feels right.

8. **Distance-Based Damage:** Create a script that damages the player based on how fast they're moving (velocity.magnitude). Faster impacts = more damage.

9. **Layered Collision:** Set up two GameObjects on different physics layers that don't collide with each other. Use Physics.IgnoreLayerCollision().

10. **Trigger Counter:** Create a trigger that counts how many times objects have passed through it. Print the count each time.

11. **Velocity Limiter:** Implement a maximum speed limit for a moving Rigidbody. If velocity exceeds the limit, clamp it.

12. **Overlap Detection:** Use Physics.OverlapSphere() to detect all objects within a radius of the player.

13. **Force Modes:** Experiment with ForceMode.Force vs ForceMode.Impulse. Explain the difference and when to use each.

14. **Object Pooling:** Instead of Destroy(), use SetActive() to reuse coins. When a coin is collected, disable it instead of destroying it.

15. **Jump Visualization:** Write a script that displays the remaining jump height in the Console as the player jumps (showing velocity.y each frame).

---

## Common Mistakes Table

| Mistake | Why It Happens | How to Avoid It |
|---------|----------------|-----------------|
| Physics code in Update() instead of FixedUpdate() | Not understanding timing differences | Always put Rigidbody changes in FixedUpdate() for consistent physics |
| Collisions don't work | Collider or Rigidbody missing | Both objects need colliders; at least one needs a Rigidbody |
| OnCollisionEnter() doesn't trigger | Script attached to wrong object | Method must be on an object with a Rigidbody or collider |
| Trigger detection doesn't work | "Is Trigger" not checked | Check the "Is Trigger" box; at least one object needs a Rigidbody |
| Object falls through ground | Ground has no collider or is a trigger | Make sure the ground collider is NOT a trigger |
| Raycast doesn't detect ground | Ray not pointing the right direction | Use Vector3.down for ground detection; ray should point downward |
| SetActive(false) doesn't hide object | GameObject still exists but disabled | SetActive hides the object AND disables all components; this is correct |
| Mass doesn't affect movement speed | Expecting incorrect physics behavior | Higher mass makes acceleration slower, not movement speed slower |
| Double-jumping is possible | Not checking isGrounded properly | Cache the raycast result and only allow jump if isGrounded == true |
| Velocity is jerky or inconsistent | Mixing force and direct velocity changes | Pick one approach: either use forces or set velocity, not both |

---

## Assessment Prep: 10 Q&As

**Q1: What is the difference between a collider and a Rigidbody?**
A: A collider defines the physical shape for collision detection. A Rigidbody simulates physics (gravity, forces). Objects can have colliders without Rigidbodies, but physics requires a Rigidbody.

**Q2: Explain the difference between OnCollisionEnter() and OnTriggerEnter().**
A: OnCollisionEnter() fires when two solid colliders touch. OnTriggerEnter() fires when an object enters a trigger volume (Is Trigger = true). Triggers don't cause physical collisions.

**Q3: Why should physics code go in FixedUpdate() instead of Update()?**
A: FixedUpdate() is called at a fixed timestep (default 50 times/sec), making physics consistent. Update() varies with frame rate. Using Update() would make physics framerate-dependent.

**Q4: What does Physics.Raycast() return, and how do you use it?**
A: It returns a boolean. True if the ray hits something, false otherwise. You pass it a start position, direction, and max distance: `Physics.Raycast(pos, dir, out hit, distance);`

**Q5: How do you prevent the player from double-jumping?**
A: Use a raycast or sphere check to detect if the player is grounded. Only allow jumping if isGrounded is true.

**Q6: Explain the purpose of tags and how to use CompareTag().**
A: Tags are string labels for GameObjects. Use CompareTag("TagName") to efficiently identify objects in collisions. Avoid using == for tag comparison.

**Q7: What is the difference between SetActive(false) and Destroy()?**
A: SetActive(false) disables the object but keeps it in memory (useful for reuse/pooling). Destroy() completely removes it from the scene.

**Q8: What does ForceMode.Impulse do compared to ForceMode.Force?**
A: Force applies constant acceleration over time. Impulse applies instant velocity change. Use Impulse for immediate effects like jumping.

**Q9: How do you set up a collectible item that disappears when touched?**
A: Add a trigger collider to the item. In OnTriggerEnter(), check if the colliding object is the player. If yes, call Destroy() or SetActive(false).

**Q10: What happens if you apply forces to a Rigidbody with infinite mass?**
A: Nothing. An infinite mass Rigidbody doesn't move. Set the Rigidbody to "Is Kinematic" if you want to move it directly without physics.

---

## Vocabulary & Quick Reference

### Key Terms

| Term | Definition |
|------|-----------|
| **Rigidbody** | Component that simulates physics (gravity, forces, collision) |
| **Collider** | Component that defines an object's physical shape |
| **Trigger** | A collider that detects entry/exit but doesn't physically collide |
| **Mass** | Weight of an object; affects acceleration from forces |
| **Gravity** | Downward force applied automatically by the engine |
| **Drag** | Air resistance that opposes movement |
| **AddForce()** | Method to apply a force to a Rigidbody |
| **FixedUpdate()** | Called at fixed physics timestep (independent of frame rate) |
| **Raycast** | A line cast from a point to detect what it hits |
| **Tag** | String label for identifying GameObjects |
| **SetActive()** | Enable or disable a GameObject |
| **Destroy()** | Remove a GameObject from the scene |
| **Collider Types** | Box, Sphere, Capsule, and others |

### Rigidbody Quick Reference

```csharp
// Get Rigidbody component
Rigidbody rb = GetComponent<Rigidbody>();

// Apply forces (use in FixedUpdate)
rb.AddForce(forceVector, ForceMode.Force);      // Constant acceleration
rb.AddForce(forceVector, ForceMode.Impulse);    // Instant velocity change
rb.AddTorque(torqueVector);                      // Rotate

// Velocity (direction and speed)
rb.velocity = new Vector3(5, 0, 0);              // Set velocity
Vector3 currentVelocity = rb.velocity;           // Get velocity
float speed = rb.velocity.magnitude;             // Speed (ignoring direction)

// Properties
rb.mass = 2f;                                     // Weight
rb.drag = 0.5f;                                   // Friction
rb.isKinematic = true;                            // Move without physics
rb.useGravity = false;                            // Disable gravity
```

### Collision Detection Quick Reference

```csharp
// Collision with physical collision
void OnCollisionEnter(Collision collision)
{
    Debug.Log("Collided with: " + collision.gameObject.name);
    Vector3 hitPoint = collision.contacts[0].point;
    Vector3 normal = collision.contacts[0].normal;
}

void OnCollisionStay(Collision collision) { }
void OnCollisionExit(Collision collision) { }

// Trigger detection (Is Trigger = true)
void OnTriggerEnter(Collider other)
{
    Debug.Log("Entered trigger: " + other.name);
}

void OnTriggerStay(Collider other) { }
void OnTriggerExit(Collider other) { }

// Raycast
RaycastHit hit;
if (Physics.Raycast(transform.position, Vector3.down, out hit, 1f))
{
    Debug.Log("Hit: " + hit.collider.gameObject.name);
    Debug.Log("Distance: " + hit.distance);
}
```

### Collider Setup Quick Reference

```csharp
// Box Collider (rectangular)
BoxCollider bc = GetComponent<BoxCollider>();
bc.size = new Vector3(1, 1, 1);  // Width, Height, Depth

// Sphere Collider (round)
SphereCollider sc = GetComponent<SphereCollider>();
sc.radius = 0.5f;

// Capsule Collider (character shape)
CapsuleCollider cc = GetComponent<CapsuleCollider>();
cc.radius = 0.5f;
cc.height = 2f;

// Trigger setup
Collider col = GetComponent<Collider>();
col.isTrigger = true;  // No physical collision; detect entry/exit
```

---

## Additional Resources

- **Physics Settings:** Edit > Project Settings > Physics
- **Raycast Visualization:** Debug.DrawRay() and Debug.DrawLine()
- **Physics Layers:** Edit > Project Settings > Tags and Layers

