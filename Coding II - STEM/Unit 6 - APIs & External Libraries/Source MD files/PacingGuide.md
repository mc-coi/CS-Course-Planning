# Unit 6 - APIs & External Libraries: Pacing & Differentiation Guide

## Unit Overview
- **Total days allocated:** 6 days / 2 weeks
- **Core topics covered:** Package management (pip), virtual environments, requests library, REST APIs and HTTP requests, JSON parsing, data visualization (matplotlib), numerical computing (numpy), and integrating multiple libraries
- **Prerequisites students need:** Comfortable with data structures (Unit 1); experience with file I/O and JSON (Unit 4); ability to read and understand API documentation

## Week-by-Week Pacing

### Week 1 (Days 1–3): Packages, APIs & Data Fetching
- **Essential days** (must teach):
  - Day 1: Pip and package management; installing packages; virtual environments (optional but recommended)
  - Day 2: Making HTTP requests with requests library; understanding API responses
  - Day 3: Parsing JSON from API responses; working with real data

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip virtual environments; focus on pip install and basic requests
  - Combine Days 1–2; teach pip and requests together in single day
  - Use provided API URLs; don't require students to research APIs

- **If ahead of pace:**
  - Extend Day 1: Explore virtual environments deeply; requirements.txt management
  - Extend Day 2: Handle errors in API requests; retry logic
  - Extend Day 3: Explore pagination; work with complex nested JSON

- **If behind pace:**
  - Provide pip commands ready to copy-paste
  - Give pre-written requests code; students modify parameters only
  - Provide simple JSON structure APIs; skip complex nested responses

### Week 2 (Days 4–6): Visualization & Integration
- **Essential days** (must teach):
  - Day 4: Data visualization with matplotlib; creating plots from data
  - Day 5: Numerical operations with numpy; performing calculations on datasets
  - Day 6: Integrated project combining multiple libraries

- **Flexible days** (can compress or cut if pressed for time):
  - If behind: Skip numpy; focus on API data visualization with matplotlib
  - Use matplotlib for basic plots only (line, bar); skip complex visualizations
  - Simplify project; use provided plotting code

- **If ahead of pace:**
  - Extend Day 4: Advanced matplotlib; multiple plots, subplots, customization
  - Extend Day 5: Advanced numpy operations; arrays, matrices, statistics
  - Extend Day 6: Build dashboard-like application with multiple visualizations

- **If behind pace:**
  - Combine Days 4–5: Focus on matplotlib only; skip numpy depth
  - Provide plotting templates; students just modify data
  - Project: Simplified; heavy scaffolding

## Differentiation Strategies

### For Struggling Students
**Scaffolding tips:**
- Explain API as "asking a website for data in a structured way"
- Use curl or browser first to show API response before code
- pip installation can be intimidating; demystify with step-by-step guide
- Emphasize that errors from external APIs are normal; teach debugging
- Matplotlib: Start with simple line plots before exploring customization
- Numpy: Focus on basic operations; don't overwhelm with advanced functions

**Which practice problems to assign first (easiest wins):**
- Unit Practice #1–2: Install package with pip; make GET request
- Unit Practice #3: Parse JSON response
- Unit Practice #5: Create simple line plot with matplotlib
- Unit Practice #6: Perform basic numpy operations
- Emphasize: Getting code to run before understanding deep concepts

**Suggested pacing adjustments:**
- Spend extra time on pip installation; many students struggle with command line
- Provide working API URLs and authentication tokens; don't require setup
- Use simple APIs (open, no authentication) for initial learning
- Matplotlib: Start with data you already have before fetching from APIs
- Numpy: Focus on practical operations (mean, sum, filtering) before theory

**What prerequisite gaps to look for:**
- Command line comfort: pip requires terminal; if students unfamiliar, allow GUI alternatives
- JSON understanding: If Unit 4 weak, parsing API responses is hard
- Data structure navigation: Accessing nested JSON requires comfort with dicts/lists
- File paths: Virtual environments and packages use paths; file path confusion amplifies

### For On-Track Students
**Standard path through the unit:**
- Complete Days 1–6 as designed
- Assign Unit Practice problems #1–10 (progression from installation to integration)
- Complete project integrating multiple libraries (API fetch, data processing, visualization)
- Weekly checks: Successfully install package, make API call, create visualization

**Which practice problems to assign:**
- Problems #1–3: Package management and API basics
- Problems #4–6: Fetching API data, processing, visualization
- Problems #7–10: Complex integrations, multiple libraries, data dashboard
- Project: Fetch from real API, process data, create multiple visualizations

### For Advanced Students
**Extension activities specific to this unit's topics:**
- **Day 2:** Explore API authentication (API keys, OAuth); handle rate limiting
- **Day 4:** Create interactive visualizations with plotly; animated charts
- **Day 5:** Advanced numpy: vectorized operations, statistics, linear algebra
- **Project:** Build complete analytics dashboard with real data

