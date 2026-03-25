# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What is the singleton pattern and why use GameManager as a singleton?

2. Explain the health component design and why it's modular.

3. What is a state machine and how does enemy AI use it?

4. How do you calculate distance between two objects?

5. What does Time.timeScale do and how is it used for pausing?

6. Explain the DontDestroyOnLoad() function.

7. How do you implement a win condition in a game?

8. What is an attack cooldown and how do you implement it?

9. Describe the complete game state flow from menu to game over.

10. How do you give feedback when an entity takes damage?

---

## Answers

1. **A singleton has only one instance globally accessible.** GameManager is a singleton so you can access `GameManager.instance.AddScore()` from anywhere without storing references.

2. **Health component tracks damage independently.** It's modular because you can attach it to any entity (player, enemy, destructible). Changes to health logic affect all entities, maintaining consistency.

3. **A state machine cycles through named states (Patrol, Chase, Attack) with transition rules.** Enemy AI uses states to organize behavior logically. Each state has its own update logic and transitions happen when conditions are met (like distance checks).

4. **Use `Vector3.Distance(objectA.position, objectB.position);`** which returns a float distance in units.

5. **Time.timeScale controls game speed.** Setting it to 0 freezes the game (Time.deltaTime becomes 0). Set to 1 to resume. Essential for pause functionality.

6. **It prevents a GameObject from being destroyed when loading a new scene.** Used for persistent managers like GameManager so the singleton persists across levels.

7. **Define win criteria (e.g., `enemiesRemaining == 0`).** Check each frame in the state machine. When true, call Win() which displays win screen and saves high score.

8. **Attack cooldown prevents attacking too frequently.** Use `if (Time.time > lastAttackTime + cooldown)` to check if enough time passed since last attack.

9. **Menu → Play (start game) → Gameplay → Pause (optional) → Resume → Win/Lose → Gameover → Menu**

10. **Visual (sprite flash, screen shake), Audio (damage sound), Physical (knockback), UI (health bar decrease).** Combine multiple feedback types for better game feel.
