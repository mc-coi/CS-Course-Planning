# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is a Sprite Renderer and what does it do?

2. Explain the difference between Tilemap and individual sprites for level design.

3. How do you implement grounded detection in 2D?

4. What is the difference between animation clips and the Animator component?

5. How do you create a prefab and why is it useful?

6. Explain what a Sprite Sheet is and how to use it in Unity.

7. How do you control which animation plays using the Animator?

8. What is object pooling and when should you use it?

9. How do you flip a 2D sprite based on movement direction?

10. Describe the components needed for a complete 2D platformer character.

---

**Answers:**

1. **A Sprite Renderer displays a 2D sprite on a GameObject.** It controls which sprite is displayed, color, sorting order, and flip state.

2. **Tilemaps use a grid of repeated tiles for efficient level building.** Individual sprites are placed manually. Tilemaps are better for large levels; individual sprites for unique objects.

3. **Use Physics2D.Raycast() downward from the player.** If it hits a collider, the player is grounded.

4. **Animation clips are sequences of frames.** The Animator plays clips and manages transitions between them based on parameters and conditions.

5. **Build a GameObject, drag it to the Project folder.** Prefabs are useful because you can spawn multiple copies and changes to the prefab affect all instances.

6. **A Sprite Sheet is an image with multiple sprites in a grid.** Set Texture Type to "Sprite (2D and UI)", adjust slice settings, and separate individual sprites.

7. **Set animator parameters (bool, float, trigger) that trigger transitions:** `animator.SetBool("IsRunning", true);`

8. **Pre-creating and reusing objects instead of instantiating/destroying.** Use it when spawning many objects frequently (bullets, enemies, particles).

9. **`spriteRenderer.flipX = (moveDirection.x < 0);`**

10. **Sprite Renderer (visual), Rigidbody2D (physics), Collider2D (collision), Animator (animation), and a script controlling input/movement.**

---
