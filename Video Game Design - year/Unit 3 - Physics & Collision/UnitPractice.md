# Unit 3 Practice Problems: Physics & Collision

15 problems ranging from beginner to advanced. Solutions provided.

---

## Problem 1: Rigidbody Basics

**Difficulty:** Beginner

Create a script that:
1. Gets the Rigidbody component attached to the GameObject
2. Prints the current mass and drag values each frame
3. Doubles the gravity scale if the object is falling (velocity.y < 0)

```csharp
using UnityEngine;

public class RigidbodyBasics : MonoBehaviour
{
    // Your code here
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class RigidbodyBasics : MonoBehaviour
{
    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        Debug.Log($"Mass: {rb.mass}, Drag: {rb.drag}");

        if (rb.velocity.y < 0)
        {
            rb.gravityScale = 2f;
        }
        else
        {
            rb.gravityScale = 1f;
        }
    }
}
```

</details>

---

## Problem 2: AddForce Patterns

**Difficulty:** Beginner

Implement a script where pressing keys applies forces:
- W: Forward force (ForceMode.Force)
- Space: Upward impulse (ForceMode.Impulse)
- A: Random force in any direction (ForceMode.VelocityChange)

```csharp
using UnityEngine;

public class AddForcePatterns : MonoBehaviour
{
    private Rigidbody rb;
    public float forwardForce = 10f;
    public float jumpForce = 5f;

    // Your code here
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class AddForcePatterns : MonoBehaviour
{
    private Rigidbody rb;
    public float forwardForce = 10f;
    public float jumpForce = 5f;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void FixedUpdate()
    {
        if (Input.GetKey(KeyCode.W))
        {
            rb.AddForce(Vector3.forward * forwardForce, ForceMode.Force);
        }

        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
        }

        if (Input.GetKeyDown(KeyCode.A))
        {
            Vector3 randomDir = Random.onUnitSphere;
            rb.AddForce(randomDir * 10f, ForceMode.VelocityChange);
        }
    }
}
```

</details>

---

## Problem 3: Collision Detection

**Difficulty:** Beginner

Create a collision-detecting script:
- Count total collisions that have occurred
- Print "Collision!" whenever a collision happens
- Display the current collision count in Update

```csharp
using UnityEngine;

public class CollisionCounter : MonoBehaviour
{
    // Your code here
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class CollisionCounter : MonoBehaviour
{
    private int collisionCount = 0;

    private void Update()
    {
        Debug.Log($"Total collisions: {collisionCount}");
    }

    private void OnCollisionEnter(Collision collision)
    {
        collisionCount++;
        Debug.Log($"Collision! Count: {collisionCount}");
    }
}
```

</details>

---

## Problem 4: Trigger Detection

**Difficulty:** Beginner

Create a pickup system:
- Detect when objects with tag "Pickup" enter a trigger
- Remove the pickup GameObject
- Count total pickups collected

```csharp
using UnityEngine;

public class PickupSystem : MonoBehaviour
{
    // Your code here
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class PickupSystem : MonoBehaviour
{
    private int pickupCount = 0;

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Pickup"))
        {
            pickupCount++;
            Debug.Log($"Pickup collected! Total: {pickupCount}");
            Destroy(other.gameObject);
        }
    }
}
```

</details>

---

## Problem 5: Layer-Based Collision

**Difficulty:** Intermediate

Create a script that:
- Only collides with objects on a specific layer (assign via Inspector)
- Uses Physics.OverlapSphere to find objects in a radius
- Applies upward force to all hit objects

```csharp
using UnityEngine;

public class LayerBasedInteraction : MonoBehaviour
{
    public LayerMask targetLayer;
    public float detectionRadius = 5f;
    public float pushForce = 10f;

    public void PushNearby()
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class LayerBasedInteraction : MonoBehaviour
{
    public LayerMask targetLayer;
    public float detectionRadius = 5f;
    public float pushForce = 10f;

    public void PushNearby()
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, detectionRadius, targetLayer);

        foreach (Collider hit in hits)
        {
            Rigidbody rb = hit.GetComponent<Rigidbody>();
            if (rb != null)
            {
                Vector3 direction = (hit.transform.position - transform.position).normalized;
                rb.AddForce(direction * pushForce, ForceMode.Impulse);
            }
        }

        Debug.DrawWireSphere(transform.position, detectionRadius, Color.blue, 0.5f);
    }
}
```

