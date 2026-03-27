# Day 49: Boolean Variables as Flags

**Learning Target:** I can use Boolean variables to track state and simplify complex conditions.

---

## Key Concepts

A **flag variable** is a Boolean variable that tracks whether something is true or false. Flags make code more readable and allow you to reuse logic.

**Benefits of flags:**
- Makes complex conditions easier to read
- Allows you to store and reuse the result of a condition
- Simplifies debugging
- Represents real-world "status" concepts (logged in, is admin, has permission, etc.)

**Common flag names:**
- `is_*`: `is_admin`, `is_student`, `is_valid`
- `has_*`: `has_license`, `has_permission`, `has_error`
- `can_*`: `can_vote`, `can_drive`, `can_enter`

---

## Code Examples

```python
# Using flags for clarity
age = 17
has_license = True
passed_test = True

# Without flags (hard to read)
if age >= 16 and has_license and passed_test:
    print("Can drive alone")

# Same logic, but flags make it clearer what's being checked
is_old_enough = age >= 16
is_licensed = has_license
is_tested = passed_test

if is_old_enough and is_licensed and is_tested:
    print("Can drive alone")  # Same result, clearer intent

# Flags as status indicators
is_logged_in = False
is_admin = True
has_permission = False

if is_logged_in and is_admin:
    print("Welcome, admin!")
else:
    print("Access denied")

# Modifying flags based on conditions
score = 85
is_passing = False

if score >= 60:
    is_passing = True

print(f"Passing: {is_passing}")  # Passing: True

# Multiple flags for different checks
password = "secret123"
username = "alice"

entered_password = input("Password: ")
entered_username = input("Username: ")

is_password_correct = entered_password == password
is_username_correct = entered_username == username

if is_username_correct and is_password_correct:
    print("Login successful")
else:
    print("Invalid credentials")

# Using flags in loops (preview)
is_valid = False
while not is_valid:
    age = int(input("Age (0-150): "))
    is_valid = 0 <= age <= 150

print(f"Your age: {age}")

# Flags for game state
has_sword = True
has_shield = True
has_potion = False

can_fight = has_sword and has_shield
can_heal = has_potion

if can_fight:
    print("You are ready for battle!")
if can_heal:
    print("You can restore health")
```

---

## Guided Practice (15 minutes)

**Activity:** Convert to Flags

Rewrite each as a flag-based version:

1. **Original:**
   ```python
   name = "Alice"
   if name == "Alice" or name == "Bob" or name == "Charlie":
       print("Known user")
   ```

   **Rewritten:**
   ```python
   name = "Alice"
   is_known_user = name in ["Alice", "Bob", "Charlie"]
   if is_known_user:
       print("Known user")
   ```

2. **Original:**
   ```python
   books_owned = 5
   books_limit = 3
   if books_owned >= books_limit:
       print("At limit")
   ```

   **Rewritten:**
   ```python
   books_owned = 5
   books_limit = 3
   is_at_limit = books_owned >= books_limit
   if is_at_limit:
       print("At limit")
   ```

3. **Create your own:** Think of a real-world scenario where you'd use flags (logged in status, admin privilege, item availability, etc.). Write 3-4 flags for that scenario.

---

## Practice Problems

### Problem 1 — Beginner
Use Boolean flags to check if a number is:
1. Positive
2. Even
3. Greater than 100

```python
num = int(input("Number: "))

is_positive =
is_even =
is_big =

if is_positive:
    print("Positive ✓")
if is_even:
    print("Even ✓")
if is_big:
    print("Greater than 100 ✓")
```

---

### Problem 2 — Intermediate
Create a permission system using flags. A user can:
- **Edit** if they are staff OR the original author
- **Delete** if they are admin
- **View** if the document is public OR they have permission

```python
is_staff = False
is_author = True
is_admin = False
is_public = True
has_permission = False

can_edit =
can_delete =
can_view =

if can_edit:
    print("Can edit ✓")
if can_delete:
    print("Can delete ✓")
if can_view:
    print("Can view ✓")
```

---

### Problem 3 — Challenge
Create a movie rating system using flags. A movie can be watched if:
- Parental approval is given (parent_approved = True) AND
- They are old enough (age >= movie_rating)

Also track:
- **should_warn:** Movie has extreme content and user is under 18
- **is_restricted:** Movie requires paid subscription

```python
age = int(input("Your age: "))
parent_approved = True
movie_rating = 13
has_subscription = False
extreme_content = True

can_watch =
should_warn =
is_restricted =

print(f"Can watch: {can_watch}")
print(f"Should warn: {should_warn}")
print(f"Is restricted: {is_restricted}")
```

---

## Hints

- **Problem 1:** `is_positive = num > 0`, `is_even = num % 2 == 0`, `is_big = num > 100`
- **Problem 2:** `can_edit = is_staff or is_author`, `can_delete = is_admin`, `can_view = is_public or has_permission`
- **Problem 3:** `can_watch = parent_approved and age >= movie_rating`, `should_warn = extreme_content and age < 18`, `is_restricted = not has_subscription`

---

## Sample Answers

### Problem 1 Example
```python
num = int(input("Number: "))

is_positive = num > 0
is_even = num % 2 == 0
is_big = num > 100

if is_positive:
    print("Positive ✓")
if is_even:
    print("Even ✓")
if is_big:
    print("Greater than 100 ✓")
```

### Problem 2 Example
```python
is_staff = False
is_author = True
is_admin = False
is_public = True
has_permission = False

can_edit = is_staff or is_author
can_delete = is_admin
can_view = is_public or has_permission

if can_edit:
    print("Can edit ✓")
if can_delete:
    print("Can delete ✓")
if can_view:
    print("Can view ✓")
```

### Problem 3 Example
```python
age = int(input("Your age: "))
parent_approved = True
movie_rating = 13
has_subscription = False
extreme_content = True

can_watch = parent_approved and age >= movie_rating
should_warn = extreme_content and age < 18
is_restricted = not has_subscription

print(f"Can watch: {can_watch}")
print(f"Should warn: {should_warn}")
print(f"Is restricted: {is_restricted}")
```

---

## Key Takeaway

Boolean flags make code readable and reusable. Instead of writing complex conditions repeatedly, create a flag and use it. This is a professional programming pattern used everywhere!
