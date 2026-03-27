# Day 15: Sprint 2 — Particles, Animations & Game Feel

**Session Goal:** Add particle effects and improve animations to make the game feel polished and responsive.

---

## Today's Focus

"Game feel" (also called "juice") is the collection of small effects that make actions feel satisfying. A jump that has a squash-and-stretch. A coin that explodes into sparkles when collected. An enemy that flashes red when hit. These tiny details make a huge difference.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up check-in.

**Minutes 5-25:** Add particle effects for at least 2 events (collection, death, impact).

**Minutes 25-45:** Add a simple animation (Animator) for player idle/run if not already done.

**Minutes 45-55:** Playtest. Compare with and without particles — feel the difference.

---

## Technical Tips

```csharp
// Particle effect on pickup (use Particle System)
// 1. Create → Effects → Particle System
// 2. Configure: Duration=0.5, Looping=false, Start Lifetime=0.3, Start Speed=4
// 3. Emission: Rate Over Time=0, Bursts: Count=15 at time 0
// 4. Make it a prefab and drag into script:

public class Collectible : MonoBehaviour
{
    public GameObject collectParticlesPrefab;

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            // Spawn particles, then destroy after 1 second
            GameObject fx = Instantiate(collectParticlesPrefab, transform.position, Quaternion.identity);
            Destroy(fx, 1f);
            GameManager.instance.AddScore(10);
            AudioManager.instance.PlaySFX(AudioManager.instance.collectClip);
            Destroy(gameObject);
        }
    }
}

// Screen shake (simple version):
public class CameraShake : MonoBehaviour
{
    public static CameraShake instance;
    void Awake() { instance = this; }

    public System.Collections.IEnumerator Shake(float duration, float magnitude)
    {
        Vector3 original = transform.localPosition;
        float elapsed = 0f;
        while (elapsed < duration)
        {
            float x = Random.Range(-1f, 1f) * magnitude;
            float y = Random.Range(-1f, 1f) * magnitude;
            transform.localPosition = new Vector3(x, y, original.z);
            elapsed += Time.deltaTime;
            yield return null;
        }
        transform.localPosition = original;
    }
}
// Usage: StartCoroutine(CameraShake.instance.Shake(0.2f, 0.3f));
```

---

## Reflection / Exit Ticket

1. Name two particle effects you added and what they're triggered by.
2. Does the game feel more satisfying with them?

---

## Progress Checklist

- [ ] At least 2 particle effects implemented
- [ ] Player has at least idle and run animations (or clear placeholder)
- [ ] Game feels more responsive and satisfying than before
- [ ] Scene saved and backed up
