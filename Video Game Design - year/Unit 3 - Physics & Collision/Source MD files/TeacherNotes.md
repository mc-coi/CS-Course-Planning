# Unit 3 - Physics & Collision: Teacher Misconception & Callout Guide

## Overview

This unit transforms students' understanding of movement. Instead of manually manipulating position in code, students delegate motion to Unity's physics engine. The biggest challenge is that physics behavior feels **magical**—a Rigidbody with velocity falls and bounces, but students don't understand why. They confuse collision detection (physical contact) with trigger detection (area sensing), leading to silent bugs where colliders don't work as expected. For a year-long course, students can productively discover these misconceptions by building physics scenes and observing failures. For a semester course, these distinctions must be explicit from day 1, as they're foundational to all gameplay.

---

## Misconceptions by Topic

### Rigidbody Basics & Forces (Days 1–2)

**⚠️ Misconception:** "I added a Rigidbody to my Cube, but it doesn't fall. The gravity must be off."

**What it looks like:** A student adds a Rigidbody component, but the object doesn't fall when Play is pressed. They check "Gravity" in the Rigidbody inspector and it's on.

**Why students think this:** Multiple causes could be at play (pun intended): (1) the object is resting on the ground plane and gravity is pulling it down at 0,0,0, (2) there's a collider on the ground plane stopping it, (3) the Rigidbody is kinematic (ignores physics), or (4) gravity in Project Settings is 0.

**How to address it:** Troubleshoot systematically. "First, check: is there a ground? Is the Cube sitting on it? If yes, it's working—gravity is pulling it down, and the ground is stopping it. If no ground, the Cube should fall. Check Project Settings (Physics) → Gravity is (0, -9.8, 0). Check the Rigidbody: Is Body Type 'Dynamic'? Is Is Kinematic unchecked? If all are correct, the physics are working."

---

**⚠️ Misconception:** "I set the Rigidbody's velocity to `Vector3.zero`, but the object still moves. It should stop."

**What it looks like:** A student writes `rb.velocity = Vector3.zero;` expecting the object to stop, but it continues moving (usually because another force is still acting on it, like AddForce).

