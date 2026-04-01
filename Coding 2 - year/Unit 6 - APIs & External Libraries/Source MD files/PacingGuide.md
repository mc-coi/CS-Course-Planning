# Unit 6 - APIs & External Libraries: Pacing & Differentiation Guide

## Unit Overview

- **Total days allocated:** 22 days (~4.5 weeks)
- **Core topics covered:**
  - What is an API? HTTP methods and REST principles
  - The requests library for HTTP requests
  - JSON parsing from API responses
  - API authentication and keys
  - Error handling and rate limiting
  - Public APIs (weather, news, social media, cryptocurrency)
  - Standard library modules (random, math, datetime, collections)
  - NumPy for numerical computing
  - Matplotlib for data visualization
  - Building complete applications with APIs and visualization
- **Prerequisites students need:**
  - Unit 4: File I/O, exception handling
  - Unit 3: Data structures, comprehensions
  - JSON parsing basics
  - HTTP and web concepts (basic understanding)
  - String manipulation and formatting

---

## Week-by-Week Pacing

### Week 1 (Days 1–5): Web APIs Fundamentals

#### Day 1: What is an API? HTTP Basics & REST
- **Essential days** (must teach): YES
  - Foundation for understanding web APIs
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Advanced HTTP concepts, SOAP vs REST, API design patterns
- **If behind pace**: Focus on GET requests only; skip POST/PUT/DELETE initially

#### Day 2: HTTP Status Codes & JSON Review
- **Essential days** (must teach): YES
  - Understanding response codes and JSON parsing is essential
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Error code strategies, JSON schema validation
- **If behind pace**: Focus on 200, 404, 500; simple JSON structures

#### Days 3–5: The requests Library & API Calls
- **Essential days** (must teach): YES
  - Making HTTP requests is core skill
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Advanced request options (headers, timeout, retries), request sessions
- **If behind pace**: Simple GET requests only with json() parsing

### Week 2 (Days 6–11): API Integration & Public APIs

#### Days 6–7: API Authentication & Error Handling
- **Essential days** (must teach): YES
  - Handling API keys and errors is critical for production code
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: OAuth, API key rotation, advanced error recovery
- **If behind pace**: Simple API key in URL; basic try/except for errors

#### Days 8–9: Using Multiple Public APIs
- **Essential days** (must teach): YES
  - Working with real APIs teaches practical skills
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: API chaining, combining data from multiple sources
- **If behind pace**: Using one API well; focus on one data source

#### Days 10–11: Building Multi-API Applications Lab
- **Essential days** (must teach): YES
  - Integration of API concepts
- **Flexible days** (can compress or cut if pressed for time): Can be 1 day if behind
- **If ahead of pace**: Complex data transformation, caching, optimization
- **If behind pace**: Provide templates; focus on working API calls

### Week 3 (Days 12–17): Standard Library & Data Processing

#### Days 12–13: Standard Library Modules (random, math, datetime, collections)
- **Essential days** (must teach): YES
  - These modules are frequently used
- **Flexible days** (can compress or cut if pressed for time): Can simplify to 1 day
- **If ahead of pace**: Advanced module features, combinations of modules
- **If behind pace**: Focus on random and math only; skip datetime/collections initially

#### Days 14–15: NumPy Basics for Numerical Computing
- **Essential days** (must teach): PARTIAL
  - NumPy is powerful but not essential for all students
- **Flexible days** (can compress or cut if pressed for time): YES — can be deferred or simplified
- **If ahead of pace**: Advanced NumPy operations, performance optimization
- **If behind pace**: Skip NumPy or use lists instead; focus on core concepts

#### Days 16–17: Matplotlib for Data Visualization
- **Essential days** (must teach): YES
  - Visualization is powerful and engaging for students
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Advanced visualization types, animation, interactive plots
- **If behind pace**: Simple line plots and bar charts only

### Week 4 (Days 18–22): Integration & Assessment

#### Days 18–19: Complete Project Lab (API + Visualization)
- **Essential days** (must teach): YES
  - Integration of all unit concepts
- **Flexible days** (can compress or cut if pressed for time): Can be 1 day if behind
- **If ahead of pace**: Complex data pipelines, multiple visualizations, advanced features
- **If behind pace**: Provide templates; focus on putting concepts together

#### Day 20: Code Review & Best Practices
- **Essential days** (must teach): YES
  - Learning from mistakes and production considerations
- **Flexible days** (can compress or cut if pressed for time): Can combine with Day 19
- **If ahead of pace**: Security practices, performance optimization, API best practices
- **If behind pace**: Teacher-led examples only

#### Days 21–22: Unit Assessment
- **Essential days** (must teach): YES
  - Assessment required
- **Flexible days** (can compress or cut if pressed for time): NONE
- **If ahead of pace**: Early completers start Unit 7 or get enrichment
- **If behind pace**: Extended time if needed

---

## Differentiation Strategies

### For Struggling Students

**Common gaps:**
- Unfamiliar with HTTP and web concepts
- Weak JSON parsing skills
- Difficulty understanding API authentication
- Limited experience with external libraries

**Specific scaffolding:**
- Provide **"API Cheat Sheet"** with request syntax and common status codes
- Use **concrete APIs** consistently (same API throughout unit)
- Create **step-by-step guides** for each API used
- Provide **code templates** for making requests and parsing responses
- Create **error code reference** with meanings and solutions
- Show **visual API documentation** examples

**Which practice problems to assign first:**
- Simple GET requests to weather API
- Parsing simple JSON responses
- Basic error handling with try/except
- Using random and math modules
- Simple matplotlib bar charts

