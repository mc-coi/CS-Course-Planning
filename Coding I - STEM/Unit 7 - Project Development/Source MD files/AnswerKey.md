# Unit 7: Project Development - Answer Key

---

## Problem 1: Temperature Converter

### Solution
```python
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit."""
    return celsius * 9/5 + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius."""
    return (fahrenheit - 32) * 5/9

def main():
    """Main program loop."""
    while True:
        print("\n=== Temperature Converter ===")
        print("1. Celsius to Fahrenheit")
        print("2. Fahrenheit to Celsius")
        print("3. Exit")

        choice = input("Choose conversion (1/2/3): ").strip()

        if choice == "1":
            try:
                celsius = float(input("Enter temperature in Celsius: "))
                fahrenheit = celsius_to_fahrenheit(celsius)
                print(f"{celsius}°C = {fahrenheit:.2f}°F")
            except ValueError:
                print("Invalid input. Please enter a number.")

        elif choice == "2":
            try:
                fahrenheit = float(input("Enter temperature in Fahrenheit: "))
                celsius = fahrenheit_to_celsius(fahrenheit)
                print(f"{fahrenheit}°F = {celsius:.2f}°C")
            except ValueError:
                print("Invalid input. Please enter a number.")

        elif choice == "3":
            print("Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

### Expected Output
```
=== Temperature Converter ===
1. Celsius to Fahrenheit
2. Fahrenheit to Celsius
3. Exit
Choose conversion (1/2/3): 1
Enter temperature in Celsius: 0
0.0°C = 32.0°F

=== Temperature Converter ===
1. Celsius to Fahrenheit
2. Fahrenheit to Celsius
3. Exit
Choose conversion (1/2/3): 3
Goodbye!
```

### Grading Checklist
- [ ] Both conversion formulas are correct
- [ ] Program loops until user chooses to exit
- [ ] Input validation (try/except for invalid numbers)
- [ ] Clear menu and output formatting
- [ ] Functions are separate from main logic
- [ ] Program handles non-numeric input gracefully

---

## Problem 2: Multiplication Table Generator

### Solution
```python
def generate_multiplication_table(number):
    """Generate multiplication table for a number."""
    table = []
    for i in range(1, 13):
        table.append(f"{number} × {i} = {number * i}")
    return table

def save_table_to_file(number, table, filename):
    """Save multiplication table to file."""
    try:
        with open(filename, "w") as f:
            f.write(f"Multiplication Table for {number}\n")
            f.write("=" * 30 + "\n")
            for line in table:
                f.write(line + "\n")
        print(f"Table saved to {filename}")
    except IOError as e:
        print(f"Error saving file: {e}")

def main():
    """Main program."""
    while True:
        try:
            number = int(input("Enter a number (1-12): "))
            if 1 <= number <= 12:
                break
            else:
                print("Please enter a number between 1 and 12")
        except ValueError:
            print("Invalid input. Please enter a number.")

    # Generate and display table
    table = generate_multiplication_table(number)
    print(f"\nMultiplication Table for {number}:")
    for line in table:
        print(line)

    # Save to file
    save_table_to_file(number, table, "times_table.txt")

if __name__ == "__main__":
    main()
```

### Expected Output
```
Enter a number (1-12): 5

Multiplication Table for 5:
5 × 1 = 5
5 × 2 = 10
5 × 3 = 15
...
5 × 12 = 60
Table saved to times_table.txt
```

### Grading Checklist
- [ ] Input validation (1-12 range)
- [ ] Correct multiplication table generation
- [ ] File I/O working properly
- [ ] Output formatting is clear
- [ ] Error handling for file operations
- [ ] Code is modular with helper functions

---

## Problem 3: Coin Flip Tracker

### Solution
```python
import random

def simulate_flips(num_flips):
    """Simulate coin flips and return counts."""
    heads = 0
    tails = 0

    for _ in range(num_flips):
        flip = random.choice(["Heads", "Tails"])
        if flip == "Heads":
            heads += 1
        else:
            tails += 1

    return heads, tails

