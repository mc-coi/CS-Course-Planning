# Unit 6: APIs & External Libraries

> Connect your programs to the world: use external libraries and web APIs to build powerful real-world applications.

---

## Unit Overview

**Duration:** 22 days / ~4.5 weeks  
**Course Days:** 134–155  
**Standards Alignment:** 9-12.CCI.5 (Use libraries and APIs)

### Learning Objectives

By the end of this unit, students will be able to:
- Make HTTP requests to external APIs using the requests library
- Parse JSON responses and extract meaningful data
- Handle API authentication and errors gracefully
- Use Python's standard library modules (random, math, datetime, collections)
- Perform numerical computing with NumPy
- Create professional data visualizations with Matplotlib
- Build complete applications integrating APIs and visualization

---

## Unit Structure

### Part 1: Web APIs (Days 1-9)
- What is an API? HTTP basics, JSON review
- The requests library: GET requests, JSON parsing
- Error handling and status codes
- API authentication and rate limiting
- Multiple public APIs integration

### Part 2: Standard Library Modules (Days 10-15)
- random module: randomness and shuffling
- math module: advanced calculations
- datetime module: working with dates and times
- collections module: specialized data structures
- NumPy and Matplotlib basics

### Part 3: Data Visualization (Days 16-22)
- NumPy advanced operations
- Matplotlib visualization techniques
- Complete data visualization projects
- Project polish and presentation
- Unit assessment

---

## Daily Lesson Structure

### Day 1: What is an API?
**Topics:** API definition, REST principles, HTTP methods, JSON review  
**Activities:** Define APIs, discuss real-world examples  
**Assessment:** Short answer questions

### Day 2: HTTP Methods & JSON Review
**Topics:** HTTP status codes, JSON parsing, format conversion  
**Activities:** Parse JSON from strings, convert between formats  
**Assessment:** Practice problems

### Day 3: The requests Library – GET Requests
**Topics:** Making GET requests, accessing response data  
**Activities:** Fetch quotes, Pokemon data  
**Assessment:** API call practice problems

### Day 4: Parsing JSON Responses
**Topics:** Navigating nested JSON, accessing lists within objects  
**Activities:** Extract specific data from complex responses  
**Assessment:** Data extraction challenges

### Day 5: Using Public APIs
**Topics:** Free public APIs, query parameters  
**Activities:** Weather API, multiple API calls, loops  
**Assessment:** Multi-API integration

### Day 6: API Keys & Authentication
**Topics:** API authentication, environment variables, best practices  
**Activities:** Discuss authentication methods, environment setup  
**Assessment:** Security practices discussion

### Day 7: Error Handling with APIs
**Topics:** Exception handling, timeouts, retry logic  
**Activities:** Robust API calls with try-except, timeout handling  
**Assessment:** Error handling implementation

### Day 8: Weather & Data APIs Integration
**Topics:** Multi-API calls, data combination, practical applications  
**Activities:** Weather dashboard, data fetching from multiple endpoints  
**Assessment:** Integrated API project

### Day 9: Building Multi-API Applications
**Topics:** Application design, workflow planning, code organization  
**Activities:** Complete multi-API project planning  
**Assessment:** Project checkpoint

### Day 10: The random Module
**Topics:** Random numbers, choice, shuffle, seed  
**Activities:** Games, randomization, reproducibility  
**Assessment:** random module practice

### Day 11: The math & datetime Modules
**Topics:** Math functions, constants, date/time objects  
**Activities:** Calculations, date arithmetic  
**Assessment:** Module usage problems

### Day 12: The datetime Module – Dates & Formatting
**Topics:** Date creation, formatting, parsing, calculations  
**Activities:** Format dates, calculate durations  
**Assessment:** DateTime practice

### Day 13: The collections Module
**Topics:** Counter, defaultdict, deque, OrderedDict  
**Activities:** Count frequencies, manage queues  
**Assessment:** Collections usage

### Day 14: Introduction to NumPy – Arrays & Operations
**Topics:** NumPy arrays, basic operations, statistics  
**Activities:** Create arrays, perform math, calculate stats  
**Assessment:** NumPy fundamentals

### Day 15: Introduction to Matplotlib – Visualization
**Topics:** Line plots, bar charts, customization  
**Activities:** Create basic charts, add formatting  
**Assessment:** Visualization basics

### Day 16: NumPy Arrays – Advanced Operations
**Topics:** Filtering, sorting, reshaping, broadcasting  
**Activities:** Advanced array manipulation  
**Assessment:** NumPy advanced practice

### Day 17: Matplotlib – Advanced Visualization
**Topics:** Subplots, styling, annotations  
**Activities:** Multi-plot dashboards, professional formatting  
**Assessment:** Advanced visualization

### Day 18: Data Visualization Project – Part 1
**Topics:** Project planning, data fetching  
**Activities:** Plan and start weather visualization project  
**Assessment:** Project planning checkpoint

### Day 19: Data Visualization Project – Part 2
**Topics:** Data processing, multiple visualizations  
**Activities:** Complete dashboard, error handling  
**Assessment:** Project functionality

### Day 20: Project Completion & Polish
**Topics:** Documentation, code quality, professional output  
**Activities:** Final polishing, saving high-quality output  
**Assessment:** Project completion

### Day 21: Project Completion & Review
**Topics:** Testing, documentation, presentation prep  
**Activities:** Review and finalize projects  
**Assessment:** Final project submission

### Day 22: Unit Assessment
**Topics:** Comprehensive evaluation  
**Assessment:** Multiple choice, short answer, coding challenges

---

## Key Concepts