**Why students think this:** They think `Vector3.zero` is permanent. Actually, forces and velocity interact. If you set velocity to zero but gravity is still pulling (or you're still calling AddForce), the object will accelerate again.

**How to address it:** Explain the relationship. "Setting `velocity = Vector3.zero` stops motion **at that instant**. But if gravity or forces are still acting, the object accelerates again. To keep an object stationary, either (a) set velocity to zero *every frame* (bad), or (b) use a kinematic Rigidbody or freeze axes in the Rigidbody settings."

---

**⚠️ Misconception:** "Mass doesn't affect how fast objects fall. I set mass to 100, and it still falls at the same speed as mass 1."

**What it looks like:** A student expects heavier objects to fall faster. They don't, because gravity accelerates all objects equally (ignoring air resistance).

**Why students think this:** Real-world intuition: heavy things *feel* stronger. But physics: F = ma. Gravity applies the same acceleration (9.8 m/s²) to all objects. Mass affects how much **force** is needed to accelerate an object, not gravity.

**How to address it:** Clarify the physics. "Gravity pulls all objects at the same rate: 9.8 m/s² downward. Mass affects how much force is needed to change direction. A heavy ball pushed with the same force as a light ball won't accelerate as much. Try it: create a light Cube (mass 1) and a heavy Cube (mass 100). Apply the same force to both. The light one accelerates more."

---

### Colliders & Collision Detection (Days 3–6)

**⚠️ Misconception:** "I created a Cube with a collider, and another Cube falls on top of it. They should collide, but the falling Cube passes through."

**What it looks like:** A student has two Cubes: one stationary (ground), one falling. When the falling Cube hits the ground, it passes through. They think collision is broken.

**Why students think this:** The most likely cause: one or both objects don't have a Rigidbody, or the ground object's collider is marked as `isTrigger = true`.

**How to address it:** Teach the collision requirements. "For physical collision, **both objects need a Collider and at least one needs a Rigidbody with Body Type = Dynamic**. If the ground is just a static Collider (no Rigidbody), that works. But if it's a Trigger (isTrigger = true), the Cube passes through. Check: Ground → Collider → isTrigger should be unchecked."

---

**⚠️ Misconception:** "I set isTrigger = true on my Cube's collider so it wouldn't block movement. Now my projectile passes through it, but I wanted it to detect hits."

**What it looks like:** A student conflates Trigger with "no collision." They think `isTrigger = true` means the object becomes invisible/passthrough, which is true. But they also expect collision callbacks to fire, which they don't (trigger callbacks fire instead).

**Why students think this:** The terminology is confusing. "Trigger" suggests "activate a trap." But `isTrigger = true` means "this collider is a sensor, not a physical wall."

**How to address it:** Separate the two. "Colliders have two modes: (1) Collision (isTrigger = false): physical wall, blocks movement, fires `OnCollisionEnter`. (2) Trigger (isTrigger = true): invisible sensor, doesn't block movement, fires `OnTriggerEnter`. Use collision for walls and floors. Use triggers for pickups, death zones, and sensors."

---

**⚠️ Misconception:** "My colliders are overlapping. I think that's bad, so I'm trying to separate them perfectly. But the game still feels weird."

**What it looks like:** A student spends time perfectly aligning colliders to not overlap, then the game still has physics glitches.

**Why students think this:** Overlapping colliders can cause issues, but slight overlaps are expected and normal. The real issue is usually something else (collider on the wrong object, rigidbody configuration, physics timestep).

**How to address it:** Reassure them. "Small overlaps are fine. Unity's physics engine handles them. The problem usually isn't overlap—it's configuration. Make sure: (a) the collider is on the right GameObject, (b) the Rigidbody is set correctly, (c) the collision callback method exists and is spelled correctly."

---

### OnCollisionEnter/Stay/Exit vs OnTriggerEnter/Stay/Exit (Days 5–8)

**⚠️ Misconception:** "`OnCollisionEnter()` doesn't fire. My collision must not be working."

**What it looks like:** A student writes `OnCollisionEnter(Collision collision)` and expects it to be called when two objects collide. It's not firing.

**Why students think this:** The code looks correct. They don't realize there are multiple possible causes: (1) isTrigger is true (should use `OnTriggerEnter` instead), (2) the method signature is wrong, (3) the objects don't actually collide, or (4) the Rigidbody configuration prevents collision.

**How to address it:** Troubleshoot in order. "First, add `Debug.Log()` inside the method to confirm it runs. If it doesn't print, check: (a) Is isTrigger = true? (If yes, use `OnTriggerEnter` instead.) (b) Is the method spelled correctly? (c) Do both objects have colliders and at least one has a Rigidbody? (d) Are they actually colliding (not just close together)?"

---

**⚠️ Misconception:** "I'm using `OnTriggerEnter()` to detect when the player enters a pickup zone. But the pickup is triggered multiple times per second, not just once."

**What it looks like:** A student uses `OnTriggerEnter()` but sees it firing repeatedly. They think it's a bug.

**Why students think this:** `OnTriggerEnter()` fires once when the player **enters** the trigger. `OnTriggerStay()` fires **every frame** while the player is inside. If they want an action to happen once, they need to track state:
```csharp
bool hasPickedUp = false;
void OnTriggerEnter(Collider other)
{
    if(!hasPickedUp)
    {
        GivePickup();
        hasPickedUp = true;
    }
}
```

**How to address it:** Teach state tracking. "OnTriggerEnter fires once. OnTriggerStay fires every frame. If you want a one-time action, use a boolean flag to prevent repeating."

---

**⚠️ Misconception:** "I used `OnTriggerEnter()` but forgot to enable `Is Trigger` on the collider. Now collisions are working when I don't want them to."

**What it looks like:** A student writes `OnTriggerEnter()` code but forgets to check `isTrigger = true` on the collider. They get `OnCollisionEnter()` callbacks instead, and the objects collide physically.

**Why students think this:** They wrote the right method name, so they expect it to work. They don't realize the collider configuration determines which callback fires.

**How to address it:** Reinforce the rule. "The **collider configuration** determines the callback: (1) isTrigger = false → `OnCollisionEnter()`. (2) isTrigger = true → `OnTriggerEnter()`. Write the right method for your configuration. If your method isn't firing, first check the collider settings."

---

### Raycasting & Ground Detection (Days 11–12)

**⚠️ Misconception:** "I raycasted downward to detect the ground, but `Physics.Raycast()` always returns false. My raycast must be broken."

**What it looks like:** A student writes:
```csharp
Physics.Raycast(transform.position, Vector3.down, 0.1f);
```
And it always returns false, even when standing on the ground.

**Why students think this:** The code looks correct. But the distance (0.1f) might be too short, the raycast might be originating inside the collider, or the layer mask is filtering out the ground.

**How to address it:** Debug with visualization. "Use `Debug.DrawRay()` to visualize the raycast:
```csharp
Debug.DrawRay(transform.position, Vector3.down * 0.1f, Color.red);
if(Physics.Raycast(transform.position, Vector3.down, 0.1f, groundLayer))
{
    Debug.Log("Ground detected!");
}
```
In the Scene View, you'll see a red line. If it doesn't reach the ground, increase the distance. If it goes through the ground, the raycast is starting inside the collider—move the start point up slightly."

---

**⚠️ Misconception:** "I'm raycasting to check if the player is on the ground, but it returns true even when I'm in mid-air. My ground detection is broken."

**What it looks like:** A student uses ground detection for jump logic, but the raycast always returns true, allowing infinite jumps.

**Why students think this:** Common causes: (1) the raycast distance is too long (it hits the ground from the air), (2) the raycast includes the player's own collider (should exclude it), or (3) the player is standing on a moving platform and the raycast is hitting it from inside.

**How to address it:** Fix the configuration. "Raycast downward from the **bottom** of the player, not the center. Use a short distance (e.g., 0.1f for a 2-unit-tall player). Exclude the player's own layer from the raycast using the layer mask. Use `Physics.Raycast(feet, Vector3.down, 0.1f, groundLayer);`" (where `feet` is a point below the player's center).

---

### Layers & Collision Matrix (Days 9–10)

**⚠️ Misconception:** "I set the Enemy on 'Enemy' layer and the Player on 'Player' layer, but they still collide. Layers aren't working."

**What it looks like:** A student assigns objects to different layers but still gets collisions. They think layers prevent collision, but they don't.

**Why students think this:** Layers don't automatically prevent collision. You have to explicitly configure the **Collision Matrix** (Physics settings) to tell Unity which layers collide with which.

**How to address it:** Teach the two-step process. "Step 1: Assign objects to layers. Step 2: Configure Physics settings. Go to Edit → Project Settings → Physics. In the Collision Matrix, **uncheck** the interaction between 'Enemy' and 'Player' layers. Now they won't collide."

---

### 2D Physics (Days 17–18)

**⚠️ Misconception:** "I'm using Rigidbody2D and Collider2D, but my 2D object is disappearing or behaving strangely."

**What it looks like:** A student mixes 2D and 3D physics (e.g., a Rigidbody2D with a BoxCollider instead of BoxCollider2D), and behavior is unpredictable.

**Why students think this:** The names are similar. They assume Collider works with Rigidbody2D, but it doesn't. The 2D physics system is separate from 3D.

**How to address it:** Set a clear rule. "Use **2D consistently**: Rigidbody2D + Collider2D. Don't mix. Similarly, 3D: Rigidbody + Collider. If you're building a 2D game, use all 2D components."

---

## Whole-Class Warning Signs

- **Everyone's game is slow or laggy, and they blame the computer.** Actually, the physics settings might be set to high quality (more solver iterations). Teach them to check Project Settings → Physics → Solver Iterations. Default is 6; for learning, 2-3 is fine.

- **Multiple students have objects "jiggling" or vibrating against the ground.** This is often caused by collision margin being too large or the object bouncing infinitesimally. Show them PhysicMaterial and set `Bounciness = 0` to stop bouncing.

- **Nobody can get jumping to feel right.** Jump feel is subjective. They need to tune `jumpForce`, `gravity`, and `groundDrag` together. Don't expect one setting to work. Have them make a "jump tuning" scene and systematically adjust values.

- **Raycasting students keep forgetting the layer mask, so raycasts hit everything.** Teach them to always include the layer mask parameter: `Physics.Raycast(..., groundLayer);`. Make it a habit from the first raycast example.

- **Everyone puts collision code in `Update()` instead of `FixedUpdate()`.** Collision callbacks work in either, but physics calculations should be in `FixedUpdate()`. Redirect: "Physics updates happen at a fixed timestep. Put physics code in `FixedUpdate()`."

---

## Questions That Reveal Understanding

1. **"You have two Cubes. One is static (no Rigidbody), one has a Rigidbody with Body Type = Dynamic. The Dynamic one falls and hits the static one. Do they collide?"**
   - Good answer: "Yes. Collision requires at least one Rigidbody on a Dynamic body and colliders on both. The static one doesn't move, but they collide."
   - Red flag: "No, because one doesn't have a Rigidbody." (They think both need Rigidbodies.)

2. **"What's the difference between `isTrigger = true` and `isTrigger = false`?"**
   - Good answer: "True: the collider is a sensor, objects pass through, fires `OnTriggerEnter()`. False: the collider is solid, objects collide, fires `OnCollisionEnter()`."
   - Red flag: "True means it triggers something" or "False means nothing happens." (Too vague.)

3. **"Why do you use `FixedUpdate()` for physics code but `Update()` for input?"**
   - Good answer: "Physics calculations happen at a fixed timestep (usually 50 Hz). `FixedUpdate()` is called at that rate, so it's the right place for Rigidbody code. Input can be checked in `Update()` because input doesn't need to be synchronized to physics."
   - Red flag: "I don't know" or "They're the same." (They haven't grasped the difference in timing.)

4. **"You raycasted downward but the raycast starts inside a collider. Will it detect the ground?"**
   - Good answer: "No. The raycast starts inside the collider and immediately detects it as a hit. Move the raycast starting point up, outside the collider, so it casts downward through empty space."
   - Red flag: "Yes, it will detect the ground." (They don't understand that raycasts starting inside colliders immediately hit the collider they're inside.)

5. **"Why would you ever use `Physics.OverlapCircle()` instead of raycasting for ground detection?"**
   - Good answer: "OverlapCircle checks a large area for colliders; raycasting is a line. OverlapCircle is better on uneven terrain or when you want a forgiving ground check. Raycasting is more precise."
   - Red flag: "They're the same" or "I don't know." (They haven't compared the two methods.)

6. **"You set a Rigidbody to `isKinematic = true`. Now you move it with script. Will gravity affect it?"**
   - Good answer: "No. Kinematic bodies ignore forces and gravity. You control movement entirely through code (`transform.position` or `rb.velocity`). This is useful for moving platforms or doors."
   - Red flag: "Yes, gravity still affects it." (They think isKinematic is cosmetic.)

---

## Common Student Questions & How to Answer Them

**Q1: "What's the difference between adding a force with `AddForce()` vs. setting `velocity` directly?"**

*A:* "`AddForce()` applies a force that accelerates the object (like pushing it). `velocity` directly sets how fast it's moving (like teleporting it to that speed). Use `AddForce()` for physics interactions (push, jump, explosion). Use `velocity` for direct control (platformer movement, jump impulse). For a jumpable character, use `AddForce()` or directly set `rb.velocity = new Vector3(rb.velocity.x, jumpForce, 0);`."

---

**Q2: "My character keeps bouncing when it lands. How do I stop it?"**

*A:* "The Rigidbody is bouncing because the PhysicMaterial has bounciness. Either: (1) Set the PhysicMaterial's `Bounciness = 0` and `Friction = 1`. (2) Or, when the player lands, explicitly set `rb.velocity.y = 0` to kill bounce. A combination works too: low bounciness + zero velocity on landing."

---

**Q3: "I used `OnCollisionEnter()`, but the method doesn't fire even though the objects definitely collide."**

*A:* "Check these in order: (1) Is `isTrigger = false` on both colliders? (If true, use `OnTriggerEnter()` instead.) (2) Does the script have a Rigidbody (not just the other object)? (3) Does at least one object have `Body Type = Dynamic`? (4) Is the method name spelled exactly `OnCollisionEnter`? (Case matters!) (5) Are they actually touching, or just close? Add `Debug.Log()` inside the method and press Play to test."

---

**Q4: "How do I make a moving platform that players can stand on?"**

*A:* "Give the platform a Rigidbody (set to `Body Type = Dynamic` if you're moving it with forces, or `isKinematic = true` if you're moving it with code). Move it either with `rb.velocity` (for kinematic) or `AddForce()` (for dynamic). Players will ride along because they're colliding with it. If the platform moves too fast, use `isKinematic = true` and move it with code—it's more stable."

---

**Q5: "My projectile passes through colliders sometimes. What's happening?"**

*A:* "This is 'bullet passing through paper' problem. If your projectile is fast and the physics timestep is long, it can miss collisions. Fix: (1) Increase the projectile's Collision Detection to 'Continuous' (or 'Continuous Dynamic'). (2) Reduce the timestep (Project Settings → Physics → Fixed Timestep = 0.01 instead of 0.02). (3) Use raycasting instead of colliders for fast projectiles."

---

## Analogies That Work

1. **"Physics bodies are like actors on stage. A Dynamic body is an actor who can move freely. A Static body is a set piece (wall, floor) that doesn't move. A Kinematic body is an actor being moved by a stage hand (your script). When an actor collides with a set piece, they stop. When a stage hand moves a set piece, an actor riding on it moves too."**
   - This maps Rigidbody types to intuitive roles.

2. **"A Collider is the actor's physical shape. If `isTrigger = false`, it's solid—other actors bounce off. If `isTrigger = true`, it's a phantom—other actors pass through but can sense they passed. Use solid for walls, phantom for sensor gates."**
   - This clarifies collision vs. trigger.

3. **"Raycasting is like shining a flashlight in a direction and checking what it hits. You control the starting point, direction, and how far the light reaches (distance). If the light hits an object, it's a hit. If it starts inside an object, it immediately detects that object."**
   - This makes raycasting visual and intuitive.

---

## Unity-Specific Gotchas

- **Physics calculations happen at a fixed timestep, not every frame.** If `Update()` runs at 120 FPS but `FixedUpdate()` runs at 50 Hz, physics code runs less frequently. This is correct but can confuse students used to frame-by-frame thinking.

- **Colliders are triggers by default on some versions/templates.** Always check `isTrigger` when setting up colliders. A student might think collision is broken when actually the colliders are triggers.

- **Layer masks are bitwise, not simple lists.** Assigning two objects to different layers doesn't prevent collision unless you configure the Collision Matrix. This is non-obvious.

- **Physics materials are shared and can affect multiple objects.** Changing a PhysicMaterial's bounciness affects all objects using it. Use `new PhysicMaterial()` to create per-object materials if needed.

- **Raycast distance is important.** A raycast with distance = 0 doesn't hit anything. A raycast with distance = 1000 might hit unexpected distant objects. Always pick a reasonable distance.

- **GetComponent is slow; cache it.** `GetComponent<Rigidbody>()` is O(n). Call it once in `Start()`, not every frame in `Update()`. This is a performance best practice.

- **Physics gizmos must be enabled to visualize colliders in Play mode.** Go to Scene View → Gizmos panel (top right) and toggle physics icons. Without this, students can't see if colliders are aligned.

- **'Rigidbody' vs 'RigidBody' — the correct spelling is 'Rigidbody'** (camelCase). Some students write it wrong and get compile errors.

---

## Year-Long Differentiators

For year-long courses, let students discover physics bugs organically:
- Assign open-ended challenges: "Build a stacking puzzle with physics." Let them struggle with collision configuration, layer masks, and material settings. Troubleshoot together when things don't work.
- Introduce raycasting when teaching platformer jumping (Unit 4). They'll see why ground detection matters.
- Revisit 2D physics in Unit 6. By then, students will have 3D intuition and the 2D system will feel familiar.
- Use Unit 3's physics project lab to let students experiment with joints, materials, and destruction systems. Encourage play-based learning.

---

**Created for:** Video Game Design course (year-long version)
**Last updated:** 2026
