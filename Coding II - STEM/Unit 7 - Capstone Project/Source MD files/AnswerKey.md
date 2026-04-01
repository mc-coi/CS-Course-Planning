# Unit 7 - Capstone Project: Answer Key & Grading Guide

> **Note:** Capstone projects are open-ended. This guide provides grading checklists, model skeletons, and key things to look for — not a single "correct" answer. Student implementations will vary; evaluate based on completeness, correctness, and code quality.

---

## General Grading Rubric (applies to all projects)

| Category | Points | Criteria |
|----------|--------|----------|
| Functionality | 40 | Core features work correctly, edge cases handled |
| Code Quality | 20 | Clean, readable, commented, consistent style |
| Data Persistence | 15 | Data saves/loads correctly (file I/O or JSON) |
| Error Handling | 15 | try/except used appropriately, no unhandled crashes |
| OOP / Structure | 10 | Uses classes where appropriate, modular design |

---

## Project 1: Task/To-Do Manager

### Feature Checklist
- [ ] Add a new task (with title, priority, due date)
- [ ] View all tasks (formatted output)
- [ ] Mark a task as complete
- [ ] Delete a task
- [ ] Filter tasks (by status, priority, or due date)
- [ ] Save tasks to a file (JSON or CSV)
- [ ] Load tasks on startup
- [ ] Input validation (no empty task names, valid dates)

### Model Skeleton
```python
import json
import os
from datetime import datetime

class Task:
    def __init__(self, title, priority="medium", due_date=None):
        self.title = title
        self.priority = priority
        self.due_date = due_date
        self.completed = False

    def to_dict(self):
        return {
            "title": self.title,
            "priority": self.priority,
            "due_date": self.due_date,
            "completed": self.completed
        }

    @classmethod
    def from_dict(cls, data):
        task = cls(data["title"], data["priority"], data["due_date"])
        task.completed = data["completed"]
        return task

    def __str__(self):
        status = "✓" if self.completed else "○"
        return f"[{status}] {self.title} | Priority: {self.priority} | Due: {self.due_date}"


class TaskManager:
    FILE = "tasks.json"

    def __init__(self):
        self.tasks = []
        self.load()

    def add(self, title, priority="medium", due_date=None):
        if not title.strip():
            print("Task title cannot be empty.")
            return
        self.tasks.append(Task(title.strip(), priority, due_date))
        self.save()
        print(f"Task '{title}' added.")

    def view(self, filter_by=None):
        filtered = self.tasks
        if filter_by == "active":
            filtered = [t for t in self.tasks if not t.completed]
        elif filter_by == "done":
            filtered = [t for t in self.tasks if t.completed]
        if not filtered:
            print("No tasks found.")
        for i, task in enumerate(filtered, 1):
            print(f"{i}. {task}")

    def complete(self, index):
        try:
            self.tasks[index - 1].completed = True
            self.save()
            print("Task marked complete.")
        except IndexError:
            print("Invalid task number.")

    def delete(self, index):
        try:
            removed = self.tasks.pop(index - 1)
            self.save()
            print(f"Deleted: {removed.title}")
        except IndexError:
            print("Invalid task number.")

    def save(self):
        with open(self.FILE, "w") as f:
            json.dump([t.to_dict() for t in self.tasks], f, indent=2)

    def load(self):
        if os.path.exists(self.FILE):
            with open(self.FILE) as f:
                self.tasks = [Task.from_dict(d) for d in json.load(f)]


def main():
    manager = TaskManager()
    while True:
        print("\n1. Add  2. View  3. Complete  4. Delete  5. Quit")
        choice = input("Choice: ").strip()
        if choice == "1":
            title = input("Title: ")
            priority = input("Priority (low/medium/high): ") or "medium"
            due = input("Due date (YYYY-MM-DD, or blank): ") or None
            manager.add(title, priority, due)
        elif choice == "2":
            f = input("Filter (all/active/done): ") or "all"
            manager.view(None if f == "all" else f)
        elif choice == "3":
            manager.view()
            n = int(input("Task number: "))
            manager.complete(n)
        elif choice == "4":
            manager.view()
            n = int(input("Task number: "))
            manager.delete(n)
        elif choice == "5":
            break

if __name__ == "__main__":
    main()
```

### Key Things to Look For
- Tasks persist between runs (JSON file created/loaded)
- Graceful handling of invalid input/index
- At least one class used (`Task` or `TaskManager`)

---

## Project 2: Expense Tracker

