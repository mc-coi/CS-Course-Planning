# Day 2: Project Selection & Brainstorming

**Session Goal:** Select your capstone project and brainstorm core features and technical approach.

---

## Today's Focus

Today you'll commit to a project and start thinking about what you'll build. If you're doing a custom project, you'll pitch it for approval. You'll also begin exploring the tech requirements and mapping out ideas. This is your chance to ask clarifying questions and get excited about the work ahead.

---

## Work Session Agenda

**Minutes 0-5:** **Standup**
- Teacher: quick reminder of 5 options, custom project requirements
- Students: think about their choice

**Minutes 5-25:** **Project Selection**
- Students commit to ONE project (form or verbal)
- If custom project: student pitches idea to teacher
  - Pitch should address: What? Who? Problem? Which units? Why?
  - Teacher approves or suggests modifications
- Teacher records selections for planning purposes

**Minutes 25-50:** **Brainstorming Session**
- Students begin brainstorming using the **Brainstorming Template** (see below)
- Think about:
  - What specific features will your project have?
  - What data will it work with?
  - Who is the user?
  - What libraries or tools will you need?
- Encourage: sketches, lists, diagrams, pseudocode starters

**Minutes 50-55:** **Wrap-up**
- Save brainstorm notes
- Prepare for Day 3 planning session

---

## Brainstorming Template

Use this template to organize your initial ideas. Bring it to Day 3.

```
PROJECT: [Name]

THE BIG IDEA:
One sentence: what does this app do?

TARGET USER:
Who will use this? (yourself, teachers, students, general public?)

CORE FEATURES (what must it have?):
1.
2.
3.
4.
5.

EXAMPLE USAGE:
Describe a specific scenario of someone using your app. What do they do? What does the app do?

DATA:
What data will your app work with? How will you get it? (file, API, user input, etc.)

TECH STACK:
What libraries, languages, or tools will you use?
- Language: Python
- Libraries: [list]
- File format: [CSV, JSON, etc.]

ROUGH BREAKDOWN:
What are the main components or classes you'll need?
1.
2.
3.

UNKNOWNS / QUESTIONS:
What are you unsure about? What do you need to research?
1.
2.

STRETCH GOALS (nice-to-haves):
1.
2.
```

---

## Technical Tips & Resources

**For Data Analyzer:**
- Remind yourself of file I/O from Unit 4: `open()`, `.read()`, parsing CSV/JSON
- matplotlib basics: `plt.bar()`, `plt.plot()`, `plt.show()`
- Consider: `json.load()` for JSON, `csv.reader()` for CSV

**For API-Powered App:**
- HTTP requests: `import requests` then `requests.get(url)`
- JSON parsing: `json.loads(response.text)` or `response.json()`
- Find a free public API: openweathermap.org, newsapi.org, api.coindesk.com, etc.

**For Student Information System:**
- Warm up on Unit 2 OOP: classes, `__init__`, methods
- File I/O: `json.dump()` to save, `json.load()` to load
- Search and sort from Unit 6: list comprehension, `sorted()` with key parameter

**For Algorithm Visualizer:**
- Brush up on Unit 6: sorting algorithms (bubble, merge, quick)
- `time.time()` for benchmarking
- `random.shuffle()` for test data
- matplotlib for charts

---

## Sample Brainstorm (Data Analyzer)

Here's what a filled-in brainstorm might look like:

```
PROJECT: Weather Trend Analyzer

THE BIG IDEA:
Analyze historical weather data to identify temperature trends and predict next week's weather pattern.

TARGET USER:
Meteorology students, anyone curious about local weather patterns.

CORE FEATURES:
1. Load historical weather data from CSV (temp, date, location)
2. Calculate average, min, max temps for each month
3. Create line chart showing temp over time
4. Search data by date range
5. Export summary report to new CSV

EXAMPLE USAGE:
User runs: python analyzer.py
App loads data/weather_2023.csv
User picks "show trends for June-August"
App displays line chart and summary stats
User exports as results.csv

DATA:
CSV file with columns: date, temp_high, temp_low, precipitation, location
Get from: download from NOAA or create sample data

TECH STACK:
- Language: Python
- Libraries: csv module, matplotlib
- Input: CSV file
- Output: CSV file, PNG chart

ROUGH BREAKDOWN:
1. DataLoader class: read CSV, store records
2. Analyzer class: compute stats, filter, search
3. Visualizer class: create charts
4. main(): orchestrate everything

UNKNOWNS:
- How do I filter CSV data by date range?
- How do I export a chart as PNG?

STRETCH GOALS:
- Predict next week's weather with simple linear regression
- Support multiple locations
```

---

## Reflection / Exit Ticket

1. What project did you choose? Why?
2. What is one feature you're most excited to build?
3. What is one question you still have?

---

## Progress Checklist

- [ ] Project selected and approved (or custom pitch approved)
- [ ] Brainstorming template filled out
- [ ] Top 5 core features identified
- [ ] One key question or unknown noted for Day 3 planning
