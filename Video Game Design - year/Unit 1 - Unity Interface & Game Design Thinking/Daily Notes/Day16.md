# Day 16: Play Mode vs Edit Mode & Scene Persistence

**Learning Target:** I can distinguish between Play Mode and Edit Mode, understand what persists, and use this knowledge to debug effectively.

---

## Key Concepts

**Play Mode Changes Are Temporary** — Any modification during Play (moving objects, changing values, instantiating objects) reverts when you press Stop.

**Scene Serialization** — Unity saves scenes to disk. Only changes in Edit Mode save.

**Undo/Redo** — Works in Edit Mode only. In Play Mode, pressing Stop reverts to the last Edit Mode state.

**Live Editing** — Some engines allow editing while playing; Unity does not (intentional design choice for clarity).

---

## What Persists vs What Reverts

| Change | Persists? | Reason |
|--------|-----------|--------|
| Move object in Play | No | Play Mode is sandboxed |
| Change public variable | No | Values reset to saved defaults |
| Instantiate objects | No | Only in-game copies exist |
| Create new scene | Yes | You manually saved it |
| Modify prefab (in Project) | Yes | It's a permanent asset |
| Undo in Play Mode | No | Undo only works in Edit Mode |

---

## Unity Setup Steps

1. **Create a cube and note its position** (e.g., X=0, Y=0, Z=0)
2. **Create a script** with a public float variable:
   ```csharp
   public float myValue = 42;
   ```
3. **Attach to the cube** and note myValue = 42 in Inspector
4. **Press Play**
5. **In the cube's Inspector (during Play), change myValue to 100**
6. **Move the cube with the Gizmo**
7. **Press Stop**
8. **Look at Inspector:** myValue is 42 again; position is reset

---

## Guided Practice

1. **Create a scene with 5 cubes** positioned in a specific pattern
2. **Press Play and rearrange them** (move them around)
3. **Press Stop** — they return to original positions
4. **Make a script** that instantiates 10 spheres when you press Space
5. **Press Play and press Space** — 10 spheres appear
6. **Press Stop** — all spheres vanish (they only existed in Play Mode)

---

## Practice Problems

**Beginner:** Demonstrate the difference: modify an object in Play Mode, verify it reverts on Stop. Modify a prefab, verify it persists.

**Intermediate:** Create a scene with a script that spawns objects and modifies their properties. Explain which changes persist and why.

**Challenge:** Write a script that tracks whether it's in Play Mode. Log a message in Start() and Update() with Time.timeScale info. Use this to understand the Play vs Edit distinction.

<details>
<summary>💡 Hints</summary>
- EditorApplication.isPlayingOrWillChangePlaymode (requires "using UnityEditor") can detect Play Mode
- Time.timeScale = 0 pauses the game (Time.deltaTime becomes 0)
- Prefabs in the Project are not affected by Play Mode; only instances in the scene are
- If you need persistent changes, save them to disk (beyond scope of this unit)
- Using Undo (Cmd/Ctrl+Z) during Play Mode doesn't work; Save your scene before experimenting
</details>

<details>
<summary>✅ Sample: Play Mode Logger</summary>

```csharp
using UnityEngine;

public class PlayModeLogger : MonoBehaviour
{
    void Start()
    {
        Debug.Log("Started. Time.timeScale = " + Time.timeScale);
    }
    
    void Update()
    {
        // This runs only in Play Mode (Time.timeScale > 0)
        Debug.Log("Frame " + Time.frameCount);
    }
}
```

In Play Mode: Start runs, Update runs every frame.
In Edit Mode: Nothing runs.
After Press Stop: Back to Edit Mode; script is "dormant."

</details>