</details>

---

## Problem 6: Raycasting for Ground Detection

**Difficulty:** Intermediate

Implement ground detection:
- Raycast downward from the GameObject
- Return true if ground is detected within 0.1 units
- Visualize the raycast in the Scene view
- Only hit objects on the "Ground" layer

```csharp
using UnityEngine;

public class GroundDetector : MonoBehaviour
{
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        // Your code here
        return false;
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class GroundDetector : MonoBehaviour
{
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        Vector3 rayOrigin = transform.position + Vector3.down * 0.5f;
        bool hit = Physics.Raycast(rayOrigin, Vector3.down, 0.1f, groundLayer);

        Debug.DrawRay(rayOrigin, Vector3.down * 0.1f, hit ? Color.green : Color.red);

        return hit;
    }
}
```

</details>

---

## Problem 7: Raycasting with Hit Information

**Difficulty:** Intermediate

Create a "tap to move" system:
- Raycast from camera through mouse position to world
- If hit, print the object's name and distance
- Draw a ray showing the raycast

```csharp
using UnityEngine;

public class TapToMove : MonoBehaviour
{
    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            // Your code here
        }
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class TapToMove : MonoBehaviour
{
    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);

            if (Physics.Raycast(ray, out RaycastHit hit))
            {
                Debug.Log($"Hit: {hit.collider.gameObject.name}, Distance: {hit.distance}");
                Debug.DrawRay(ray.origin, ray.direction * hit.distance, Color.green, 2f);
            }
        }
    }
}
```

</details>

---

## Problem 8: Hinge Joint Door

**Difficulty:** Intermediate

Create a simple door mechanism:
- Use HingeJoint to allow rotation
- Set limits to 90 degrees max
- Press Space to toggle door open/closed using motor velocity

```csharp
using UnityEngine;

public class DoorController : MonoBehaviour
{
    private HingeJoint hinge;
    private bool isOpen = false;

    private void Start()
    {
        hinge = GetComponent<HingeJoint>();
        // Set up limits
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            // Toggle door
        }
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class DoorController : MonoBehaviour
{
    private HingeJoint hinge;
    private bool isOpen = false;

    private void Start()
    {
        hinge = GetComponent<HingeJoint>();
        JointLimits limits = hinge.limits;
        limits.min = 0;
        limits.max = 90;
        hinge.limits = limits;
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            isOpen = !isOpen;

            if (isOpen)
            {
                hinge.motor = new JointMotor { targetVelocity = 100f, force = 1000f };
            }
            else
            {
                hinge.motor = new JointMotor { targetVelocity = -100f, force = 1000f };
            }

            hinge.useMotor = true;
        }
    }
}
```

</details>

---

## Problem 9: Physics Material Assignment

**Difficulty:** Intermediate

Create a script that:
- Creates a PhysicsMaterial with custom friction and bounciness
- Applies it to the object's collider
- Tests different material properties

```csharp
using UnityEngine;

public class CustomMaterial : MonoBehaviour
{
    private void Start()
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class CustomMaterial : MonoBehaviour
{
    private void Start()
    {
        PhysicsMaterial mat = new PhysicsMaterial("SlipperyMaterial");
        mat.dynamicFriction = 0f;
        mat.staticFriction = 0f;
        mat.bounciness = 0.8f;

        Collider collider = GetComponent<Collider>();
        collider.material = mat;

        Debug.Log("Material applied!");
    }
}
```

</details>

---

## Problem 10: Bouncing Ball with Physics Materials

**Difficulty:** Intermediate

Create a sphere that:
- Bounces with configurable bounciness
- Falls due to gravity
- Loses energy over time (damping)
- Resets position when falling below ground

