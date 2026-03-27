# Day 15: Audio System Basics

**Learning Target:** I can play sound effects and background music using AudioSource.

---

## Key Concepts

**AudioSource**: Component that plays sound.
- **AudioClip**: The sound file (imported .wav, .mp3, .ogg)
- **Volume**: 0 = silent, 1 = full volume
- **Pitch**: 1 = normal speed, 0.5 = half speed, 2 = double speed
- **Loop**: Play continuously

**AudioListener**: Receives audio from all AudioSources (usually on Main Camera).

**Play vs PlayOneShot**: 
- `Play()`: Stops previous sound, starts new one
- `PlayOneShot()`: Overlaps with current sound

---

## Code Example

```csharp
using UnityEngine;

public class AudioManager : MonoBehaviour
{
    public AudioSource musicSource;
    public AudioSource sfxSource;
    
    public AudioClip bgMusic;
    public AudioClip jumpSFX;
    public AudioClip hitSFX;

    private void Start()
    {
        // Start background music
        musicSource.clip = bgMusic;
        musicSource.loop = true;
        musicSource.volume = 0.7f;
        musicSource.Play();
    }

    public void PlayJumpSound()
    {
        // PlayOneShot = can overlap with music
        sfxSource.PlayOneShot(jumpSFX, 1f);
    }

    public void PlayHitSound(float volume = 1f)
    {
        sfxSource.PlayOneShot(hitSFX, volume);
    }

    public void SetMusicVolume(float volume)
    {
        musicSource.volume = Mathf.Clamp01(volume);
    }

    public void StopMusic()
    {
        musicSource.Stop();
    }
}
```

---

## Unity Setup Steps

1. **Import Audio Files**:
   - Add .wav, .mp3, or .ogg files to Assets folder
   - Verify they import correctly

2. **Create AudioSources**:
   - Add empty GameObject: "AudioManager"
   - Add component: AudioSource (for music)
   - Add another: AudioSource (for SFX)
   - Or use one source and switch clips

3. **Configure Music Source**:
   - AudioClip: Assign your music file
   - Volume: 0.7
   - Loop: Checked
   - Pitch: 1
   - Leave Play On Awake unchecked (we'll play in code)

4. **Configure SFX Source**:
   - Volume: 0.8
   - Loop: Unchecked
   - Play On Awake: Unchecked

5. **Attach Script**:
   - Create `AudioManager.cs`
   - Attach to AudioManager GameObject
   - Assign clip references in Inspector

---

## Guided Practice

1. **Play Background Music**:
   - Attach AudioManager script
   - Play scene
   - Music should loop continuously

2. **Play SFX on Button Click**:
   - Create button that calls `PlayJumpSound()`
   - SFX plays without stopping music

3. **Volume Control**:
   - Create a slider for music volume
   - Connect slider to `SetMusicVolume()`
   - Adjust volume smoothly

---

## Practice Problems

**Beginner:**
Create a script that plays a different SFX based on enemy type (goblin = growl, knight = clash).

**Intermediate:**
Implement a fade-in effect: Music starts silent, gradually reaches full volume over 3 seconds.

**Challenge:**
Create an audio manager that plays footstep sounds based on surface type (grass, stone, water) with different audio clips.

<details><summary>💡 Hints</summary>
- Beginner: Pass audio clip as parameter, or use a dictionary to map types to clips
- Intermediate: Use Coroutine with Lerp to animate volume
- Challenge: Use raycast or physics to detect surface, select appropriate clip
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public void PlayEnemySound(EnemyType type)
{
    AudioClip clip = type == EnemyType.Goblin ? goblinSFX : knightSFX;
    sfxSource.PlayOneShot(clip);
}
```

**Intermediate:**
```csharp
public IEnumerator FadeInMusic(float duration)
{
    float elapsed = 0;
    while (elapsed < duration)
    {
        musicSource.volume = Mathf.Lerp(0, 0.7f, elapsed / duration);
        elapsed += Time.deltaTime;
        yield return null;
    }
    musicSource.volume = 0.7f;
}
```

**Challenge:**
```csharp
public void PlayFootstep(Vector3 position)
{
    RaycastHit hit;
    if (Physics.Raycast(position, Vector3.down, out hit))
    {
        if (hit.collider.CompareTag("Grass"))
            sfxSource.PlayOneShot(grassFootstep);
        else if (hit.collider.CompareTag("Stone"))
            sfxSource.PlayOneShot(stoneFootstep);
    }
}
```
</details>
