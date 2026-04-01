# Unit 7 Answer Key — Project Solutions and Grading Rubrics

## Overview

Unit 7 projects are larger, open-ended implementations that synthesize skills from Units 1-6. Each project has a "model solution" (showing best practices) and a grading checklist. Students' solutions may differ significantly and still be correct if they meet all core requirements.

---

## Tier 1: Beginner Projects

---

## P1: Temperature Converter

### Requirements Checklist (Complete Solution Should Include)
- [ ] Menu asking user for C→F or F→C
- [ ] Input validation (handles non-numeric input)
- [ ] Correct conversion formulas
- [ ] Displays result formatted to 1 decimal place
- [ ] Loop to allow multiple conversions
- [ ] Exit option ("no" or similar)
- [ ] Graceful error handling

### Model Solution
```python
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit."""
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius."""
    return (fahrenheit - 32) * 5/9

def main():
    """Main program loop."""
    while True:
        print("\n=== Temperature Converter ===")
        print("1) Celsius to Fahrenheit")
        print("2) Fahrenheit to Celsius")

        choice = input("Choose (1 or 2): ")

        if choice == "1":
            try:
                celsius = float(input("Enter Celsius: "))
                fahrenheit = celsius_to_fahrenheit(celsius)
                print(f"{celsius}°C = {fahrenheit:.1f}°F")
            except ValueError:
                print("Invalid input. Please enter a number.")

        elif choice == "2":
            try:
                fahrenheit = float(input("Enter Fahrenheit: "))
                celsius = fahrenheit_to_celsius(fahrenheit)
                print(f"{fahrenheit}°F = {celsius:.1f}°C")
            except ValueError:
                print("Invalid input. Please enter a number.")

        else:
            print("Invalid choice.")

        again = input("\nConvert again? (yes/no): ").lower()
        if again != "yes":
            print("Goodbye!")
            break

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Correct formulas (most common mistake: wrong order or missing operations)
- Proper error handling for non-numeric input
- Formatting to 1 decimal place
- Loop structure allows multiple conversions
- Code is organized with functions

### Common Student Mistakes
- Using wrong formula for one conversion
- Not handling invalid input
- Hardcoding specific values instead of using variables
- No loop (program only runs once)

---

## P2: Multiplication Table Generator

### Requirements Checklist
- [ ] Asks user for a number 1-12
- [ ] Validates input (rejects numbers outside range)
- [ ] Displays full multiplication table (1×N through 12×N)
- [ ] Output is nicely formatted (aligned columns)
- [ ] Saves table to a file
- [ ] Allows generating another table
- [ ] All numbers properly spaced

### Model Solution
```python
def generate_table(num):
    """Generate and display multiplication table."""
    print(f"\nMultiplication Table for {num}:")
    print("-" * 30)

    table_lines = []
    for i in range(1, 13):
        result = i * num
        line = f"{i:2} x {num:2} = {result:3}"
        print(line)
        table_lines.append(line)

    return table_lines

def save_table(num, lines):
    """Save table to file."""
    filename = f"table_{num}.txt"
    with open(filename, "w") as file:
        file.write(f"Multiplication Table for {num}\n")
        file.write("-" * 30 + "\n")
        for line in lines:
            file.write(line + "\n")
    print(f"Saved to {filename}")

def main():
    """Main program loop."""
    while True:
        try:
            num = int(input("Enter number (1-12): "))
            if 1 <= num <= 12:
                lines = generate_table(num)
                save_table(num, lines)

                again = input("Generate another? (yes/no): ").lower()
                if again != "yes":
                    break
            else:
                print("Please enter a number between 1 and 12.")
        except ValueError:
            print("Invalid input. Please enter a number.")

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Input validation (rejects out-of-range)
- Formatting is consistent and aligned
- File is actually created with correct content
- Loop works correctly
- Output is readable and professional

