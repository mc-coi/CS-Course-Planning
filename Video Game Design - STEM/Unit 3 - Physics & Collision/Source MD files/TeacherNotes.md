# Unit 3 - Physics & Collision: Teacher Misconception & Callout Guide

## Overview

This unit introduces Unity's physics engine—Rigidbody, colliders, forces, and raycasting. In a STEM semester course, students arrive faster but have less play-testing intuition; many have physics class background but don't realize game physics is simplified, deterministic, and often deliberately wrong for "feel." The biggest mistakes are using Transform.position instead of Rigidbody forces (which breaks physics), confusing OnCollisionEnter with OnTriggerEnter (leads to ghost collisions), and not understanding why FixedUpdate exists (causes jitter on fast machines). Unlike the year-long course, you don't have time for extended experimentation—use 🚨 flags below to know when to stop everything and teach the whole class.

---

## Misconceptions by Topic

### Rigidbody & Forces (Days 1–3)

**⚠️ Misconception:** "I want my object to move, so I'll update Transform.position directly. It moves!"

**What it looks like:** A student uses `transform.position += new Vector3(speed * Time.deltaTime, 0, 0);` on an object with a Rigidbody. The object moves but clips through walls, stutters, or tunnels through fast-moving objects.

**Why students think this:** Moving a Transform directly is the simplest mental model. They don't see the collision break immediately.

**How to address it:** Use Rigidbody for physics objects. "If your object has a Rigidbody, move it with physics—not Transform. Use `rb.velocity = new Vector3(speed, rb.velocity.y, 0);` or `rb.AddForce(Vector3.right * speed);`. Moving Transform directly bypasses the physics engine. It causes tunneling (fast objects skip through walls) and breaks collision detection."

🚨 **STEM Priority — STOP THE CLASS:** If multiple students are doing this, halt and teach it before they build broken movement systems.

```csharp
// WRONG — breaks physics
transform.position += new Vector3(speed * Time.deltaTime, 0, 0);

// RIGHT — let the physics engine handle it
rb.velocity = new Vector3(speed, rb.velocity.y, 0);
```

---

**⚠️ Misconception:** "I want to apply a force every frame to keep my player moving. I'll use AddForce() in Update()."

**What it looks like:** A student calls `rb.AddForce(Vector3.right * 10f);` in Update(). The object accelerates forever without a top speed, or moves inconsistently between machines.

**Why students think this:** AddForce sounds like "push once." They don't realize it accumulates.

**How to address it:** Separate force type and loop. "AddForce() in Update() applies a force EVERY frame—the object accelerates forever. Either: (1) Use `ForceMode.Impulse` for a single push: `rb.AddForce(Vector3.right * jumpForce, ForceMode.Impulse);`. Or (2) Set velocity directly for constant movement: `rb.velocity = new Vector3(speed, rb.velocity.y, 0);`. If you use AddForce for continuous movement, cap the velocity: `if (rb.velocity.magnitude > maxSpeed) rb.velocity = rb.velocity.normalized * maxSpeed;`"

---

**⚠️ Misconception:** "Physics is running in Update(), but my game stutters or feels inconsistent. The physics must be broken."

**What it looks like:** A student puts Rigidbody logic in Update() instead of FixedUpdate(). The game runs fine on their machine but stutters on others.

**Why students think this:** Update() is the default loop. They don't know FixedUpdate() exists.

**How to address it:** Explain the two loops. "Unity runs two loops: Update() runs every frame (varies by machine—60 fps on one, 120 on another). FixedUpdate() runs at a fixed rate (50 times/second by default). Physics calculations must go in FixedUpdate() because physics needs a consistent timestep. Movement that feels smooth on your machine may jitter on a faster or slower machine if it's in Update()."

🚨 **STEM Priority — STOP THE CLASS:** If no one knows about FixedUpdate(), demonstrate it before they build movement.

```csharp
void FixedUpdate()
{
    // Physics and Rigidbody here
    rb.velocity = new Vector3(moveInput * speed, rb.velocity.y, 0);
}

void Update()
{
    // Input polling here (more responsive)
    moveInput = Input.GetAxisRaw("Horizontal");
}
```

