# Day 12: Sprint 2 — Audio & Sound Effects

**Session Goal:** Add background music and at least 3 sound effects to your game.

---

## Today's Focus

Sound transforms a game from a visual exercise to an experience. Even one well-placed "coin pickup" sound creates satisfaction that no amount of visual polish can replicate. Today: music + at least 3 SFX.

---

## Work Session Agenda

**Minutes 0-5:** Stand-up check-in.

**Minutes 5-20:** Find and import audio assets (see sources below).

**Minutes 20-45:** Wire up SFX to jump, collect, damage-taken, and enemy defeat events.

**Minutes 45-55:** Playtest with headphones. Adjust volumes. Save.

---

## Free Audio Sources

- **Kenney.nl/assets** → Interface Sounds, Impact Sounds (free, no attribution required)
- **freesound.org** → search for "jump", "coin", "explosion" (check license)
- **mixkit.co/free-sound-effects** → free game sounds
- **opengameart.org** → music and SFX (check license — CC0 is fully free)

---

## Technical Tips

```csharp
using UnityEngine;

public class AudioManager : MonoBehaviour
{
    public static AudioManager instance;

    [Header("Music")]
    public AudioSource musicSource;

    [Header("SFX")]
    public AudioSource sfxSource;
    public AudioClip jumpClip;
    public AudioClip collectClip;
    public AudioClip hurtClip;
    public AudioClip enemyDeathClip;

    void Awake()
    {
        if (instance == null) { instance = this; DontDestroyOnLoad(gameObject); }
        else Destroy(gameObject);
    }

    public void PlaySFX(AudioClip clip)
    {
        sfxSource.PlayOneShot(clip);
    }
}

// Usage in PlayerController:
// AudioManager.instance.PlaySFX(AudioManager.instance.jumpClip);

// Usage in Collectible:
// AudioManager.instance.PlaySFX(AudioManager.instance.collectClip);
```

---

## Reflection / Exit Ticket

1. How many sound effects are in your game now?
2. Which sound made the biggest difference to the game feel?

---

## Progress Checklist

- [ ] Background music playing (looping, appropriate volume)
- [ ] At least 3 SFX: jump/action, collect/reward, hurt/damage
- [ ] AudioManager singleton created
- [ ] Volumes balanced (SFX not louder than music)
- [ ] Scene saved and backed up
