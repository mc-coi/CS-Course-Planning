# Unit Practice Bank

1. **Rigidbody Exploration:** Create three objects with different masses. Apply the same force to all three. Which accelerates fastest? Explain why.

2. **Collision Tags:** Create a scene with multiple GameObjects of different types. Tag them appropriately (Enemy, Coin, Wall, etc.). Use OnCollisionEnter() to detect each type.

3. **Trigger Volume:** Create a large trigger zone that counts how many objects are inside it. Print the count to the Console.

4. **Raycast Visualization:** Write a script that casts raycasts in multiple directions and uses Debug.DrawRay() to visualize them in the Scene view.

5. **Mass and Gravity:** Create two objects with the same size but different mass values. Drop them from the same height. Time how long they take to fall. What do you observe?

6. **Friction Simulation:** Without using the Rigidbody's drag, implement friction manually in FixedUpdate() by reducing velocity each frame.

7. **Bouncing Ball:** Create a ball that bounces realistically using Rigidbody physics. Adjust mass, drag, and material properties until it feels right.

8. **Distance-Based Damage:** Create a script that damages the player based on how fast they're moving (velocity.magnitude). Faster impacts = more damage.

9. **Layered Collision:** Set up two GameObjects on different physics layers that don't collide with each other. Use Physics.IgnoreLayerCollision().

10. **Trigger Counter:** Create a trigger that counts how many times objects have passed through it. Print the count each time.

11. **Velocity Limiter:** Implement a maximum speed limit for a moving Rigidbody. If velocity exceeds the limit, clamp it.

12. **Overlap Detection:** Use Physics.OverlapSphere() to detect all objects within a radius of the player.

13. **Force Modes:** Experiment with ForceMode.Force vs ForceMode.Impulse. Explain the difference and when to use each.

14. **Object Pooling:** Instead of Destroy(), use SetActive() to reuse coins. When a coin is collected, disable it instead of destroying it.

15. **Jump Visualization:** Write a script that displays the remaining jump height in the Console as the player jumps (showing velocity.y each frame).

---
