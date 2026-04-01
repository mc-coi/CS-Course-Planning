# Unit 3 Answer Key: Physics & Collision

Comprehensive answer key for all 15 practice problems covering Rigidbody, collision detection, raycasting, and physics materials.

---

## Problem 1: Rigidbody Basics

### Solution

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

### What Success Looks Like
Console logs mass and drag each frame. Gravity doubles when object falls (velocity.y < 0). Object falls faster while descending.

### Common Mistakes
- Using `gravity` instead of `gravityScale` (gravityScale is the multiplier)
- Checking velocity without Rigidbody assignment
- Setting gravityScale in FixedUpdate instead of Update (works but inconsistent with physics)

---

## Problem 2: AddForce Patterns

### Solution

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

### What Success Looks Like
- W: Object accelerates forward smoothly (accumulates)
- Space: Object jumps instantly upward (impulse)
- A: Object gets random burst in any direction (immediate velocity change)

### Common Mistakes
- Using Update instead of FixedUpdate (inconsistent with physics)
- Using GetKeyDown for continuous force (only fires once)
- ForceMode choices incorrect for intended effect

---

## Problem 3: Collision Detection

### Solution

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

### What Success Looks Like
Console shows collision count incrementing each time object hits something. "Collision!" message appears immediately on impact.

### Common Mistakes
- Using OnCollisionStay instead of OnCollisionEnter (fires every frame)
- Not having a Collider component on the object
- Forgetting to check if target also has a Collider

---

## Problem 4: Trigger Detection

### Solution

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

### What Success Looks Like
Each pickup collected increments counter. Pickup GameObject destroyed on collection. Console confirms each collection.

### Common Mistakes
- Using OnCollisionEnter instead of OnTriggerEnter (trigger is a non-physical collider)
- Forgetting to set Collider "Is Trigger" checkbox
- Not tagging pickup objects
- Destroying the script owner instead of the pickup

---

## Problem 5: Layer-Based Collision

### Solution

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

### What Success Looks Like
OverlapSphere finds all objects on specified layer. All found objects pushed outward. Sphere visualized in Scene view.

### Common Mistakes
- Forgetting to normalize direction vector (inconsistent push force)
- Not checking if Rigidbody exists before using
- Using Physics.OverlapSphere without layer mask (finds everything)

---

## Problem 6: Raycasting for Ground Detection

### Solution

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

### What Success Looks Like
Raycast shoots downward from slightly below object center. Green ray when grounded, red when airborne. IsGrounded() returns correct boolean.

### Common Mistakes
- Ray origin at center instead of below (off by half unit)
- Distance too large or too small (should be ~0.1 for precision)
- Forgetting layer mask (hits everything)
- Not visualizing rays (Debug.DrawRay helps debugging)

---

## Problem 7: Raycasting with Hit Information

### Solution

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

### What Success Looks Like
Click in scene and console shows hit object name and distance. Green ray drawn from camera through click point to object.

