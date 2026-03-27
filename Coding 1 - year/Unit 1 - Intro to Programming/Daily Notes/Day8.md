# Day 8: User Input & String Concatenation
**Learning Target:** I can collect user input and combine text and variables using concatenation.

### Key Concepts
The `input()` function pauses the program and waits for the user to type something, then press Enter. It displays a prompt (message) to guide the user. **Important:** `input()` always returns a **string**, even if the user types numbers like `17`.

**String concatenation** means combining strings together using the `+` operator. Example: `"Hello" + " " + "World"` = `"Hello World"`

You can concatenate:
- String literals (text in quotes)
- String variables
- Multiple strings in one statement

**Example:**
```python
first_name = "Alex"
last_name = "Smith"
full_name = first_name + " " + last_name  # "Alex Smith"
```

**Important:** You can only concatenate strings. To combine strings with numbers, you must convert the number to a string first (or use f-strings, which we'll learn later).

### Code Examples
```python
# Basic input with prompt
name = input("What is your name? ")
print("Hello, " + name + "!")

# Multiple inputs
first = input("First name: ")
last = input("Last name: ")
full = first + " " + last
print("Your name is: " + full)

# Concatenation examples
greeting = "Hello"
username = "Alex"
message = greeting + ", " + username + "!"
print(message)  # Hello, Alex!

# Mixing variables and literals
age = "17"  # Note: this is a string!
print("I am " + age + " years old")

# Multiple concatenations in one statement
hobby = input("What is your hobby? ")
print("You told me your hobby is " + hobby + ".")
```

### Guided Practice
Create a program that:
1. Asks the user for their first and last name
2. Combines them into a full name using concatenation
3. Asks for their favorite hobby
4. Prints a sentence using all the information with proper formatting
5. Include at least one comment

### Practice Problems

**Problem 1 — Beginner:** Write a program that asks the user for their name and favorite color, then prints a sentence combining both using concatenation.

```python
# Starter code
name = input()
color = input()
print()  # Print the combined message
```

**Problem 2 — Intermediate:** Write a program that asks for a student's name, school, and grade, then prints a formatted introduction sentence.

**Problem 3 — Challenge:** Write a program that asks for three favorite things (foods, games, or activities), then prints a sentence combining all three.

<details>
<summary>💡 Hints</summary>

- Problem 1: Use + to combine the strings
- Problem 2: Make sure to include spaces in your concatenation
- Problem 3: Remember to include spaces between your concatenated strings
</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1 Example
name = input("What is your name? ")
color = input("What is your favorite color? ")
print("Hello, " + name + "! I like " + color + " too!")

# Problem 2 Example
student_name = input("Student name: ")
school = input("School name: ")
grade = input("Grade: ")
print(student_name + " goes to " + school + " and is in grade " + grade)

# Problem 3 Example
food = input("Favorite food: ")
game = input("Favorite game: ")
activity = input("Favorite activity: ")
print("I love " + food + ", playing " + game + ", and " + activity + "!")
```

</details>

---