### APIs & HTTP
- **API (Application Programming Interface):** Set of rules for software communication
- **HTTP (HyperText Transfer Protocol):** Standard for web communication
- **REST (Representational State Transfer):** API design using HTTP methods
- **Endpoint:** Specific URL handling requests
- **Status Codes:** 2xx (success), 4xx (client error), 5xx (server error)

### Data Formats
- **JSON:** Lightweight data format with key-value pairs
- **Query Parameters:** URL parameters to customize API requests
- **Headers:** Metadata about HTTP requests/responses

### Standard Library
- **random:** Generate random values, shuffle, seed
- **math:** Mathematical constants and functions
- **datetime:** Work with dates and times
- **collections:** Specialized data structures (Counter, deque, defaultdict)

### NumPy & Data Science
- **NumPy Array:** Efficient numerical data structure
- **Vectorization:** Operations on entire arrays without loops
- **Boolean Indexing:** Filter arrays using conditions
- **Broadcasting:** Apply operations across different-sized arrays

### Visualization
- **Matplotlib:** Create static and interactive plots
- **Chart Types:** Line, bar, scatter, histogram
- **Subplots:** Multiple charts in one figure
- **Customization:** Colors, styles, annotations, labels

---

## Common Mistakes & How to Avoid Them

| Mistake | Impact | Solution |
|---------|--------|----------|
| Hardcoded API keys | Security risk | Use environment variables |
| No error handling | Program crashes | Use try-except blocks |
| Ignoring status codes | Silently fails | Check `response.status_code` |
| Parsing wrong data | KeyError exceptions | Explore JSON structure first |
| Not setting timeout | Program hangs | Use `timeout=5` parameter |
| Using lists for math | Slow performance | Use NumPy arrays |
| Poor visualization | Unclear data | Add titles, labels, legends |
| Hardcoded test data | Can't use real data | Fetch from APIs instead |

---

## Assessment Preparation

### Topics Covered on Assessment
- HTTP methods and status codes
- JSON parsing and conversion
- requests library usage
- Error handling patterns
- Standard library modules
- NumPy array operations
- Matplotlib visualization
- API integration
- Data processing workflows

### Practice Resources
- Daily lesson practice problems (3 per day)
- Unit practice problems (15 comprehensive)
- Reference guide for quick lookup
- Sample assessment answers

### Study Tips
1. Review daily notes from Days 1-21
2. Practice writing code (don't just read examples)
3. Test your code with different inputs
4. Use the reference guide during practice
5. Focus on understanding concepts, not memorizing
6. Test error handling with bad inputs
7. Create your own test cases

---

## Vocabulary Reference

| Term | Definition |
|------|-----------|
| **API** | Application Programming Interface; rules for software communication |
| **Endpoint** | Specific URL that handles requests |
| **HTTP** | HyperText Transfer Protocol; standard for web data transfer |
| **JSON** | JavaScript Object Notation; lightweight data format |
| **REST** | Representational State Transfer; API design pattern |
| **Status Code** | Number indicating HTTP response result (200, 404, etc.) |
| **Timeout** | Maximum time to wait for API response |
| **Authentication** | Verifying identity (usually with API key) |
| **Query Parameter** | URL parameter to customize request |
| **Exception** | Error that interrupts normal program flow |
| **Vectorization** | Operations on entire arrays without loops |
| **Visualization** | Creating charts/graphs from data |
| **Matplotlib** | Python library for creating plots |
| **NumPy** | Python library for numerical computing |
| **Seed** | Starting point for random number generator |
| **Filtering** | Selecting elements based on conditions |
| **Subplot** | Multiple plots in one figure |

---

## Resources & References

### Official Documentation
- requests: https://docs.python-requests.org
- NumPy: https://numpy.org/doc
- Matplotlib: https://matplotlib.org/docs
- Python datetime: https://docs.python.org/3/library/datetime.html
- Python collections: https://docs.python.org/3/library/collections.html

### Public APIs (Free, No Key)
- Quotes: https://api.quotable.io
- Pokemon: https://pokeapi.co
- Weather: https://api.open-meteo.com
- Jokes: https://v2.jokeapi.dev
- Cat Facts: https://catfact.ninja

### Tools & Setup
- Python 3.8+
- pip (package manager)
- requests library: `pip install requests`
- NumPy: `pip install numpy`
- Matplotlib: `pip install matplotlib`

---

## Extension Activities

For advanced students:

1. **Interactive Dashboards:** Use Plotly for interactive visualizations
2. **Multi-Threading:** Fetch from multiple APIs concurrently
3. **Database Integration:** Store API data in a database
4. **Web Scraping:** Extract data from HTML pages
5. **Machine Learning:** Analyze fetched data with ML models
6. **API Creation:** Build your own API using Flask
7. **Real-Time Updates:** Create live-updating dashboards
8. **Data Pipeline:** Automate data collection and processing

---

## Unit Completion Checklist

By the end of this unit, you should be able to:

- [ ] Explain what an API is and how it works
- [ ] Make GET and POST requests using the requests library
- [ ] Parse JSON data and extract specific values
- [ ] Handle API errors gracefully
- [ ] Use query parameters to customize API requests
- [ ] Work securely with API keys using environment variables
- [ ] Use the random module for randomization
- [ ] Perform date/time operations with datetime
- [ ] Count frequencies with Counter
- [ ] Create and manipulate NumPy arrays
- [ ] Perform filtering and sorting on arrays
- [ ] Create basic and advanced matplotlib visualizations
- [ ] Integrate multiple APIs into a single application
- [ ] Build and polish a complete data visualization project
- [ ] Demonstrate unit mastery on the assessment

---

## Grade Distribution

| Component | Weight |
|-----------|--------|
| Daily Activities & Practice | 30% |
| Project (Days 18-21) | 30% |
| Unit Assessment (Day 22) | 40% |

---

**Next Unit:** Unit 7 - [Upcoming Topic]