### Common Mistakes
- Not using `out RaycastHit hit` (can't get hit information)
- Ray direction not normalized (distance values incorrect)
- Debug.DrawRay drawn in Update instead of within raycast (won't persist)

---

## Problem 8: Hinge Joint Door

### Solution

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

### What Success Looks Like
Door rotates smoothly open (0° to 90°) and closed. Space toggle controls door state. Motor velocity controls direction.

### Common Mistakes
- Not setting joint limits (door rotates freely)
- Forgetting to enable `useMotor` (motor doesn't apply)
- Motor force too low (door moves slowly)
- Not toggling direction (always rotates one way)

---

## Problem 9: Physics Material Assignment

### Solution

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

### What Success Looks Like
Material created at runtime. Object becomes slippery (no friction) and bouncy (0.8 elasticity). Console confirms application.

### Common Mistakes
- Setting values on material before assigning to collider
- Using wrong friction values (should be 0-1)
- Forgetting to get Collider component

---

## Problem 10: Bouncing Ball with Physics Materials

### Solution

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

### What Success Looks Like
Sphere bounces with high elasticity (0.9). Loses energy gradually due to damping. Resets when falling below threshold. Multiple bounces visible.

### Common Mistakes
- Bounciness too high (1.0 bounces forever violating physics)
- Not resetting velocity (continues falling infinitely)
- Friction too high (ball doesn't bounce, just slides)

---

## Problem 11: Melee Attack Detection

### Solution

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

### What Success Looks Like
Click to attack. All enemies within radius take knockback. Cooldown prevents spam. Gizmo shows attack radius in editor.

### Common Mistakes
- Using GetKeyDown every frame (attack fires multiple times)
- Not normalizing knockback direction (inconsistent force)
- Not implementing cooldown (attacks spam)

---

## Problem 12: 2D Physics - Ground Detection with Raycast

### Solution

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

### What Success Looks Like
IsGrounded() returns true when object above ground. Green ray when grounded, red when airborne. Works in 2D scenes.

### Common Mistakes
- Using Physics.Raycast instead of Physics2D.Raycast (wrong dimension)
- Checking `hit.collider` instead of `hit.collider != null`
- Ray distance too small (fails to detect ground slightly below)

---

## Problem 13: 2D One-Way Platform

### Solution

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

### What Success Looks Like
Player can pass through platform from below by jumping. Player lands on platform from above. Relative velocity correctly determines direction.

### Common Mistakes
- Using OnCollisionEnter only (needs OnCollisionStay for continuous checking)
- Using player velocity instead of relative velocity (wrong reference frame)
- Direction check inverted (passes through from top instead of bottom)

---

## Problem 14: Line-of-Sight Detection with Raycast

### Solution

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

### What Success Looks Like
Guard detects player only when within sight distance and line of sight is clear. Obstacles block vision. Ray color indicates detection state.

### Common Mistakes
- Not checking distance limit (guards see through walls from far away)
- Using entire sightDistance for raycast instead of distanceToPlayer
- Not inverting raycast result (function returns if obstacle blocks, but we want line of sight)

---

## Problem 15: Complex Physics Scene

### Solution

```csharp
using UnityEngine;

public class PhysicsPuzzle : MonoBehaviour
{
    // This scene demonstrates:
    // 1. Gravity & falling (Rigidbody with useGravity = true)
    // 2. Spring joints connecting platforms
    // 3. One-way platform (Physics2D.IgnoreCollision)
    // 4. Pickup zone (OnTriggerEnter)
    // 5. Explosion on collision (AddExplosionForce)

    private int pickupCount = 0;

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

### What Success Looks Like
Complex scene with all 5 physics concepts functioning. Gravity pulls objects down. Spring joints wobble. Pickups disappear on contact. Explosion creates area effect. One-way platform works correctly.

### Common Mistakes
- Not implementing all 5 systems (incomplete scene)
- Not integrating systems (disconnected mechanics)
- Physics inconsistencies (gravity working differently on different objects)

---

## Summary Table

| Problem | Concept | Difficulty |
|---------|---------|-----------|
| 1 | Rigidbody Properties | Beginner |
| 2 | Force Modes | Intermediate |
| 3 | Collision Detection | Beginner |
| 4 | Trigger Volumes | Beginner |
| 5 | Layer Masks | Intermediate |
| 6 | Raycasting Basics | Intermediate |
| 7 | Raycast Hit Info | Intermediate |
| 8 | Joint Motors | Intermediate |
| 9 | Physics Materials | Intermediate |
| 10 | Material Properties | Intermediate |
| 11 | Area Detection | Advanced |
| 12 | 2D Raycasting | Intermediate |
| 13 | 2D One-Way Platforms | Advanced |
| 14 | Line of Sight | Advanced |
| 15 | Integrated Systems | Advanced |