### Feature Checklist
- [ ] Add an expense (amount, category, date, description)
- [ ] View all expenses (sorted by date or category)
- [ ] Calculate total spending
- [ ] Filter by category or date range
- [ ] Generate a summary report (totals per category)
- [ ] Save/load data (CSV or JSON)
- [ ] Validate that amounts are positive numbers

### Model Skeleton
```python
import csv
import os
from datetime import datetime

class Expense:
    def __init__(self, amount, category, date, description=""):
        self.amount = float(amount)
        self.category = category
        self.date = date
        self.description = description

    def to_dict(self):
        return {"amount": self.amount, "category": self.category,
                "date": self.date, "description": self.description}


class ExpenseTracker:
    FILE = "expenses.csv"
    FIELDS = ["amount", "category", "date", "description"]

    def __init__(self):
        self.expenses = []
        self.load()

    def add(self, amount, category, date=None, description=""):
        try:
            if float(amount) <= 0:
                raise ValueError
        except ValueError:
            print("Amount must be a positive number.")
            return
        date = date or datetime.today().strftime("%Y-%m-%d")
        self.expenses.append(Expense(amount, category, date, description))
        self.save()

    def report(self):
        if not self.expenses:
            print("No expenses recorded.")
            return
        totals = {}
        for e in self.expenses:
            totals[e.category] = totals.get(e.category, 0) + e.amount
        print("\n--- Expense Report ---")
        for cat, total in sorted(totals.items()):
            print(f"  {cat:20s}: ${total:.2f}")
        print(f"  {'TOTAL':20s}: ${sum(totals.values()):.2f}")

    def save(self):
        with open(self.FILE, "w", newline="") as f:
            writer = csv.DictWriter(f, fieldnames=self.FIELDS)
            writer.writeheader()
            writer.writerows([e.to_dict() for e in self.expenses])

    def load(self):
        if os.path.exists(self.FILE):
            with open(self.FILE) as f:
                self.expenses = [Expense(**row) for row in csv.DictReader(f)]
```

### Key Things to Look For
- CSV or JSON file used for persistence
- Report groups and totals by category
- Amount validation prevents negative/zero entries

---

## Project 3: Grade Calculator

### Feature Checklist
- [ ] Add student with name and list of grades
- [ ] Calculate average, letter grade, GPA points
- [ ] View individual student report
- [ ] View class summary (highest/lowest average, class average)
- [ ] Save/load data (JSON or CSV)
- [ ] Handle edge case of no grades entered

### Model Skeleton
```python
import json, os

def letter_grade(avg):
    if avg >= 90: return "A"
    elif avg >= 80: return "B"
    elif avg >= 70: return "C"
    elif avg >= 60: return "D"
    else: return "F"

def gpa_points(letter):
    return {"A": 4.0, "B": 3.0, "C": 2.0, "D": 1.0, "F": 0.0}.get(letter, 0.0)

class Student:
    def __init__(self, name, grades=None):
        self.name = name
        self.grades = grades or []

    @property
    def average(self):
        return sum(self.grades) / len(self.grades) if self.grades else 0

    def report(self):
        avg = self.average
        letter = letter_grade(avg)
        print(f"\n{self.name}")
        print(f"  Grades : {self.grades}")
        print(f"  Average: {avg:.1f}  |  Grade: {letter}  |  GPA: {gpa_points(letter):.1f}")

    def to_dict(self):
        return {"name": self.name, "grades": self.grades}
```

### Key Things to Look For
- Letter grade and GPA calculated correctly
- Class-wide summary statistics shown
- Edge case handled when student has no grades

---

## Project 4: Quiz Application

### Feature Checklist
- [ ] Load questions from a file (JSON or CSV)
- [ ] Present questions one at a time with multiple choice options
- [ ] Track score as quiz progresses
- [ ] Show final score and percentage at the end
- [ ] Show correct answer for any missed questions
- [ ] Allow multiple quiz attempts
- [ ] At least 5 questions in the question bank

### Model Skeleton
```python
import json, random

class Quiz:
    def __init__(self, filepath):
        with open(filepath) as f:
            self.questions = json.load(f)

    def run(self):
        random.shuffle(self.questions)
        score = 0
        for i, q in enumerate(self.questions, 1):
            print(f"\nQ{i}: {q['question']}")
            for j, opt in enumerate(q["options"], 1):
                print(f"  {j}. {opt}")
            try:
                answer = int(input("Your answer: "))
                if q["options"][answer - 1] == q["answer"]:
                    print("Correct!")
                    score += 1
                else:
                    print(f"Wrong. Answer: {q['answer']}")
            except (ValueError, IndexError):
                print(f"Invalid. Answer: {q['answer']}")
        pct = score / len(self.questions) * 100
        print(f"\nFinal Score: {score}/{len(self.questions)} ({pct:.1f}%)")
```