def main():
    """Main program."""
    try:
        num_flips = int(input("How many times to flip the coin? "))
        if num_flips <= 0:
            print("Please enter a positive number")
            return

        # Simulate flips
        heads, tails = simulate_flips(num_flips)

        # Calculate percentages
        heads_pct = (heads / num_flips) * 100
        tails_pct = (tails / num_flips) * 100

        # Display results
        print(f"\n=== Coin Flip Results ===")
        print(f"Total flips: {num_flips}")
        print(f"Heads: {heads} ({heads_pct:.1f}%)")
        print(f"Tails: {tails} ({tails_pct:.1f}%)")

    except ValueError:
        print("Invalid input. Please enter a number.")

if __name__ == "__main__":
    main()
```

### Expected Output
```
How many times to flip the coin? 100

=== Coin Flip Results ===
Total flips: 100
Heads: 48 (48.0%)
Tails: 52 (52.0%)
```

### Grading Checklist
- [ ] Uses random.choice for simulation
- [ ] Correct counting of heads and tails
- [ ] Percentage calculation is accurate
- [ ] Input validation for positive numbers
- [ ] Output clearly formatted
- [ ] Results are roughly balanced (not perfectly 50-50)

---

## Problem 4: Grade Book

### Solution
```python
def load_gradebook(filename):
    """Load gradebook from file."""
    gradebook = {}
    try:
        with open(filename, "r") as f:
            for line in f:
                line = line.strip()
                if line and ":" in line:
                    name, scores_str = line.split(":")
                    scores = [float(s) for s in scores_str.split(",") if s]
                    gradebook[name.strip()] = scores
    except FileNotFoundError:
        pass
    return gradebook

def save_gradebook(filename, gradebook):
    """Save gradebook to file."""
    try:
        with open(filename, "w") as f:
            for name, scores in gradebook.items():
                scores_str = ",".join(str(s) for s in scores)
                f.write(f"{name}:{scores_str}\n")
    except IOError as e:
        print(f"Error saving: {e}")

def add_student(gradebook, name):
    """Add a new student."""
    if name not in gradebook:
        gradebook[name] = []
        return f"Student {name} added"
    else:
        return f"Student {name} already exists"

def add_score(gradebook, name, score):
    """Add a score for a student."""
    if name in gradebook:
        gradebook[name].append(score)
        return f"Score {score} added for {name}"
    else:
        return f"Student {name} not found"

def view_average(gradebook, name):
    """View average for a student."""
    if name in gradebook:
        if gradebook[name]:
            avg = sum(gradebook[name]) / len(gradebook[name])
            return f"{name}'s average: {avg:.2f}"
        else:
            return f"{name} has no scores"
    else:
        return f"Student {name} not found"

def view_ranking(gradebook):
    """View class ranking."""
    if not gradebook:
        return "No students in gradebook"

    # Calculate averages
    averages = {}
    for name, scores in gradebook.items():
        if scores:
            averages[name] = sum(scores) / len(scores)

    # Sort by average (descending)
    sorted_students = sorted(averages.items(), key=lambda x: x[1], reverse=True)

    ranking = "=== Class Ranking ===\n"
    for rank, (name, avg) in enumerate(sorted_students, 1):
        ranking += f"{rank}. {name}: {avg:.2f}\n"

    return ranking

def menu(gradebook, filename):
    """Menu system."""
    while True:
        print("\n=== Grade Book ===")
        print("1. Add student")
        print("2. Add score")
        print("3. View average")
        print("4. View ranking")
        print("5. Save and exit")

        choice = input("Choose: ").strip()

        if choice == "1":
            name = input("Student name: ")
            print(add_student(gradebook, name))

        elif choice == "2":
            name = input("Student name: ")
            try:
                score = float(input("Score: "))
                print(add_score(gradebook, name, score))
            except ValueError:
                print("Invalid score")

        elif choice == "3":
            name = input("Student name: ")
            print(view_average(gradebook, name))

        elif choice == "4":
            print(view_ranking(gradebook))

        elif choice == "5":
            save_gradebook(filename, gradebook)
            print("Gradebook saved. Goodbye!")
            break

        else:
            print("Invalid choice")

