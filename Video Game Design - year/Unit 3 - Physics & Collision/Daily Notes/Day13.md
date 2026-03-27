# Day 13: Joints Introduction — HingeJoint

**Learning Target:** I can use HingeJoint to create rotating physics-based doors, wheels, and connected objects.

---

## Key Concepts

**Joint** — A component that connects two Rigidbodies with physical constraints. Found in Add Component → Physics → Joints.

**HingeJoint** — Allows rotation around a single axis (like a door hinge or wheel axle).

**Connected Body** — The Rigidbody the joint connects to. If empty, joint connects to world/ground.

**Anchor & Axis** — Position and direction of the hinge pivot.

**Use Limits** — When checked, you can set min/max rotation angles (e.g., door can't open more than 120 degrees).

**Use Spring** — Add torque to return to target angle (springy, bouncy doors).

**Real-world examples:**
- **Minecraft:** Doors and trapdoors use HingeJoints
- **Half-Life:** Physics-based doors and gates
- **Portal 2:** Chamber doors with physics constraints
- **Vehicles:** Wheels use HingeJoints on axles

---

## Code Example

```csharp
using UnityEngine;

public class HingeDoorController : MonoBehaviour
{
    private HingeJoint hingeJoint;
    public float openAngle = 120f;
    public float closeAngle = 0f;
    public float motorSpeed = 50f;
    
    private bool isOpen = false;

    private void Start()
    {
        hingeJoint = GetComponent<HingeJoint>();
        
        // Set up motor for automated opening
        JointMotor motor = hingeJoint.motor;
        motor.force = 100f;
        motor.freeSpin = false;
        hingeJoint.motor = motor;
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.E))
        {
            ToggleDoor();
        }
    }

    private void ToggleDoor()
    {
        isOpen = !isOpen;

        JointMotor motor = hingeJoint.motor;
        motor.targetVelocity = isOpen ? motorSpeed : -motorSpeed;
        hingeJoint.motor = motor;
        hingeJoint.useMotor = true;

        Debug.Log(isOpen ? "Door opening..." : "Door closing...");
    }

    private void OnTriggerEnter(Collider other)
    {
        // Auto-open when player approaches
        if (other.CompareTag("Player"))
        {
            if (!isOpen)
            {
                ToggleDoor();
            }
        }
    }
}

public class BreakableJoint : MonoBehaviour
{
    private HingeJoint hingeJoint;
    public float breakForce = 1000f;

    private void Start()
    {
        hingeJoint = GetComponent<HingeJoint>();
    }

    private void Update()
    {
        // Check current torque (rotation force)
        float currentTorque = hingeJoint.currentTorque.magnitude;
        
        if (currentTorque > breakForce)
        {
            Debug.Log("Joint broken!");
            Destroy(hingeJoint);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a door:** Cube scaled to look like a door (tall, thin)
2. **Add Rigidbody:** Not kinematic, high drag to reduce spinning
3. **Add HingeJoint:** Inspector → Add Component → Physics → Hinge Joint
4. **Set Anchor:** Position on the door's edge (where hinge would be)
5. **Set Axis:** Y-axis (0, 1, 0) for vertical door rotation
6. **Check "Use Limits":** Set min -120, max 0 (door can't open backwards)
7. **Check "Use Motor":** Will allow code to control opening
8. **Create trigger zone** in front of door with HingeDoorController script
9. **Press Play:** Stand near door, press E to open

---

## Guided Practice

1. Create a door with HingeJoint
2. In Scene view, manually rotate it to see constraint limits work
3. Add code to open door on keypress
4. Add spring effect (Use Spring checkbox) — door bounces back
5. Add multiple doors to a hallway, test performance

---

## Practice Problems

**Beginner:** Create a simple door that opens on key press. No animation, just instant open to max angle.

**Intermediate:** Build a gate system. Gate opens slowly with motor. When closed, it blocks passage. When open, player can walk through.

**Challenge:** Create a physics-based catapult. Use HingeJoint with spring for the arm. When E is pressed, launch objects placed on the catapult.

<details><summary>💡 Hints</summary>
- Set Connected Body to empty (connects to world)
- Motor provides torque to rotate the joint
- Limits prevent rotation beyond specified angles
- Spring makes joint return to target angle with bounce
- Use high drag on door Rigidbody to prevent overspin
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Catapult
public class CatapultLauncher : MonoBehaviour
{
    private HingeJoint hingeJoint;
    public float launchForce = 100f;

    private void Start()
    {
        hingeJoint = GetComponent<HingeJoint>();
    }

    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Launch();
        }
    }

    private void Launch()
    {
        JointMotor motor = hingeJoint.motor;
        motor.targetVelocity = launchForce;
        hingeJoint.motor = motor;
        hingeJoint.useMotor = true;
        
        Invoke("StopMotor", 0.5f);
    }

    private void StopMotor()
    {
        JointMotor motor = hingeJoint.motor;
        motor.targetVelocity = 0f;
        hingeJoint.motor = motor;
    }
}
```

</details>
