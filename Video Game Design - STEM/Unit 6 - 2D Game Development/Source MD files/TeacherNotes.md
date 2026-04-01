# Unit 6 - 2D Game Development: Teacher Misconception & Callout Guide

## Overview

This unit applies everything from Units 1–5 to 2D games using Unity's 2D-specific tools: Rigidbody2D, Collider2D, Tilemaps, the Sprite Editor, and the Animator. In a STEM semester course, students often assume "2D is simpler than 3D"—it isn't, just different. The most common pitfalls are sprite import settings (blurry pixel art, wrong filtering), TilemapCollider2D not working because the player has no Rigidbody2D, and 3D physics code that breaks when dropped into a 2D project. Unlike the year-long course, provide a pre-configured 2D scene with working physics and let students paint tiles and add their logic on top. Use 🚨 flags to know when to stop.

---

## Misconceptions by Topic

### Sprites & Import Settings (Days 1–3)

**⚠️ Misconception:** "I imported a PNG sprite and it looks blurry. The asset must be low quality."

**What it looks like:** A student imports a pixel art sprite and it renders blurry in the Game view. The image looks fine in the Project panel but is blurry on screen.

**Why students think this:** They don't know about sprite import settings. Unity's default filter mode (Bilinear) blurs low-resolution pixel art.

**How to address it:** Set Filter Mode to Point. "Select the sprite in the Project panel → Inspector → Filter Mode = 'Point (no filter)'. Click Apply. Point filtering renders each pixel as a sharp square—correct for pixel art. Bilinear smooths pixels together—correct for high-res art or photos. Also check Compression = 'None' for crisp art."

🚨 **STEM Priority — STOP THE CLASS:** Demo this before anyone imports sprites. Every student will hit it, and once they see the fix, they'll remember it.

---

**⚠️ Misconception:** "I need to split my sprite sheet into frames for animation. I drag the image in—now what?"

**What it looks like:** A student imports a sprite sheet but doesn't know how to slice it into individual frames.

**Why students think this:** The Sprite Editor is not discoverable—it's hidden behind import settings.

**How to address it:** Walk through slicing. "Select the sprite in Project panel → Inspector → Sprite Mode = 'Multiple' → Click Apply → Click 'Sprite Editor'. In the Sprite Editor: (1) Click Slice → Type = 'Grid By Cell Count' or 'Grid By Cell Size'. (2) Set the cell count or size to match your sprite sheet (e.g., 4 columns × 2 rows). (3) Click Slice → Apply. The sheet is now split into individual frames you can drag into the Animator."

🚨 **STEM Priority — Handle 1-on-1:** Sprite slicing is mechanical and fast once seen. Walk the first student through it; others can follow the same steps.

---

**⚠️ Misconception:** "My sprite sheet is 2048×2048 and my game slows down when I add more sprites."

**What it looks like:** A student uses large uncompressed sprite sheets and the project's memory and frame rate drop.

**Why students think this:** Larger files look higher quality. They don't understand GPU texture memory.

**How to address it:** Optimize import settings. "Large sprite sheets use GPU memory proportional to pixel count, not file size. A 2048×2048 RGBA texture = 16MB in GPU memory regardless of the PNG's compressed size. Solutions: (1) Reduce Max Texture Size in Import Settings to 1024 or 512. (2) Set Compression = 'Normal Quality'. (3) Disable Generate Mip Maps for 2D sprites (Mip Maps are for 3D). (4) Use multiple smaller sheets instead of one giant one."

---

### 2D Physics: Rigidbody2D & Collider2D (Days 3–5)

**⚠️ Misconception:** "I copied my 3D movement script to a 2D project and nothing works. Physics must be different."

**What it looks like:** A student has a working 3D controller with Rigidbody and copies it to a 2D project. The script references Rigidbody and Vector3, which are wrong for 2D.

**Why students think this:** Component names look similar. Rigidbody vs. Rigidbody2D, Collider vs. Collider2D.

**How to address it:** Teach the 2D equivalents. "2D and 3D physics are separate systems. Swap: Rigidbody → Rigidbody2D. Vector3 → Vector2 for movement. Physics.Raycast() → Physics2D.Raycast(). Most of the logic is identical—just different types. The method name for velocity is the same: `rb.velocity`, but it's now a Vector2: `rb.velocity = new Vector2(speed, rb.velocity.y);`."

