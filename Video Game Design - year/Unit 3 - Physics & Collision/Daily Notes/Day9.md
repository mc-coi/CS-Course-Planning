# Day 9: Physics Layers & Layer Mask Setup

**Learning Target:** I can use physics layers to control which objects collide with which other objects.

---

## Key Concepts

**Physics Layer** — A way to group GameObjects (found in Inspector → Layer dropdown). Default layers: Default, TransparentFX, Ignore Raycast, Water, UI, etc.

**Layer Collision Matrix** — Edit → Project Settings → Physics → Layer Collision Matrix. Shows which layers collide with each other.

**LayerMask** — A bitmask representing which layers to interact with. Used in Physics.Raycast, Physics.OverlapSphere, etc.

**Use cases:**
- Enemy A doesn't collide with Enemy B (same team)
- Player only collides with walls, not with coins (coins are triggers)
- Bullets pass through allies but hit enemies

**Real-world examples:**
- **Team-based games:** Red team vs Blue team—use separate layers so teammates don't block each other
- **Portal 2:** Portals only affect certain objects, not walls
- **Zelda:** Bombs explode trigger zones but don't collide with certain walls

---

## Code Example

```csharp
using UnityEngine;

public class LayerMaskExample : MonoBehaviour
{
    // In Inspector, you can select layers from dropdown
    public LayerMask enemyLayer;
    public LayerMask wallLayer;

    private void Start()
    {
        // Set this object's layer
        gameObject.layer = LayerMask.NameToLayer("Player");

        // Check if another object is on a specific layer
        if (((1 << other.gameObject.layer) & enemyLayer) != 0)
        {
            Debug.Log("Other object is on enemy layer!");
        }
    }

    private void OnTriggerEnter(Collider other)
    {
        // Only react to objects on specific layers
        if (((1 << other.gameObject.layer) & enemyLayer) != 0)
        {
            Debug.Log("Hit an enemy!");
        }
    }
}
```

---

## Unity Setup Steps

1. **Create custom layers:** Edit → Project Settings → Physics → Layers tab
   - New layer "Enemy"
   - New layer "Ally"
   - New layer "Player"
   - New layer "Coin"

2. **Assign layers to objects:**
   - Select Player cube → Inspector → Layer dropdown → "Player"
   - Select Enemy cube → Layer dropdown → "Enemy"
   - Select Coin sphere → Layer dropdown → "Coin"

3. **Set Layer Collision Matrix:** Edit → Project Settings → Physics
   - Uncheck "Enemy" vs "Enemy" (enemies don't hit each other)
   - Uncheck "Player" vs "Coin" (coins don't block player)
   - Keep "Player" vs "Enemy" checked

4. **Press Play and test:** Enemies pass through each other, player passes through coins

---

## Guided Practice

1. Create Player, 3 Enemies, 5 Coins
2. Assign appropriate layers to each
3. Configure collision matrix so:
   - Enemies don't collide with each other
   - Coins don't collide with player (make coins triggers or use layers)
   - Player collides with enemies
4. Test: Enemies should pass through each other but stop player

---

## Practice Problems

**Beginner:** Create three layers: Player, Enemy, Wall. Configure collision matrix so enemies and walls collide, but enemies don't collide with each other.

**Intermediate:** Build a game with two teams (Red and Blue). Teammates pass through each other, but collide with enemies and walls.

**Challenge:** Create a "radar" system that only detects enemies on a specific layer within a certain radius. Use Physics.OverlapSphere with a LayerMask.

<details><summary>💡 Hints</summary>
- Layers are created in Project Settings, not in the scene
- `LayerMask.NameToLayer("LayerName")` converts string to layer number
- `1 << layer` creates a bitmask for a single layer
- Use bitwise AND (&) to check if object is on a specific layer
</details>

<details><summary>✅ Sample Answers</summary>

```csharp
// Challenge: Radar system
public class Radar : MonoBehaviour
{
    public LayerMask enemyLayer;
    public float radarRadius = 10f;

    private void Update()
    {
        Collider[] enemies = Physics.OverlapSphere(transform.position, radarRadius, enemyLayer);
        
        Debug.Log("Enemies in range: " + enemies.Length);
        
        foreach (Collider enemy in enemies)
        {
            Debug.Log("Found enemy: " + enemy.gameObject.name);
        }
    }

    private void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position, radarRadius);
    }
}
```

</details>
