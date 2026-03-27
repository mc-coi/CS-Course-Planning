# Day 5: Unity Canvas System Fundamentals

**Learning Target:** I can set up a Canvas and position UI elements using RectTransform.

---

## Key Concepts

**Canvas**: A plane where all UI is drawn. Every UI element must be a child of the Canvas.

**Canvas Render Mode**:
- **Screen Space - Overlay**: UI appears on top of everything (most common for menus)
- **Screen Space - Camera**: UI rendered to a camera texture (for 3D scenes)
- **World Space**: UI exists in the 3D world (for in-game labels)

**RectTransform** (not Transform): Controls UI position, size, and anchor.
- **Anchor**: What point on the screen does this element's position reference? (top-left, center, bottom-right, stretch, etc.)
- **Pivot**: Which point on the element itself is the "origin"?
- **Pos X/Y**: Position relative to the anchor
- **Width/Height**: Size in pixels

**Aspect Ratio Fitter**: Automatically scales elements to maintain proportions on different screen sizes.

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;

public class CanvasSetup : MonoBehaviour
{
    public void SetupBasicUI()
    {
        // In code, you rarely create UI from scratch
        // But you might adjust it at runtime:
        
        RectTransform rect = GetComponent<RectTransform>();
        
        // Center this element on screen
        rect.anchorMin = Vector2.one * 0.5f;  // Anchor to center
        rect.anchorMax = Vector2.one * 0.5f;  // Same center
        rect.pivot = Vector2.one * 0.5f;      // Pivot at center
        rect.offsetMin = new Vector2(-50, -50);  // 50 pixels in each direction
        rect.offsetMax = new Vector2(50, 50);    // Creates 100x100 element
    }
}
```

---

## Unity Setup Steps

1. **Create Canvas**:
   - Right-click Hierarchy → UI → Canvas (built-in)
   - This creates a Canvas with a GraphicsRaycaster component
   
2. **Inspect Canvas**:
   - Canvas Scaler: Set to "Scale with Screen Size" (responsive design)
   - Reference Resolution: 1920x1080

3. **Add a Panel to Canvas**:
   - Right-click Canvas → UI → Panel - ImageTarget
   - In Inspector, set:
     - Anchors: Top, Left (or use preset button)
     - Pos X: 100, Pos Y: -100
     - Width: 200, Height: 100

4. **Add a Button to Panel**:
   - Right-click Panel → UI → Button
   - Observe how it's positioned relative to the parent

5. **Preview different screen sizes**:
   - In Game view, change aspect ratio dropdown
   - Does layout hold? Adjust anchors as needed

---

## Guided Practice

1. **Create a Title Screen Layout**:
   - Canvas with black background
   - Title text (centered, large)
   - Three buttons below it (New Game, Load, Quit)
   - Use anchors to keep everything centered

2. **Anchor Practice**:
   - Create 4 panels, each anchored to a corner (top-left, top-right, bottom-left, bottom-right)
   - Resize the Game view—each should stay in its corner

3. **Responsive Layout**:
   - Create a panel that always takes up 80% of screen width, centered
   - Use Anchor preset "Stretch → Horizontal" and adjust offset

---

## Practice Problems

**Beginner:**
What's the difference between Canvas Anchor and RectTransform Pivot?

**Intermediate:**
You have a button at position (0, 0). Its anchor is set to top-left. Now you change the anchor to center. Where does the button appear?

**Challenge:**
Design a responsive health bar that sticks to the top-left, is 300 pixels wide, and maintains 16:9 aspect ratio. Write the RectTransform settings.

<details><summary>💡 Hints</summary>
- Beginner: Anchor is "where on the screen," Pivot is "which part of the element points to that spot"
- Intermediate: The position stays the same in space, but relative to the new anchor point, the element moves
- Challenge: Use Anchor Preset (Stretch → Horizontal), then apply AspectRatioFitter
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:** Anchor is the reference point on the screen (top-left corner, center, etc.). Pivot is which part of the element points to the anchor. If anchor is at (0,0) and pivot is (0,0), the top-left of the element is at screen top-left. If pivot is (0.5, 0.5), the center of the element is at screen top-left.

**Intermediate:** It stays at (0, 0), but now relative to the screen center instead of top-left. The button appears in the center-left area of screen.

**Challenge:**
- Anchor Preset: Top-Left
- Pos X: 10, Pos Y: -10 (10px inset from corner)
- Width: 300, Height: 169 (300 * 9/16)
- Add Aspect Ratio Fitter with 16:9 ratio
</details>