def main():
    """Main program."""
    filename = "gradebook.txt"
    gradebook = load_gradebook(filename)
    menu(gradebook, filename)

if __name__ == "__main__":
    main()
```

### Expected Output
```
=== Grade Book ===
1. Add student
2. Add score
3. View average
4. View ranking
5. Save and exit
Choose: 1
Student name: Alice
Student Alice added
...
```

### Grading Checklist
- [ ] Data persists to file between runs
- [ ] Can add multiple students
- [ ] Can add multiple scores per student
- [ ] Average calculation is correct
- [ ] Ranking is sorted by grade (highest first)
- [ ] Input validation and error handling
- [ ] Menu-driven interface is user-friendly
- [ ] Code is modular and well-organized

---

## Problem 5: Number Guessing Game

### Solution
```python
import random

def load_high_score(filename):
    """Load the best game score from file."""
    try:
        with open(filename, "r") as f:
            return int(f.read().strip())
    except (FileNotFoundError, ValueError):
        return float('inf')

def save_high_score(filename, score):
    """Save a new high score."""
    try:
        with open(filename, "w") as f:
            f.write(str(score))
    except IOError:
        pass

def rate_performance(guesses):
    """Rate player's guessing performance."""
    if guesses <= 7:
        return "Excellent!"
    elif guesses <= 15:
        return "Good!"
    elif guesses <= 25:
        return "Okay"
    else:
        return "Keep practicing"

def play_game(high_score):
    """Play one round of the guessing game."""
    secret = random.randint(1, 100)
    guesses = 0

    print("\nI'm thinking of a number 1-100. Can you guess it?")

    while True:
        try:
            guess = int(input("Guess: "))
            guesses += 1

            if guess == secret:
                print(f"Correct! You got it in {guesses} guesses!")
                rating = rate_performance(guesses)
                print(f"Performance: {rating}")

                if guesses < high_score:
                    print(f"New high score! (Previous: {high_score})")
                    return guesses
                return guesses

            elif guess < secret:
                print("Too low")
            else:
                print("Too high")

        except ValueError:
            print("Invalid input. Enter a number.")

def main():
    """Main program."""
    filename = "high_scores.txt"
    high_score = load_high_score(filename)

    if high_score == float('inf'):
        print("Welcome! No high score yet.")
    else:
        print(f"High score: {high_score} guesses")

    while True:
        score = play_game(high_score)

        if score < high_score:
            high_score = score
            save_high_score(filename, score)

        play_again = input("\nPlay again? (yes/no): ").lower().strip()
        if play_again != "yes":
            print("Thanks for playing!")
            break

if __name__ == "__main__":
    main()
```

### Expected Output
```
Welcome! No high score yet.

I'm thinking of a number 1-100. Can you guess it?
Guess: 50
Too high
Guess: 25
Too low
Guess: 37
Correct! You got it in 3 guesses!
Performance: Excellent!
New high score! (Previous: inf)

