# Day 13: Prefabs (Part 1)

**Learning Target:** I can create prefabs, understand the prefab system, and instantiate prefabs from scripts.

---

## Key Concepts

**Prefab** — A template/blueprint for a GameObject that can be reused and saved. When you instantiate a prefab, you create a copy.

**Prefab Instance** — A copy of a prefab in the scene. Linked to the original prefab; changes to the prefab apply to all instances.

**Prefab Variant** — A prefab that inherits from another prefab but can override specific properties (advanced).

**Instantiate()** — C# method that creates a copy of a prefab at runtime (during Play mode).

**Prefab vs Scene GameObject** — A GameObject in a scene is unique to that scene. A Prefab exists in the Project and can be used in multiple scenes.

---

## Creating and Using Prefabs

```csharp
// Drag a prefab into a public variable to reference it
public GameObject cubePrefab;

void Start()
{
    // Create an instance at position (0, 1, 0)
    Instantiate(cubePrefab, new Vector3(0, 1, 0), Quaternion.identity);
}
```

---

## Unity Setup Steps

1. **Create a cube in your scene** and customize it:
   - Scale: (1, 2, 0.5)
   - Material: Red
   - Add a Rigidbody
   - Position: (0, 3, 0)
2. **Drag this cube into the Project window** (Assets folder or a "Prefabs" subfolder)
3. **A new prefab file appears** — this is your blueprint
4. **Delete the cube from the scene** (it's just an instance now; the prefab still exists)
5. **Drag the prefab from Project back into the Scene** — a new instance appears
6. **Duplicate (Cmd/Ctrl+D) the instance** — another copy appears
7. **Select the prefab in the Project** and modify its Material color
8. **All instances in the scene update** (they inherit from the prefab)

---

## Guided Practice

1. **Create a "Cube" prefab** (red, with Rigidbody)
2. **Create a "Sphere" prefab** (blue, with Rigidbody)
3. **In the scene, place 3 Cube prefabs and 2 Sphere prefabs**
4. **Select the Cube prefab in the Project** and change its color to green
5. **All cube instances turn green** — confirm the prefab system works
6. **Create a script that instantiates a sphere prefab every time you click** (pseudocode in practice)

---

## Practice Problems

**Beginner:** Create a simple cube prefab with a custom material. Drag it into the scene 5 times. Verify they're all instances of the same prefab.

**Intermediate:** Create 3 prefabs (cube, sphere, cylinder), each with different materials. Use them to build a decorative scene.

**Challenge:** Create a prefab with a script attached. Instantiate it 10 times in the scene. Modify the prefab's script and verify all instances run the updated behavior.

<details>
<summary>💡 Hints</summary>
- Drag a GameObject from Hierarchy to Project to create a prefab
- Instances in the scene show a blue name (vs white for unique GameObjects)
- You can "unpack" an instance (Right-click → Prefab → Unlink/Unpack) to make it independent
- Modifying an instance doesn't affect the prefab; modifying the prefab affects all instances
- Prefabs can be nested (a prefab containing other prefab instances)
</details>

<details>
<summary>✅ Sample: Simple Prefabs</summary>

1. Create a cube, customize it (red material, scale 1,1,1), save as "RedCube" prefab
2. Create a sphere, customize it (blue material), save as "BlueSphere" prefab
3. Drag both into the scene multiple times to create instances
4. In the Project, double-click the RedCube prefab to edit it directly
5. Change the material to yellow — all RedCube instances turn yellow

</details>
