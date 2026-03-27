# Day 60: Practice Lab — Login System & Eligibility Checker

**Learning Target:** I can build interactive systems using nested conditionals, complex logic, and input validation.

---

## Learning Summary (Week 12 Review)

This week you learned:
1. **Nested conditionals:** Decisions inside decisions
2. **Complex conditions with and/or:** Replacing nesting with operators
3. **Short-circuit evaluation:** Efficient Boolean evaluation
4. **Truthy/falsy values:** Using any value in Boolean context
5. **Input validation:** Checking input before using it

---

## Practice Lab: Complex Interactive Systems

### Project Overview

Build one of these complete programs. Your program must:
- Accept user input and validate it
- Use nested conditionals and/or complex logic
- Include error handling
- Provide clear feedback
- Handle edge cases

---

## Option A: Simple Login System

```
1. Ask for username and password
2. Check username (must match stored value)
3. If correct, check password
4. If both correct, show options
5. Track failed attempts
```

**Requirements:**
- [ ] Username validation
- [ ] Password validation
- [ ] Nested if structure (username → password)
- [ ] Failed attempt counter
- [ ] Lock after 3 failed attempts
- [ ] Options menu if login successful

**Starter:**
```python
# Stored credentials
ADMIN_USER = "admin"
ADMIN_PASS = "admin123"

failed_attempts = 0
max_attempts = 3

while failed_attempts < max_attempts:
    username = input("Username: ")

    if username == ADMIN_USER:
        password = input("Password: ")
        if password == ADMIN_PASS:
            print("✓ Login successful!")
            # Show options
            print("1. View profile")
            print("2. Change password")
            print("3. Logout")
            break
        else:
            print("✗ Wrong password")
            failed_attempts += 1
    else:
        print("✗ User not found")
        failed_attempts += 1

if failed_attempts >= max_attempts:
    print("Account locked!")
```

---

## Option B: Eligibility Checker

```
Check if person meets requirements for a program/opportunity.
Multiple requirements, all must pass.
Provide specific feedback.
```

**Example: College Admission**
- GPA >= 3.0
- SAT score >= 1000
- Essay submitted
- No disciplinary issues

