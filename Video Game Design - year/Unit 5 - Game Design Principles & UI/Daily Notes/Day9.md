# Day 9: Health Bars & Sliders

**Learning Target:** I can create and update a health bar using the Slider component.

---

## Key Concepts

**Slider Component**: Visual representation of a value between min and max.
- **Value**: Current health (0-100)
- **Min Value / Max Value**: Range
- **Direction**: Horizontal or vertical fill
- **On Value Changed**: Event fired when value changes

**Fill-based Health Bar**: Slider's fill image represents remaining health visually.

**Color Transitions**: Health bar changes color as player takes damage (green → yellow → red).

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;

public class HealthBar : MonoBehaviour
{
    public Slider healthSlider;
    public Image fillImage;
    private float maxHealth = 100f;
    private float currentHealth;

    private void Start()
    {
        currentHealth = maxHealth;
        healthSlider.maxValue = maxHealth;
        healthSlider.value = currentHealth;
        healthSlider.onValueChanged.AddListener(OnHealthChanged);
    }

    public void TakeDamage(float damage)
    {
        currentHealth -= damage;
        currentHealth = Mathf.Max(0, currentHealth);
        healthSlider.value = currentHealth;
    }

    private void OnHealthChanged(float newHealth)
    {
        // Change color based on health percentage
        float healthPercent = newHealth / maxHealth;
        
        if (healthPercent > 0.5f)
            fillImage.color = Color.green;
        else if (healthPercent > 0.25f)
            fillImage.color = Color.yellow;
        else
            fillImage.color = Color.red;
    }
}
```

---

## Unity Setup Steps

1. **Create Slider**:
   - Right-click Canvas → UI → Slider - Horizontal
   - This creates Slider with Background, Fill, and Handle

2. **Configure Slider**:
   - Slider component:
     - Min Value: 0
     - Max Value: 100
     - Value: 100
     - Interactable: FALSE (so player can't drag it)
   
3. **Style the Fill**:
   - Find "Fill" child of Slider
   - Select Image component
   - Color: Green

4. **Position it**:
   - Top-left corner, 300 pixels wide
   - RectTransform → Anchor Preset: Top, Left
   - Pos: 10, -10

5. **Attach Script**:
   - Create `HealthBar.cs`
   - In Inspector, assign the Slider reference

---

## Guided Practice

1. **Create a Working Health Bar**:
   - Build the UI as described above
   - Attach HealthBar script
   - In Play mode, press Space to deal 10 damage
   - Verify bar drains and changes color

2. **Add Damage Animation**:
   - When damage is taken, shake the health bar slightly
   - Use `Vector3.Lerp()` to smooth the color transition

3. **Add Healing**:
   - Add a Heal() method that increases health
   - Cap it at maxHealth

---

## Practice Problems

**Beginner:**
Create a script that displays both the slider AND a text label (e.g., "Health: 75/100").

**Intermediate:**
Create multiple sliders: Health, Stamina, Mana. Each has different colors and behaviors.

**Challenge:**
Create a boss health bar that shows above the enemy's head in world space, always facing the camera.

<details><summary>💡 Hints</summary>
- Beginner: Get TextMeshProUGUI reference, update `.text` whenever health changes
- Intermediate: Each slider needs its own script or shared data model
- Challenge: Use Canvas render mode "World Space" or billboard the camera-facing text
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
public TextMeshProUGUI healthLabel;

private void OnHealthChanged(float newHealth)
{
    healthLabel.text = $"Health: {newHealth}/{maxHealth}";
}
```

**Intermediate:**
```csharp
public Slider healthSlider, staminaSlider, manaSlider;
public float health = 100, stamina = 100, mana = 100;

void Update()
{
    healthSlider.value = health;
    staminaSlider.value = stamina;
    manaSlider.value = mana;
}
```

**Challenge:**
```csharp
// Use Canvas with Render Mode = World Space
// Position the health bar at: enemyTransform.position + Vector3.up * 2
// Parent to the enemy so it moves with them
```
</details>