---

### Colliders & Collision Events (Days 3–5)

**⚠️ Misconception:** "I added a Collider to my object, but OnCollisionEnter() never fires. Collisions must not be working."

**What it looks like:** A student has two objects with Colliders, adds OnCollisionEnter(), and nothing happens.

**Why students think this:** They don't know that at least one object needs a Rigidbody for physics collision events to fire.

**How to address it:** Check the setup. "OnCollisionEnter() requires: (1) Both objects have Colliders. (2) At least ONE of them has a non-Kinematic Rigidbody. Two static Colliders without Rigidbodies don't generate collision events—Unity skips the event for performance. Add a Rigidbody to the moving object."

🚨 **STEM Priority — STOP THE CLASS:** This is the most common blocker. If half the class is stuck here, stop and demo it.

---

**⚠️ Misconception:** "I want my collectible to disappear when the player touches it. I used OnCollisionEnter() but the player bounces off the collectible."

**What it looks like:** A student uses a solid Collider for a pickup. The player collides and is pushed back instead of passing through.

**Why students think this:** They don't know the difference between a Collider (solid) and a Trigger (passthrough).

**How to address it:** Use the right collision type. "For objects you can walk through (collectibles, checkpoints, hazards, doors), check 'Is Trigger' on the Collider. Then use OnTriggerEnter() instead of OnCollisionEnter(). Triggers detect overlaps without pushing objects apart. Solid Colliders use OnCollisionEnter() and physically block movement."

```csharp
// For triggers (collectibles, checkpoints)
void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Player"))
        Destroy(gameObject);
}

// For solid collisions (walls, floors)
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.CompareTag("Enemy"))
        TakeDamage();
}
```

---

**⚠️ Misconception:** "My collision detection works sometimes but misses fast-moving objects. The game must be laggy."

**What it looks like:** A student's bullet or fast projectile passes through walls occasionally.

**Why students think this:** Fast objects can skip over thin colliders between physics frames (tunneling).

**How to address it:** Enable Continuous Collision Detection. "This is 'tunneling'—fast objects move so far in one physics step that they skip over thin colliders. Fix: Select the Rigidbody → Collision Detection → change from 'Discrete' to 'Continuous' (for fast-moving objects like bullets) or 'Continuous Dynamic' (for collisions between two fast objects). Note: this has a performance cost, so only use it on fast objects."

---

### Raycasting & Ground Detection (Days 5–7)

**⚠️ Misconception:** "I used OnCollisionEnter() to check if the player is grounded, but jumping is unreliable. Sometimes the player can jump in the air."

**What it looks like:** A student uses `isGrounded = true` in OnCollisionEnter() and `isGrounded = false` in OnCollisionExit(). Double-jumping or infinite jumping occurs when objects briefly separate.

**Why students think this:** OnCollisionEnter/Exit sounds like the right tool for "is touching floor."

**How to address it:** Use raycasting for ground checks. "OnCollisionEnter/Exit is unreliable for ground detection—it fires when any part of the object touches anything (walls, ceilings, other objects). Use a raycast instead: shoot a short ray downward from the player's feet. If it hits ground, isGrounded = true. This is precise and doesn't trigger on wall collisions."

🚨 **STEM Priority — Handle 1-on-1:** Common source of unfixable jump bugs. Address early before students build the whole movement system around OnCollision.

```csharp
void Update()
{
    // Raycast downward from player feet
    isGrounded = Physics.Raycast(transform.position, Vector3.down, 0.6f, groundLayer);
}
```

---

**⚠️ Misconception:** "My raycast hits the player itself! It's detecting the wrong object."

**What it looks like:** A student's ground raycast fires from the object's center, but the first thing it hits is the object's own collider.

**Why students think this:** The ray starts inside the object's collider.

**How to address it:** Use layers and offset. "Two solutions: (1) Use a Layer Mask to exclude the player's own layer: `Physics.Raycast(transform.position, Vector3.down, distance, groundLayer)` where groundLayer doesn't include the player. (2) Start the ray slightly below the object's center: `Vector3 origin = transform.position + Vector3.down * 0.4f;`. Both are commonly combined."

