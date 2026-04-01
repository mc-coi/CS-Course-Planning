# Unit 3 Reference Guide: Physics & Collision

A quick-reference for common physics concepts, components, and code patterns.

---

## Table of Contents

1. [Rigidbody Properties](#rigidbody-properties)
2. [Collider Types](#collider-types)
3. [Collision vs Trigger Callbacks](#collision-vs-trigger-callbacks)
4. [Physics.Raycast](#physicsraycast)
5. [Overlap Detection](#overlap-detection)
6. [Joints](#joints)
7. [PhysicsMaterial](#physicsmaterial)
8. [2D Physics (Rigidbody2D & Collider2D)](#2d-physics)
9. [Common Patterns](#common-patterns)
10. [Debugging Tips](#debugging-tips)

---

## Rigidbody Properties

### Component Access
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
```

### Common Properties & Methods

| Property/Method | Type | Purpose | Example |
|-----------------|------|---------|---------|
| `mass` | float | Object weight | `rb.mass = 2f;` |
| `velocity` | Vector3 | Current movement | `rb.velocity = Vector3.zero;` |
| `angularVelocity` | Vector3 | Rotation speed | `rb.angularVelocity *= 0.95f;` |
| `drag` | float | Linear air resistance | `rb.drag = 0.5f;` |
| `angularDrag` | float | Rotational resistance | `rb.angularDrag = 0.05f;` |
| `gravityScale` | float | Gravity multiplier | `rb.gravityScale = 2f;` |
| `useGravity` | bool | Enable/disable gravity | `rb.useGravity = false;` |
| `isKinematic` | bool | Manual movement only | `rb.isKinematic = true;` |
| `constraints` | RigidbodyConstraints | Freeze axes | `rb.constraints = RigidbodyConstraints.FreezeRotation;` |
| `AddForce()` | method | Apply force | `rb.AddForce(Vector3.up * 5f, ForceMode.Impulse);` |
| `AddTorque()` | method | Apply rotation | `rb.AddTorque(Vector3.up * 10f);` |
| `MovePosition()` | method | Kinematic movement | `rb.MovePosition(transform.position + Vector3.right);` |

### ForceMode Options

| Mode | Behavior | Use Case |
|------|----------|----------|
| `Force` | Applies continuous force (default) | Rockets, pushing, driving |
| `Impulse` | Instant velocity change | Jumping, explosions, punches |
| `Acceleration` | Applies acceleration (ignores mass) | Feel-based movement |
| `VelocityChange` | Direct velocity addition (ignores mass) | Teleports, knockback |

### Common Rigidbody Constraints

```csharp
// Freeze all rotations (prevents tipping)
rb.constraints = RigidbodyConstraints.FreezeRotation;

// Freeze rotation on Z axis only
rb.constraints = RigidbodyConstraints.FreezeRotationZ;

// Freeze position on Y axis (locks height)
rb.constraints = RigidbodyConstraints.FreezePositionY;

// Combine constraints
rb.constraints = RigidbodyConstraints.FreezeRotationX | RigidbodyConstraints.FreezeRotationY;
```

### Collision Detection

```csharp
// For fast-moving objects that might pass through colliders
rb.collisionDetectionMode = CollisionDetectionMode.Continuous;

// Options: Discrete (default, fast), Continuous, ContinuousDynamic
```

---

## Collider Types

### Component Access
```csharp
Collider collider = GetComponent<Collider>();
BoxCollider box = GetComponent<BoxCollider>();
```

### Collider Comparison

| Type | Shape | Use Case | Performance |
|------|-------|----------|-------------|
| **BoxCollider** | Rectangular prism | Walls, boxes, ground | Fast |
| **SphereCollider** | Sphere | Balls, explosions, pickups | Fast |
| **CapsuleCollider** | Cylinder with rounded ends | Characters, projectiles | Fast |
| **MeshCollider** | Exact mesh shape | Complex terrain (static only) | Slow if moving |
| **TerrainCollider** | Terrain heightmap | Large landscapes | Optimized |
| **CharacterController** | Specialized capsule | Character movement (non-physics) | Very fast |

### Setting up Colliders

```csharp
// Add to GameObject at runtime
BoxCollider box = gameObject.AddComponent<BoxCollider>();
box.size = new Vector3(1f, 2f, 1f);
box.center = Vector3.zero;

// Common properties
collider.enabled = false; // Disable/enable collision
collider.isTrigger = false; // Is it a trigger?
collider.tag = "Player"; // Optional tag
```

### isTrigger Property

```csharp
// Trigger = area detection (no physical collision)
collider.isTrigger = true;
// Objects pass through, but OnTriggerEnter/Stay/Exit called

// Solid = physical collision
collider.isTrigger = false;
// Objects bump into each other, OnCollisionEnter/Stay/Exit called
```

---

## Collision vs Trigger Callbacks

### Collision (Physical Contact)

Requirements:
- Both GameObjects must have Colliders
- At least one must have a Rigidbody
- Both colliders must have `isTrigger = false`

Callbacks:

```csharp
private void OnCollisionEnter(Collision collision)
{
    // Called once when collision starts
    Debug.Log("Hit: " + collision.gameObject.name);
    Debug.Log("Contact normal: " + collision.contacts[0].normal);
    Debug.Log("Impulse magnitude: " + collision.relativeVelocity.magnitude);
}

private void OnCollisionStay(Collision collision)
{
    // Called every frame while colliding
}

private void OnCollisionExit(Collision collision)
{
    // Called once when collision ends
}
```

Collision Properties:

```csharp
// Access info from Collision parameter
Collision collision = ...;
GameObject other = collision.gameObject;
Rigidbody otherRb = collision.rigidbody;
Vector3 contactPoint = collision.GetContact(0).point;
Vector3 contactNormal = collision.GetContact(0).normal;
float relativeVelocity = collision.relativeVelocity.magnitude;
int contactCount = collision.contactCount;
```

### Trigger (Area Detection)

Requirements:
- One GameObject must have a Collider with `isTrigger = true`
- That GameObject should ideally have a Rigidbody (set isKinematic = true)
- Other object needs Collider (Rigidbody optional)

Callbacks:

```csharp
private void OnTriggerEnter(Collider other)
{
    // Called once when entering trigger
    if (other.CompareTag("Player"))
    {
        Debug.Log("Player entered!");
    }
}

private void OnTriggerStay(Collider other)
{
    // Called every frame while in trigger
}

private void OnTriggerExit(Collider other)
{
    // Called once when exiting trigger
}
```

### Quick Comparison

| Aspect | Collision | Trigger |
|--------|-----------|---------|
| **Physical?** | Yes | No |
| **isTrigger** | false | true |
| **Pass through?** | No | Yes |
| **Callbacks** | OnCollision* | OnTrigger* |
| **Requires Rigidbody** | At least one | Recommended |
| **Use** | Physical interaction | Area detection |

---

## Physics.Raycast

### Basic Syntax

```csharp
bool hit = Physics.Raycast(origin, direction, distance);

// Full signature with output parameter
bool hit = Physics.Raycast(origin, direction, out RaycastHit hitInfo, distance);

// With layer mask
bool hit = Physics.Raycast(origin, direction, out RaycastHit hitInfo, distance, layerMask);
```

### Common Ground Detection

```csharp
using UnityEngine;

public class GroundDetector : MonoBehaviour
{
    private Rigidbody rb;
    public float groundCheckDistance = 0.1f;
    public LayerMask groundLayer;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    public bool IsGrounded()
    {
        Vector3 rayOrigin = transform.position + Vector3.down * 0.5f;
        bool grounded = Physics.Raycast(rayOrigin, Vector3.down, groundCheckDistance, groundLayer);

        // Optional: visualize
        Debug.DrawRay(rayOrigin, Vector3.down * groundCheckDistance, grounded ? Color.green : Color.red);

        return grounded;
    }
}
```

### Raycast with Hit Information

```csharp
RaycastHit hit;
if (Physics.Raycast(transform.position, Vector3.down, out hit, 10f))
{
    // Successful hit
    GameObject hitObject = hit.collider.gameObject;
    Vector3 hitPoint = hit.point;
    Vector3 hitNormal = hit.normal;
    float distance = hit.distance;
    Rigidbody hitRb = hit.rigidbody;
}
else
{
    // No hit
}
```

### Raycast with Layer Mask

```csharp
// Create layer mask in Inspector and assign
public LayerMask targetLayer;

// Only hit objects on "Enemy" layer
int layerMask = LayerMask.GetMask("Enemy");
bool hit = Physics.Raycast(transform.position, Vector3.forward, 10f, layerMask);

// Ignore specific layer
int ignoreLayer = ~LayerMask.GetMask("Water");
bool hit = Physics.Raycast(transform.position, Vector3.forward, 10f, ignoreLayer);
```

### Common Patterns

**Ground Detection:**
```csharp
public bool IsGrounded()
{
    return Physics.Raycast(transform.position + Vector3.down * 0.5f, Vector3.down, 0.1f, groundLayer);
}
```

**Line-of-Sight Check:**
```csharp
public bool CanSee(Transform target)
{
    Vector3 directionToTarget = (target.position - transform.position).normalized;
    float distanceToTarget = Vector3.Distance(transform.position, target.position);
    return !Physics.Raycast(transform.position, directionToTarget, distanceToTarget, obstacleLayer);
}
```

**Shooting:**
```csharp
if (Physics.Raycast(transform.position, transform.forward, out RaycastHit hit, shootDistance))
{
    Enemy enemy = hit.collider.GetComponent<Enemy>();
    if (enemy != null)
        enemy.TakeDamage(10f);
}
```

---

## Overlap Detection

### Overlap Methods

```csharp
// Check if sphere overlaps colliders
Collider[] hits = Physics.OverlapSphere(center, radius, layerMask);
foreach (Collider hit in hits)
{
    // Do something with each collider
}

// Check if box overlaps
Collider[] hits = Physics.OverlapBox(center, halfExtents, Quaternion.identity, layerMask);

// Check if capsule overlaps
Collider[] hits = Physics.OverlapCapsule(point1, point2, radius, layerMask);
```

### Ground Detection with OverlapCircle

```csharp
public class GroundDetectorOverlap : MonoBehaviour
{
    public float groundCheckRadius = 0.3f;
    public LayerMask groundLayer;

    public bool IsGrounded()
    {
        Vector3 checkPos = transform.position + Vector3.down * 0.5f;
        Collider[] hits = Physics.OverlapSphere(checkPos, groundCheckRadius, groundLayer);

        // Draw debug sphere
        Debug.DrawWireSphere(checkPos, groundCheckRadius, hits.Length > 0 ? Color.green : Color.red);

        return hits.Length > 0;
    }
}
```

### Melee Attack Detection

```csharp
public class MeleeAttack : MonoBehaviour
{
    public float attackRadius = 1f;
    public LayerMask enemyLayer;

    public void Attack()
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, attackRadius, enemyLayer);

        foreach (Collider hit in hits)
        {
            Enemy enemy = hit.GetComponent<Enemy>();
            if (enemy != null)
            {
                enemy.TakeDamage(20f);
            }
        }
    }
}
```

---

## Joints

### Hinge Joint (Rotating Door)

```csharp
public class DoorController : MonoBehaviour
{
    private HingeJoint hinge;

    private void Start()
    {
        hinge = GetComponent<HingeJoint>();
        hinge.limits = new JointLimits { min = 0, max = 90 };
    }

    public void Open()
    {
        hinge.motor = new JointMotor { targetVelocity = 100f, force = 1000f };
        hinge.useMotor = true;
    }

    public void Close()
    {
        hinge.motor = new JointMotor { targetVelocity = -100f, force = 1000f };
        hinge.useMotor = true;
    }
}
```

### Fixed Joint (Glue Two Objects)

```csharp
public class AttachToObject : MonoBehaviour
{
    public void GlueTo(GameObject target)
    {
        FixedJoint joint = gameObject.AddComponent<FixedJoint>();
        joint.connectedBody = target.GetComponent<Rigidbody>();
    }
}
```

### Spring Joint (Springy Constraint)

```csharp
public class SpringTrap : MonoBehaviour
{
    private SpringJoint spring;

    private void Start()
    {
        spring = GetComponent<SpringJoint>();
        spring.spring = 100f;
        spring.damper = 5f;
    }
}
```

### Common Joint Properties

```csharp
joint.anchor = Vector3.zero; // Connection point on this object
joint.connectedBody = otherRb; // Connected Rigidbody
joint.enableCollision = false; // Whether to collide after connecting
joint.enablePreprocessing = true; // Enable preprocessing for stability
```

---

## PhysicsMaterial

### Creating and Applying

```csharp
// In code
PhysicsMaterial mat = new PhysicsMaterial("SlipperyIce");
mat.dynamicFriction = 0f;
mat.staticFriction = 0f;
mat.bounciness = 0.5f;

Collider collider = GetComponent<Collider>();
collider.material = mat;
```

### Common Material Configurations

**Ice (Slippery):**
```csharp
mat.dynamicFriction = 0f;
mat.staticFriction = 0f;
mat.bounciness = 0.2f;
```

**Rubber (Bouncy):**
```csharp
mat.dynamicFriction = 0.7f;
mat.staticFriction = 0.7f;
mat.bounciness = 0.9f;
```

**Concrete (Rough):**
```csharp
mat.dynamicFriction = 0.7f;
mat.staticFriction = 0.9f;
mat.bounciness = 0.1f;
```

**Jump Pad (Super Bouncy):**
```csharp
mat.dynamicFriction = 0f;
mat.staticFriction = 0f;
mat.bounciness = 1.5f; // Can be > 1 for energy gain
```

### Friction vs Bounciness

| Property | Effect | Range |
|----------|--------|-------|
| **dynamicFriction** | Sliding resistance | 0 = slippery, 1+ = sticky |
| **staticFriction** | Resting friction | Usually > dynamicFriction |
| **bounciness** | Bounce on impact | 0 = absorb, 1 = perfect bounce, >1 = gain energy |

---

## 2D Physics

### Rigidbody2D Access

```csharp
Rigidbody2D rb2d = GetComponent<Rigidbody2D>();
```

### Key Differences from 3D

| Property | 3D | 2D |
|----------|----|----|
| **Rigidbody** | `Rigidbody` | `Rigidbody2D` |
| **Gravity** | `useGravity` | `gravityScale` |
| **Velocity** | `Vector3` | `Vector2` |
| **Rotation** | `Quaternion` | `float (degrees)` |
| **Raycast** | `Physics.Raycast()` | `Physics2D.Raycast()` |
| **Overlap** | `Physics.OverlapCircle()` | `Physics2D.OverlapCircle()` |

### Common 2D Colliders

```csharp
// BoxCollider2D (rectangular)
BoxCollider2D box = GetComponent<BoxCollider2D>();
box.size = new Vector2(1f, 2f);

// CircleCollider2D (circular)
CircleCollider2D circle = GetComponent<CircleCollider2D>();
circle.radius = 0.5f;

// CapsuleCollider2D (elongated)
CapsuleCollider2D capsule = GetComponent<CapsuleCollider2D>();
capsule.size = new Vector2(1f, 2f);

// EdgeCollider2D (line segment)
EdgeCollider2D edge = GetComponent<EdgeCollider2D>();
edge.points = new[] { Vector2.zero, new Vector2(5f, 0) };

// PolygonCollider2D (custom polygon)
PolygonCollider2D poly = GetComponent<PolygonCollider2D>();
```

### 2D Callbacks (Same as 3D, but with Collider2D)

```csharp
private void OnCollisionEnter2D(Collision2D collision)
{
    Debug.Log("2D Collision: " + collision.gameObject.name);
}

private void OnTriggerEnter2D(Collider2D other)
{
    Debug.Log("2D Trigger: " + other.gameObject.name);
}
```

### 2D Raycast

```csharp
RaycastHit2D hit = Physics2D.Raycast(origin, direction, distance, layerMask);
if (hit.collider != null)
{
    Debug.Log("Hit: " + hit.collider.gameObject.name);
}

// Multiple raycasts
RaycastHit2D[] hits = Physics2D.RaycastAll(origin, direction, distance, layerMask);
```

### 2D Overlap

```csharp
Collider2D[] hits = Physics2D.OverlapCircleAll(center, radius, layerMask);
Collider2D[] hits = Physics2D.OverlapBoxAll(center, size, angle, layerMask);
```

---

## Common Patterns

### Pick Up Item on Collision

```csharp
public class ItemPickup : MonoBehaviour
{
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            Player player = other.GetComponent<Player>();
            player.AddItem(gameObject);
            Destroy(gameObject);
        }
    }
}
```

### Damage on Contact

```csharp
public class DamageZone : MonoBehaviour
{
    public int damagePerSecond = 10;

    private void OnTriggerStay(Collider other)
    {
        Health health = other.GetComponent<Health>();
        if (health != null)
        {
            health.TakeDamage(damagePerSecond * Time.deltaTime);
        }
    }
}
```

### Push Away from Object

```csharp
public class Pusher : MonoBehaviour
{
    public float pushForce = 10f;
    public float pushRadius = 5f;
    public LayerMask targetLayer;

    public void Push()
    {
        Collider[] hits = Physics.OverlapSphere(transform.position, pushRadius, targetLayer);
        foreach (Collider hit in hits)
        {
            Rigidbody rb = hit.GetComponent<Rigidbody>();
            if (rb != null && rb != GetComponent<Rigidbody>())
            {
                Vector3 direction = (hit.transform.position - transform.position).normalized;
                rb.AddForce(direction * pushForce, ForceMode.Impulse);
            }
        }
    }
}
```

### One-Way Platform (2D)

```csharp
public class OneWayPlatform : MonoBehaviour
{
    private Collider2D platformCollider;
    private Collider2D playerCollider;

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            playerCollider = collision.collider;
            // Allow passing through from below
        }
    }

    private void OnCollisionStay2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            // If player is below, ignore collision
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
}
```

---

## Debugging Tips

### Visual Debugging

```csharp
// Draw raycast
Debug.DrawRay(origin, direction * distance, Color.red, duration);

// Draw line
Debug.DrawLine(pointA, pointB, Color.green);

// Draw wire sphere (for overlap detection)
Debug.DrawWireSphere(center, radius, Color.blue);

// Draw wire cube (for box overlap)
Debug.DrawWireCube(center, size, Color.yellow);
```

### Log Physics Events

```csharp
private void OnCollisionEnter(Collision collision)
{
    Debug.Log($"Collision: {collision.gameObject.name} (force: {collision.relativeVelocity.magnitude})");
}

private void OnTriggerEnter(Collider other)
{
    Debug.Log($"Trigger: {other.gameObject.name}");
}
```

### Check Physics Settings

Edit → Project Settings → Physics:
- Gravity (usually 0, -9.81, 0)
- Default Solver Iterations (default 6)
- Default Max Angular Velocity
- Layer Collision Matrix (which layers collide with which)

### Common Issues & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| Objects fall through floor | Too fast, Discrete detection | Use Continuous, add Rigidbody to ground |
| No collision detected | Missing Rigidbody | Add Rigidbody (can be Kinematic) |
| Collision too bouncy | High bounciness | Reduce PhysicsMaterial bounciness |
| Movement feels floaty | High drag | Reduce drag or increase acceleration |
| Can't jump reliably | No ground detection | Implement Raycast or Overlap check |

