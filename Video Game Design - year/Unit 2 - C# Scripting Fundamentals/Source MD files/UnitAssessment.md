# Unit 2 Assessment

**Name:** ________________  
**Date:** ________________  
**Total Points:** 50

---

## Part A: Multiple Choice (10 questions, 1 point each)

**1.** Which data type represents decimal numbers in C#?
- A) int
- B) float
- C) double
- D) decimal

**2.** What does `Time.deltaTime` represent?
- A) Total seconds since game start
- B) Seconds elapsed since last frame
- C) Current frame number
- D) Frame rate in FPS

**3.** Which method runs once per frame during gameplay?
- A) Start()
- B) Awake()
- C) Update()
- D) OnEnable()

**4.** What is the correct syntax for a for loop that runs 10 times?
- A) `for(int i = 0; i <= 10; i++)`
- B) `for(int i = 1; i < 10; i++)`
- C) `for(int i = 0; i < 10; i++)`
- D) `for(int i = 0; i == 10; i++)`

**5.** Which comparison operator is used to check equality?
- A) `=`
- B) `==`
- C) `!=`
- D) `<`

**6.** What does `GetComponent<Rigidbody>()` do?
- A) Creates a new Rigidbody
- B) Retrieves the Rigidbody component from the GameObject
- C) Deletes a Rigidbody
- D) Finds all Rigidbodies in the scene

**7.** How do you access the first element of an array?
- A) `array[1]`
- B) `array[0]`
- C) `array.First()`
- D) `array.Get(0)`

**8.** Which of the following correctly adds an item to a List?
- A) `list.Push("item")`
- B) `list.Add("item")`
- C) `list.Insert("item")`
- D) `list.Append("item")`

**9.** What is the output of `10 % 3`?
- A) 3
- B) 3.33
- C) 1
- D) 0

**10.** String concatenation in C# can be done with which of these?
- A) `"Hello" + " World"`
- B) `$"Hello {variable}"`
- C) Both A and B
- D) Neither

---

## Part B: Short Answer (5 questions, 3 points each)

**11.** Explain the difference between `Input.GetKey()` and `Input.GetKeyDown()`. When would you use each?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**12.** Why is `Time.deltaTime` important for movement? What happens if you don't use it?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**13.** What does `GetComponent<T>()` return if the component doesn't exist? How should you handle this?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**14.** What is the difference between an Array and a List? Name one advantage of each.

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

**15.** Describe the flow of these methods: Start(), Update(), FixedUpdate(). When is each called?

_________________________________________________________________________
_________________________________________________________________________
_________________________________________________________________________

---

## Part C: Coding Challenges (3 questions, 7 points each)

**16. Health System (7 points)**

