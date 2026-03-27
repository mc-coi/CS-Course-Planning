# Day 6: OnCollisionStay & Collision Feedback

**Learning Target:** I can detect ongoing collisions and provide player feedback (sounds, particles, visual effects).

---

## Key Concepts

**OnCollisionStay(Collision collision)** — Fires every FixedUpdate while two objects remain in contact. Useful for continuous effects.

**Collision.contacts[]** — Array of contact points where objects touch. Each ContactPoint has position and normal direction.

**Collision.impulse** — Force applied during collision (useful for impact effects).

**Visual feedback** — Particle effects, screen shake, or color changes on collision.

**Audio feedback** — Play collision sounds based on impact force.

**Real-world examples:**
- **Tetris:** OnCollisionStay detects when pieces settle on rows
- **Racing games:** OnCollisionStay with walls causes friction/sliding sounds
- **Zelda:** Picking up items uses OnCollisionStay with item trigger zones

---

## Code Example

```csharp
using UnityEngine;

public class CollisionFeedback : MonoBehaviour
{
    private Rigidbody rb;
    private AudioSource audioSource;
    private float lastCollisionTime = 0f;
    public float collisionCooldown = 0.1f; // Prevent sound spam

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        audioSource = GetComponent<AudioSource>();
        if (audioSource == null)
        {
            audioSource = gameObject.AddComponent<AudioSource>();
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        // Play sound only if enough time has passed
        if (Time.time - lastCollisionTime > collisionCooldown)
        {
            float impactForce = collision.relativeVelocity.magnitude;
            
            // Adjust volume based on impact force
            audioSource.volume = Mathf.Min(impactForce / 10f, 1f);
            audioSource.Play();
            
            lastCollisionTime = Time.time;

            // Print contact info
            foreach (ContactPoint contact in collision.contacts)
            {
                Debug.Log("Contact at: " + contact.point);
                Debug.Log("Contact normal: " + contact.normal);
            }
        }
    }

    private void OnCollisionStay(Collision collision)
    {
        // This fires every frame while touching
        if (collision.gameObject.CompareTag("SlipperyFloor"))
        {
            // Reduce friction by applying movement
            rb.velocity *= 0.99f; // Slight deceleration
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a ball with Rigidbody** and BoxCollider
2. **Add AudioSource component:** Inspector → Add Component → Audio → Audio Source
3. **Import or create a collision sound:** Assign to AudioSource's AudioClip field
4. **Create ground platform** with BoxCollider and tag it
5. **Attach CollisionFeedback script to the ball**
6. **Press Play:** Drop the ball and hear sound on collision

---

## Guided Practice

1. Create a ball and three different surface materials (wood floor, metal floor, ice)
2. Each surface has its own tag and AudioClip
3. In OnCollisionEnter, play different sounds based on tag
4. Adjust volume based on `collision.relativeVelocity.magnitude`

---

## Practice Problems

**Beginner:** Create a collision counter. Print "Collision #1", "Collision #2", etc. each time the object hits something.

**Intermediate:** Build a "surface type" system. Different surfaces play different sounds. Ice reduces friction, mud increases drag.

**Challenge:** Create a ball that leaves a particle trail when rolling on surfaces. Particles spawn from `contact.point` positions during OnCollisionStay.

<details><summary>💡 Hints</summary>
- Use `collision.contacts[0].point` to get the collision position
- Set up collisionCooldown to prevent audio spam when objects jitter
- Instantiate particle effects at contact points for visual feedback
- `collision.relativeVelocity` is relative speed between objects
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Particle trail on collision
public class ParticleTrail : MonoBehaviour
{
    public GameObject particlePrefab;

    private void OnCollisionStay(Collision collision)
    {
        if (collision.contacts.Length > 0)
        {
            ContactPoint contact = collision.contacts[0];
            Instantiate(particlePrefab, contact.point, Quaternion.identity);
        }
    }
}
```

</details>
