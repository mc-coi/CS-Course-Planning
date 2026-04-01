# Unit 6 - 2D Game Development: Teacher Misconception & Callout Guide

## Overview

This unit applies lessons from Units 1-5 to 2D games, the dominant genre in indie development. Students now understand physics, animation, and design theory—but 2D-specific tools (sprite slicing, tilemaps, sorting layers) are new. The biggest challenge is that 2D seems simpler than 3D (it's not—just different), and students often transfer 3D assumptions incorrectly. For example, they think "2D" means fewer components when it actually means different components (Rigidbody2D, Collider2D, SpriteRenderer instead of Renderer). Tilemaps are powerful but confusing—students don't understand how TilemapCollider2D works and why it's slow. For a year-long course, students can productively experiment with 2D workflows. For a semester course, tilemaps and animation chaining must be pre-taught or template-provided.

---

## Misconceptions by Topic

### Sprites & Import Settings (Days 2–6)

**⚠️ Misconception:** "I imported a PNG image, but it looks blurry in the Game View. The image must be low quality."**

**What it looks like:** A student imports a sprite and it appears pixelated or blurry compared to what they see in the Project panel.

**Why students think this:** They don't understand sprite import settings. The issue is usually filtering or texture compression.

**How to address it:** Check import settings. "Select the sprite → Inspector → Sprite Importer settings. Check: (1) Texture Type = 'Sprite (2D and UI)'. (2) Filter Mode = 'Point (no filter)' for pixel art, or 'Bilinear' for smooth art. (3) Compression = 'None' for crisp graphics. Click 'Apply' and it should look better."

---

**⚠️ Misconception:** "I tried to split a sprite sheet, but the Sprite Editor isn't showing. It's broken."**

**What it looks like:** A student opens the Sprite Editor window and nothing appears.

**Why students think this:** The Sprite Editor requires a sprite asset selected in the Project panel, not the Scene. Also, the sprite must be set to Sprite type.

**How to address it:** Select the sprite correctly. "Click the sprite in the Project panel (not in the scene). In the Inspector, set Sprite Mode = 'Multiple' (for sprite sheets). Click 'Sprite Editor'. The editor window should open. If it's blank, check that the sprite is actually a texture file (.png, .jpg), not a folder."

---

**⚠️ Misconception:** "My sprite sheet is huge and slow. But I need all the frames for animation."**

**What it looks like:** A student imports a 2048x2048 sprite sheet and notices performance issues.

**Why students think this:** Sprite sheets can be large. The issue is usually not size but improper import settings (compression, mipmaps) or not using sprite atlasing.

**How to address it:** Optimize. "Check import settings: (1) Max Size = 2048 or lower (not unlimited). (2) Compression = 'Normal Quality' (not 'None'). (3) Disable Mipmaps if it's a sprite sheet. Also consider splitting large sprite sheets into multiple files (e.g., one for character, one for tiles) and using multiple SpriteRenderer layers."

---

### 2D Physics (Days 20–22)

**⚠️ Misconception:** "I'm using Rigidbody2D and Collider2D, but my 2D character is falling through the floor. The physics must be broken."**

**What it looks like:** A student has a Rigidbody2D character and a static floor collider, but the character clips through.

**Why students think this:** They likely used 3D physics components or configured 2D physics incorrectly.

**How to address it:** Check the setup. "Verify: (1) Character has Rigidbody2D (Body Type = 'Dynamic'). (2) Floor has Collider2D and no Rigidbody2D (or Rigidbody2D with Body Type = 'Static'). (3) Both have Collider2D components (BoxCollider2D, etc.). (4) Project Settings → Physics2D → Gravity = (0, -9.8). If still falling through, increase Rigidbody2D → Constraints → Freeze Rotation Z to prevent spinning."

---

**⚠️ Misconception:** "My 2D character controller from Unit 4 doesn't work in 2D. The physics must be different."**

**What it looks like:** A student copies 3D movement code (using Rigidbody) to a 2D project with Rigidbody2D and nothing works.

**Why students think this:** The component names are similar, but the APIs are slightly different. `rb.velocity` works for both, but some properties don't.

**How to address it:** Teach the differences. "Rigidbody (3D) and Rigidbody2D (2D) are separate components. Use `rb.velocity.x` for horizontal, `rb.velocity.y` for vertical. Use `rb.AddForce()` for forces. Most code transfers directly, but check the API documentation. Also, raycasting uses `Physics2D.Raycast()` (not `Physics.Raycast()`)."

---

### Tilemaps & Level Design (Days 11–14)

**⚠️ Misconception:** "I created a Tilemap and painted some tiles, but nothing appears. The Tilemap must be broken."**

**What it looks like:** A student creates a Tilemap component but doesn't see the painted tiles.

**Why students think this:** They forgot to assign tiles to the palette or the Tilemap is hidden by camera settings or sorting order.

**How to address it:** Troubleshoot. "Check: (1) Tilemap Renderer → Enabled = true. (2) Tile Palette is populated (Window → 2D → Tile Palette). (3) Camera is set to orthographic (for 2D). (4) Sorting Order of Tilemap isn't behind everything else. (5) The Tilemap GameObject isn't hidden in the hierarchy." Test by moving the camera or changing the sorting order.

---

**⚠️ Misconception:** "I created a Tilemap with a TilemapCollider2D, but my character doesn't collide with the tiles. Physics must be broken."**

**What it looks like:** A student adds TilemapCollider2D but the character passes through tiles.

**Why students think this:** TilemapCollider2D is a collider component, so they expect it to work like any collider. But the player also needs a Rigidbody2D.

**How to address it:** Set up collision. "For a tilemap and player to collide: (1) Tilemap has TilemapCollider2D (and no Rigidbody2D, or Rigidbody2D with Body Type = 'Static'). (2) Player has Rigidbody2D (Body Type = 'Dynamic') and Collider2D. (3) Both must be on the same physics layer (check Project Settings → Physics2D → Layer Collision Matrix). Test: add a temporary debug plane and verify the player collides with it."

---

**⚠️ Misconception:** "My tilemap level is large, and the frame rate drops. Tilemaps must be inefficient."**

**What it looks like:** A student builds a large level with a single tilemap and notices lag.

**Why students think this:** TilemapCollider2D can be slow on large tilemaps because it generates a collider for every tile. The solution is to bake it or split into zones.

**How to address it:** Optimize. "Large tilemaps are slow because TilemapCollider2D recalculates colliders every frame. Solutions: (1) Use 'Bake' on TilemapCollider2D to generate a static mesh collider (faster but can't change tiles at runtime). (2) Split the tilemap into smaller chunks (each ~32x32 tiles). (3) Use different TilemapCollider2D for different tile types (decoration vs. solid)."

---

### Animation & Animator (Days 7–10)

**⚠️ Misconception:** "I created animation clips from sprite frames, but they play too fast or too slow. I can't control the speed."**

**What it looks like:** A student imports a sprite sheet, creates animation clips, and they play at the wrong speed.

**Why students think this:** Animation speed is controlled in two places: the clip's Sample Rate and the Animator's speed. Students don't know about both.

**How to address it:** Adjust speed. "Animation speed is set in the clip: select the animation clip → Inspector → Samples Per Second (usually 10 for pixel art, 30 for smooth). Or adjust in code: `animator.speed = 0.5f;` to slow down by half. Or in the Animator window, you can scale the playback speed. If one animation is too fast compared to others, adjust its Samples Per Second."

---

**⚠️ Misconception:** "I have animation transitions set up, but the character gets stuck between animations (e.g., stuck in Jump even after landing)."**

**What it looks like:** A student's Animator state machine has transitions that don't properly change states.

**Why students think this:** The transition conditions are probably wrong, or the code isn't updating the parameters correctly.

**How to address it:** Debug the state machine. "In the Animator window, click 'Show Layers' and enable 'Preview'. Play the game and watch which state the character is in. Add `Debug.Log()` in code to confirm parameters are updating: `anim.SetBool("isGrounded", isGrounded);`. Check if the transition condition matches: if you set `isGrounded = false` but the condition is `isGrounded == true`, the transition won't fire."

---

### Camera & Parallax (Days 15–19)

**⚠️ Misconception:** "I created a parallax background (moving slower than the camera), but it doesn't look right. The layers are at the wrong depths."**

**What it looks like:** A student implements parallax but the effect is subtle or backwards.

**Why students think this:** Parallax speed calculation is wrong, or the camera is moving too fast.

**How to address it:** Implement correctly. "Parallax works by moving background layers slower than the camera. Formula: `background.x = camera.x * (1 - parallaxFactor);` where parallaxFactor = 0.5 (half speed) or 0.2 (one-fifth speed). Or use Cinemachine (Window → Cinemachine → Create Virtual Camera) and add a 'Transposer' with Camera Distance = 10 to create depth. Test: adjust parallaxFactor and see the background move at different speeds."

---

### Sorting Layers & Render Order (Days 2, 12)

**⚠️ Misconception:** "I have multiple sprites but they're rendering in the wrong order. I think the sorting order setting is broken."**

**What it looks like:** A player sprite renders behind a background, or UI renders behind game objects.

**Why students think this:** Sorting order is determined by Sorting Layer first, then Order in Layer. Students forget to set the sorting layer.

**How to address it:** Set sorting correctly. "Every sprite has two sorting settings: (1) Sorting Layer (created in the tag/layer panel). (2) Order in Layer (integer, higher = on top). Create layers like 'Background', 'Terrain', 'Player', 'UI'. Assign each sprite to the right layer. Background < Terrain < Player < UI. Within each layer, use Order in Layer to fine-tune. Test: select a sprite and change its Sorting Layer to 'UI'—it should jump to the front."

---

## Whole-Class Warning Signs

- **Everyone's sprite looks blurry or wrong.** They didn't set import settings. Show them how to open Sprite Importer settings and set Filter Mode to 'Point' for pixel art.

- **Nobody can figure out TilemapCollider2D.** It's complex. Provide a template with a working tilemap and collider pre-configured, then have them paint tiles into it.

- **Animations play at inconsistent speeds.** They created clips with different Sample Rates. Make a rule: all character clips use 10 FPS for pixel art, all UI clips use 30 FPS.

- **Character is falling through slopes.** Ground detection (raycast) works on flat ground but not slopes. Show them how to use multiple raycasts or OverlapCircle.

- **Parallax scrolling isn't working at all.** They hardcoded camera position instead of making parallax layers follow. Provide a script template with the parallax formula.

---

## Questions That Reveal Understanding

1. **"You have a sprite sheet with 16 frames of animation. What's the first step to use it in a game?"**
   - Good answer: "Import the sprite in the Project. Select it → Inspector → Sprite Mode = 'Multiple'. Open Sprite Editor, slice the sprite sheet into individual frames. Create an animation clip from the slices."
   - Red flag: "Drag it into the scene" or "Edit it in Photoshop." (They're skipping the slicing step.)

2. **"Explain the difference between Sorting Layer and Order in Layer."**
   - Good answer: "Sorting Layer is the primary sort (Background, Terrain, Player, UI). Order in Layer sorts within that layer. An object on the 'UI' layer always renders on top of 'Player', regardless of Order in Layer."
   - Red flag: "They're the same thing" or "One is for sprites, one is for 3D." (Not understanding the hierarchy.)

3. **"Why does your tilemap level cause frame rate drops, and how would you fix it?"**
   - Good answer: "TilemapCollider2D is slow on large maps. Fix: bake it, split into chunks, or use a different collider type. Baking turns the collider into a static mesh (faster but can't change tiles)."
   - Red flag: "Use a different tilemap tool" or "Reduce texture size." (Not addressing the root cause.)

4. **"Your parallax scrolling doesn't look right. The background isn't moving. What's wrong?"**
   - Good answer: "The parallax formula might be wrong, or the background layer isn't moving at all. Check: `background.position = camera.position * parallaxFactor;`. If parallaxFactor = 1, it moves with the camera (no parallax). Use 0.5 or lower."
   - Red flag: "The layers are in the wrong order." (Sorting doesn't control parallax effect.)

---

## Common Student Questions & How to Answer Them

**Q1: "I imported a sprite, but it has a big transparent border. How do I remove it?"**

*A:* "Use the Sprite Editor to crop it. Select the sprite → Sprite Editor → the image displays. Click 'Crop' button (or manually drag the borders). The transparent areas are removed. Click 'Apply'. This saves space in the atlas and makes animations cleaner."

---

**Q2: "My animation looks choppy. I want smoother animation."**

*A:* "Increase the Samples Per Second in the animation clip. Pixel art typically uses 10 FPS (animated frames). Smoother art uses 24-30 FPS. Select the clip → Inspector → Samples Per Second. Also, add more frames to your animation (each frame lasts longer at lower FPS)."

---

**Q3: "How do I make a tile that's not solid (e.g., a decoration that doesn't block movement)?"**

*A:* "Create two tilemaps: one for solid tiles (with TilemapCollider2D), one for decoration (no collider). Or, use tiles with isTrigger colliders for special tiles. Or, exclude decoration tiles from the collision matrix (Physics2D → Layer Collision Matrix)."

---

**Q4: "I want a parallax background that scrolls horizontally when the player moves. How?"**

*A:* "Create a background sprite with `Position.x = camera.position.x * 0.5f;` (half speed). Or for multiple layers:
```csharp
bg1.position.x = camera.position.x * 0.3f;
bg2.position.x = camera.position.x * 0.6f;
```
Layers with lower parallax factors move slower, creating depth."

---

**Q5: "My character animation transitions are jittery. How do I smooth them?"**

*A:* "In the Animator window, select the transition arrow. Set 'Transition Duration' to something > 0 (e.g., 0.15). This blends between animations instead of snapping. Also, check 'Has Exit Time' if you want the animation to finish before transitioning."

---

## Analogies That Work

1. **"A sprite sheet is like a deck of cards. Each card is a frame. The Sprite Editor cuts the deck into individual cards. Animation plays the cards in order, creating motion—like a flipbook."**
   - This makes sprite slicing and animation intuitive.

2. **"Sorting Layers are like books on a shelf. Each book is a layer. Order in Layer is the position within each book. Books on the 'UI' shelf always appear in front of books on the 'Player' shelf, no matter the position within their shelf."**
   - This clarifies the two-level sorting system.

3. **"Parallax scrolling is like looking out a car window. The close trees move fast (Parallax Factor = 0.9). Far mountains move slow (Parallax Factor = 0.2). This creates the illusion of depth."**
   - This makes parallax feel natural.

---

## Unity-Specific Gotchas

- **Sprite Pivot affects animation alignment.** If pivot is at the bottom, the sprite is anchored at the feet. Top pivot anchors at the head. Inconsistent pivots make animations jerky. Keep all frames of an animation with the same pivot.

- **TilemapCollider2D with Rigidbody2D must have Body Type = 'Static'.** If you set Body Type = 'Dynamic', the entire tilemap becomes a physics object (and falls). Use Static for static terrain.

- **Orthographic camera has a fixed view size regardless of screen aspect ratio.** This can cause pillarboxing (black bars). Use the Canvas scale mode "Scale with Screen Size" for UI or adjust the camera's orthographic size based on screen aspect.

- **Sprites have a Pixels Per Unit setting that affects their visual size.** A sprite with PPU = 100 is 100 pixels per unit in world space. PPU = 16 (common for pixel art) means a 16-pixel sprite is 1 unit. Inconsistent PPU across sprites makes them render at different scales.

- **2D lighting requires the sprite's material to support it.** By default, sprites use the 'Sprite' material which doesn't respond to lights. Use 'Sprite Lit' material to add lighting.

- **Cinemachine Virtual Cameras are powerful but add complexity.** For simple camera follow, just update the camera position in script. Cinemachine is great for advanced effects (deadzone, look-ahead, damping).

---

## Year-Long Differentiators

For year-long courses:
- Let students build a full level with all components (sprites, tiles, animation, physics, parallax, camera). This is Unit 6's capstone and sets them up for Units 7 and 8.
- Introduce optimizations late (sprite atlasing, batching, profiling). Focus first on correctness, then performance.
- Have them refactor 3D code to 2D. This reinforces the difference between Rigidbody/Rigidbody2D and builds flexibility.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
