# Vocabulary & Quick Reference

## Key Terms

| Term | Definition |
|------|-----------|
| **GetAxis()** | Returns smooth float input from -1 to 1 |
| **GetAxisRaw()** | Returns -1, 0, or 1 (no smoothing) |
| **Input Manager** | Configuration panel for input axes |
| **LateUpdate()** | Called after Update(); perfect for camera |
| **Vector3.Lerp()** | Smooth interpolation between two vectors |
| **Damping** | Smoothness factor for following (0-1) |
| **Game Feel** | Responsiveness and satisfaction of interaction |
| **Juice** | Polish and feedback that enhances feel |
| **State Machine** | System for managing and transitioning between states |
| **Enum** | Type listing possible states or values |
| **Modular** | Code organized into focused, reusable components |
| **Particle Effect** | Visual effect made of many small particles |
| **Screen Shake** | Camera movement simulating impact |

## Key Syntax

### Input Quick Reference

```csharp
// Smooth axis input (0 to 1 range, accelerates)
float horizontal = Input.GetAxis("Horizontal");     // A/D, Left Stick
float vertical = Input.GetAxis("Vertical");         // W/S, Left Stick
float mouseX = Input.GetAxis("Mouse X");            // Mouse X movement
float mouseY = Input.GetAxis("Mouse Y");            // Mouse Y movement

// Raw axis (instant -1/0/1)
float hRaw = Input.GetAxisRaw("Horizontal");

// Discrete input
if (Input.GetKeyDown(KeyCode.Space))    // Pressed this frame
if (Input.GetKey(KeyCode.Space))        // Held down
if (Input.GetKeyUp(KeyCode.Space))      // Released this frame

// Mouse
if (Input.GetMouseButtonDown(0))        // Left click
if (Input.GetMouseButton(1))            // Right hold
```

### Camera & Lerp Quick Reference

```csharp
// Smooth camera follow
void LateUpdate()
{
    Vector3 targetPos = player.position + offset;
    transform.position = Vector3.Lerp(transform.position, targetPos, dampingSpeed);
}

// Look at target
transform.LookAt(target);

// Smooth color transition
Color targetColor = Color.blue;
renderer.material.color = Color.Lerp(renderer.material.color, targetColor, Time.deltaTime);

// Smooth value interpolation
currentValue = Mathf.Lerp(currentValue, targetValue, dampingSpeed);
```

### State Machine Quick Reference

```csharp
public enum PlayerState { Idle, Running, Jumping, Falling }
private PlayerState currentState = PlayerState.Idle;

void Update()
{
    switch (currentState)
    {
        case PlayerState.Idle:
            // Idle logic
            if (hasInput) currentState = PlayerState.Running;
            break;

        case PlayerState.Running:
            // Running logic
            if (!hasInput) currentState = PlayerState.Idle;
            break;

        // ... more states
    }
}
```

### Game Feel Quick Reference

```csharp
// Play particle effect
Instantiate(particles, transform.position, Quaternion.identity);

// Play sound
audioSource.PlayOneShot(jumpClip);

// Screen shake
StartCoroutine(ShakeScreen(duration, strength));

// Visual feedback (scaling)
StartCoroutine(PopAnimation(gameObject, targetScale, duration));

// Color feedback
renderer.material.color = Color.red;
Invoke("ResetColor", 0.2f);
```

---

## Common Mistakes & How to Fix Them

| Mistake | What Happens | Fix |
|---------|--------------|-----|
| Camera movement is jerky | Using Update() instead of LateUpdate() | Always update camera in LateUpdate(), after player has moved |
| GetAxis() doesn't work | Wrong axis name (case-sensitive) | Check Input Manager for exact names: "Horizontal", "Vertical" |
| Particle effects don't show | Particle system set to stopped or duration = 0 | Set autoplay = true; duration > 0 |
| Audio doesn't play | AudioSource missing or volume = 0 | Add AudioSource component; check volume slider |
| State machine behavior is erratic | Transitions happen every frame instead of once | Use conditions that persist, or use GetKeyDown() for one-time events |
| Camera clips through objects | Near plane too large or far plane too small | Adjust camera's Near and Far planes in Inspector |
| Smooth movement overshoots | Damping value too high (> 0.3) | Keep Lerp damping between 0.05 and 0.2 for smooth follow |
| Multiple updates to same component | Code spread across multiple scripts fighting each other | Consolidate or use a single source of truth |
| Input not responsive | Reading input in FixedUpdate | Always read input in Update(), then apply in FixedUpdate() |
| Screen shake is continuous | Shake timer doesn't reset properly | Reset timer = 0 after shake ends |