Write a script that:
- Has public variables for maxHealth and currentHealth (both int)
- Has a `TakeDamage(int amount)` method that reduces health
- Has a `Heal(int amount)` method that increases health (can't exceed max)
- Logs health status after each action
- In Start(), demonstrate: take 25 damage, heal 10, take 50 damage

```csharp
using UnityEngine;

public class HealthSystem : MonoBehaviour
{
    // Your code here
}
```

**17. Enemy Patrol Loop (7 points)**

Write a script that:
- Uses a for loop to simulate 5 enemies
- Each enemy has a "patrol" with 3 waypoints
- Uses nested loops to visit each waypoint
- Logs: "Enemy X: Visiting waypoint Y"
- After all waypoints, logs: "Enemy X: Patrol complete"

```csharp
using UnityEngine;

public class EnemyPatrol : MonoBehaviour
{
    void Start()
    {
        // Your code here
    }
}
```

**18. Input-Controlled Movement (7 points)**

Write a script that:
- Moves a GameObject forward/backward with W/S (5 units/sec)
- Rotates left/right with A/D (90°/sec)
- Displays current position and rotation in Console each frame
- Use Time.deltaTime for frame-independent movement

```csharp
using UnityEngine;

public class PlayerMover : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 90f;
    
    void Update()
    {
        // Your code here
    }
}
```

---

## Answer Key

### Part A: Multiple Choice (1 point each)

| Q | Answer | Q | Answer |
|---|--------|---|--------|
| 1 | B | 6 | B |
| 2 | B | 7 | B |
| 3 | C | 8 | B |
| 4 | C | 9 | C |
| 5 | B | 10 | C |

---

### Part B: Short Answer (3 points each)

**11.** `GetKey()` returns true every frame while the key is held (continuous). `GetKeyDown()` returns true only on the first frame the key is pressed (once). Use `GetKey()` for continuous actions (walking, holding a button). Use `GetKeyDown()` for one-time actions (jumping, shooting, picking up items). (1 point: GetKey, 1 point: GetKeyDown, 1 point: examples)

**12.** `Time.deltaTime` is the time elapsed since the last frame. It makes movement **frame-rate independent**: the same physical distance is covered regardless of FPS. Without it, movement speed varies with frame rate (faster machines move faster, inconsistent gameplay). Always multiply movement by `Time.deltaTime`. (1 point: definition, 1 point: frame-independence, 1 point: consequence)

**13.** `GetComponent<T>()` returns `null` if the component doesn't exist. You should check for null before using it:
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
if(rb != null)
{
    rb.velocity = new Vector3(10, 0, 0);
}
```
(1 point: returns null, 1 point: null check, 1 point: code example)

**14.** **Array:** Fixed size, declared with `[]`, efficient memory. **List:** Dynamic size, declared with `List<T>`, flexible. Advantages: Array is fast/simple for known counts; List is flexible for unknown/changing counts. (1 point: Array characteristics, 1 point: List characteristics, 1 point: advantages)

**15.** **Start()** is called once on the first frame before any Update(). **Update()** is called every frame (input, game logic). **FixedUpdate()** is called at a fixed timestep (physics calculations). Order: Awake → Start → Update → FixedUpdate → LateUpdate. (1 point per method's timing)

---

### Part C: Coding Challenges (7 points each)

**16. Health System**

```csharp
using UnityEngine;

public class HealthSystem : MonoBehaviour
{
    public int maxHealth = 100;
    public int currentHealth;
    
    void Start()
    {
        currentHealth = maxHealth;
        
        TakeDamage(25);  // 75/100
        Heal(10);        // 85/100
        TakeDamage(50);  // 35/100
    }
    
    public void TakeDamage(int amount)
    {
        currentHealth -= amount;
        if(currentHealth < 0) currentHealth = 0;
        Debug.Log("Health: " + currentHealth + "/" + maxHealth);
    }
    
    public void Heal(int amount)
    {
        currentHealth += amount;
        if(currentHealth > maxHealth) currentHealth = maxHealth;
        Debug.Log("Health: " + currentHealth + "/" + maxHealth);
    }
}
```

**Grading:** 2 pts (methods), 2 pts (logic), 2 pts (logging), 1 pt (syntax)

**17. Enemy Patrol**

```csharp
using UnityEngine;

public class EnemyPatrol : MonoBehaviour
{
    void Start()
    {
        for(int enemy = 0; enemy < 5; enemy++)
        {
            for(int waypoint = 0; waypoint < 3; waypoint++)
            {
                Debug.Log("Enemy " + enemy + ": Visiting waypoint " + waypoint);
            }
            Debug.Log("Enemy " + enemy + ": Patrol complete");
        }
    }
}
```

**Grading:** 2 pts (nested loops), 2 pts (logging), 2 pts (correct output), 1 pt (syntax)

**18. Input Movement**

```csharp
using UnityEngine;

public class PlayerMover : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 90f;
    
    void Update()
    {
        // Movement
        if(Input.GetKey(KeyCode.W))
            transform.position += transform.forward * moveSpeed * Time.deltaTime;
        if(Input.GetKey(KeyCode.S))
            transform.position -= transform.forward * moveSpeed * Time.deltaTime;
        
        // Rotation
        if(Input.GetKey(KeyCode.A))
            transform.Rotate(0, -rotateSpeed * Time.deltaTime, 0);
        if(Input.GetKey(KeyCode.D))
            transform.Rotate(0, rotateSpeed * Time.deltaTime, 0);
        
        // Log position and rotation
        Debug.Log("Position: " + transform.position + " | Rotation: " + transform.eulerAngles);
    }
}
```

**Grading:** 2 pts (movement), 2 pts (rotation), 2 pts (Time.deltaTime usage), 1 pt (logging)

---

## Scoring Rubric

| Section | Points | Criteria |
|---------|--------|----------|
| Part A (MC) | 10 | 1 point per correct |
| Part B (SA) | 15 | 3 points per question |
| Part C (Code) | 21 | 7 points per challenge (see above) |
| **Total** | **50** | Passing: 35+ (70%) |

---

## Remediation & Next Steps

**If score < 35 (70%):**
- Review weak sections in daily notes
- Redo UnitPractice problems
- Schedule office hours for targeted help

**If score 35-42 (70-84%):**
- Good progress; some gaps remain
- Focus on Problem Areas before next unit

**If score > 42 (84%+):**
- Strong mastery achieved
- Ready for Unit 3 (Advanced Scripting/Systems)
- Consider advanced challenges for enrichment

