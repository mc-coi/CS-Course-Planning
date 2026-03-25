# Day 15: Game Feel, Juice & Feedback

**Learning Target:** Add visual, audio, and physical feedback to make gameplay feel satisfying and responsive.

### Key Concepts

- **Game Feel:** The responsiveness and satisfaction players feel when interacting with the game
- **Juice:** Visual and audio feedback that makes gameplay more satisfying
- **Particle Effects:** Visual particles for impact, explosions, or effects
- **Screen Shake:** Camera movement that creates impact feedback
- **Audio Feedback:** Sounds for actions (jump, land, collect, impact)
- **Screenshake Strength:** How intense and how long the shake lasts
- **Feedback Loop:** The relationship between player input and game response

### Content

Game feel is the difference between a game that feels satisfying and one that feels dead. It comes from multiple sources:

1. **Visual Feedback:** Particle effects, animations, color changes
2. **Audio Feedback:** Sound effects, music, volume changes
3. **Physical Feedback:** Screen shake, controller rumble
4. **Responsive Controls:** No input lag, immediate response

"Juice" refers to extra polish that makes games feel alive. A jump with a particle effect, sound, and screen shake feels much better than a silent jump.

### Code Examples

```csharp
using UnityEngine;

public class JuicyGameFeels : MonoBehaviour
{
    public ParticleSystem jumpEffect;
    public AudioSource jumpSound;
    public float screenShakeStrength = 0.1f;
    public float screenShakeDuration = 0.2f;

    private Camera mainCamera;
    private float shakeTimer = 0f;
    private Vector3 originalCameraPosition;

    void Start()
    {
        mainCamera = Camera.main;
        originalCameraPosition = mainCamera.transform.position;
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Jump();
        }

        // Update screen shake
        if (shakeTimer > 0)
        {
            shakeTimer -= Time.deltaTime;
            Vector3 randomShake = Random.insideUnitSphere * screenShakeStrength;
            mainCamera.transform.position = originalCameraPosition + randomShake;
        }
        else
        {
            mainCamera.transform.position = originalCameraPosition;
        }
    }

    void Jump()
    {
        Debug.Log("Jumped with juice!");

        // Play particle effect at jump location
        if (jumpEffect != null)
        {
            Instantiate(jumpEffect, transform.position, Quaternion.identity);
        }

        // Play sound effect
        if (jumpSound != null)
        {
            jumpSound.PlayOneShot(jumpSound.clip);
        }

        // Apply screen shake
        StartScreenShake();

        // Physics
        GetComponent<Rigidbody>().AddForce(Vector3.up * 5f, ForceMode.Impulse);
    }

    void StartScreenShake()
    {
        shakeTimer = screenShakeDuration;
    }
}
```

```csharp
using UnityEngine;

public class CollectionFeedback : MonoBehaviour
{
    public ParticleSystem collectEffect;
    public AudioClip collectSound;
    public float popScale = 1.2f;  // How large the collected item becomes

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Collectible"))
        {
            // Particle effect
            if (collectEffect != null)
            {
                Instantiate(collectEffect, transform.position, Quaternion.identity);
            }

            // Sound effect
            if (collectSound != null)
            {
                AudioSource.PlayClipAtPoint(collectSound, transform.position);
            }

            // Visual pop (scale up briefly)
            StartCoroutine(PopAndDestroy(other.gameObject));
        }
    }

    System.Collections.IEnumerator PopAndDestroy(GameObject obj)
    {
        Vector3 originalScale = obj.transform.localScale;
        obj.transform.localScale = originalScale * popScale;
        yield return new WaitForSeconds(0.1f);
        Destroy(obj);
    }
}
```

### Guided Practice

1. Create a player character and a jump script
2. Add a ParticleSystem to the scene and reference it
3. Add an AudioSource with a sound effect
4. Implement the JuicyGameFeels script to add feedback
5. Test the jump with all feedback enabled
6. Test disabling each feedback type one at a time
7. Compare the feel - notice how much better it feels with all the juice!

### Practice Problems

**Problem 1 — Beginner:** Create a script that plays a sound when the player jumps.

**Problem 2 — Intermediate:** Add a screen shake effect that triggers when the player jumps.

**Problem 3 — Challenge:** Implement a complete player control system with state machine, camera follow, particle effects on jump, and audio feedback.

<details>
<summary>Hints</summary>

**Hint 1:** Use audioSource.PlayOneShot() to play sound without interrupting other audio.

**Hint 2:** Screen shake works by temporarily offsetting the camera position with Random.insideUnitSphere * strength.

**Hint 3:** Use Instantiate() for particle effects and StartCoroutine() for delayed actions.

</details>

<details>
<summary>Sample Answers</summary>

**Answer 1:**
```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        audioSource.PlayOneShot(jumpClip);
    }
}
```

**Answer 2:**
```csharp
if (shakeTimer > 0)
{
    shakeTimer -= Time.deltaTime;
    Vector3 shake = Random.insideUnitSphere * shakeStrength;
    cam.transform.position = originalPos + shake;
}
else
{
    cam.transform.position = originalPos;
}
```

**Answer 3:** Combine the code examples from Days 14, 15, and 16. Add particle and audio references and trigger them appropriately.

</details>