Play again? (yes/no): no
Thanks for playing!
```

### Grading Checklist
- [ ] Random number generation works (1-100)
- [ ] Hints (too high/too low) are correct
- [ ] Guess counter is accurate
- [ ] Performance rating is appropriate
- [ ] High score persists to file
- [ ] Can play multiple rounds
- [ ] Input validation for guesses
- [ ] User-friendly interface

---

## Problem 6: Text Analyzer

### Solution
```python
def analyze_text(filename):
    """Analyze a text file and return statistics."""
    try:
        with open(filename, "r") as f:
            text = f.read()
    except FileNotFoundError:
        return None

    # Count words
    words = text.split()
    total_words = len(words)

    # Count unique words
    unique_words = len(set(word.lower() for word in words))

    # Count sentences
    sentences = len([s for s in text.split('.') if s.strip()])

    # Find most common words
    word_freq = {}
    for word in words:
        word_clean = word.lower().strip('.,!?;:')
        word_freq[word_clean] = word_freq.get(word_clean, 0) + 1

    # Sort and get top 5
    top_words = sorted(word_freq.items(), key=lambda x: x[1], reverse=True)[:5]

    # Average word length
    avg_length = sum(len(w.strip('.,!?;:')) for w in words) / total_words if words else 0

    return {
        'total_words': total_words,
        'unique_words': unique_words,
        'sentences': sentences,
        'top_words': top_words,
        'avg_length': avg_length
    }

def save_analysis(filename, analysis):
    """Save analysis results to file."""
    try:
        with open(filename, "w") as f:
            f.write("=== Text Analysis Results ===\n\n")
            f.write(f"Total words: {analysis['total_words']}\n")
            f.write(f"Unique words: {analysis['unique_words']}\n")
            f.write(f"Sentences: {analysis['sentences']}\n")
            f.write(f"Average word length: {analysis['avg_length']:.2f}\n\n")
            f.write("Top 5 most common words:\n")
            for i, (word, freq) in enumerate(analysis['top_words'], 1):
                f.write(f"  {i}. {word}: {freq}\n")
    except IOError as e:
        print(f"Error saving: {e}")

def main():
    """Main program."""
    input_file = input("Enter filename to analyze: ")
    analysis = analyze_text(input_file)

    if analysis is None:
        print(f"Error: File '{input_file}' not found")
        return

    # Display results
    print("\n=== Analysis Results ===")
    print(f"Total words: {analysis['total_words']}")
    print(f"Unique words: {analysis['unique_words']}")
    print(f"Sentences: {analysis['sentences']}")
    print(f"Average word length: {analysis['avg_length']:.2f}")
    print("\nTop 5 most common words:")
    for i, (word, freq) in enumerate(analysis['top_words'], 1):
        print(f"  {i}. {word}: {freq}")

    # Save results
    save_analysis("analysis.txt", analysis)
    print("\nAnalysis saved to analysis.txt")

if __name__ == "__main__":
    main()
```

### Expected Output
```
Enter filename to analyze: sample.txt

=== Analysis Results ===
Total words: 47
Unique words: 35
Sentences: 3
Average word length: 4.87

Top 5 most common words:
  1. the: 8
  2. and: 5
  3. is: 3
  4. to: 3
  5. of: 2

Analysis saved to analysis.txt
```

### Grading Checklist
- [ ] Correctly counts total words
- [ ] Correctly counts unique words (case-insensitive)
- [ ] Correctly counts sentences
- [ ] Identifies top 5 most common words
- [ ] Calculates average word length
- [ ] Saves results to file
- [ ] Handles file not found error
- [ ] Output is well-formatted

---

## Problem 7: Simple To-Do List

### Solution
```python
def load_tasks(filename):
    """Load tasks from file."""
    tasks = []
    try:
        with open(filename, "r") as f:
            for line in f:
                line = line.strip()
                if line:
                    is_complete = line.startswith("[X]")
                    task = line[4:] if is_complete else line[3:]
                    tasks.append({"task": task, "complete": is_complete})
    except FileNotFoundError:
        pass
    return tasks

def save_tasks(filename, tasks):
    """Save tasks to file."""
    try:
        with open(filename, "w") as f:
            for task in tasks:
                marker = "[X]" if task["complete"] else "[ ]"
                f.write(f"{marker} {task['task']}\n")
    except IOError as e:
        print(f"Error: {e}")

def add_task(tasks, description):
    """Add a new task."""
    tasks.append({"task": description, "complete": False})
    return f"Added: {description}"