**Challenge problems to assign:**
- Unit Practice #11–15: Real-time data fetcher, statistical analysis, interactive visualizations, multiple APIs, complete analytics app
- Advanced: Fetch from multiple APIs; combine datasets; create comprehensive dashboard
- Challenge: Build real-time monitoring system (continuously fetch and update)
- Challenge: Create data pipeline (fetch API, clean, analyze, visualize)
- Challenge: Implement caching to avoid excessive API calls

**Ways to deepen understanding beyond the curriculum:**
- Explore pandas library for data analysis (more powerful than numpy for tabular data)
- Discuss API design; REST principles
- Build real project: Use public API (weather, news, crypto) for meaningful analysis
- Explore authentication patterns: API keys, OAuth
- Challenge: Create web scraper (alternative to APIs for data collection)

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 3:** Before visualization, ensure API data fetching works—students need confidence
- **After Day 5:** Before project, review data structures and plotting together
- **During project:** Checkpoint at 50% complete to ensure progress

### Topics students most commonly struggle with:
1. **pip installation:** Command line intimidation; understanding packages vs. modules
2. **Virtual environments:** Complexity of isolated environments; when/why needed
3. **API response interpretation:** Understanding JSON structure varies by API; frustration with complexity
4. **HTTP status codes:** Confusion on what 200, 404, 500 mean; debugging failed requests
5. **Rate limiting:** Understanding APIs have limits; handling errors gracefully
6. **Matplotlib syntax:** Many parameters; feels overwhelming at first
7. **Numpy arrays vs. lists:** Different behavior; confusing when to use each

### Topics students typically move through quickly:
1. **Making first API call:** Once `requests.get()` works, students feel success
2. **Parsing simple JSON:** `response.json()` is straightforward
3. **Creating basic line plot:** `plt.plot()` and `plt.show()` are intuitive
4. **Installing packages:** After first success, pip becomes routine
5. **Understanding API concept:** "Getting data from the internet" is relatable

## Suggested Checkpoints

### Quick formative checks to use mid-unit:

**Day 1 Check (5 min):**
- "Install a package using pip" (can be any simple package)
- "Show installed packages with `pip list`"
- Check: Successful installation, understanding of pip command

**Day 2 Check (5 min):**
- "Make a GET request to a simple API"
- "What does `response.status_code` tell you?"
- Check: Correct requests syntax, understanding of HTTP status

**Day 3 Check (5 min):**
- "Fetch JSON from API and parse it"
- "Access a specific nested value"
- Check: Correct `.json()` usage, nested data access

**Day 4 Check (5 min):**
- "Create a line plot with matplotlib"
- "Add title, axis labels"
- Check: Basic matplotlib syntax, customization

**Day 5 Check (5 min):**
- "Create numpy array; calculate mean and std"
- "Perform operation on array elements"
- Check: numpy syntax, understanding of vectorized operations

**Day 6 Check (Project submission):**
- Integration project demonstrates: API fetching, data processing, visualization
- Rubric: Working API integration, correct data handling, functional visualizations, clean code, comments

## STEM-Specific Pacing Notes

**Important:** Unit 6 brings real-world relevance to programming. Tight STEM timeline requires pragmatism about depth.

- **Essential vs. Optional:**
  - Essential: pip, requests library, basic API calls, simple JSON parsing (Days 1–3)
  - Optional: Virtual environments, authentication, advanced visualization (Days 4–6)
  - Cut if behind: numpy, advanced matplotlib, real-time updates

- **Coding 1 Prerequisite Gaps**
  - Watch for students weak in: data structures (reading JSON), loops (processing API data)
  - Unit 4 (File I/O) should be strong; JSON format is same
  - Command line comfort varies; have GUI alternatives ready

- **When to cut:**
  - Skip virtual environments for STEM timeline; use simple pip install
  - Skip numpy entirely if behind; use Python lists instead
  - Focus matplotlib on simple plots only
  - Project: Use provided API and data; reduce visualizations to 2–3

- **When to accelerate:**
  - Fast students explore real-world APIs (weather, news, cryptocurrency, sports)
  - Implement caching to avoid API call limits
  - Build monitoring/alerting system (meaningful real-world application)
  - Have advanced students help peers

**Project scope by level:**
- Minimum: Fetch from 1 simple API, display data in 1 plot, handle errors
- Standard: Fetch from API, process/filter data, create 2–3 visualizations, document API
- Extended: Multiple APIs, data pipeline with cleaning, interactive dashboard, real-time updates

**Connection to other units:**
- **Unit 4:** APIs return JSON; strong Unit 4 skills essential
- **Unit 1:** Data structures needed to navigate API responses
- **Unit 3:** Lambda/comprehensions useful for filtering API data
- **Unit 5:** Sorting/searching real API data is practical application

**Real-world value:**
Unit 6 shows how programming connects to the internet and real data. High engagement opportunity if you choose relevant APIs (crypto, weather, sports, news).
