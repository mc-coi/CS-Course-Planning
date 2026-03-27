# Day 8: Cinemachine & Advanced Camera Systems

**Learning Target:** I can use Unity's Cinemachine package to build sophisticated camera behaviors with minimal code.

---

## Key Concepts

**Cinemachine** — A powerful camera system in Unity that handles smooth following, framing, collision avoidance, and complex camera animations. It's used in AAA games and handles the heavy lifting for you.

**Key Components:**
- **CinemachineVirtualCamera** — A "virtual" camera that Cinemachine blends and prioritizes
- **Cinemachine Impulse** — Camera shakes for impact feedback (explosions, landing)
- **Collider** — Prevents camera from going through walls

**Advantages over manual Lerp:**
- Built-in collision detection
- Framing options (keep player in center, or off-center compositions)
- Shake/impulse responses
- Body and Aim options (Framing Transposer, Follow Camera, etc.)

**When to use Cinemachine:** Complex camera behaviors, cinematic sequences, polish.

---

## Code Example

```csharp
using UnityEngine;
using Cinemachine;

public class CinemachineSetup : MonoBehaviour
{
    // Cinemachine handles camera follow automatically
    // Just set up the virtual camera in the editor!
}

// Optional: Trigger camera shake on impact
public class CameraShakeOnLand : MonoBehaviour
{
    public CinemachineVirtualCamera virtualCam;
    private CinemachineBasicMultiChannelPerlin perlin;

    private void Start()
    {
        perlin = virtualCam.GetCinemachineComponent<CinemachineBasicMultiChannelPerlin>();
    }

    public void ShakeOnLand()
    {
        if (perlin != null)
            perlin.m_AmplitudeGain = 1f; // Shake intensity
        
        Invoke("StopShake", 0.2f);
    }

    private void StopShake()
    {
        if (perlin != null)
            perlin.m_AmplitudeGain = 0f;
    }
}
```

---

## Unity Setup Steps

1. **Install Cinemachine**
   - Window → TextMesh Pro → Import TMP Essentials (if needed)
   - Package Manager → Search "Cinemachine"
   - Install the latest version

2. **Create Virtual Camera**
   - Hierarchy: Right-click → Cinemachine → Create CM vcam
   - Name it "Player Camera"
   - In the Inspector, set "Follow" to your Player transform
   - Set "Look At" to your Player transform (optional)

3. **Configure Virtual Camera Body**
   - Framing Transposer → Horizontal/Vertical Damping: `0.5` (smoothness)
   - Dead Zone: small area in center where player doesn't move camera
   - Screen X: `0.5`, Screen Y: `0.4` (position on screen)

4. **Test**
   - Press Play and move around
   - Cinemachine should smoothly follow without manual code

---

## Guided Practice

1. **Set Up Cinemachine** (10 min)
   - Install Cinemachine from Package Manager
   - Create a Virtual Camera
   - Assign the Player as "Follow" target

2. **Configure Follow Behavior** (10 min)
   - Adjust damping (smoothness)
   - Change screen position to put player off-center (cinematic)
   - Test different settings

3. **Add Collision Avoidance** (5 min)
   - Add Collider to the virtual camera
   - Test that camera doesn't clip through walls

---

## Practice Problems

**Beginner:** Set up Cinemachine to follow the player with smooth motion. Adjust damping to feel responsive.

**Intermediate:** Create **two virtual cameras**: one for normal gameplay (3rd person), one for aiming. Switch between them when the player aims. (Hint: Set vcam.Priority higher to switch.)

**Challenge:** Implement **camera impulse feedback**: when the player lands from a jump, trigger a camera shake. Use `CinemachineImpulseSource.GenerateImpulse()`.

<details><summary>💡 Hints</summary>
- Cinemachine is a package; install it from Package Manager if not present.
- Adjust Framing Transposer damping to change smoothness (lower = snappier, higher = floaty).
- Camera shakes add impact to actions; keep them short (0.2s) so they don't feel annoying.
</details>

<details><summary>✅ Sample Answers</summary>

**Intermediate Solution (Camera Switching):**
```csharp
public CinemachineVirtualCamera normalCam;
public CinemachineVirtualCamera aimCam;

void Update()
{
    if (Input.GetMouseButton(1)) // Right-click to aim
    {
        aimCam.Priority = 20; // Higher priority = active
        normalCam.Priority = 10;
    }
    else
    {
        normalCam.Priority = 20;
        aimCam.Priority = 10;
    }
}
```

**Challenge Solution (Impulse Shake):**
```csharp
public CinemachineImpulseSource impulseSource;

void OnLand()
{
    impulseSource.GenerateImpulse(1f); // Magnitude = 1
}
```

</details>