def mark_complete(tasks, index):
    """Mark a task as complete."""
    if 0 <= index < len(tasks):
        tasks[index]["complete"] = True
        return f"Marked complete: {tasks[index]['task']}"
    return "Invalid task number"

def delete_task(tasks, index):
    """Delete a task."""
    if 0 <= index < len(tasks):
        task = tasks.pop(index)
        return f"Deleted: {task['task']}"
    return "Invalid task number"

def view_tasks(tasks):
    """Display all tasks."""
    if not tasks:
        return "No tasks"

    output = "=== To-Do List ===\n"
    for i, task in enumerate(tasks, 1):
        marker = "[X]" if task["complete"] else "[ ]"
        output += f"{i}. {marker} {task['task']}\n"
    return output

def menu(tasks, filename):
    """Menu system."""
    while True:
        print("\n" + view_tasks(tasks))
        print("\n1. Add  2. Complete  3. Delete  4. Save & Exit")
        choice = input("Choose: ").strip()

        if choice == "1":
            desc = input("Task: ")
            print(add_task(tasks, desc))

        elif choice == "2":
            try:
                index = int(input("Task number: ")) - 1
                print(mark_complete(tasks, index))
            except ValueError:
                print("Invalid input")

        elif choice == "3":
            try:
                index = int(input("Task number: ")) - 1
                print(delete_task(tasks, index))
            except ValueError:
                print("Invalid input")

        elif choice == "4":
            save_tasks(filename, tasks)
            print("Tasks saved. Goodbye!")
            break

        else:
            print("Invalid choice")

def main():
    """Main program."""
    filename = "tasks.txt"
    tasks = load_tasks(filename)
    menu(tasks, filename)

if __name__ == "__main__":
    main()
```

### Expected Output
```
=== To-Do List ===
1. [ ] Buy groceries
2. [ ] Write code
3. [X] Complete project

1. Add  2. Complete  3. Delete  4. Save & Exit
Choose: ...
```

### Grading Checklist
- [ ] Tasks load from file on startup
- [ ] Can add new tasks
- [ ] Can mark tasks complete with [X]
- [ ] Can delete tasks
- [ ] Tasks save to file on exit
- [ ] Completed tasks show [X] marker
- [ ] Tasks survive between runs
- [ ] Menu is clear and user-friendly

---

## Tier 3 Challenge Projects - Grading Guidelines

For the challenge projects (P8-P15), use these general grading criteria:

### Project Structure Checklist
- [ ] Code is organized into logical functions
- [ ] Each function has a clear single purpose
- [ ] Functions are documented with docstrings
- [ ] Variable names are descriptive
- [ ] Code follows consistent indentation and style

### Functionality Checklist
- [ ] Core features work as specified
- [ ] User input is validated
- [ ] File I/O works correctly
- [ ] Data persists between runs
- [ ] Errors are handled gracefully (try/except)
- [ ] Program doesn't crash on bad input

### User Experience Checklist
- [ ] Clear menu/interface
- [ ] Helpful error messages
- [ ] Logical flow through the program
- [ ] Appropriate output formatting
- [ ] No confusing or unclear prompts

### Code Quality Checklist
- [ ] Code is modular and reusable
- [ ] No unnecessary duplication
- [ ] Functions are reasonably sized
- [ ] Comments clarify complex logic
- [ ] Demonstrates mastery of concepts learned

### Testing Notes
- Test with normal inputs
- Test with edge cases (empty, zero, negative values)
- Test error conditions (missing files, invalid input)
- Test the complete workflow from start to finish
- Verify data persistence between program runs

---

### Partial Credit Guidelines

**Full Credit (90-100%):** Program meets all requirements, handles edge cases, well-organized

**Good (80-89%):** Program meets requirements, minor issues with organization or error handling

**Satisfactory (70-79%):** Program works but missing some features or has significant issues

**Needs Work (Below 70%):** Program incomplete or major functionality missing

---