### Sample questions.json format
```json
[
  {
    "question": "What does OOP stand for?",
    "options": ["Object-Oriented Programming", "Open Output Protocol", "Ordered Object Processing", "None of these"],
    "answer": "Object-Oriented Programming"
  }
]
```

### Key Things to Look For
- Questions loaded from external file (not hardcoded)
- Score tracked and reported at end
- Wrong answers show the correct answer

---

## Project 5: Weather Dashboard

### Feature Checklist
- [ ] Fetch current weather from a public API (e.g., Open-Meteo, wttr.in)
- [ ] Display temperature, conditions, humidity
- [ ] Allow user to enter any city
- [ ] Show a 3–5 day forecast
- [ ] Handle API errors and invalid city names
- [ ] Optional: visualize temperature trend with Matplotlib

### Model Skeleton
```python
import requests

def get_weather(city):
    # Using wttr.in JSON API (no key required)
    url = f"https://wttr.in/{city}?format=j1"
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        data = response.json()
        current = data["current_condition"][0]
        print(f"\nWeather in {city}:")
        print(f"  Temp     : {current['temp_F']}°F")
        print(f"  Feels like: {current['FeelsLikeF']}°F")
        print(f"  Condition : {current['weatherDesc'][0]['value']}")
        print(f"  Humidity  : {current['humidity']}%")
        # 3-day forecast
        print("\n3-Day Forecast:")
        for day in data["weather"]:
            print(f"  {day['date']}: High {day['maxtempF']}°F / Low {day['mintempF']}°F")
    except requests.exceptions.RequestException as e:
        print(f"Error fetching weather: {e}")
    except (KeyError, IndexError):
        print("City not found or unexpected data format.")
```

### Key Things to Look For
- API call made with error handling
- At least current conditions displayed
- City not found handled gracefully

---

## Project 6: Contact Manager

### Feature Checklist
- [ ] Add contact (name, phone, email, optional notes)
- [ ] Search contacts by name or phone
- [ ] Edit an existing contact
- [ ] Delete a contact
- [ ] List all contacts (alphabetically)
- [ ] Export/import contacts (CSV or JSON)
- [ ] Input validation (valid email format check, non-empty name)

### Model Skeleton
```python
import json, os, re

class Contact:
    def __init__(self, name, phone, email, notes=""):
        self.name = name
        self.phone = phone
        self.email = email
        self.notes = notes

    def to_dict(self):
        return vars(self)

    def __str__(self):
        return f"{self.name} | {self.phone} | {self.email}"

def valid_email(email):
    return bool(re.match(r"[^@]+@[^@]+\.[^@]+", email))
```

### Key Things to Look For
- Search works by partial name match
- Contacts persist between runs
- Email validated before saving

---

## Project 7: Habit Tracker

### Feature Checklist
- [ ] Add a habit to track (name, frequency goal)
- [ ] Log completion of a habit for today
- [ ] View habit history and current streak
- [ ] Calculate completion percentage over last 30 days
- [ ] Save/load data (JSON)
- [ ] Prevent duplicate logging for the same day

### Model Skeleton
```python
import json, os
from datetime import date, timedelta

class Habit:
    def __init__(self, name):
        self.name = name
        self.log = []  # list of date strings "YYYY-MM-DD"

    def check_in(self):
        today = str(date.today())
        if today in self.log:
            print(f"Already logged '{self.name}' today.")
        else:
            self.log.append(today)
            print(f"'{self.name}' logged for {today}!")

    @property
    def streak(self):
        if not self.log:
            return 0
        sorted_log = sorted(self.log, reverse=True)
        streak = 0
        check = date.today()
        for entry in sorted_log:
            if str(check) == entry:
                streak += 1
                check -= timedelta(days=1)
            else:
                break
        return streak

    def to_dict(self):
        return {"name": self.name, "log": self.log}
```

### Key Things to Look For
- Streak calculated correctly (consecutive days ending today)
- Duplicate log entries for same day prevented
- Data persists between sessions

---

## Project 8: Movie Database

### Feature Checklist
- [ ] Add a movie (title, genre, year, rating, watched status)
- [ ] Search movies by title or genre
- [ ] Rate/update a movie's rating
- [ ] View watchlist (unwatched movies)
- [ ] View watched movies sorted by rating
- [ ] Save/load database (JSON or CSV)

