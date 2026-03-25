# Vocabulary & Quick Reference

## Key Terms

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

## Key Syntax

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

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Physics code in Update() instead of FixedUpdate() | Physics framerate-dependent, inconsistent behavior | Always put Rigidbody changes in FixedUpdate() for consistent physics |
| Collisions don't work | Objects pass through each other | Both objects need colliders; at least one needs a Rigidbody |
| OnCollisionEnter() doesn't trigger | Method never called | Method must be on an object with a Rigidbody or collider |
| Trigger detection doesn't work | OnTriggerEnter() never fires | Check the "Is Trigger" box; at least one object needs a Rigidbody |
| Object falls through ground | Ground disappears when player touches it | Make sure the ground collider is NOT set to "Is Trigger" |
| Raycast doesn't detect ground | Raycast returns false when it should return true | Use Vector3.down for ground detection; ray should point downward |
| SetActive(false) doesn't hide object | GameObject still visible in scene | SetActive hides the object AND disables all components; this is correct |
| Mass doesn't affect movement speed | Object moves same speed regardless of mass | Higher mass makes acceleration slower, not movement speed slower |
| Double-jumping is possible | Player can jump multiple times in air | Cache the raycast result and only allow jump if isGrounded == true |
| Velocity is jerky or inconsistent | Movement feels stuttery or wrong | Pick one approach: either use forces or set velocity, not both |
