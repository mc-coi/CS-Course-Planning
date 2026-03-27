# Day 8: Dynamic Button Lists & Menu Navigation

**Learning Target:** I can create dynamic button lists and navigate between menus.

---

## Key Concepts

**Dynamic Buttons**: Create buttons at runtime based on data (inventory items, level select, etc.).

**Menu Stack**: Track which menu is open so you can back out. Use a Stack or simple state tracking.

**Highlighting**: Remember which button was last selected for keyboard/gamepad navigation.

**Prefabs**: Create a button prefab template, then instantiate copies at runtime.

---

## Code Example

```csharp
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class MenuNavigator : MonoBehaviour
{
    public Transform buttonContainer;      // Parent for buttons
    public GameObject buttonPrefab;        // Button template
    private Stack<GameObject> menuStack = new Stack<GameObject>();

    public void PopulateMenu(string[] items)
    {
        // Clear old buttons
        foreach (Transform child in buttonContainer)
            Destroy(child.gameObject);

        // Create button for each item
        foreach (string item in items)
        {
            GameObject buttonGO = Instantiate(buttonPrefab, buttonContainer);
            Button btn = buttonGO.GetComponent<Button>();
            TextMeshProUGUI btnText = buttonGO.GetComponentInChildren<TextMeshProUGUI>();
            
            btnText.text = item;
            btn.onClick.AddListener(() => OnItemSelected(item));
        }
    }

    public void OnItemSelected(string item)
    {
        Debug.Log($"Selected: {item}");
    }

    public void BackToMenu()
    {
        if (menuStack.Count > 0)
        {
            GameObject currentMenu = menuStack.Pop();
            currentMenu.SetActive(false);
        }
    }
}
```

---

## Unity Setup Steps

1. **Create a Button Prefab**:
   - Create a Button in the scene (UI → Button)
   - Add TextMeshPro child with text "Item Template"
   - Drag the Button from Hierarchy into a Prefabs folder
   - Delete from Hierarchy

2. **Create Menu Manager**:
   - Right-click Canvas → Create empty → name "MenuContainer"
   - Attach `MenuNavigator.cs` script
   - In Inspector:
     - Assign Canvas as the button container
     - Assign Button prefab reference

3. **Test Dynamic Creation**:
   - Create a test script that calls `PopulateMenu()`
   - Play scene, verify buttons appear

4. **Add Back Button**:
   - Create a Button that calls `BackToMenu()`
   - Position it at top of screen

---

## Guided Practice

1. **Create a Level Select Menu**:
   - Dynamically create buttons for "Level 1" through "Level 5"
   - Each button should log which level was selected
   - Add a Back button that exits the menu

2. **Highlight System**:
   - Track which button was last selected
   - Restore highlight when returning to this menu
   - Use `EventSystem.current.SetSelectedGameObject(button)`

3. **Menu Transitions**:
   - Main Menu → Settings Menu
   - Settings Menu → Back to Main Menu
   - Use `SetActive()` to show/hide menus

---

## Practice Problems

**Beginner:**
Create a shop menu with 3 items: Sword ($10), Shield ($15), Potion ($5). Each button should show the price and name.

**Intermediate:**
Create an inventory menu that displays only items the player owns. Add quantities (e.g., "Health Potion x3").

**Challenge:**
Create a nested menu system: Main → Difficulty Settings → Back to Main. Ensure you can navigate forward and back, and selected options persist.

<details><summary>💡 Hints</summary>
- Beginner: Include price in the button text or show in a separate text element
- Intermediate: Filter items by a "owned" boolean, show count from item data
- Challenge: Use Stack to track menu hierarchy, or simple state enum
</details>

<details><summary>✅ Sample Answers</summary>
**Beginner:**
```csharp
string[] shopItems = { "Sword - $10", "Shield - $15", "Potion - $5" };
PopulateMenu(shopItems);
```

**Intermediate:**
```csharp
public class Item { public string name; public int quantity; }
Item[] inventory = { new Item { name = "Health Potion", quantity = 3 } };

string[] itemNames = inventory
    .Select(i => $"{i.name} x{i.quantity}")
    .ToArray();
PopulateMenu(itemNames);
```

**Challenge:**
```csharp
private string currentMenu = "Main";

public void OpenMenu(string menuName)
{
    menuStack.Push(currentMenu);
    currentMenu = menuName;
    LoadMenu(menuName);
}

public void GoBack()
{
    if (menuStack.Count > 0)
    {
        currentMenu = menuStack.Pop();
        LoadMenu(currentMenu);
    }
}
```
</details>
