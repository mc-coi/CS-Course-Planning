# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is the difference between Update() and LateUpdate()?

2. Explain how Vector3.Lerp() works.

3. What is the difference between GetAxis() and GetKey()?

4. How do you set up a state machine and why is it useful?

5. What is "game feel" and why does it matter?

6. How do you play a sound effect with an AudioSource?

7. Explain the purpose of screen shake and how to implement it.

8. What is caching a component, and why is it important?

9. How do you create a particle effect when the player collects an item?

10. What is the relationship between game feel and player retention?

---

## Answers

1. **Update() is called once per frame. LateUpdate() is called after all Update() methods. Use LateUpdate() for camera follow so the player moves first.**

2. **Lerp(a, b, t) smoothly transitions from a to b. t=0 returns a, t=1 returns b, t=0.5 returns halfway point. Useful for smooth movement and damping.**

3. **GetAxis() returns smooth values from -1 to 1 (good for movement). GetKey() returns true/false (good for instant actions like jumping).**

4. **Use an enum for states and a switch statement to handle each state's logic. State machines organize complex behavior and make transitions clear.**

5. **Game feel is the responsiveness and satisfaction players feel. It comes from smooth controls, visual feedback, audio, and polish. Great game feel makes games feel alive.**

6. **Use `audioSource.PlayOneShot(audioClip);` to play a one-time sound without interrupting other audio.**

7. **Screen shake adds impact to actions (jumping, explosions, impacts). Apply random offsets to the camera for a short time, then restore it.**

8. **Caching is storing a component reference (e.g., in Start()). It's faster than GetComponent() every frame, improving performance.**

9. **Use `Instantiate(particleEffect, collectionPoint, Quaternion.identity);` to spawn the effect at the correct position.**

10. **Great game feel makes games more satisfying and addictive. Players keep playing when actions feel responsive. Poor game feel drives players away.**

---
