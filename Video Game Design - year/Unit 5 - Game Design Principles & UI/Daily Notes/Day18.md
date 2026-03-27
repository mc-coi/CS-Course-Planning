# Day 18: Game Feel—Screen Shake & Visual Feedback

**Learning Target:** I can add screen shake, flash effects, and camera feedback to enhance game feel.

---

## Key Concepts

**Screen Shake**: Camera vibrates on impact or explosion—feels impactful.

**Hit Flash**: Objects briefly flash white/red on impact—shows that something happened.

**Camera Knockback**: Camera recoils slightly when player gets hit—emphasizes damage.

**Audio-Visual Sync**: Sound + visual effect + screen shake = satisfying hit.

---

## Code Example

```csharp
using UnityEngine;

public class GameFeel : MonoBehaviour
{
    public Transform cameraTransform;
    private Vector3 originalCameraPos;

    public void ScreenShake(float intensity = 0.3f, float duration = 0.1f)
    {
        StartCoroutine(ScreenShakeCoroutine(intensity, duration));
    }

    private IEnumerator ScreenShakeCoroutine(float intensity, float duration)
    {
        originalCameraPos = cameraTransform.position;
        float elapsed = 0;

        while (elapsed < duration)
        {
            // Shake camera by random offset
            Vector3 randomOffset = Random.insideUnitSphere * intensity;
            cameraTransform.position = originalCameraPos + randomOffset;
            
            elapsed += Time.deltaTime;
            intensity *= 0.9f;  // Dampen over time
            yield return null;
        }

        cameraTransform.position = originalCameraPos;
    }

    public void FlashObject(SpriteRenderer sprite, Color flashColor, float duration = 0.1f)
    {
        StartCoroutine(FlashCoroutine(sprite, flashColor, duration));
    }

    private IEnumerator FlashCoroutine(SpriteRenderer sprite, Color flashColor, float duration)
    {
        Color originalColor = sprite.color;
        sprite.color = flashColor;
        
        yield return new WaitForSeconds(duration);
        
        sprite.color = originalColor;
    }
}
```

---

## Unity Setup Steps

1. **Get Camera Reference**:
   - Attach GameFeel script to Main Camera or UI GameObject
   - In Inspector, assign Main Camera transform

2. **Test Screen Shake**:
   - Call `ScreenShake(0.2f, 0.15f)` when something impactful happens
   - Adjust intensity and duration to taste

3. **Test Hit Flash**:
   - On enemy or player, get SpriteRenderer
   - Call `FlashObject(sprite, Color.white, 0.1f)` on hit
   - Should flash white briefly

4. **Combine Effects**:
   - Call ScreenShake + Flash + Sound together
   - Much more satisfying than just one effect

---

## Guided Practice

1. **Impact Feedback**:
   - When player shoots a projectile:
     - Screen shake (small)
     - Sound effect
     - Flash the enemy

2. **Enemy Hit**:
   - Flash the enemy white
   - Larger screen shake
   - Play impact sound

3. **Player Damage**:
   - Medium screen shake
   - Flash player red
   - Play damage sound

---

## Practice Problems

**Beginner:**
Create a function that plays all hit feedback at once: screen shake, flash, and sound.

**Intermediate:**
Create a knockback effect: When player gets hit, push camera backward slightly and away from enemy.

**Challenge:**
Create a "bullet time" effect: When player gets hit, slow down time (0.25x speed), screen shake intensely, then fade back to normal.

<details><summary>💡 Hints</summary>
- Beginner: Call all three methods in sequence from one function
- Intermediate: Add velocity to camera movement based on hit direction
- Challenge: Lower Time.timeScale, use Lerp to restore it
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public void PlayHitFeedback(Vector3 hitPos)
{
    ScreenShake(0.2f, 0.1f);
    FlashObject(playerSprite, Color.white, 0.1f);
    AudioManager.PlaySFX(hitSound);
}
```

**Intermediate:**
```csharp
public void KnockbackCamera(Vector3 hitDirection, float force = 0.5f)
{
    Vector3 knockback = -hitDirection.normalized * force;
    cameraTransform.position += knockback;
    StartCoroutine(ResetCameraPosition(knockback, 0.2f));
}
```

**Challenge:**
```csharp
public IEnumerator BulletTimeHit(float slowSpeed = 0.25f, float duration = 0.5f)
{
    Time.timeScale = slowSpeed;
    ScreenShake(0.5f, duration);
    yield return new WaitForSecondsRealtime(duration);
    Time.timeScale = 1f;
}
```
</details>
