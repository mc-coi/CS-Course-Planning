# Day 16: Audio Manager & Dynamic Audio Control

**Learning Target:** I can build a centralized audio manager that controls all game sounds.

---

## Key Concepts

**Singleton Audio Manager**: One script controls all audio in the game, accessible from anywhere.

**Audio Groups**: Separate volumes for music, SFX, UI (master volume controls all).

**Volume Persistence**: Save audio settings to PlayerPrefs.

**Dynamic Pitch**: Vary pitch slightly for repetitive sounds (footsteps, hits) to avoid monotony.

---

## Code Example

```csharp
using UnityEngine;

public class AudioManager : MonoBehaviour
{
    public static AudioManager instance;
    
    public AudioSource musicSource;
    public AudioSource sfxSource;
    public AudioSource uiSource;
    
    private float masterVolume = 1f;
    private float musicVolume = 0.7f;
    private float sfxVolume = 0.8f;

    private void Awake()
    {
        if (instance != null && instance != this)
            Destroy(gameObject);
        else
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
            LoadAudioSettings();
        }
    }

    public static void PlaySFX(AudioClip clip, float volumeScale = 1f)
    {
        instance.sfxSource.PlayOneShot(clip, instance.sfxVolume * volumeScale);
    }

    public static void PlayMusic(AudioClip clip, float fadeInDuration = 0f)
    {
        instance.musicSource.clip = clip;
        instance.musicSource.Play();
        // Optional fade-in here
    }

    public static void SetMusicVolume(float volume)
    {
        instance.musicVolume = Mathf.Clamp01(volume);
        instance.musicSource.volume = instance.musicVolume * instance.masterVolume;
        PlayerPrefs.SetFloat("MusicVolume", instance.musicVolume);
    }

    private void LoadAudioSettings()
    {
        musicVolume = PlayerPrefs.GetFloat("MusicVolume", 0.7f);
        sfxVolume = PlayerPrefs.GetFloat("SFXVolume", 0.8f);
        masterVolume = PlayerPrefs.GetFloat("MasterVolume", 1f);
        
        ApplyAudioSettings();
    }

    private void ApplyAudioSettings()
    {
        musicSource.volume = musicVolume * masterVolume;
        sfxSource.volume = sfxVolume * masterVolume;
        uiSource.volume = 1f * masterVolume;
    }
}
```

---

## Unity Setup Steps

1. **Create Persistent AudioManager**:
   - GameObject → "AudioManager"
   - Add 3 AudioSources (Music, SFX, UI)
   - Configure each with appropriate settings

2. **Attach Script**:
   - Create `AudioManager.cs`
   - Set instance in Awake()
   - Call `DontDestroyOnLoad()` so it persists

3. **Load Audio Settings on Startup**:
   - Check PlayerPrefs for saved volume levels
   - Apply on Start()

4. **Test Persistence**:
   - Change volumes
   - Close and reopen game
   - Volumes should remain

---

## Guided Practice

1. **Centralized Control**:
   - From any script, call `AudioManager.PlaySFX(clip)`
   - No need to reference AudioManager directly

2. **Volume Sliders**:
   - Create UI sliders for Master, Music, SFX volumes
   - Connect to AudioManager methods
   - Verify changes save and persist

3. **Dynamic Pitch Variation**:
   - When playing footstep SFX, vary pitch: 0.9 to 1.1
   - Sounds less repetitive

---

## Practice Problems

**Beginner:**
Create a mute button that toggles all audio on/off.

**Intermediate:**
Implement separate UI sound effects: button hover, button click, error sound. All controlled via AudioManager.

**Challenge:**
Create a music crossfade system: When switching tracks, fade out old music while fading in new music over 2 seconds.

<details><summary>💡 Hints</summary>
- Beginner: Store previous volume, set to 0, restore when toggled
- Intermediate: Create separate methods for each UI sound type
- Challenge: Use two AudioSources, animate volume with Coroutine
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
private bool isMuted = false;
private float prevVolume = 1f;

public void ToggleMute()
{
    isMuted = !isMuted;
    if (isMuted)
    {
        prevVolume = musicSource.volume;
        musicSource.volume = 0;
    }
    else
        musicSource.volume = prevVolume;
}
```

**Intermediate:**
```csharp
public static void PlayUIHover(AudioClip clip)
{
    instance.uiSource.PlayOneShot(clip, 0.3f);
}

public static void PlayUIClick(AudioClip clip)
{
    instance.uiSource.PlayOneShot(clip, 0.5f);
}
```

**Challenge:**
```csharp
public static void CrossfadeMusic(AudioClip newClip, float duration = 2f)
{
    instance.StartCoroutine(instance.CrossfadeCoroutine(newClip, duration));
}

private IEnumerator CrossfadeCoroutine(AudioClip clip, float duration)
{
    for (float t = 0; t < duration; t += Time.deltaTime)
    {
        musicSource.volume = Mathf.Lerp(musicVolume, 0, t / duration);
        yield return null;
    }
    musicSource.clip = clip;
    musicSource.Play();
    // Fade back in...
}
```
</details>
