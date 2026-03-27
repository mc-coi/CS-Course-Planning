# Day 16: Physics Material Applications & Advanced Friction

**Learning Target:** I can design physics materials strategically to create interesting gameplay and environmental feedback.

---

## Key Concepts

**Friction curves** — Different static vs dynamic friction creates "sticky start, slippery slide" feel.

**Bounciness tuning** — Create predictable bounces for gameplay (puzzle games, platformers).

**Material combinations** — How different materials interact (steel on ice vs steel on concrete).

**Performance materials** — Optimize physics by using materials instead of code checks.

**Directional friction** — Asymmetric friction for special effects (one-way slopes).

**Real-world examples:**
- **Mario:** Jump pads use high bounciness
- **Sonic:** Loops use friction to slow rolling ball
- **Marble Madness:** Careful friction balance for control
- **Portal 2:** Gel surfaces have ultra-low friction

---

## Code Example

```csharp
using UnityEngine;

public class DynamicMaterialSwapper : MonoBehaviour
{
    private Collider col;
    private PhysicMaterial originalMaterial;
    private PhysicMaterial slipperyMaterial;
    private PhysicMaterial stickeyMaterial;

    private void Start()
    {
        col = GetComponent<Collider>();
        originalMaterial = col.material;

        // Create slippery variant
        slipperyMaterial = new PhysicMaterial("Slippery");
        slipperyMaterial.staticFriction = 0.2f;
        slipperyMaterial.dynamicFriction = 0.2f;
        slipperyMaterial.bounciness = 0.3f;

        // Create sticky variant
        stickeyMaterial = new PhysicMaterial("Sticky");
        stickeyMaterial.staticFriction = 1.5f;
        stickeyMaterial.dynamicFriction = 1.5f;
        stickeyMaterial.bounciness = 0f;
    }

    public void MakeSlippery()
    {
        col.material = slipperyMaterial;
    }

    public void MakeSticky()
    {
        col.material = stickeyMaterial;
    }

    public void ResetMaterial()
    {
        col.material = originalMaterial;
    }
}

public class BouncePadMaterial : MonoBehaviour
{
    private void Start()
    {
        // Create super-bouncy material for jump pads
        PhysicMaterial bouncePad = new PhysicMaterial("BouncePad");
        bouncePad.staticFriction = 0f;
        bouncePad.dynamicFriction = 0f;
        bouncePad.bounciness = 1.2f; // Over 1 = gains energy
        
        GetComponent<Collider>().material = bouncePad;
    }

    private void OnCollisionEnter(Collision collision)
    {
        Rigidbody rb = collision.gameObject.GetComponent<Rigidbody>();
        if (rb != null)
        {
            Debug.Log("Bounced! Velocity: " + rb.velocity.magnitude);
        }
    }
}

public class SlopeSlider : MonoBehaviour
{
    // Demonstrates how material works on slopes
    private void OnCollisionStay(Collision collision)
    {
        // Check slope angle
        Vector3 normal = collision.contacts[0].normal;
        float slopeAngle = Vector3.Angle(normal, Vector3.up);

        if (slopeAngle > 30f)
        {
            Debug.Log("Sliding down steep slope at " + slopeAngle + " degrees");
        }
    }
}
```

---

## Unity Setup Steps

1. **Create ramp (plane rotated 45 degrees)**
2. **Create 3 material presets:**
   - Normal: friction 0.6, bounciness 0.5
   - Icy: friction 0.1, bounciness 0.8
   - Muddy: friction 1.5, bounciness 0
3. **Test ball sliding down each ramp** with different materials
4. **Create jump pad:** High bounciness (1.0+), zero friction
5. **Drop ball on jump pad** and observe energy amplification

---

## Guided Practice

1. Design 5 different surface materials for a mini-golf game
2. Each material affects ball speed, bounce, control
3. Test rolling and bouncing on slopes
4. Adjust values until gameplay feels good
5. Document recommended material settings for designers

---

## Practice Problems

**Beginner:** Create a ramp with medium friction. Roll a ball down and measure stopping distance.

**Intermediate:** Build a pinball table with bumpers (high bounciness) and guides (high friction). Test gameplay.

**Challenge:** Design a marble race course. Different sections use different materials to create interesting physics puzzles (speed sections, braking sections, bouncy shortcuts).

<details><summary>💡 Hints</summary>
- Static friction > dynamic friction = sticky start, then slide
- Bounciness over 1.0 amplifies energy (use carefully!)
- Test materials in-game, not just in Inspector
- Combine materials with level design for best results
- Document material settings for level designers
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Marble race with material zones
public class RaceMaterial : MonoBehaviour
{
    private void Start()
    {
        string zoneName = gameObject.name;
        PhysicMaterial mat = new PhysicMaterial("RaceMat_" + zoneName);

        switch (zoneName)
        {
            case "SpeedZone":
                mat.staticFriction = 0.2f;
                mat.dynamicFriction = 0.2f;
                mat.bounciness = 0f;
                break;
            case "BrakeZone":
                mat.staticFriction = 1.0f;
                mat.dynamicFriction = 1.0f;
                mat.bounciness = 0f;
                break;
            case "BounceZone":
                mat.staticFriction = 0f;
                mat.dynamicFriction = 0f;
                mat.bounciness = 0.9f;
                break;
        }

        GetComponent<Collider>().material = mat;
    }
}
```

</details>