```csharp
using UnityEngine;

public class BouncingBall : MonoBehaviour
{
    private Rigidbody rb;
    public float resetYPosition = -10f;

    // Your code here
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class BouncingBall : MonoBehaviour
{
    private Rigidbody rb;
    public float resetYPosition = -10f;
    private Vector3 startPosition;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        startPosition = transform.position;

        PhysicsMaterial mat = new PhysicsMaterial("Bouncy");
        mat.bounciness = 0.9f;
        mat.dynamicFriction = 0.1f;
        GetComponent<Collider>().material = mat;
    }

    private void Update()
    {
        if (transform.position.y < resetYPosition)
        {
            transform.position = startPosition;
            rb.velocity = Vector3.zero;
        }
    }
}
```

</details>

---

## Problem 11: Melee Attack Detection

**Difficulty:** Advanced

Create a melee attack system:
- Use OverlapSphere to detect enemies in attack range
- Apply knockback force to hit enemies
- Implement a visual gizmo showing attack radius
- Add cooldown between attacks

```csharp
using UnityEngine;

public class MeleeAttack : MonoBehaviour
{
    public float attackRadius = 1.5f;
    public float knockbackForce = 10f;
    public LayerMask enemyLayer;
    public float attackCooldown = 0.5f;

    private float attackTimer = 0f;

    private void Update()
    {
        // Your code here
    }

    private void OnDrawGizmosSelected()
    {
        // Visualize attack radius
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class MeleeAttack : MonoBehaviour
{
    public float attackRadius = 1.5f;
    public float knockbackForce = 10f;
    public LayerMask enemyLayer;
    public float attackCooldown = 0.5f;

    private float attackTimer = 0f;

    private void Update()
    {
        attackTimer -= Time.deltaTime;

        if (Input.GetMouseButtonDown(0) && attackTimer <= 0)
        {
            Attack();
            attackTimer = attackCooldown;
        }
    }

    private void Attack()
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, attackRadius, enemyLayer);

        foreach (Collider hit in hits)
        {
            Rigidbody rb = hit.GetComponent<Rigidbody>();
            if (rb != null)
            {
                Vector3 knockback = (hit.transform.position - transform.position).normalized;
                rb.AddForce(knockback * knockbackForce, ForceMode.Impulse);
            }
        }

        Debug.Log($"Attack! Hit {hits.Length} enemies");
    }

    private void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position, attackRadius);
    }
}
```

</details>

---

## Problem 12: 2D Physics - Ground Detection with Raycast

**Difficulty:** Intermediate

Create a 2D ground detector:
- Use Physics2D.Raycast to detect ground
- Return true if ground detected
- Visualize with Debug.DrawRay (works in 2D too)
- Use proper 2D layer mask

```csharp
using UnityEngine;

public class GroundDetector2D : MonoBehaviour
{
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        // Your code here
        return false;
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class GroundDetector2D : MonoBehaviour
{
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, 0.1f, groundLayer);

        Debug.DrawRay(transform.position, Vector2.down * 0.1f, hit.collider != null ? Color.green : Color.red);

        return hit.collider != null;
    }
}
```

</details>

---

## Problem 13: 2D One-Way Platform

**Difficulty:** Advanced

Create a one-way platform system:
- Platform only collides when player comes from above
- Use OnCollisionEnter to detect direction
- Temporarily ignore collision if player is below
- Re-enable collision when player lands on top

```csharp
using UnityEngine;

public class OneWayPlatform : MonoBehaviour
{
    private Collider2D platformCollider;

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            platformCollider = GetComponent<Collider2D>();
            CheckDirection(collision);
        }
    }

    private void CheckDirection(Collision2D collision)
    {
        // Your code here
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class OneWayPlatform : MonoBehaviour
{
    private Collider2D platformCollider;
    private Collider2D playerCollider;

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            platformCollider = GetComponent<Collider2D>();
            playerCollider = collision.collider;
            CheckDirection(collision);
        }
    }

    private void OnCollisionStay2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            CheckDirection(collision);
        }
    }

    private void CheckDirection(Collision2D collision)
    {
        // If player moving upward (jumping through from below), ignore collision
        if (collision.relativeVelocity.y > 0)
        {
            Physics2D.IgnoreCollision(playerCollider, platformCollider, true);
        }
        else
        {
            Physics2D.IgnoreCollision(playerCollider, platformCollider, false);
        }
    }
}
```