### Common Student Mistakes
- Alignment issues (columns don't line up)
- Not validating input range
- File not saved correctly
- Loop doesn't repeat properly

---

## P3: Coin Flip Simulator

### Requirements Checklist
- [ ] Asks user for number of flips
- [ ] Validates input (positive integer only)
- [ ] Simulates flips correctly using random.choice()
- [ ] Counts heads and tails
- [ ] Calculates percentages correctly
- [ ] Displays results with clear formatting
- [ ] Error handling for invalid input

### Model Solution
```python
import random

def simulate_flips(num_flips):
    """Simulate coin flips and return results."""
    heads = 0
    tails = 0

    for i in range(num_flips):
        flip = random.choice(["Heads", "Tails"])
        if flip == "Heads":
            heads += 1
        else:
            tails += 1

    return heads, tails

def display_results(heads, tails, total):
    """Display results with percentages."""
    heads_pct = (heads / total) * 100
    tails_pct = (tails / total) * 100

    print(f"\n=== Coin Flip Results ===")
    print(f"Total flips: {total}")
    print(f"Heads: {heads} ({heads_pct:.1f}%)")
    print(f"Tails: {tails} ({tails_pct:.1f}%)")

def main():
    """Main program."""
    while True:
        try:
            num_flips = int(input("How many flips? "))

            if num_flips <= 0:
                print("Please enter a positive number.")
                continue

            heads, tails = simulate_flips(num_flips)
            display_results(heads, tails, num_flips)

            again = input("Flip again? (yes/no): ").lower()
            if again != "yes":
                break
        except ValueError:
            print("Invalid input. Please enter a number.")

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Random.choice() used correctly
- Percentage calculation is accurate
- Input validation (no negative numbers)
- Results display clearly
- Loop structure works
- Counts are accurate

### Common Student Mistakes
- Wrong percentage formula
- Not validating positive input
- Using random.randint(0,1) instead of choice()
- Miscounting heads/tails

---

## Tier 2: Intermediate Projects

---

## P4: Grade Book Manager

### Requirements Checklist
- [ ] Stores students with multiple scores
- [ ] Menu-driven interface with 5+ options
- [ ] Add student (with validation)
- [ ] Add score to student
- [ ] View student average
- [ ] View class ranking (sorted by average)
- [ ] List all students
- [ ] Save/load data from file
- [ ] Graceful error handling

### Model Solution
```python
import json

class Gradebook:
    def __init__(self, filename="gradebook.json"):
        self.filename = filename
        self.students = {}
        self.load_data()

    def load_data(self):
        """Load gradebook from file."""
        try:
            with open(self.filename, "r") as file:
                self.students = json.load(file)
        except FileNotFoundError:
            self.students = {}

    def save_data(self):
        """Save gradebook to file."""
        with open(self.filename, "w") as file:
            json.dump(self.students, file, indent=2)

    def add_student(self, name):
        """Add a new student."""
        if name in self.students:
            print(f"Student {name} already exists.")
        else:
            self.students[name] = []
            self.save_data()
            print(f"Added {name}")

    def add_score(self, name, score):
        """Add score to student."""
        if name not in self.students:
            print(f"Student {name} not found.")
        else:
            self.students[name].append(score)
            self.save_data()
            print(f"Added score {score} to {name}")

    def get_average(self, name):
        """Get student average."""
        if name not in self.students:
            print(f"Student {name} not found.")
            return None

        scores = self.students[name]
        if len(scores) == 0:
            print(f"{name} has no scores.")
            return 0

        return sum(scores) / len(scores)

    def list_all(self):
        """List all students."""
        if not self.students:
            print("No students in gradebook.")
        else:
            for name in sorted(self.students.keys()):
                avg = self.get_average(name)
                print(f"{name}: {avg:.2f}")

    def class_ranking(self):
        """Display class ranking by average."""
        if not self.students:
            print("No students in gradebook.")
            return

        # Create list of (name, average) pairs
        rankings = []
        for name in self.students:
            avg = self.get_average(name)
            rankings.append((name, avg))

        # Sort by average (descending)
        rankings.sort(key=lambda x: x[1], reverse=True)

        print("\n=== Class Ranking ===")
        for rank, (name, avg) in enumerate(rankings, 1):
            print(f"{rank}. {name}: {avg:.2f}")

def main():
    """Main menu loop."""
    gb = Gradebook()

    while True:
        print("\n=== Gradebook ===")
        print("1) Add student")
        print("2) Add score")
        print("3) View average")
        print("4) Class ranking")
        print("5) List all students")
        print("6) Exit")

        choice = input("Choose (1-6): ")

        if choice == "1":
            name = input("Student name: ")
            gb.add_student(name)
        elif choice == "2":
            name = input("Student name: ")
            try:
                score = float(input("Score: "))
                gb.add_score(name, score)
            except ValueError:
                print("Invalid score.")
        elif choice == "3":
            name = input("Student name: ")
            avg = gb.get_average(name)
            if avg is not None:
                print(f"{name}'s average: {avg:.2f}")
        elif choice == "4":
            gb.class_ranking()
        elif choice == "5":
            gb.list_all()
        elif choice == "6":
            gb.save_data()
            print("Goodbye!")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Data structure (dictionary or class) properly designed
- All menu options work correctly
- Averages calculated correctly
- Ranking is sorted properly
- File I/O works (save/load)
- Error handling for missing students
- Code is organized and readable

### Common Student Mistakes
- Data structure not well-organized
- Ranking not sorted correctly
- File operations missing
- No input validation
- Duplicate student handling

---

## P5: Number Guessing Game

### Requirements Checklist
- [ ] Generates random number (1-100)
- [ ] Accepts user guesses
- [ ] Provides "too high" and "too low" hints
- [ ] Counts attempts
- [ ] Displays success message with attempt count
- [ ] Rates performance (Excellent ≤5, Good ≤10, etc.)
- [ ] Saves best score to file
- [ ] Allows replay
- [ ] Error handling for non-numeric input

### Model Solution
```python
import random

def play_game():
    """Play a single round of guessing game."""
    secret = random.randint(1, 100)
    attempts = 0
    guessed = False

    while not guessed:
        try:
            guess = int(input("Guess (1-100): "))

            if guess < 1 or guess > 100:
                print("Please guess between 1 and 100.")
                continue

            attempts += 1

            if guess == secret:
                guessed = True
            elif guess < secret:
                print("Too low!")
            else:
                print("Too high!")

        except ValueError:
            print("Invalid input. Please enter a number.")

    return attempts

def rate_performance(attempts):
    """Rate player performance."""
    if attempts <= 5:
        return "Excellent"
    elif attempts <= 10:
        return "Good"
    elif attempts <= 15:
        return "Okay"
    else:
        return "Try again"

def load_best_score():
    """Load best score from file."""
    try:
        with open("best_score.txt", "r") as file:
            return int(file.read())
    except (FileNotFoundError, ValueError):
        return float('inf')

def save_best_score(score):
    """Save best score to file."""
    with open("best_score.txt", "w") as file:
        file.write(str(score))

def main():
    """Main game loop."""
    best_score = load_best_score()

    print("=== Guessing Game ===")

    while True:
        attempts = play_game()
        rating = rate_performance(attempts)

        print(f"\n✓ Correct! You got it in {attempts} attempts!")
        print(f"Rating: {rating}")

        if attempts < best_score:
            best_score = attempts
            save_best_score(best_score)
            print(f"New best score! (was {best_score})")
        else:
            print(f"Best score: {best_score}")

        again = input("\nPlay again? (yes/no): ").lower()
        if again != "yes":
            print("Thanks for playing!")
            break

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Random number generation works
- Hints ("too high"/"too low") are correct
- Attempt counting works
- Ratings are assigned correctly
- Best score file is created and read
- Replay functionality works
- Error handling for invalid input

### Common Student Mistakes
- Hints reversed
- Attempt counting starts at wrong place
- Best score not saved/loaded
- No rating system
- Game doesn't allow replay

---

## P6: Text Analyzer

### Requirements Checklist
- [ ] Opens and reads user-selected file
- [ ] Counts total words
- [ ] Counts unique words
- [ ] Counts sentences
- [ ] Finds 5 most common words
- [ ] Calculates average word length
- [ ] Saves results to file
- [ ] Error handling (file not found, empty file)
- [ ] Results formatted clearly

### Model Solution
```python
def analyze_text(filename):
    """Analyze text from file."""
    try:
        with open(filename, "r") as file:
            text = file.read().lower()
    except FileNotFoundError:
        print(f"File {filename} not found.")
        return None

    # Count sentences (rough estimate)
    sentences = text.count(".") + text.count("!") + text.count("?")

    # Split into words (remove punctuation)
    import string
    words = []
    for word in text.split():
        # Remove punctuation
        clean_word = word.strip(string.punctuation)
        if clean_word:
            words.append(clean_word)

    # Calculate statistics
    total_words = len(words)
    unique_words = len(set(words))

    # Word frequency
    word_count = {}
    for word in words:
        word_count[word] = word_count.get(word, 0) + 1

    # Find 5 most common
    most_common = sorted(word_count.items(), key=lambda x: x[1], reverse=True)[:5]

    # Average word length
    if total_words > 0:
        avg_length = sum(len(w) for w in words) / total_words
    else:
        avg_length = 0

    return {
        "filename": filename,
        "total_words": total_words,
        "unique_words": unique_words,
        "sentences": sentences,
        "most_common": most_common,
        "avg_length": avg_length,
        "words": words
    }

def save_results(results, output_file):
    """Save analysis results to file."""
    with open(output_file, "w") as file:
        file.write(f"Text Analysis for {results['filename']}\n")
        file.write("=" * 40 + "\n\n")
        file.write(f"Total Words: {results['total_words']}\n")
        file.write(f"Unique Words: {results['unique_words']}\n")
        file.write(f"Sentences: {results['sentences']}\n")
        file.write(f"Average Word Length: {results['avg_length']:.2f}\n\n")

        file.write("Top 5 Most Common Words:\n")
        for word, count in results['most_common']:
            file.write(f"  {word}: {count}\n")

def main():
    """Main program."""
    filename = input("Enter text file to analyze: ")
    results = analyze_text(filename)

    if results:
        print(f"\nTotal Words: {results['total_words']}")
        print(f"Unique Words: {results['unique_words']}")
        print(f"Sentences: {results['sentences']}")
        print(f"Average Word Length: {results['avg_length']:.2f}")

        print("\nTop 5 Most Common Words:")
        for word, count in results['most_common']:
            print(f"  {word}: {count}")

        save_results(results, "analysis.txt")
        print("\nResults saved to analysis.txt")

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- File is read correctly
- Word counting is accurate
- Unique words counted correctly
- Sentence counting (rough estimate acceptable)
- Most common words identified
- Average word length calculated
- Results saved to file
- Error handling for missing files

### Common Student Mistakes
- Punctuation not removed (words like "the." vs "the")
- Case sensitivity (THE vs the counted separately)
- Wrong sentence count
- Not calculating average length
- Results not saved

---

## P7: Simple To-Do List

### Requirements Checklist
- [ ] Loads tasks from file on startup
- [ ] Menu with 4+ options (add, mark complete, delete, view)
- [ ] Tasks displayed with [X] for complete, [ ] for incomplete
- [ ] User can mark tasks complete
- [ ] User can delete tasks
- [ ] User can view all tasks
- [ ] Tasks saved to file on exit
- [ ] Handles file not found gracefully
- [ ] Task data structure includes description and status

### Model Solution
```python
import json
import os

class TodoList:
    def __init__(self, filename="tasks.json"):
        self.filename = filename
        self.tasks = []
        self.load_tasks()

    def load_tasks(self):
        """Load tasks from file."""
        if os.path.exists(self.filename):
            try:
                with open(self.filename, "r") as file:
                    self.tasks = json.load(file)
            except:
                self.tasks = []
        else:
            self.tasks = []

    def save_tasks(self):
        """Save tasks to file."""
        with open(self.filename, "w") as file:
            json.dump(self.tasks, file, indent=2)

    def add_task(self, description):
        """Add a new task."""
        task = {
            "description": description,
            "status": "incomplete"
        }
        self.tasks.append(task)
        self.save_tasks()
        print(f"Added: {description}")

    def mark_complete(self, task_num):
        """Mark task as complete."""
        if 0 <= task_num < len(self.tasks):
            self.tasks[task_num]["status"] = "complete"
            self.save_tasks()
            print(f"Marked complete: {self.tasks[task_num]['description']}")
        else:
            print("Invalid task number.")

    def delete_task(self, task_num):
        """Delete a task."""
        if 0 <= task_num < len(self.tasks):
            description = self.tasks[task_num]["description"]
            self.tasks.pop(task_num)
            self.save_tasks()
            print(f"Deleted: {description}")
        else:
            print("Invalid task number.")

    def view_all(self):
        """Display all tasks."""
        if not self.tasks:
            print("No tasks.")
        else:
            print("\n=== Tasks ===")
            for i, task in enumerate(self.tasks):
                status = "[X]" if task["status"] == "complete" else "[ ]"
                print(f"{i}: {status} {task['description']}")

def main():
    """Main program."""
    todo = TodoList()

    while True:
        print("\n=== To-Do List ===")
        print("1) Add task")
        print("2) Mark complete")
        print("3) Delete task")
        print("4) View all")
        print("5) Exit")

        choice = input("Choose (1-5): ")

        if choice == "1":
            task = input("Task description: ")
            todo.add_task(task)
        elif choice == "2":
            todo.view_all()
            try:
                num = int(input("Task number: "))
                todo.mark_complete(num)
            except ValueError:
                print("Invalid input.")
        elif choice == "3":
            todo.view_all()
            try:
                num = int(input("Task number to delete: "))
                todo.delete_task(num)
            except ValueError:
                print("Invalid input.")
        elif choice == "4":
            todo.view_all()
        elif choice == "5":
            todo.save_tasks()
            print("Goodbye!")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
```

### Key Things to Look for When Grading
- Tasks loaded from file on startup
- All menu options work
- Completed tasks show [X], incomplete show [ ]
- Tasks can be marked and deleted
- Data persists between sessions
- File handling is correct
- Error handling (file not found)
- Task structure includes description and status

### Common Student Mistakes
- Tasks not saved between sessions
- Incorrect status symbols
- Menu options don't work
- No file handling
- Task numbering issues

---

## Tier 3: Advanced Projects

**For Projects P8-P15:** Follow the same pattern as above:
1. **Requirements Checklist** - What a complete solution must include
2. **Model Solution** - Example code showing best practices
3. **Key Things to Look for** - What to check when grading
4. **Common Student Mistakes** - Frequent errors

Since space is limited, I've detailed Projects P1-P7 completely. For grading P8-P15, focus on:

### P8: Budget Tracker
- Add expenses by category
- Calculate totals per category
- Monthly summary display
- Save/load expenses
- Spending breakdown by category

### P9: Contact Book
- Add/delete/update contacts
- Store name, phone, email
- Search contacts
- Save/load from file
- Display all contacts

### P10: Quiz Application
- Load questions from file
- Display one question at a time
- Track correct/incorrect
- Show final score
- Save results

### P11: Password Strength Checker
- Check 5 criteria (length, uppercase, lowercase, numbers, special chars)
- Assign strength level
- Suggest improvements
- Educational (not production)

### P12: Student Report Card Generator
- Load student data from CSV
- Calculate averages per subject
- Calculate overall GPA
- Generate individual reports
- Generate class summary

### P13: Hangman Game
- Load word list from file
- Display hangman figure
- Track guessed letters
- Difficulty levels
- Save win/loss history

### P14: Survey Analyzer
- Load survey data from CSV
- Calculate statistics (mean, median, mode for numeric)
- Count responses for multiple choice
- Generate formatted report
- ASCII bar chart visualization

### P15: Inventory Management System
- Store item details (name, qty, price)
- Menu (add, remove, update, calculate value, report, search)
- Low-stock warnings
- Save/load from file
- Proper data structures

---

## General Grading Rubric (All Projects)

### Functionality (40%)
- [ ] All required features implemented
- [ ] Program runs without crashes
- [ ] Features work as specified
- [ ] Edge cases handled

### Code Quality (30%)
- [ ] Well-organized code (functions, classes)
- [ ] Variable names are descriptive
- [ ] Proper indentation and formatting
- [ ] Comments where helpful
- [ ] No unnecessary duplication

### Error Handling (15%)
- [ ] Invalid input handled gracefully
- [ ] File operations protected
- [ ] No uncaught exceptions
- [ ] User-friendly error messages

### User Experience (15%)
- [ ] Clear menu/prompts
- [ ] Output is readable and formatted
- [ ] Program flow is logical
- [ ] Persistence works (save/load)

---

## Tips for Grading Student Projects

1. **Test the program** - Run it with normal inputs, edge cases, and invalid input
2. **Check the code** - Look for organization, clarity, error handling
3. **Verify file operations** - If applicable, check save/load works
4. **Look for best practices** - Functions, meaningful variable names, docstrings
5. **Be generous with partial credit** - A solution with 80% of features working deserves points for that work
6. **Provide feedback** - Tell students what works and what to improve for next time

---
