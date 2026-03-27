# Day 14: Other Joints — FixedJoint & SpringJoint

**Learning Target:** I can use FixedJoint for rigid connections and SpringJoint for elastic connections.

---

## Key Concepts

**FixedJoint** — Locks two Rigidbodies together. They move/rotate as one. Remove joint to break connection.

**SpringJoint** — Elastic connection between objects. Objects bounce back and forth. Similar to springs in real physics.

**FixedJoint use cases:**
- Compound objects (sword handle + blade glued together)
- Pickup and carry (grab object, fix to hand)
- Weld two objects together

**SpringJoint use cases:**
- Ropes and cables
- Suspension systems
- Bouncy bridges
- Elastic platforms

**Joint properties:**
- **Spring** — Stiffness of spring (higher = stiffer)
- **Damper** — How much oscillation is absorbed
- **Break Force** — Force needed to break the joint

**Real-world examples:**
- **Pikmin:** Pikmin attached to Olimar uses FixedJoint
- **Portal 2:** Bouncy bridges use SpringJoints
- **Minecraft:** Chains use SpringJoint connections
- **Ragdoll physics:** Limbs connected with joints

---

## Code Example

```csharp
using UnityEngine;

public class CarryableObject : MonoBehaviour
{
    private FixedJoint fixedJoint;
    private Rigidbody rb;
    private Vector3 originalPosition;
    private Quaternion originalRotation;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        originalPosition = transform.position;
        originalRotation = transform.rotation;
    }

    public void PickUp(Transform hand)
    {
        // Create fixed joint to hand
        fixedJoint = gameObject.AddComponent<FixedJoint>();
        fixedJoint.connectedBody = hand.GetComponent<Rigidbody>();
        
        Debug.Log("Object picked up!");
    }

    public void Drop()
    {
        if (fixedJoint != null)
        {
            Destroy(fixedJoint);
            Debug.Log("Object dropped!");
        }
    }

    public void Reset()
    {
        Drop();
        transform.position = originalPosition;
        transform.rotation = originalRotation;
        rb.velocity = Vector3.zero;
    }
}

public class BounceplatformWithSpring : MonoBehaviour
{
    private void Start()
    {
        // Create spring joint to center point
        SpringJoint spring = gameObject.AddComponent<SpringJoint>();
        
        // Create anchor point (empty object at center)
        GameObject anchor = new GameObject("Anchor");
        anchor.transform.SetParent(transform);
        anchor.transform.localPosition = Vector3.zero;
        
        spring.connectedBody = anchor.AddComponent<Rigidbody>();
        spring.connectedBody.isKinematic = true;
        
        // Configure spring
        spring.spring = 100f; // Stiffness
        spring.damper = 5f;   // Bounce reduction
        spring.minDistance = 0f;
        spring.maxDistance = 1f; // Max extension
    }
}

public class RopeBridge : MonoBehaviour
{
    public int segments = 10;
    public float segmentDistance = 0.5f;
    public Transform startPoint;
    public Transform endPoint;

    private void Start()
    {
        // Create rope segments connected with SpringJoints
        Transform previousSegment = startPoint;

        for (int i = 0; i < segments; i++)
        {
            // Create segment
            GameObject segment = GameObject.CreatePrimitive(PrimitiveType.Cube);
            segment.transform.localScale = new Vector3(0.2f, 0.2f, segmentDistance);
            segment.transform.position = startPoint.position + (endPoint.position - startPoint.position) * (i / (float)segments);

            Rigidbody segmentRb = segment.GetComponent<Rigidbody>();

            if (i == 0 || i == segments - 1)
            {
                // First and last are kinematic (fixed)
                segmentRb.isKinematic = true;
            }

            // Connect to previous segment with spring
            if (previousSegment != startPoint)
            {
                SpringJoint joint = segment.AddComponent<SpringJoint>();
                joint.connectedBody = previousSegment.GetComponent<Rigidbody>();
                joint.spring = 100f;
                joint.damper = 5f;
            }

            previousSegment = segment.transform;
        }
    }
}
```

---

## Unity Setup Steps

**For FixedJoint Pickup:**
1. Create object to pick up (cube)
2. Add Rigidbody (not kinematic)
3. Create hand (empty object)
4. Attach CarryableObject script to the object
5. In script, set hand transform and call PickUp() when E pressed
6. Press Play: Pick up object and move it around

**For SpringJoint Bridge:**
1. Create cylinder (platform)
2. Add Rigidbody (not kinematic)
3. Add SpringJoint: Inspector → Add Component → Physics → Spring Joint
4. Leave Connected Body empty (connects to world)
5. Set Spring = 100, Damper = 10
6. Press Play: Bounce on platform

---

## Guided Practice

1. Build a FixedJoint pickup system
2. Grab and carry objects
3. Create a springy platform using SpringJoint
4. Test oscillation with different damper values
5. Create rope bridge with multiple SpringJoint segments

---

## Practice Problems

**Beginner:** Create a springy platform. When player lands on it, they bounce back up.

**Intermediate:** Build a grab system where player holds object with FixedJoint. Drop it with a key press.

**Challenge:** Create a rope bridge with 8 segments connected by SpringJoints. Test walking across and jumping on it.

<details><summary>💡 Hints</summary>
- FixedJoint removes degrees of freedom (position and rotation locked)
- SpringJoint allows movement but with spring resistance
- High damper reduces bouncing; low damper = more bouncy
- Rope bridges need kinematic end points fixed to world
- Use `Destroy(fixedJoint)` to break connection
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Interactive rope bridge
public class InteractiveBridge : MonoBehaviour
{
    public int segmentCount = 8;
    public float segmentMass = 1f;
    public float springForce = 100f;
    public float damping = 5f;

    private void Start()
    {
        CreateBridge();
    }

    private void CreateBridge()
    {
        Transform prev = transform;

        for (int i = 0; i < segmentCount; i++)
        {
            GameObject seg = GameObject.CreatePrimitive(PrimitiveType.Cube);
            seg.name = "BridgeSegment" + i;
            seg.transform.position = transform.position + Vector3.right * (i * 1.5f);
            seg.transform.localScale = new Vector3(1, 0.5f, 1.5f);

            Rigidbody rbSeg = seg.GetComponent<Rigidbody>();
            rbSeg.mass = segmentMass;

            if (i == 0 || i == segmentCount - 1)
                rbSeg.isKinematic = true;

            SpringJoint joint = seg.AddComponent<SpringJoint>();
            joint.connectedBody = prev.GetComponent<Rigidbody>();
            joint.spring = springForce;
            joint.damper = damping;

            prev = seg.transform;
        }
    }
}
```

</details>
