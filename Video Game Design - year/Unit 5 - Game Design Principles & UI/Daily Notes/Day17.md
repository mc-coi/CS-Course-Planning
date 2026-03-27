# Day 17: Game Feel & Polish—Particle Systems

**Learning Target:** I can add particle effects to enhance gameplay feedback.

---

## Key Concepts

**Particle System**: Emits lots of small objects (sparks, smoke, blood) to create visual effects.

**Key Properties**:
- **Duration**: How long particles emit
- **Start Lifetime**: How long each particle lives
- **Start Speed**: How fast particles move
- **Start Color**: Color of particles
- **Gravity Modifier**: How much gravity affects particles
- **Emission Rate**: How many particles per second

**Feedback Loop**: Particles show player that something happened (hit, explosion, pickup).

---

## Code Example

```csharp
using UnityEngine;

public class ParticleEffects : MonoBehaviour
{
    public ParticleSystem hitParticles;
    public ParticleSystem pickupParticles;
    public ParticleSystem explosionParticles;

    public void PlayHitEffect(Vector3 position)
    {
        // Instantiate particles at hit location
        ParticleSystem ps = Instantiate(hitParticles, position, Quaternion.identity);
        Destroy(ps.gameObject, ps.main.duration);
    }

    public void PlayPickupEffect(Vector3 position)
    {
        ParticleSystem ps = Instantiate(pickupParticles, position, Quaternion.identity);
        Destroy(ps.gameObject, ps.main.duration);
    }

    public void PlayExplosion(Vector3 position)
    {
        ParticleSystem ps = Instantiate(explosionParticles, position, Quaternion.identity);
        Destroy(ps.gameObject, ps.main.duration);
    }
}
```

---

## Unity Setup Steps

1. **Create Particle System**:
   - Right-click in Hierarchy → Effects → Particle System
   - This creates a new GameObject with ParticleSystem component

2. **Configure for Hit Effect**:
   - In Inspector, find Particle System component
   - Duration: 1
   - Start Lifetime: 0.5
   - Start Speed: 5
   - Start Color: Red
   - Max Particles: 20
   - Gravity Modifier: 1

3. **Assign Material** (optional):
   - Default uses a sprite
   - For glow effects, change the material

4. **Prefab It**:
   - Drag the Particle System into Prefabs folder
   - Delete from scene
   - Instantiate when needed

5. **Test**:
   - Attach ParticleEffects script
   - Call `PlayHitEffect(position)` on impact
   - Particles should appear

---

## Guided Practice

1. **Create Hit Feedback**:
   - Create a red particle effect for enemy hits
   - Play when enemy takes damage
   - Verify it looks satisfying

2. **Pickup Effect**:
   - Create gold/yellow particles for item pickup
   - Play upward and outward

3. **Explosion Effect**:
   - Create a larger explosion with smoke and fire colors
   - Use for boss defeats or explosives

---

## Practice Problems

**Beginner:**
Create a simple particle effect for a coin pickup (gold, floating upward, fading).

**Intermediate:**
Create a blood splatter effect that plays in different colors based on enemy type.

**Challenge:**
Create a trail effect that follows the player's sword swing, with smoke particles that fade out.

<details><summary>💡 Hints</summary>
- Beginner: Use Start Color with fade-out, Start Speed upward
- Intermediate: Instantiate same particle effect, change color via script
- Challenge: Use GetComponent<ParticleSystem>() to modify properties before play
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public void PlayCoinPickup(Vector3 pos)
{
    ParticleSystem ps = Instantiate(coinParticles, pos, Quaternion.identity);
    ps.GetComponent<ParticleSystem>().Play();
}
```

**Intermediate:**
```csharp
public void PlayBlood(Vector3 pos, EnemyType type)
{
    ParticleSystem ps = Instantiate(bloodParticles, pos, Quaternion.identity);
    Color color = type == EnemyType.Goblin ? green : red;
    var psMain = ps.main;
    psMain.startColor = color;
    ps.Play();
}
```

**Challenge:**
```csharp
public void PlaySwordSlash(Vector3 startPos, Vector3 endPos)
{
    for (float t = 0; t < 0.5f; t += Time.deltaTime)
    {
        Vector3 pos = Vector3.Lerp(startPos, endPos, t / 0.5f);
        ParticleSystem ps = Instantiate(slashParticles, pos, Quaternion.identity);
        ps.Play();
    }
}
```
</details>
