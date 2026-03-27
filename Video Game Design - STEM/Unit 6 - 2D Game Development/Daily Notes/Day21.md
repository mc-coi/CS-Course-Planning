# Day 21: Sprite Renderer & Tilemaps

**Learning Target:** Import and display 2D sprites, organize them with sorting orders, and build efficient levels using Tilemaps.

### Key Concepts

- **Sprite:** A 2D image used in 2D games
- **Sprite Renderer:** Component that displays a sprite on a GameObject
- **Texture Import Settings:** Determines how a sprite is processed (pixel perfect, compression, etc.)
- **Sorting Order:** Z-order of sprites (higher = in front)
- **Tilemap:** A grid of sprites used to build levels
- **Tile Palette:** A set of tiles available for painting
- **Tile:** Individual sprite in a tilemap
- **Isometric vs. Orthographic:** Different 2D perspectives

### Content

Sprites are the foundation of 2D games. A Sprite Renderer displays a sprite on any GameObject.

**Setting Up Sprites:**
1. Import an image (PNG or JPG)
2. In the Inspector, set Texture Type to "Sprite (2D and UI)"
3. Click "Apply"
4. Drag the sprite onto a GameObject
5. A Sprite Renderer component is created automatically

**Sorting Order:**
When multiple sprites overlap, the one with higher Sorting Order appears in front.
- Background = 0
- Player = 5
- UI = 10

Organize your project with a consistent sorting order system.

**Tilemaps:**
Tilemaps are efficient for level design. Instead of placing 100 individual sprites, paint tiles on a grid.

**Creating a Tilemap:**
1. Right-click Hierarchy > 2D Object > Tilemap
2. In the Tile Palette, select a tile
3. Paint on the tilemap with the brush
4. Use the eraser to remove tiles

### Code Examples

```csharp
using UnityEngine;

public class SpriteManager : MonoBehaviour
{
    // Reference to the Sprite Renderer
    public SpriteRenderer spriteRenderer;
    public Sprite[] spriteFrames;  // Array of sprite images

    // Current sprite index for animation
    private int currentFrameIndex = 0;

    void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();

        // Set initial sprite
        spriteRenderer.sprite = spriteFrames[0];

        // Set sorting order
        spriteRenderer.sortingOrder = 5;  // Player layer
    }

    // Switch to a different sprite
    public void SetSprite(int frameIndex)
    {
        if (frameIndex >= 0 && frameIndex < spriteFrames.Length)
        {
            spriteRenderer.sprite = spriteFrames[frameIndex];
            currentFrameIndex = frameIndex;
        }
    }

    // Flip sprite horizontally
    public void FlipSprite(bool faceRight)
    {
        spriteRenderer.flipX = !faceRight;
    }

    // Change sprite color (useful for hit feedback)
    public void SetSpriteColor(Color newColor)
    {
        spriteRenderer.color = newColor;
    }

    // Example: Flash white when taking damage
    public void DamageFlash()
    {
        spriteRenderer.color = Color.white;
        Invoke("ResetColor", 0.1f);
    }

    void ResetColor()
    {
        spriteRenderer.color = Color.white;  // or new Color(1, 1, 1, 1) for fully opaque white
    }
}

// Tilemap usage example
public class TilemapBuilder : MonoBehaviour
{
    // Tilemaps are created via the editor, not in code
    // But you can reference and modify them programmatically:

    public Tilemap tilemap;
    public TileBase emptyTile;

    void Start()
    {
        // Clear a tile at position
        tilemap.SetTile(new Vector3Int(5, 5, 0), null);
    }

    // Detect if there's a tile at a position
    public bool HasTileAt(Vector3Int gridPosition)
    {
        TileBase tile = tilemap.GetTile(gridPosition);
        return tile != null;
    }
}
```

### Guided Practice

**Activity:** Create a simple 2D scene with layered sprites

1. Create a new 2D scene
2. Import or create 3 simple sprite images (background, character, foreground)
3. Create 3 GameObjects with Sprite Renderers
4. Assign different sorting orders (Background: 0, Character: 5, Foreground: 10)
5. Verify the layering is correct when they overlap

### Practice Problems

**Problem 1 — Beginner:** Import a sprite image and display it using Sprite Renderer. Change its sorting order and color.

**Problem 2 — Intermediate:** Create a simple 2D platformer level using Tilemaps. Include platforms and a player spawning area.

**Problem 3 — Challenge:** Create a scene with 5 different sprite layers (sky, background, platforms, player, UI) each with appropriate sorting orders.

<details>
<summary>Hints</summary>

**Problem 1:** Import PNG, set Texture Type to "Sprite". Drag onto GameObject. Access SpriteRenderer in Inspector or script.

**Problem 2:** Create a Tilemap. Create a Tile Palette. Paint tiles on the grid. Position a player GameObject on the platform.

**Problem 3:** Create multiple GameObjects with SpriteRenderers. Set each to a different sorting order. Make sure they layer correctly when they overlap.

</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
using UnityEngine;

public class SpriteDisplay : MonoBehaviour
{
    void Start()
    {
        SpriteRenderer sr = GetComponent<SpriteRenderer>();
        sr.sortingOrder = 5;
        sr.color = new Color(1, 0.5f, 0);  // Orange
    }
}
```

**Problem 2:**
This is a visual design task. Create a Tilemap, paint platforms, add ground, add platforms at varying heights.

**Problem 3:**
Create 5 GameObjects with SpriteRenderers:
- Sky (sortingOrder = 0)
- Background (sortingOrder = 1)
- Platforms (sortingOrder = 2)
- Player (sortingOrder = 5)
- UI/Effects (sortingOrder = 10)

</details>
