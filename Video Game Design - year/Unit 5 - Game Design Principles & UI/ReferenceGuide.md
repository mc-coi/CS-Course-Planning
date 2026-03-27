# Unit 5 Reference Guide: Game Design Principles & UI

## Game Design Theory

### MDA Framework
- **Mechanics**: Rules and systems (jump height, damage formula)
- **Dynamics**: Emergent player behavior (learning to timing jumps)
- **Aesthetics**: Emotional experience (fun, tension, accomplishment)

Key insight: Designers control mechanics; players experience aesthetics through dynamics.

### Flow State (Csikszentmihalyi)
- **Sweet spot**: Challenge matches skill level
- **Too easy**: Boredom
- **Too hard**: Frustration
- **Perfect**: Flow = focus, satisfaction, engagement

### Level Design Loop
1. **Safe Zone**: Learn mechanic without consequence
2. **Challenge Zone**: Apply mechanic under pressure
3. **Reward Zone**: Victory, next level, story reveal

### Player Motivation (Bartle)
- **Achievers**: Goals, high scores, progression
- **Explorers**: Secrets, discovery, world knowledge
- **Socializers**: Cooperation, community, sharing
- **Killers**: Competition, dominance, skill display

---

## Canvas & UI Setup

### Canvas Render Modes

| Mode | Use Case | Parent |
|------|----------|--------|
| Screen Space - Overlay | Menus, HUD | Direct to Canvas |
| Screen Space - Camera | In-world UI | Camera plane |
| World Space | In-game labels | World GameObject |

### Canvas Scaler Settings
- **Scale with Screen Size**: Best for responsive design
- **Reference Resolution**: 1920x1080 (or your target)
- **Screen Match Mode**: Match Width or Height

### RectTransform Properties

| Property | Purpose |
|----------|---------|
| Anchor | Reference point on screen (top-left, center, stretch, etc.) |
| Pivot | Which point of element points to anchor |
| Offset Min/Max | Distance from anchor |
| Pos X/Y | Position relative to anchor |
| Width/Height | Size in pixels |

**Anchor Presets**: Use built-in presets for quick layout
- Top Left, Top Center, Top Right
- Middle Left, Center, Middle Right
- Bottom Left, Bottom Center, Bottom Right
- Stretch (horizontal, vertical, both)

---

## TextMeshPro

### Import & Setup
- First use: Window → TextMeshPro → Import TMP Essentials
- Create text: UI → Text - TextMeshPro

### Key Components
- **Font**: TMP_FontAsset (LiberationSans default)
- **Size**: Point size (36 = large text)
- **Alignment**: Left, Center, Right, Justified
- **Color**: Text color
- **Wrapping**: Enables word wrap

### Rich Text Tags
| Tag | Effect |
|-----|--------|
| `<b>text</b>` | Bold |
| `<i>text</i>` | Italic |
| `<color=red>text</color>` | Red color |
| `<size=50>text</size>` | 50pt font |
| `<sprite=0>` | Emoji/icon |

### C# Code Example
```csharp
using TMPro;
TextMeshProUGUI text = GetComponent<TextMeshProUGUI>();
text.text = $"Score: {score}";
text.text = "<color=gold><b>Victory!</b></color>";
```

---

## Button Component

### Inspector Setup
1. **Button** component
   - Interactable: Enable/disable button
   - Navigation: Automatic (keyboard nav)
   - Colors: Normal, Highlighted, Pressed, Disabled
   - On Click (): Events to trigger

2. **Two methods to hook buttons**:
   - **Inspector**: Drag object → select method
   - **Code**: `button.onClick.AddListener(Method)`

### Button States
| State | Appearance |
|-------|-----------|
| Normal | Default color |
| Highlighted | Hover color (keyboard/mouse over) |
| Pressed | Click color |
| Disabled | Grayed out, non-interactive |

---

## Slider Component

### Properties
| Property | Purpose |
|----------|---------|
| Min Value | Minimum value (e.g., 0) |
| Max Value | Maximum value (e.g., 100) |
| Value | Current value |
| Whole Numbers | Only integers |
| Fill Rect | Image that represents fill |
| Handle | Draggable element |

### Setup Steps
1. Create Slider: UI → Slider
2. Set Min: 0, Max: 100
3. Set Interactable: False (for display-only bars)
4. Configure fill color
5. Attach script to update value: `slider.value = health`

---

## AudioSource & Audio Manager

### AudioSource Properties
| Property | Range | Purpose |
|----------|-------|---------|
| Volume | 0-1 | Loudness |
| Pitch | -3 to 3 | Speed (1 = normal) |
| Pan | -1 to 1 | Left/right speaker |
| Loop | Bool | Repeat after finish |
| Clip | AudioClip | Sound file |

### Playing Audio
```csharp
// Play from start (stops previous)
audioSource.Play();

// Play once, overlaps with current
audioSource.PlayOneShot(clip, volume);

// Stop immediately
audioSource.Stop();

// Pause (can resume)
audioSource.Pause();
```

### Singleton Audio Manager Pattern
```csharp
public static AudioManager instance;

void Awake()
{
    if (instance != null) Destroy(gameObject);
    else {
        instance = this;
        DontDestroyOnLoad(gameObject); // Persists between scenes
    }
}

public static void PlaySFX(AudioClip clip)
{
    instance.sfxSource.PlayOneShot(clip);
}
```

---

## PlayerPrefs (Save/Load)

### Methods
```csharp
// Save
PlayerPrefs.SetInt("HighScore", 1000);
PlayerPrefs.SetFloat("Volume", 0.8f);
PlayerPrefs.SetString("PlayerName", "Hero");

// Load (with default value)
int highScore = PlayerPrefs.GetInt("HighScore", 0);
float volume = PlayerPrefs.GetFloat("Volume", 1f);
string name = PlayerPrefs.GetString("PlayerName", "Player");

// Delete
PlayerPrefs.DeleteKey("HighScore");
PlayerPrefs.DeleteAll();

// Force save to disk (optional, auto-saves on quit)
PlayerPrefs.Save();
```

### Limitations
- Only int, float, string (no arrays, objects)
- Platform-specific storage location
- For complex data, use JSON serialization instead

---

## Time Control

### Time.timeScale
```csharp
Time.timeScale = 1f;  // Normal speed
Time.timeScale = 0.5f;  // Half speed
Time.timeScale = 0f;  // PAUSED

// Important: Time.deltaTime is affected by timeScale
// Use Time.unscaledDeltaTime for pause menu animations
```

### When to Use timeScale
- Pause menu (set to 0)
- Slow-motion effects (0.25)
- Speedup (1.5)

---

## Particle System Quick Reference

### Key Components
| Property | Effect |
|----------|--------|
| Duration | How long particles emit |
| Start Lifetime | How long each particle lives |
| Max Particles | Upper limit |
| Start Speed | Emission velocity |
| Start Color | Initial color (with fade) |
| Gravity Modifier | Gravity effect |
| Emission Rate | Particles per second |

### Common Effects
- **Hit**: Red, fast, short life, explosive spread
- **Pickup**: Gold, upward, medium speed, fade
- **Explosion**: Orange/smoke, large radius, outward

---

## Game Feel Checklist

- [ ] Sound on every action
- [ ] Visual feedback (color change, flash, animation)
- [ ] Screen shake on impact
- [ ] Particle effects for rewards/hits
- [ ] Smooth transitions between states
- [ ] Button hover effects
- [ ] Loading/waiting feedback
- [ ] Success/failure audio cues