**Requirements:**
- [ ] Check 4+ requirements
- [ ] Validate input types
- [ ] Approved/Denied decision
- [ ] Detailed feedback (what's missing)
- [ ] Handle invalid input gracefully

**Starter:**
```python
print("=== College Admission Checker ===\n")

# Get inputs
name = input("Student name: ")
gpa = float(input("GPA (0-4.0): "))
sat = int(input("SAT (400-1600): "))
essay = input("Essay submitted? (yes/no): ").lower()
issues = input("Any disciplinary issues? (yes/no): ").lower()

# Validate ranges
gpa_valid = 0 <= gpa <= 4.0
sat_valid = 400 <= sat <= 1600

if not gpa_valid or not sat_valid:
    print("Invalid scores")
else:
    # Check eligibility
    meets_gpa = gpa >= 3.0
    meets_sat = sat >= 1000
    submitted_essay = essay == "yes"
    no_issues = issues == "no"

    if meets_gpa and meets_sat and submitted_essay and no_issues:
        print(f"✓ {name}: APPROVED")
    else:
        print(f"✗ {name}: DENIED")
        print("Missing requirements:")
        if not meets_gpa:
            print(f"  - GPA (need 3.0+, have {gpa})")
        if not meets_sat:
            print(f"  - SAT (need 1000+, have {sat})")
        if not submitted_essay:
            print("  - Essay submission")
        if not no_issues:
            print("  - Disciplinary issues")
```

---

## Option C: Advanced Access Control

```
Determine user permissions based on:
- User role (guest, user, moderator, admin)
- Account status (active, suspended, banned)
- Specific permissions
```

**Requirements:**
- [ ] 3+ user roles with different permissions
- [ ] Nested conditionals for role checking
- [ ] Permission validation
- [ ] Clear output showing what user can do
- [ ] Handle role not found

**Starter:**
```python
print("=== Access Control System ===\n")

username = input("Username: ")
user_role = input("Role (guest/user/moderator/admin): ").lower()
status = input("Status (active/suspended/banned): ").lower()

# Check if account is active
if status == "banned":
    print("✗ This account is banned")
elif status == "suspended":
    print("⚠ This account is suspended")
else:
    # Check permissions by role
    if user_role == "guest":
        can_view = True
        can_comment = False
        can_delete = False
        can_admin = False
    elif user_role == "user":
        can_view = True
        can_comment = True
        can_delete = False
        can_admin = False
    elif user_role == "moderator":
        can_view = True
        can_comment = True
        can_delete = True
        can_admin = False
    elif user_role == "admin":
        can_view = True
        can_comment = True
        can_delete = True
        can_admin = True
    else:
        print("Unknown role")
        can_view = False

    # Display permissions
    if can_view:
        print("✓ Can view content")
    if can_comment:
        print("✓ Can post comments")
    if can_delete:
        print("✓ Can delete posts")
    if can_admin:
        print("✓ Can manage users")
```

---

## Option D: Game Eligibility & Setup

```
Check player eligibility, set difficulty, give equipment.
Multiple tiers of logic.
```

**Requirements:**
- [ ] Check age requirement
- [ ] Check experience level
- [ ] Assign difficulty level
- [ ] Assign starting equipment
- [ ] Calculate starting stats
- [ ] Validate all inputs

**Starter:**
```python
print("=== RPG Character Creation ===\n")

age = int(input("Your age: "))
experience = int(input("Experience level (1-10): "))

# Age requirement
if age < 13:
    print("Sorry, you must be at least 13 to play")
else:
    # Validate experience
    if 1 <= experience <= 10:
        # Assign difficulty
        if experience <= 3:
            difficulty = "Easy"
            starting_health = 150
        elif experience <= 6:
            difficulty = "Normal"
            starting_health = 100
        else:
            difficulty = "Hard"
            starting_health = 75

        # Assign equipment
        if experience <= 2:
            weapon = "Wooden Sword"
            armor = "Cloth"
        elif experience <= 5:
            weapon = "Iron Sword"
            armor = "Leather"
        else:
            weapon = "Steel Sword"
            armor = "Chain Mail"

        print(f"\n✓ Character Created")
        print(f"Difficulty: {difficulty}")
        print(f"Health: {starting_health}")
        print(f"Weapon: {weapon}")
        print(f"Armor: {armor}")
    else:
        print("Experience must be 1-10")
```

---

## Requirements Checklist

Your program must have:
- [ ] Clear user prompts
- [ ] Input validation (type or range)
- [ ] Nested conditionals or complex logic
- [ ] Multiple decision branches
- [ ] Detailed feedback/output
- [ ] At least 5 comments explaining logic
- [ ] No syntax errors
- [ ] Handles invalid input gracefully

---

## Testing Checklist

Before submitting, test:
- [ ] Program runs without crashes
- [ ] Valid inputs produce correct output
- [ ] Invalid inputs are handled
- [ ] All branches have been executed
- [ ] Output is clear and well-formatted
- [ ] Variable names are descriptive
- [ ] Edge cases work (min/max values, etc.)

---

## Grading Rubric

| Criteria | Points | Notes |
|----------|--------|-------|
| Functionality | 40 | Logic correct; all branches work |
| Validation | 20 | Input validated properly |
| Code Quality | 25 | Clear names; good indentation |
| Documentation | 15 | Comments explain logic |

---

## Challenge Extensions

**If you finish early:**
1. Add ability to retry (loop) until valid input
2. Add more detailed output/reporting
3. Create multiple test cases
4. Add file I/O (save results)
5. Build a mini game around the system

---

## Reflection Questions

After completing your program:

1. How many different execution paths does your program have?
2. What input would cause each path?
3. What edge cases could break your program?
4. How would you test each branch?
5. What improvements would you make?

---

## Key Skills Demonstrated

By completing this lab, you can:
- [ ] Write nested conditionals correctly
- [ ] Use complex compound conditions
- [ ] Validate user input effectively
- [ ] Handle multiple decision paths
- [ ] Build interactive, user-friendly systems
- [ ] Provide clear feedback
