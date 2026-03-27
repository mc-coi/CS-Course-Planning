# Unit 3: Physics & Collision

> Give your game world real physical laws. Learn to use Unity's physics engine to create gravity, bouncing, sliding, and collision detection that makes your game feel alive.

## Unit Overview

- **Duration:** 22 days / ~4.5 weeks
- **TN Standard:** 9-12.VGD.3 — Implement physics and collision detection systems in Unity
- **Prerequisites:** Unit 1 (Unity Interface), Unit 2 (C# Scripting)
- **Key Skills:** Rigidbody manipulation, collision detection, raycasting, physics optimization

---

## Learning Objectives

By the end of this unit, students will be able to:

1. **Manipulate Rigidbody properties** to create realistic physics behavior
2. **Detect collisions and triggers** using callback methods
3. **Use raycasting and overlap detection** for ground checks and shooting
4. **Implement joints and constraints** for complex interactions
5. **Optimize physics performance** using layers and collision matrices
6. **Build 2D physics systems** with Rigidbody2D and Collider2D
7. **Debug physics issues** effectively using visualization tools
8. **Design physics-based mechanics** that enhance gameplay

---

## Unit Structure

### Week 1: Foundations (Days 1–6)
- **Days 1–2:** Rigidbody basics — mass, gravity, drag
- **Days 3–4:** Colliders and component setup
- **Days 5–6:** Collision callbacks and data

### Week 2: Detection & Interaction (Days 7–14)
- **Days 7–8:** Trigger zones and event-based interactions
- **Days 9–10:** Tags, layers, and organization
- **Days 11–12:** Raycasting fundamentals
- **Days 13–14:** Joints and complex interactions

### Week 3: Advanced Systems (Days 15–20)
- **Days 15–16:** Physics materials and friction
- **Days 17–18:** 2D physics systems
- **Days 19–20:** Physics project lab

### Week 4: Assessment (Days 21–22)
- **Day 21:** Review and debugging
- **Day 22:** Unit assessment

---

## Daily Topics at a Glance

| Day | Topic | Key Concept |
|-----|-------|------------|
| 1 | Rigidbody Basics | Mass, gravity, drag |
| 2 | Velocity & AddForce | Force application, movement |
| 3 | Collider Types | Box, Sphere, Capsule |
| 4 | isTrigger vs Solid | Collision vs triggers |
| 5 | OnCollisionEnter/Stay/Exit | Collision detection |
| 6 | Collision Info | Impulse, contact points |
| 7 | OnTriggerEnter/Stay/Exit | Trigger interactions |
| 8 | Trigger Zones | Pickups, portals, death zones |
| 9 | Tags & Identification | CompareTag, tag management |
| 10 | Layers & Collision Matrix | Performance, organization |
| 11 | Raycasting Fundamentals | Physics.Raycast basics |
| 12 | Ground Detection | Raycasting for platformers |
| 13 | Hinge Joints | Doors, rotating mechanisms |
| 14 | Fixed & Spring Joints | Chains, bridges, spring physics |
| 15 | PhysicsMaterial | Friction, bounciness |
| 16 | Advanced Materials | Special surfaces, ice, rubber |
| 17 | Rigidbody2D Basics | 2D physics component |
| 18 | Collider2D & Physics2D | 2D collision systems |
| 19 | Physics Project | Build a physics game |
| 20 | Project Continuation | Polish and refinement |
| 21 | Review & Debugging | Troubleshooting, optimization |
| 22 | Unit Assessment | Comprehensive evaluation |

---

## Essential Concepts

### Rigidbody Properties
- **Mass** — Object weight; affects force response
- **Drag** — Air resistance (linear motion)
- **Angular Drag** — Rotational resistance
- **Gravity Scale** — How much global gravity affects this object
- **isKinematic** — Can move via script, unaffected by physics forces
- **Collision Detection** — Discrete vs Continuous (for fast-moving objects)
- **Constraints** — Freeze position or rotation axes

### Collider Types
- **BoxCollider** — Rectangular collision (most common)
- **SphereCollider** — Spherical collision (rolling objects)
- **CapsuleCollider** — Cylinder-like (characters, organic shapes)
- **MeshCollider** — Exact mesh shape (static only for performance)
- **isTrigger** — Passthrough (area detection, not physical collision)

### Collision vs Triggers
- **Collision** — Physical interaction; both objects must have Rigidbodies
  - Callbacks: `OnCollisionEnter`, `OnCollisionStay`, `OnCollisionExit`
- **Trigger** — Area detection; passes through; one object has isTrigger = true
  - Callbacks: `OnTriggerEnter`, `OnTriggerStay`, `OnTriggerExit`

### Detection Methods
- **Collision Callbacks** — Detect physical contact
- **Raycasting** — Cast a ray and check for hits
- **Overlap Detection** — Check if shapes overlap (OverlapSphere, OverlapBox, etc.)
- **Physics Queries** — General-purpose detection queries

### Common Patterns
- **Ground Detection** — Raycast downward or OverlapCircle below object
- **Melee Attack** — OverlapSphere around weapon; apply damage to hit objects
- **Projectile Shooting** — Instantiate rigidbody with initial velocity
- **One-Way Platforms** — Use triggers to enable/disable collision
- **Physics Puzzles** — Combine joints and materials for complex interactions

---

## Tools & Components

### Inspector Components
- **Rigidbody / Rigidbody2D** — Physics component
- **Colliders** — Collision shapes
- **PhysicMaterial / PhysicsMaterial2D** — Friction and bounciness
- **Joints** — Constraints and connections

### Physics Editor Windows
- **Physics Settings** (Edit → Project Settings → Physics)
  - Gravity, default materials
  - Solver iterations (accuracy)
  - Layer Collision Matrix
- **Gizmos** — Visual debugging
  - Enable physics gizmos in Scene view
  - Debug.DrawRay, Physics.Raycast visualization

### Scripting Namespace
```csharp
using UnityEngine; // Includes all physics classes
// Common classes:
// - Rigidbody / Rigidbody2D
// - Collider / Collider2D
// - Physics / Physics2D
// - RaycastHit / RaycastHit2D
// - Joint (HingeJoint, FixedJoint, etc.)
```

---

## Success Criteria

**By Day 22, you should:**
- [ ] Understand Rigidbody properties and how they affect object behavior
- [ ] Implement collision and trigger detection in scripts
- [ ] Use raycasting for game mechanics (ground checks, aiming)
- [ ] Design and build physics-based game mechanics
- [ ] Optimize physics using layers and collision matrices
- [ ] Debug physics issues effectively
- [ ] Build both 3D and 2D physics systems
- [ ] Score 70%+ on the Unit Assessment

---

## Real-World Applications

- **Platformer Games** — Jump mechanics, ground detection, collision feedback
- **Physics Puzzles** — Boxes, balls, ramps; joints and constraints
- **Shooting Games** — Raycasting for hit detection; ballistics
- **Destruction Systems** — Breaking walls, ragdoll physics
- **Vehicle Games** — Wheel colliders, suspension simulation
- **Particle Effects** — Physical collisions triggering VFX

---

## Resources & References

### Documentation
- [Unity Physics Manual](https://docs.unity3d.com/Manual/PhysicsSection.html)
- [Rigidbody API](https://docs.unity3d.com/ScriptReference/Rigidbody.html)
- [Collider API](https://docs.unity3d.com/ScriptReference/Collider.html)
- [Physics2D Scripting](https://docs.unity3d.com/Manual/Physics2DReference.html)

### Helpful Tools
- Gizmos (Scene view debugging)
- Debug.DrawRay, Debug.DrawLine
- Physics Profiler
- Physics Debug Visualizer (Unity 2022+)

### Bonus: Game Feel Principles
- Responsive collision feedback
- Satisfying "weight" through physics
- Visual impact of forces
- Audio cues for collision events

---

## Notes for Teachers

**Pacing Suggestions:**
- Days 1–6: Move quickly; students likely familiar with components
- Days 7–14: Spend more time; callbacks and detection are fundamental
- Days 15–18: Can move faster; 2D is similar to 3D
- Days 19–20: Project week; give flexibility for exploration
- Day 21: Review & practice; address weak areas
- Day 22: Assessment (may extend to Day 23 if needed)

**Common Struggles:**
- Forgetting to use FixedUpdate for physics code
- Mixing up Collision vs Trigger callbacks
- Raycast direction and distance parameters
- Layer collision matrix setup

**Enrichment Ideas:**
- Advanced joint constraints (6D freedom)
- Vehicle physics with wheel colliders
- Rope/chain simulation with springs
- Destruction system with instantiation
- Physics optimization for large scenes

---

## Final Project Ideas

Students can apply these skills to build:
1. **Physics Platformer** — Gravity, collision, custom jump feel
2. **Breakable Walls** — Raycast hit, apply force to break structures
3. **Marble Puzzle** — Roll ball through obstacles using joints and friction
4. **Physics-Based Shooter** — Ballistics, ricochet, impact feedback
5. **Ragdoll System** — Chain joints to create articulated bodies

