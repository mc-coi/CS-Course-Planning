# Day 1: 2D vs 3D—Project Setup

**Learning Target:** I can set up a 2D project and understand 2D-specific tools.

---

## Key Concepts

**2D Coordinates**: Only X (horizontal) and Y (vertical); Z determines render order (layer depth).

**Orthographic Camera**: Projects flat 2D view (vs. Perspective 3D). Set camera to Orthographic.

**Physics2D**: Separate physics engine optimized for 2D (Rigidbody2D, Collider2D).

**Sorting Layer**: Controls render order (back to front). Multiple layers prevent z-fighting.

---

## Code Example

```csharp
using UnityEngine;

public class Player2D : MonoBehaviour
{
    private Rigidbody2D rb;
    private Vector2 moveDirection;
    
    private void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        // 2D input: only X and Y
        moveDirection = new Vector2(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"));
    }

    private void FixedUpdate()
    {
        // Physics in 2D: use velocity (not position)
        rb.velocity = moveDirection * 5f;
    }
}
```

---

## Unity Setup Steps

1. **Create 2D Project** (or convert existing):
   - Verify camera is set to Orthographic mode
   - Camera → Projection: Orthographic
   - Camera → Size: 5-10 (controls zoom level)

2. **Create Sprite Gameobject**:
   - Right-click Hierarchy → 2D Object → Sprites → Square
   - Add SpriteRenderer component

3. **Add Physics2D**:
   - GameObject → Add Component → Rigidbody2D
   - Set Body Type: Dynamic (for moving), Kinematic (for control)
   - Add Collider2D: BoxCollider2D or CircleCollider2D

4. **Test Movement**:
   - Attach Player2D script
   - Press Play, use arrow keys to move

---

## Guided Practice

1. Create a simple player square that moves with arrow keys
2. Create a floor platform (static Rigidbody2D)
3. Make player fall and land on floor

---

## Practice Problems

**Beginner:** Set up a 2D scene with a player sprite and a platform sprite. List the steps.

**Intermediate:** Create a script that moves a Rigidbody2D using AddForce() instead of velocity.

**Challenge:** Implement jump mechanic: player falls due to gravity, can jump once while grounded.

<details><summary>✅ Answers</summary>
**Challenge:**
```csharp
private bool isGrounded = false;

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space) && isGrounded)
        rb.velocity = new Vector2(rb.velocity.x, 5f);
}

void OnCollisionStay2D(Collision2D col)
{
    isGrounded = true;
}

void OnCollisionExit2D(Collision2D col)
{
    isGrounded = false;
}
```
</details>
