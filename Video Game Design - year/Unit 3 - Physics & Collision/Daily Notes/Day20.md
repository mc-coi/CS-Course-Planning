# Day 20: Physics Lab Continued — Physics Puzzle Level

**Learning Target:** I can design and build a physics-based puzzle level using multiple physics systems.

---

## Project Overview

Build a **Physics Puzzle Level** where:
1. Player pushes/rolls objects to solve puzzles
2. Multiple collider types (boxes, spheres, ramps)
3. Triggers control doors and gates
4. Physics materials create varied surfaces
5. Requires understanding of mass, friction, momentum

**Physics concepts used:**
- Varied masses (heavy blocks, light balls)
- Friction and drag for realistic movement
- Trigger zones for puzzle mechanics
- Raycasting for ground detection
- Joints for connected objects
- Multiple collider types

---

## Puzzle Mechanics

**Example 1: Weight Puzzle**
- Place 3 heavy blocks on a pressure plate to open door
- Door trigger checks total weight on plate

**Example 2: Ball Path Puzzle**
- Roll ball through checkpoints
- Each checkpoint activates next section
- Use ramps and funnels (BoxColliders) to guide ball

**Example 3: Momentum Puzzle**
- Heavy sphere blocks door
- Player must build momentum to push it
- Friction values determine difficulty

---

## Code Example

```csharp
using UnityEngine;
using System.Collections.Generic;

public class PressurePlateTrigger : MonoBehaviour
{
    private List<Rigidbody> objectsOnPlate = new List<Rigidbody>();
    public float requiredWeight = 30f;
    public Transform doorToOpen;
    
    private bool doorOpen = false;

    private void Update()
    {
        CheckWeight();
    }

    private void CheckWeight()
    {
        float totalWeight = 0f;

        // Remove destroyed objects
        objectsOnPlate.RemoveAll(rb => rb == null);

        // Sum remaining weights
        foreach (Rigidbody rb in objectsOnPlate)
        {
            totalWeight += rb.mass;
        }

        if (totalWeight >= requiredWeight && !doorOpen)
        {
            OpenDoor();
        }
        else if (totalWeight < requiredWeight && doorOpen)
        {
            CloseDoor();
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        Rigidbody rb = collision.gameObject.GetComponent<Rigidbody>();
        if (rb != null && !objectsOnPlate.Contains(rb))
        {
            objectsOnPlate.Add(rb);
        }
    }

    private void OnCollisionExit(Collision collision)
    {
        Rigidbody rb = collision.gameObject.GetComponent<Rigidbody>();
        if (rb != null)
        {
            objectsOnPlate.Remove(rb);
        }
    }

    private void OpenDoor()
    {
        doorOpen = true;
        doorToOpen.gameObject.SetActive(false); // Or slide door open
        Debug.Log("Door opened!");
    }

    private void CloseDoor()
    {
        doorOpen = false;
        doorToOpen.gameObject.SetActive(true);
    }
}

public class CheckpointTrigger : MonoBehaviour
{
    public int checkpointNumber = 1;
    public GameObject nextSection;
    
    private bool activated = false;

    private void OnTriggerEnter(Collider other)
    {
        if (!activated && other.CompareTag("Ball"))
        {
            activated = true;
            Debug.Log("Checkpoint " + checkpointNumber + " reached!");
            
            if (nextSection != null)
            {
                nextSection.SetActive(true);
            }
        }
    }
}

public class RampFunnel : MonoBehaviour
{
    // Curved path guides ball toward goal
    private void OnTriggerStay(Collider other)
    {
        Rigidbody rb = other.GetComponent<Rigidbody>();
        if (rb != null)
        {
            // Gentle steering toward center
            Vector3 directionToCenter = (transform.position - rb.position).normalized;
            rb.AddForce(directionToCenter * 2f);
        }
    }
}

public class MomentumGate : MonoBehaviour
{
    private Rigidbody rb;
    public float minimumVelocityToOpen = 5f;
    public float doorMoveDistance = 3f;
    
    private Vector3 originalPos;
    private bool isOpen = false;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        originalPos = transform.position;
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.relativeVelocity.magnitude > minimumVelocityToOpen && !isOpen)
        {
            OpenGate();
        }
    }

    private void OpenGate()
    {
        isOpen = true;
        transform.Translate(Vector3.right * doorMoveDistance);
        Debug.Log("Gate opened by momentum!");
    }
}
```

---

## Unity Setup Steps

1. **Design puzzle layout on paper** (sketch sections and solution)
2. **Create Level Scene**
3. **Build Puzzle Section 1: Weight Puzzle**
   - Pressure plate (BoxCollider, not kinematic, no Rigidbody or Static)
   - 3 heavy blocks (Rigidbody, mass = 10 each)
   - Door (can move or deactivate)
   - PressurePlateTrigger script

4. **Build Puzzle Section 2: Ball Path**
   - Ramps (rotated cubes with BoxColliders)
   - Checkpoints (trigger zones)
   - Ball (Rigidbody, SphereCollider)

5. **Build Puzzle Section 3: Momentum Gate**
   - Heavy sliding block (Rigidbody, high mass)
   - Gate that opens when pushed hard
   - MomentumGate script

6. **Test:** Solve each puzzle to progress

---

## Practice Problems

**Beginner:** Create a weight puzzle. Two blocks needed on plate to open door.

**Intermediate:** Build a 3-section puzzle with weight, ball path, and momentum challenges.

**Challenge:** Design a puzzle that requires combining multiple mechanics (push block onto pressure plate, which opens gate allowing ball through ramp, which triggers final door).

<details><summary>💡 Hints</summary>
- Use checkpoints to control puzzle progression
- Mass is key to puzzle difficulty—adjust block weights
- Friction values guide ball movement on ramps
- Test puzzle multiple times to ensure it's solvable but challenging
- Provide visual feedback when puzzles are solved (doors moving, lights, sounds)
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Combined puzzle: Block triggers gate that allows ball through
public class SequencePuzzle : MonoBehaviour
{
    public Transform pressurePlate;
    public Transform gate;
    public Transform ballCheckpoint;
    
    private bool gateOpen = false;
    private bool completed = false;

    public void OnBlockPlaced()
    {
        if (!gateOpen)
        {
            gateOpen = true;
            gate.gameObject.SetActive(false); // Open gate
        }
    }

    public void OnBallCheckpoint()
    {
        if (!completed)
        {
            completed = true;
            Debug.Log("Puzzle solved!");
        }
    }
}
```

</details>