🚨 **STEM Priority — STOP THE CLASS:** If students are pasting 3D scripts into 2D projects, stop and explain the 2D equivalents before they spend 30 minutes debugging type mismatches.

```csharp
// 3D → 2D conversion
Rigidbody rb;            →    Rigidbody2D rb;
rb.velocity = new Vector3(...)  →  rb.velocity = new Vector2(...)
Physics.Raycast(...)     →    Physics2D.Raycast(...)
OnCollisionEnter(...)    →    OnCollisionEnter2D(...)
OnTriggerEnter(...)      →    OnTriggerEnter2D(...)
```

---

**⚠️ Misconception:** "My 2D player falls through the floor. Both objects have Collider2D components."

**What it looks like:** A student has a BoxCollider2D on the player and the floor, but the player falls through.

**Why students think this:** They don't know the player also needs a Rigidbody2D for collisions to resolve.

**How to address it:** Add Rigidbody2D. "For 2D physics: player needs Rigidbody2D (Body Type = Dynamic) AND a Collider2D. Floor needs a Collider2D (no Rigidbody2D, or Body Type = Static). Without Rigidbody2D on the player, Unity won't simulate movement or resolve collisions. Add Rigidbody2D → Body Type = Dynamic → Gravity Scale = 1."

---

**⚠️ Misconception:** "My tilemap has a TilemapCollider2D but the player walks right through the tiles."

**What it looks like:** A student adds TilemapCollider2D to their tilemap but the character doesn't collide with it.

**Why students think this:** They think the collider alone handles collision. But the character (not the tilemap) needs Rigidbody2D for collision resolution.

**How to address it:** Check the character setup. "Collision works between a Rigidbody2D (dynamic) and a Collider2D (static). The tilemap's TilemapCollider2D is static—correct. The player needs Rigidbody2D (Dynamic) + Collider2D. If both are present but still falling through, check: (1) Layer Collision Matrix—are both layers set to collide? (2) TilemapCollider2D → Is Trigger = false. (3) Player's Rigidbody2D → Collision Detection = Continuous for fast movement."

---

### Tilemaps & Level Design (Days 4–6)

**⚠️ Misconception:** "I created a Tilemap but I can't paint tiles—the palette is empty."

**What it looks like:** A student opens the Tile Palette (Window → 2D → Tile Palette) but can't drag any tiles onto the grid.

**Why students think this:** They don't know how to create a Tile Asset from a sprite, or they're dragging from the wrong place.

**How to address it:** Set up the Tile Palette. "Drag sprites from the Project panel INTO the Tile Palette window. Unity will ask you to save the Tile Assets—choose a folder. Once saved, the palette populates. Then select a tile from the palette and paint on the Tilemap in the Scene view. Common error: trying to drag the original sprite sheet before slicing. Make sure sprites are sliced first."

🚨 **STEM Priority — Handle 1-on-1:** Tile Palette setup is unintuitive. Walk through it with each student who gets stuck; it's a 2-minute fix once shown.

---

**⚠️ Misconception:** "My large tilemap level causes massive frame rate drops. What's wrong?"

**What it looks like:** A student builds a 200×100 tile level with TilemapCollider2D and performance tanks.

**Why students think this:** Large tilemaps generate thousands of individual colliders, which Unity recalculates every physics step.

**How to address it:** Add Composite Collider. "Add a CompositeCollider2D component to the Tilemap → set TilemapCollider2D → 'Used by Composite' = true. Unity merges all tile colliders into one efficient shape. Also set Rigidbody2D (on the Tilemap) → Body Type = 'Static'. This is a massive performance improvement for large levels."

---

### Animation & Animator (Days 6–8)

**⚠️ Misconception:** "I created animation clips but they play too fast. I can't change the speed."

**What it looks like:** A student's character animations run at 60 FPS when they should be 10 FPS (pixel art).

**Why students think this:** Animation speed is set in the clip's Sample Rate, not in the Animator or Rigidbody.

**How to address it:** Change Samples Per Second. "Select the animation clip in the Project panel → Inspector → Samples Per Second. Pixel art typically uses 8–12 FPS. Smooth art uses 24–30 FPS. This is the playback rate of the clip's frames, not the game's frame rate. Also make sure animation clips were created with the correct frame count."

---

**⚠️ Misconception:** "I set up walk, idle, and jump animations, but the character gets stuck in the jump animation even after landing."