---

### Physics Materials & Friction (Days 6–7)

**⚠️ Misconception:** "My player slides for a long time after I stop pressing a key. How do I add friction?"

**What it looks like:** A student's character has ice-like movement because the Rigidbody has low friction.

**Why students think this:** They don't know about Physics Materials or how to zero out velocity.

**How to address it:** Control deceleration manually. "Two approaches: (1) Create a Physics Material (Assets → Create → Physics Material) with high friction and assign it to the floor. (2) In code, manually decelerate when no input: `if (Mathf.Abs(moveInput) < 0.1f) rb.velocity = new Vector3(0, rb.velocity.y, 0);`. Option 2 gives more control and is typical in game code. Physics Materials are better for environmental surfaces (ice floors, sticky mud)."

---

## Whole-Class Warning Signs

- **Multiple students are moving objects with Transform.position instead of Rigidbody.** STOP THE CLASS. This is the most fundamental physics error and will corrupt every project built on it.

- **Nobody understands FixedUpdate vs Update.** Demo before any movement code is written. Draw the analogy: Update = frames per second (variable), FixedUpdate = physics clock (fixed).

- **Everyone's Triggers fire on nothing.** They've set IsTrigger but still call OnCollisionEnter(). Triggers use OnTriggerEnter()—different method name. Five-minute demo fixes this for everyone.

- **Multiple students have "ghost jumps" (can jump in mid-air).** Their ground detection uses OnCollisionEnter/Exit instead of raycasting. Address 1-on-1 or do a whole-class raycast demo.

- **Fast projectiles pass through walls (tunneling).** Show the class Continuous Collision Detection as a quick fix. This is expected when they build shooting mechanics.

- **Students' Rigidbody objects spin uncontrollably on collision.** They forgot to freeze rotation. Show: Rigidbody → Constraints → Freeze Rotation (X, Z for 2D-style games; all three for top-down).

---

## Questions That Reveal Understanding

1. **"What's the difference between OnCollisionEnter() and OnTriggerEnter()? When do you use each?"**
   - Good answer: "OnCollisionEnter() is for solid physical collisions—objects push each other. OnTriggerEnter() is for overlap detection without physical response—collectibles, zones, checkpoints."
   - Red flag: "They're the same—just different events" or "I use whichever one works." (No understanding of the physics vs. trigger distinction.)

2. **"Why does physics code go in FixedUpdate() instead of Update()?"**
   - Good answer: "FixedUpdate runs at a fixed rate regardless of frame rate. Physics calculations need a consistent timestep or behavior changes depending on machine speed. Update varies per frame."
   - Red flag: "I don't know what FixedUpdate is" or "It doesn't matter which one." (Critical gap.)

3. **"Your player is falling through the floor. The floor has a BoxCollider. What's the first thing you check?"**
   - Good answer: "Check if the player has a Rigidbody and a Collider. Make sure the floor's Collider is not a Trigger. Verify the Layer Collision Matrix includes both layers."
   - Red flag: "I'd add more force" or "The physics is broken." (Symptom-chasing without diagnosis.)

4. **"What causes bullet tunneling and how do you fix it?"**
   - Good answer: "Fast objects move so far per physics step that they skip thin colliders. Fix: Set Rigidbody Collision Detection to Continuous on the bullet."
   - Red flag: "Make the bullet slower" or "Make the wall thicker." (Workarounds, not the real fix.)

5. **"Your player jumps fine but can jump again in mid-air. Where's the bug?"**
   - Good answer: "Ground detection is wrong. Probably using OnCollisionEnter/Exit which can briefly un-detect ground. Switch to a downward raycast."
   - Red flag: "Add a boolean and set it to false on jump" without fixing detection root cause. (Might work but is fragile.)

---

## Common Student Questions & How to Answer Them

**Q1: "My Rigidbody object rotates and falls over. How do I keep it upright?"**

*A:* "Freeze the rotation axis in the Rigidbody Inspector. For a side-scrolling game: Rigidbody → Constraints → Freeze Rotation Z. For a top-down game: Freeze Rotation X, Y, Z. For a 3D character: Freeze X and Z. This prevents physics torque from spinning your character."