</details>

---

## Problem 14: Line-of-Sight Detection with Raycast

**Difficulty:** Advanced

Create a guard AI detection system:
- Raycast to player to check line-of-sight
- Only "see" player if no obstacles block the ray
- Check distance limit (e.g., 10 units)
- Visualize detection ray and awareness state

```csharp
using UnityEngine;

public class GuardAI : MonoBehaviour
{
    public Transform player;
    public float sightDistance = 10f;
    public LayerMask obstacleLayer;

    public bool CanSeePlayer()
    {
        // Your code here
        return false;
    }

    private void Update()
    {
        if (CanSeePlayer())
        {
            Debug.Log("Guard sees player!");
        }
    }
}
```

<details><summary>✅ Solution</summary>

```csharp
using UnityEngine;

public class GuardAI : MonoBehaviour
{
    public Transform player;
    public float sightDistance = 10f;
    public LayerMask obstacleLayer;

    public bool CanSeePlayer()
    {
        Vector3 directionToPlayer = (player.position - transform.position).normalized;
        float distanceToPlayer = Vector3.Distance(transform.position, player.position);

        if (distanceToPlayer > sightDistance)
            return false;

        // Raycast to check if path is clear
        bool canSee = !Physics.Raycast(
            transform.position,
            directionToPlayer,
            distanceToPlayer,
            obstacleLayer
        );

        // Visualize
        Color rayColor = canSee ? Color.green : Color.red;
        Debug.DrawRay(transform.position, directionToPlayer * sightDistance, rayColor);

        return canSee;
    }

    private void Update()
    {
        if (CanSeePlayer())
        {
            Debug.Log("Guard sees player!");
        }
    }
}
```

</details>

---

## Problem 15: Complex Physics Scene

**Difficulty:** Advanced

Build a physics puzzle scene with at least 5 concepts:
1. Gravity and falling objects (Rigidbody)
2. Spring joint connecting objects
3. One-way platform
4. Pickup zone (trigger)
5. Explosive force on collision

Create scripts for each system and document which physics concepts each uses.

<details><summary>✅ Solution Outline</summary>

**PhysicsPuzzle.cs** — Main controller
```csharp
using UnityEngine;

public class PhysicsPuzzle : MonoBehaviour
{
    // This scene demonstrates:
    // 1. Gravity & falling (Rigidbody with useGravity = true)
    // 2. Spring joints connecting platforms
    // 3. One-way platform (Physics2D.IgnoreCollision)
    // 4. Pickup zone (OnTriggerEnter)
    // 5. Explosion on collision (AddForce with radial falloff)

    private int pickupCount = 0;

    // Pickup detection
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Pickup"))
        {
            pickupCount++;
            Destroy(other.gameObject);
        }
    }
}

public class ExplosiveCollider : MonoBehaviour
{
    public float explosionForce = 100f;
    public float explosionRadius = 5f;

    private void OnCollisionEnter(Collision collision)
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, explosionRadius);
        foreach (Collider hit in hits)
        {
            Rigidbody rb = hit.GetComponent<Rigidbody>();
            if (rb != null)
            {
                rb.AddExplosionForce(explosionForce, transform.position, explosionRadius);
            }
        }
    }
}

public class OneWayPlatform : MonoBehaviour
{
    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.relativeVelocity.y > 0)
        {
            Physics2D.IgnoreCollision(collision.collider, GetComponent<Collider2D>());
        }
    }
}
```

</details>

---

## Challenge Extension Problems

**Problem A:** Create a rope/chain system using multiple FixedJoints in sequence.

**Problem B:** Implement a grappling hook that pulls the player toward a raycasted point.

**Problem C:** Build a destructible wall that breaks when hit with sufficient force.

**Problem D:** Create a "push" mechanic that shows physics-based object interaction.

**Problem E:** Design a physics-based puzzle requiring the player to stack objects to reach a goal.