**What it looks like:** A student's Animator state machine has a Jump → Idle transition that never fires after landing.

**Why students think this:** The transition condition isn't being set correctly in code, or 'Has Exit Time' is blocking the transition.

**How to address it:** Debug the Animator. "Open the Animator window in Play mode—the active state highlights in blue. Add Debug.Log() to confirm the parameter is being set: `anim.SetBool('isGrounded', isGrounded); Debug.Log('isGrounded: ' + isGrounded);`. Check: (1) 'Has Exit Time' on the transition—if checked, the animation must finish before transitioning (usually bad for jumping). Uncheck it. (2) Transition condition must match the parameter value exactly."

---

### Sorting Layers & Camera (Days 5–6)

**⚠️ Misconception:** "My player renders behind the background tiles. I can't see the character."

**What it looks like:** A student's player sprite renders behind the tilemap or background.

**Why students think this:** Sorting Layers control render order in 2D, but students don't know they exist or how to set them.

**How to address it:** Use Sorting Layers. "In 2D, render order is controlled by Sorting Layer and Order in Layer, not by Z position (unlike 3D). Create layers: Edit → Project Settings → Tags and Layers → Sorting Layers. Add: Background, Terrain, Player, UI. Assign each sprite/tilemap to the right layer in SpriteRenderer → Sorting Layer. Player must be on a layer above Background and Terrain."

---

## Whole-Class Warning Signs

- **All sprites are blurry.** They didn't change Filter Mode. Stop the class and show the Point filter setting. Set a rule: pixel art always uses Point filtering.

- **Nobody can paint tiles—palettes are empty.** They don't know the drag-sprite-into-palette workflow. Demo it once for everyone; it's a 3-minute fix.

- **Players falling through tilemaps everywhere.** Missing Rigidbody2D on the player, or TilemapCollider2D not set up with CompositeCollider2D. Show the correct setup hierarchy: Tilemap → TilemapCollider2D + CompositeCollider2D + Static Rigidbody2D. Player → Rigidbody2D (Dynamic) + Collider2D.

- **3D scripts pasted into 2D projects—compile errors everywhere.** Stop and teach the 2D equivalents table. Provide a 2D movement template so they don't have to convert manually.

- **Animations play at the wrong speed or get stuck.** Check Sample Rate on the clips and 'Has Exit Time' on transitions. Both are common quick fixes.

---

## Questions That Reveal Understanding

1. **"What's the difference between Rigidbody and Rigidbody2D?"**
   - Good answer: "They're separate components for 3D and 2D physics. Rigidbody2D uses Vector2 instead of Vector3, and pairs with Collider2D instead of Collider. The API is similar but they're not interchangeable."
   - Red flag: "Rigidbody2D is the newer version of Rigidbody." (Incorrect—they coexist for different use cases.)

2. **"How do you set up a tilemap so the player can walk on it without falling through?"**
   - Good answer: "Tilemap needs TilemapCollider2D (and optionally CompositeCollider2D for performance) and a Static Rigidbody2D. Player needs Rigidbody2D (Dynamic) and a Collider2D."
   - Red flag: "Add a BoxCollider2D to each tile." (Correct concept, wrong approach—TilemapCollider2D handles this automatically.)

3. **"Your pixel art looks blurry in-game. What's the first thing you check?"**
   - Good answer: "Filter Mode in the sprite's Import Settings. Set it to 'Point (no filter)' for pixel art."
   - Red flag: "Use a higher resolution image." (Missing the root cause.)