**Suggested pacing adjustments:**
- Skip OAuth and complex authentication; use simple API keys only
- Skip NumPy or use lists instead
- Simplify visualization to basic plots
- Provide full request templates
- Use same API throughout instead of multiple APIs
- Skip advanced library modules (datetime, collections)

**Prerequisite gaps to watch for:**
- If weak on JSON, parsing API responses will be hard; review JSON
- If weak on exception handling, error handling will struggle; review try/except
- If weak on data structures, working with API data will be slow; review dicts/lists

**Reteaching strategies:**
- Use the same API and same data throughout
- Show successful request and response side-by-side
- Trace through JSON parsing step-by-step
- Demonstrate common errors and how to fix them
- Pair with stronger students for lab days

### For On-Track Students

**Standard path:**
- Follow the daily breakdown as outlined
- Make requests to multiple public APIs
- Parse JSON responses and extract data
- Handle basic authentication and errors
- Create visualizations with Matplotlib
- Build a complete API application

**Which practice problems to assign:**
- Making requests to 2-3 different APIs
- Parsing nested JSON structures
- Error handling with multiple exception types
- Using standard library modules
- Creating multiple visualization types
- Building a functional API application

**Pacing tips:**
- Days 1–5 should feel manageable (requests fundamentals)
- Days 6–11 get more complex (multiple APIs, error handling); monitor closely
- Days 12–17 introduce new libraries (NumPy, Matplotlib); manage expectations
- Days 18–19 are consolidation; should feel rewarding

### For Advanced Students

**Extension activities:**
- Build advanced API applications with multiple data sources
- Implement caching strategies for API responses
- Create interactive visualizations with plotly
- Use pandas for advanced data processing
- Implement API rate limiting strategies
- Build API wrappers and custom libraries
- Study API design and create their own endpoints
- Explore web scraping as alternative to APIs

**Challenge problems to assign:**
- Chaining multiple API calls to combine data
- Advanced data visualization with multiple plots
- Building a complete dashboard application
- Handling complex authentication schemes
- Implementing robust error recovery
- Performance optimization for API calls
- Creating reusable API client classes

**Ways to deepen understanding:**
- Study real-world API documentation and usage
- Learn about OAuth and API security
- Explore different HTTP methods (POST, PUT, DELETE)
- Study GraphQL as alternative to REST
- Learn about API versioning and backwards compatibility
- Study caching and CDN strategies
- Build and document their own simple API

---

## Flexibility Notes

### Natural pause points for re-teaching:
- **After Day 5:** Checkpoint for requests library before moving to authentication
- **After Day 11:** Checkpoint for API integration before libraries
- **After Day 17:** Checkpoint for visualization before assessment

### Topics students typically struggle with:
1. **HTTP concepts** (Day 1): Abstract web concepts
   - *Fix:* Concrete examples, visualizations, show request/response pairs
2. **JSON parsing** (Days 2–5): Navigating nested structures
   - *Fix:* Print intermediate steps, visual walkthroughs
3. **API authentication** (Days 6–7): Managing secrets and keys
   - *Fix:* Show examples, emphasize never hardcoding keys
4. **Error handling** (Days 6–7): Knowing what can go wrong
   - *Fix:* Show common errors, how to recover
5. **NumPy and Matplotlib** (Days 14–17): New libraries and concepts
   - *Fix:* Provide templates, focus on understanding usage

### Topics students typically move through quickly:
1. **Making GET requests** (Days 3–5): Once they see it working
2. **Parsing simple JSON** (Days 2, 4): Once they understand the structure
3. **Using standard library** (Days 12–13): Functions are straightforward
4. **Basic visualization** (Days 16–17): Matplotlib is intuitive once explained

---

## Suggested Checkpoints

### Formative checks (mid-unit, low-stakes):
1. **After Day 5:** Can students make successful API requests?
   - Quick task: "Get weather data from API and print temperature"
2. **After Day 11:** Can students handle errors and authentication?
   - Quick task: "Make request with API key and handle 404 error"
3. **After Day 17:** Can students visualize data?
   - Quick task: "Create bar chart from API data"

### Summative checks (end-of-unit):
1. **Days 21–22 Assessment:**
   - Part A: Multiple choice (API concepts, HTTP, JSON)
   - Part B: Short answer (API design, error handling)
   - Part C: Coding (make API request, parse response, visualize data)

### Lab checkpoints (Days 11, 17, 18–19):
- Demonstrate API integration and visualization in practice

---

## Notes on Unit 5 Prerequisites

This unit builds on Unit 5 (algorithms and data processing). Watch for:

- **JSON:** If weak, API response parsing will be hard; review JSON basics
- **Exception handling:** If weak, error handling will struggle; review try/except
- **Data structures:** Must understand dicts and lists for working with API responses
- **String manipulation:** May need to work with URLs and response text

---

## Time Management Tips

- **If 5 days ahead:** Use time for advanced APIs, interactive visualizations, or early Unit 7 start
- **If 3 days behind:** Simplify to one API, skip NumPy, provide visualization templates
- **If 1 week behind:** Focus only on requests library and basic visualization; skip NumPy and advanced topics
- **If 2 weeks behind:** Teach only basic API requests and simple Matplotlib; skip libraries

---

## Key Assessment Targets

By the end of Unit 6, all students should demonstrate:
1. Making HTTP requests with the requests library
2. Parsing JSON responses from APIs
3. Handling basic API authentication
4. Error handling for API calls
5. Using standard library modules (random, math, datetime)
6. Creating visualizations with Matplotlib
7. Building a working application that uses APIs

Students working at advanced level should additionally demonstrate:
- Multiple API integration
- Complex data processing with NumPy
- Advanced visualizations
- Caching and performance optimization
- Robust error recovery
- API security best practices
