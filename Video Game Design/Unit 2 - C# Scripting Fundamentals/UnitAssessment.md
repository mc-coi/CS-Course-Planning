# Unit Assessment Prep

**Review Questions:** Answer these to prepare for the unit assessment.

1. What are the five common data types in C#?

2. What is the difference between public and private variables?

3. Explain the purpose of Time.deltaTime.

4. What is the difference between Input.GetKeyDown() and Input.GetKey()?

5. Write a simple if/else statement that checks if a variable x is positive.

6. What is a method, and why are they useful?

7. How do you calculate the distance between two GameObjects?

8. What does Vector3.normalized do?

9. Explain the difference between transform.Translate() and setting transform.position directly.

10. What is the purpose of GetComponent() and when would you use it?

---

**Answers:**

1. int (whole numbers), float (decimals), string (text), bool (true/false), and Vector3 (3D position/direction).

2. Public variables are visible and editable in the Inspector. Private variables are hidden and only accessible within the script. Use public for values you want to tune in the editor.

3. Time.deltaTime is the time elapsed since the last frame. It makes movement frame-rate independent: moving at 5 * Time.deltaTime units per frame moves at 5 units per second regardless of frame rate.

4. GetKeyDown() returns true only the frame a key is pressed (one-time action). GetKey() returns true while the key is held down (continuous action).

5.
```csharp
if (x > 0)
    Debug.Log("Positive");
else
    Debug.Log("Not positive");
```

6. A method is a reusable block of code that performs a specific task. Methods organize code, reduce repetition, and make programs easier to understand and maintain.

7.
```csharp
Vector3 direction = objectB.transform.position - objectA.transform.position;
float distance = direction.magnitude;
```

8. It returns a unit vector (length = 1) pointing in the same direction. Useful for finding direction without distance: `Vector3 direction = (targetPos - myPos).normalized;`

9. Translate() moves relative to the object's current orientation. Setting position directly moves to an absolute world position. Translate is more intuitive for "forward" movement.

10. GetComponent() accesses other components on the same GameObject (e.g., GetComponent<Renderer>()). Use it when you need to modify another component from your script.

---