4. **"Explain the difference between Sorting Layer and Order in Layer."**
   - Good answer: "Sorting Layer is the primary order (Background < Terrain < Player < UI). Order in Layer is a secondary sort within each layer. A sprite on the Player layer always renders on top of the Terrain layer, regardless of Order in Layer."
   - Red flag: "They're the same thing—just different names." (Doesn't understand the hierarchy.)

5. **"Your character animation gets stuck in Jump. How do you diagnose it?"**
   - Good answer: "Open the Animator in Play mode to see the active state. Add Debug.Log to check if the isGrounded parameter is updating. Check if 'Has Exit Time' is blocking the transition."
   - Red flag: "Delete the transition and add a new one." (Shotgun debugging—may accidentally fix it but teaches nothing.)

---

## Common Student Questions & How to Answer Them

**Q1: "I imported a sprite sheet but when I slice it the Sprite Editor is blank."**

*A:* "Make sure you: (1) Set Sprite Mode = 'Multiple' in the Inspector before clicking Apply. (2) Click the sprite in the Project panel (not in the Scene or Hierarchy). (3) The file must be a supported image type (.png, .jpg, etc.). If the Sprite Editor is still blank, close and reopen it. If it shows a warning about URP or 2D packages, import the 2D Sprite package via Package Manager."

---

**Q2: "How do I make decorative tiles that don't block movement?"**

*A:* "Create two separate Tilemaps: one for solid tiles (with TilemapCollider2D) and one for decoration (no collider). Parent both under the same Grid object. Paint collision tiles on the solid tilemap and decorative tiles on the decoration tilemap. This is standard 2D game architecture."

---

**Q3: "My camera doesn't follow the player. How do I add camera follow?"**

*A:* "Simple script on the Camera: `void LateUpdate() { transform.position = new Vector3(target.position.x, target.position.y, transform.position.z); }`. Use LateUpdate() so the camera updates after the player moves. For smooth follow: `transform.position = Vector3.Lerp(transform.position, targetPos, smoothSpeed * Time.deltaTime);`. For advanced follow with deadzone and limits, use Cinemachine."

---

**Q4: "How do I flip my sprite when moving left vs. right?"**

*A:* "Use SpriteRenderer.flipX: `spriteRenderer.flipX = (rb.velocity.x < 0);`. This flips the sprite horizontally when moving left. No need to rotate the object. Alternatively, use `transform.localScale = new Vector3(Mathf.Sign(rb.velocity.x), 1, 1);` but this can break child object positioning."

---

**Q5: "I want a parallax scrolling background. How do I set it up?"**

*A:* "Create background sprites behind the level. In a script on each background layer: `transform.position = new Vector3(cam.position.x * parallaxFactor, transform.position.y, transform.position.z);`. ParallaxFactor = 0 means it doesn't move (static). ParallaxFactor = 1 means it moves with the camera (no parallax). Use 0.2–0.7 for different depth layers."

---

## Analogies That Work

1. **"Sorting Layers are like transparencies stacked on an overhead projector. The Background transparency goes on the bottom, Terrain on top of that, Player on top of Terrain. Order in Layer is which transparency goes on top when two are in the same stack."**
   - Makes the two-level system immediately visual.

2. **"A sprite sheet is like a flip book. The Sprite Editor cuts the pages apart. The Animator plays the pages in sequence to create motion. Without slicing, you're trying to flip a book that's still glued shut."**
   - Makes the sprite workflow intuitive.

3. **"Rigidbody2D and Rigidbody are like metric and imperial wrenches. Both work on bolts, but you can't mix them—metric bolts need metric wrenches, 2D physics objects need 2D components. Don't mix them in the same project."**
   - Clarifies why 3D scripts break in 2D projects.

---

## Unity-Specific Gotchas

- **Sprite Pivot affects animation alignment.** Inconsistent pivot points between animation frames cause sprites to jitter. Set all frames in an animation to the same pivot point (usually Bottom Center for characters). Open Sprite Editor → select each sprite → set Pivot.

- **TilemapCollider2D with CompositeCollider2D requires a Static Rigidbody2D on the same object.** The CompositeCollider2D is a Rigidbody2D-dependent component. Without it, the composite can't generate. Set Rigidbody2D Body Type = Static to prevent the tilemap from falling.

- **Orthographic camera size controls visible area, not zoom.** For 2D games, set the Camera to Orthographic. Camera Size = half the visible height in Unity units. If your sprites are 1 unit tall and you want 10 sprites visible vertically, set Camera Size = 5.

- **Pixels Per Unit (PPU) affects sprite scale in the world.** A sprite with PPU = 100 is 100 pixels per world unit. Pixel art sprites often use PPU = 16 or 32 to match grid-based levels. Inconsistent PPU across sprites makes them render at different sizes. Set PPU to a consistent value across all art assets.

- **Animation events in the Animator must match method names exactly.** If an animation clip has an event that calls "PlayFootstep" but your script has "playFootstep" (lowercase), it silently fails. Unity is case-sensitive for animation event method names.

- **Physics2D.Raycast() requires a Vector2, not Vector3.** `Physics2D.Raycast(transform.position, Vector2.down, distance, groundLayer)`. Passing Vector3 to a Vector2 parameter implicitly converts (drops Z), which usually works, but be explicit to avoid confusion.

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