### Model Skeleton
```python
import json, os

class Movie:
    def __init__(self, title, genre, year, rating=None, watched=False):
        self.title = title
        self.genre = genre
        self.year = int(year)
        self.rating = float(rating) if rating else None
        self.watched = watched

    def __str__(self):
        stars = f"{self.rating}/10" if self.rating else "Unrated"
        status = "Watched" if self.watched else "Unwatched"
        return f"{self.title} ({self.year}) | {self.genre} | {stars} | {status}"

    def to_dict(self):
        return vars(self)
```

### Key Things to Look For
- Search is case-insensitive
- Rating stored as float, validated 0–10
- Watchlist filtered correctly

---

## Project 9: Personal Finance Tracker

### Feature Checklist
- [ ] Log income and expenses with categories
- [ ] View current balance (income minus expenses)
- [ ] Set a monthly budget per category
- [ ] Alert when spending exceeds budget in a category
- [ ] Show monthly summary report
- [ ] Save/load transactions (JSON or CSV)

### Key Things to Look For
- Balance calculation is accurate
- Budget alerts trigger correctly
- Report clearly separates income vs expenses

---

## Project 10: Study Aid / Flashcard App

### Feature Checklist
- [ ] Create a deck with a name
- [ ] Add cards (front/back) to a deck
- [ ] Study mode: show front, user guesses, reveal back
- [ ] Track correct/incorrect for each card in a session
- [ ] Show session summary (% correct)
- [ ] Save/load decks (JSON)
- [ ] Optional: spaced repetition (show harder cards more often)

### Model Skeleton
```python
import json, os, random

class Card:
    def __init__(self, front, back):
        self.front = front
        self.back = back

class Deck:
    def __init__(self, name):
        self.name = name
        self.cards = []

    def add_card(self, front, back):
        self.cards.append(Card(front, back))

    def study(self):
        if not self.cards:
            print("No cards in this deck.")
            return
        random.shuffle(self.cards)
        correct = 0
        for card in self.cards:
            print(f"\nFront: {card.front}")
            input("Press Enter to reveal...")
            print(f"Back: {card.back}")
            got_it = input("Did you get it? (y/n): ").lower()
            if got_it == "y":
                correct += 1
        pct = correct / len(self.cards) * 100
        print(f"\nSession complete: {correct}/{len(self.cards)} correct ({pct:.0f}%)")
```

### Key Things to Look For
- Cards randomized each session
- Session score tracked and reported
- Decks saved and reloaded correctly

---

## Projects 11–15: Quick Checklists

### Project 11: Workout Planner
- [ ] Create/save workout routines (exercise, sets, reps)
- [ ] Log completed workouts with date
- [ ] View progress over time
- [ ] Calculate totals (sets, reps, days active)
- [ ] Save data to file

### Project 12: Meal Planner
- [ ] Plan meals for the week (breakfast, lunch, dinner)
- [ ] Generate consolidated shopping list
- [ ] Track calories/nutrition (optional)
- [ ] Save/load weekly plan to JSON

### Project 13: Reading Tracker
- [ ] Add books (title, author, pages, status: reading/read/want to read)
- [ ] Update reading progress (current page)
- [ ] Rate finished books
- [ ] View reading stats (books finished, pages read)
- [ ] Save to JSON

### Project 14: Discord/Chat Bot (Advanced)
- [ ] Uses `discord.py` library
- [ ] Responds to at least 3 commands (e.g., `!help`, `!hello`, `!roll`)
- [ ] Error handling for unknown commands
- [ ] Token stored securely (not hardcoded)
- [ ] Bot goes online and stays responsive

### Project 15: Data Analysis Tool
- [ ] Accept a CSV file as input
- [ ] Calculate descriptive stats (mean, median, std, min, max) for numeric columns
- [ ] Filter rows by a condition
- [ ] Export cleaned/filtered data to new CSV
- [ ] Plot at least one chart with Matplotlib
- [ ] Handle missing/malformed data gracefully

---

## General Code Quality Checklist (all projects)

- [ ] No hardcoded data that should be dynamic
- [ ] Functions/methods are focused (single responsibility)
- [ ] At least one class used where appropriate
- [ ] No bare `except:` clauses (catch specific exceptions)
- [ ] All file operations use `with` statement
- [ ] Variable and function names are descriptive
- [ ] Code is commented where logic is non-obvious
- [ ] Program doesn't crash on bad user input
- [ ] Main logic wrapped in `if __name__ == "__main__":`
