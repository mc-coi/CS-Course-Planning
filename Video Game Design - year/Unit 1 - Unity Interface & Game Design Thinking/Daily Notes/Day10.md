# Day 10: Script Fundamentals & Accessing GameObjects

**Learning Target:** I can access and modify a GameObject's Transform from a script, and understand the relationship between scripts and GameObjects.

---

## Key Concepts

**this.gameObject** — Reference to the GameObject the script is attached to.

**transform** — Shortcut to the GameObject's Transform component. Allows you to read/write Position, Rotation, Scale.

**GetComponent<T>()** — Retrieve a component from the GameObject. **Example:** `GetComponent<Rigidbody>()` gets the Rigidbody component.

**Public variables** — Visible in the Inspector; can be set without recompiling. **Good for:** tweaking values (speed, health, damage).

**Private variables** — Hidden in Inspector; only accessible within the script. **Good for:** internal tracking.

---

## Common Transform Operations

```csharp
// Reading position
Vector3 myPos = transform.position;
Debug.Log("Current position: " + myPos);

// Writing position
transform.position = new Vector3(5, 2, 0);

// Accessing individual axes
float x = transform.position.x;
transform.position = new Vector3(x + 1, transform.position.y, transform.position.z);

// Rotation (Euler angles in degrees)
transform.rotation = Quaternion.Euler(0, 45, 0);

// Scale
transform.localScale = new Vector3(2, 2, 2);
```

---

## Unity Setup Steps

1. **Create a script:** "MoveMe"
2. **Inside, add a public float variable:**
   ```csharp
   public float moveSpeed = 2.0f;
   ```
3. **In Update(), add:**
   ```csharp
   transform.position = transform.position + Vector3.right * moveSpeed * Time.deltaTime;
   ```
4. **Save and return to Unity**
5. **Create a cube and attach MoveMe script**
6. **Select the cube and look at Inspector:** You'll see "Move Speed" field (default 2.0)
7. **Press Play:** The cube moves right
8. **Stop Play. Change Move Speed to 5.0** and Press Play again: it moves faster
9. **Stop Play. Change to -2.0** and Play: it moves left

---

## Guided Practice

1. **Create a script that moves an object in a circle** (hint: use Mathf.Sin and Mathf.Cos with Time.time)
2. **Attach it to a sphere**
3. **Press Play and watch it orbit**
4. **Stop Play and adjust a public variable (radius or speed)** — see the difference

---

## Practice Problems

**Beginner:** Write a script that moves the object up 1 unit per second. (Use transform.position += Vector3.up * speed * Time.deltaTime)

**Intermediate:** Create a script that rotates an object 45 degrees per second on the Y axis. (Use transform.Rotate(0, angle, 0))

**Challenge:** Write a script that makes an object "bounce" between two positions (e.g., between Y=0 and Y=5) smoothly using Mathf.PingPong(Time.time, maxDistance).

<details>
<summary>💡 Hints</summary>
- Vector3.right = (1, 0, 0), Vector3.up = (0, 1, 0), Vector3.forward = (0, 0, 1)
- Time.deltaTime ensures smooth, frame-rate-independent movement
- Public variables appear in Inspector and can be tweaked without coding
- GetComponent can fail if the component doesn't exist; always check!
- transform.Rotate adds to the current rotation; transform.rotation sets it directly
</details>

<details>
<summary>✅ Sample: Circular Orbit</summary>

```csharp
using UnityEngine;

public class Orbiter : MonoBehaviour
{
    public float radius = 3.0f;
    public float speed = 1.0f;
    
    void Update()
    {
        // Create a circular path
        float x = Mathf.Cos(Time.time * speed) * radius;
        float z = Mathf.Sin(Time.time * speed) * radius;
        transform.position = new Vector3(x, 0, z);
    }
}
```

Attach this to a cube. It orbits around (0,0,0) at the radius you set.

</details>