---

**Q2: "My collider doesn't match the shape of my sprite/mesh. How do I fix it?"**

*A:* "Use a more specific collider: BoxCollider (rectangular), SphereCollider (round), CapsuleCollider (elongated—good for characters), or MeshCollider (exact shape but expensive). For characters, CapsuleCollider is standard—it handles slopes and ledges better than BoxCollider. Edit the collider bounds by clicking 'Edit Collider' in the Inspector."

---

**Q3: "I set up a ground layer but my raycast still hits everything. How do layers work?"**

*A:* "Layer masks use bit shifting. In your code, declare: `public LayerMask groundLayer;` then in the Inspector, set it to your ground layer. In Physics.Raycast(), pass it as the last argument: `Physics.Raycast(origin, Vector3.down, distance, groundLayer)`. Make sure your ground objects are actually assigned to that layer in their Inspector → Layer dropdown."

---

**Q4: "My player gets pushed sideways when walking into walls. How do I stop that?"**

*A:* "This is a friction/slope issue. Solutions: (1) Zero out horizontal velocity directly: `rb.velocity = new Vector3(0, rb.velocity.y, 0)` when no input. (2) Use a Physics Material with 0 friction on the player's collider. (3) Use a CapsuleCollider—its curved bottom slides against walls more naturally. Most games use a combination of these."

---

**Q5: "My explosion force pushes objects but they don't go up—only outward. How do I make them fly up?"**

*A:* "AddExplosionForce() has an upward modifier parameter. Signature: `rb.AddExplosionForce(force, explosionPos, radius, upwardModifier, ForceMode.Impulse);`. Set upwardModifier to 1.0–3.0 to add an upward component. Alternatively, add a separate upward force: `rb.AddForce(Vector3.up * upForce, ForceMode.Impulse);`."

---

## Analogies That Work

1. **"Rigidbody is like a car engine—without it, the car (GameObject) just sits there. With it, physics can push it around. Transform.position is like picking the car up and placing it somewhere new—it teleports, bypassing roads and walls. Always drive, don't teleport."**
   - This makes the Transform vs. Rigidbody distinction intuitive.

2. **"FixedUpdate is like a metronome—it clicks at the same rate no matter what. Update is like a drummer who speeds up when excited. Physics needs the metronome, not the drummer."**
   - Students who play instruments immediately understand this.

3. **"OnCollisionEnter is a brick wall—it stops you cold. OnTriggerEnter is a motion sensor—it detects you passing through without stopping you."**
   - Clarifies when to use each.

---

## Unity-Specific Gotchas

- **Rigidbody 'Kinematic' mode disables physics forces.** Kinematic Rigidbodies can collide but aren't moved by forces—they're moved by script. Use Kinematic for moving platforms, not for the player character (unless you're implementing fully custom movement).

- **Layer Collision Matrix defaults to all layers colliding.** If a bullet hits the player who fires it, check Project Settings → Physics → Layer Collision Matrix and uncheck the Player–Bullet interaction.

- **OnCollisionEnter/Stay/Exit vs. OnTriggerEnter/Stay/Exit** — there are six separate events. Students often use OnCollisionEnter when the object is a trigger, then wonder why it never fires. Quick check: if Is Trigger is checked, use OnTriggerEnter.

- **Rigidbody.Sleep()** — Rigidbodies at rest enter a sleep state to save performance. If an object stops responding to forces, call `rb.WakeUp();`. This trips students who dynamically enable/disable objects.

- **Physics.Raycast() returns false if no hit** — students often forget to check the return value. Always: `if (Physics.Raycast(...)) { ... }` or use RaycastHit to inspect what was hit.

- **Negative gravity doesn't invert correctly** — changing Project Settings → Physics → Gravity to positive Y doesn't flip all physics behavior. Objects that depend on `Vector3.down` for ground checks will break. Avoid changing gravity; add upward forces instead for zero-G effects.

---

**Created for:** Video Game Design course (STEM semester version)
**Last updated:** 2026
