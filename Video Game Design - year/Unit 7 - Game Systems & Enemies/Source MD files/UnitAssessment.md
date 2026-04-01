# Unit 7 Assessment: Game Systems & Enemies

**Total Points: 40**

---

## Part A: Multiple Choice (1 point each)

1. FSM stands for:
   - A) Fast State Memory B) Finite State Machine C) Fixed State Motion D) Formatted System Module

2. Object pooling avoids:
   - A) Physics B) Collisions C) Destroy() overhead D) Performance gains

3. Which detects player proximity for chase behavior?
   - A) Physics.Raycast B) Physics2D.OverlapCircle C) GetDistance() D) Tag comparison

4. Inventory item limit is called:
   - A) Quantity B) Stack limit C) Max count D) Item cap

5. JSON serialization is better than PlayerPrefs for:
   - A) Small data B) Complex data C) High scores D) Settings

6. DontDestroyOnLoad persists across:
   - A) Frames B) Scenes C) Levels D) Quit

7. What does Wave Spawner do?
   - A) Moves enemies B) Spawns multiple waves C) Detects waves D) Creates animations

8. Health component should:
   - A) Be player-only B) Be reusable (on many objects) C) Hold weapon data D) Control input

9. ScriptableObject is created:
   - A) In script only B) In Editor menu C) At runtime D) In prefabs

10. Event system provides:
    - A) Game events B) Loose coupling C) Communication D) All of above

---

## Part B: Short Answer (2 points each)

1. Explain the three main states in a basic enemy FSM and when transitions occur.

2. Why is object pooling better than Instantiate/Destroy for bullets?

3. What's the advantage of using an IDamageable interface instead of calling Health directly?

4. How does difficulty scaling work in a wave spawner?

5. Why use ScriptableObject for item data instead of hardcoding values?

---

## Part C: Coding Challenges (≈7 points each)

**Challenge 1: Enemy FSM**
Create an enemy with Idle and Chase states. Chase activates when player is within 10 units. Return to Idle if player leaves 15 unit range.

```csharp
// Your solution
```

**Challenge 2: Health & Damage**
Create a Health component and an IDamageable interface. Enemy takes 10 damage on collision with bullets.

```csharp
// Your solution
```

**Challenge 3: Save/Load System**
Save player position, health, and score to JSON. Load on game start.

```csharp
// Your solution
```

---

## Answer Key

### Part A
1. B | 2. C | 3. B | 4. B | 5. B | 6. B | 7. B | 8. B | 9. B | 10. D

### Part B

**1. Three Main States:**
- Idle: Waiting, no input. Transition to Chase if player detected
- Chase: Following player. Transition to Attack if close, Idle if player lost
- Attack: Dealing damage. Transition to Chase if player moves away

**2. Object Pooling:**
Instantiate/Destroy are expensive (garbage collection). Pooling reuses objects, eliminates allocation overhead, smoother gameplay with many bullets.

**3. IDamageable Interface:**
Decouples systems. Bullets don't need to know about Health component. Any object with IDamageable can take damage (enemy, player, destructible wall).

**4. Difficulty Scaling:**
Each wave spawns more enemies: 5 + (wave * 2). Or increase enemy speed, health. Player must improve skills or die.

**5. ScriptableObject for Items:**
Designer can create items without coding. Easy to balance (change values in Inspector). Items are data, not code. Reusable across many game instances.

### Part C

**Challenge 1:**
```csharp
public class Enemy : MonoBehaviour
{
    enum State { Idle, Chase }
    private State state = State.Idle;
    private Transform player;
    private float chaseRange = 10f;
    private float returnRange = 15f;
    
    void Update()
    {
        float dist = Vector3.Distance(transform.position, player.position);
        
        if (state == State.Idle && dist < chaseRange)
            state = State.Chase;
        else if (state == State.Chase && dist > returnRange)
            state = State.Idle;
        
        if (state == State.Chase)
        {
            Vector3 dir = (player.position - transform.position).normalized;
            transform.position += dir * 3f * Time.deltaTime;
        }
    }
}
```

**Challenge 2:**
```csharp
public interface IDamageable { void TakeDamage(float damage); }

public class Health : MonoBehaviour, IDamageable
{
    public float maxHealth = 100;
    private float current;
    
    void Start() => current = maxHealth;
    public void TakeDamage(float damage)
    {
        current -= damage;
        if (current <= 0) Destroy(gameObject);
    }
}

public class Bullet : MonoBehaviour
{
    void OnTriggerEnter2D(Collider2D col)
    {
        IDamageable dmg = col.GetComponent<IDamageable>();
        if (dmg != null) dmg.TakeDamage(10);
        Destroy(gameObject);
    }
}
```

**Challenge 3:**
```csharp
[System.Serializable]
public class GameState
{
    public Vector3 playerPos;
    public float health;
    public int score;
}

public class SaveSystem : MonoBehaviour
{
    public void SaveGame(Vector3 pos, float hp, int pts)
    {
        GameState state = new GameState { playerPos = pos, health = hp, score = pts };
        string json = JsonUtility.ToJson(state);
        System.IO.File.WriteAllText("save.json", json);
    }
    
    public GameState LoadGame()
    {
        string json = System.IO.File.ReadAllText("save.json");
        return JsonUtility.FromJson<GameState>(json);
    }
}
```
