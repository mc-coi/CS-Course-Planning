# Day 6: Methods & Functions

**Learning Target:** I can write and call methods with parameters and return types.

## Key Concepts

- **Method:** A block of code that performs a specific task
- **Method Signature:** Defines the return type, name, and parameters
- **void:** A method that doesn't return a value
- **Return Type:** The type of value the method returns (int, float, string, bool)
- **Parameter:** A value passed to a method
- **Calling a Method:** Executing the method by writing its name with parentheses
- **Local Variables:** Variables declared inside a method; only exist while the method runs

Methods organize code into reusable blocks. Every method has:
1. **Access Modifier:** public, private, etc.
2. **Return Type:** void (no return) or a specific type (int, float, bool, etc.)
3. **Method Name:** Descriptive name using PascalCase (e.g., CalculateDamage)
4. **Parameters:** Optional inputs, enclosed in parentheses
5. **Body:** The code that runs when the method is called

**Example:**
```
public void Jump(float force)
{
    // This method accepts one parameter: force
    // And doesn't return a value (void)
}

public int Add(int a, int b)
{
    // This method accepts two parameters
    // And returns an int (the sum)
    return a + b;
}
```

Methods should have a single responsibility. If a method does too much, break it into smaller methods. This makes code easier to test and reuse.

## Code Examples

```csharp
using UnityEngine;

public class Combat : MonoBehaviour
{
    public int baseAttackDamage = 10;
    private int currentHealth = 50;

    void Start()
    {
        // Call the TakeDamage method to test it
        TakeDamage(25);
    }

    // A method that takes a parameter and modifies health
    public void TakeDamage(int damageAmount)
    {
        currentHealth -= damageAmount;
        Debug.Log("Took " + damageAmount + " damage. Health: " + currentHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    // A method that calculates and returns a damage value
    public int CalculateDamage(int enemyDefense)
    {
        int damage = baseAttackDamage - enemyDefense;
        // Ensure damage is at least 1
        if (damage < 1)
            damage = 1;
        return damage;
    }

    // A method with no parameters and no return value
    private void Die()
    {
        Debug.Log("Player died!");
        Destroy(gameObject); // Remove this GameObject from the scene
    }

    void Update()
    {
        // Call CalculateDamage with an enemy defense value
        int finalDamage = CalculateDamage(5);
        Debug.Log("Final damage: " + finalDamage);
    }
}
```

## Guided Practice

1. Create a script called "MethodPractice"
2. Write a method called `Greet()` with no parameters that prints a greeting
3. Write a method called `Add()` that takes two integers and returns their sum
4. Call both methods from Start() and print the results
5. Attach the script to a GameObject and run the scene

## Practice Problems

**Problem 1 — Beginner:** Write a method called AddNumbers that takes two integers as parameters and returns their sum.

**Problem 2 — Intermediate:** Write a script that has a method `CalculateArea()` that takes width and height and returns the area of a rectangle.

**Problem 3 — Challenge:** Write a method called `GetHealthPercentage()` that returns the current health as a percentage of max health. Call it repeatedly and observe the values.

<details>
<summary>Hints</summary>

**Problem 1:** The method signature should be: `public int AddNumbers(int a, int b)` Inside, add the two numbers and return the result.

**Problem 2:** Area = width * height. The method should be: `public float CalculateArea(float width, float height)` Return the result.

**Problem 3:** Health percentage = (currentHealth / maxHealth) * 100. Make sure to cast to float to avoid integer division issues.
</details>

<details>
<summary>Sample Answers</summary>

**Problem 1:**
```csharp
public int AddNumbers(int a, int b)
{
    return a + b;
}
```

**Problem 2:**
```csharp
public float CalculateArea(float width, float height)
{
    return width * height;
}
```

**Problem 3:**
```csharp
public float GetHealthPercentage()
{
    return (currentHealth / (float)maxHealth) * 100f;
}
```
</details>
