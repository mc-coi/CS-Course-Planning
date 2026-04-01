# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is the difference between a collider and a Rigidbody?

2. Explain the difference between OnCollisionEnter() and OnTriggerEnter().

3. Why should physics code go in FixedUpdate() instead of Update()?

4. What does Physics.Raycast() return, and how do you use it?

5. How do you prevent the player from double-jumping?

6. Explain the purpose of tags and how to use CompareTag().

7. What is the difference between SetActive(false) and Destroy()?

8. What does ForceMode.Impulse do compared to ForceMode.Force?

9. How do you set up a collectible item that disappears when touched?

10. What happens if you apply forces to a Rigidbody with infinite mass?

---

## Answers

1. **A collider defines the physical shape for collision detection. A Rigidbody simulates physics (gravity, forces). Objects can have colliders without Rigidbodies, but physics requires a Rigidbody.**

2. **OnCollisionEnter() fires when two solid colliders touch. OnTriggerEnter() fires when an object enters a trigger volume (Is Trigger = true). Triggers don't cause physical collisions.**

3. **FixedUpdate() is called at a fixed timestep (default 50 times/sec), making physics consistent. Update() varies with frame rate. Using Update() would make physics framerate-dependent.**

4. **It returns a boolean. True if the ray hits something, false otherwise. You pass it a start position, direction, and max distance: `Physics.Raycast(pos, dir, out hit, distance);`**

5. **Use a raycast or sphere check to detect if the player is grounded. Only allow jumping if isGrounded is true.**

6. **Tags are string labels for GameObjects. Use CompareTag("TagName") to efficiently identify objects in collisions. Avoid using == for tag comparison.**

7. **SetActive(false) disables the object but keeps it in memory (useful for reuse/pooling). Destroy() completely removes it from the scene.**

8. **Force applies constant acceleration over time. Impulse applies instant velocity change. Use Impulse for immediate effects like jumping.**

9. **Add a trigger collider to the item. In OnTriggerEnter(), check if the colliding object is the player. If yes, call Destroy() or SetActive(false).**

10. **Nothing. An infinite mass Rigidbody doesn't move. Set the Rigidbody to "Is Kinematic" if you want to move it directly without physics.**

---
