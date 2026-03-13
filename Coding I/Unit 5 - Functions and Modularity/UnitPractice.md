##  Unit 5 Practice Bank (15 Problems)

### Tier 1 — Beginner

**P1.** Write `say_hello(name)` that prints `"Hello, <name>!"`. Call it three times with different names.

**P2.** Write `square(n)` that *returns* n². Store the result in a variable and print it.

**P3.** Write `is_odd(n)` that returns `True` if n is odd, `False` if even.

**P4.** Write `full_name(first, last)` that returns the full name as a string.

**P5.** Write `bigger(a, b)` that returns the larger of two numbers.

### Tier 2 — Intermediate

**P6.** Write `clamp(value, low, high)` that returns `low` if value < low, `high` if value > high, and value otherwise.

<details>
<summary>💡 Hint for P6</summary>

```python
def clamp(value, low, high):
    if value < low:
        return low
    if value > high:
        return high
    return value
```
</details>

**P7.** Write `count_vowels(text)` that returns the number of vowels in a string.

**P8.** Write `list_stats(numbers)` that returns a tuple of (sum, average, min, max).

**P9.** Write `temperature_converter(temp, scale="C")` where scale can be `"C"` (convert to F) or `"F"` (convert to C). Use a default parameter.

**P10.** Write three functions: `add(a, b)`, `subtract(a, b)`, `multiply(a, b)`, then write `calculate(a, op, b)` that calls the appropriate function based on op (`"+"`, `"-"`, `"*"`).

### Tier 3 — Challenge

**P11.** Write a modular word counter: `get_text()` prompts for input, `count_words(text)` returns word count, `count_unique(text)` returns count of unique words, `print_word_report(text)` calls and displays both.

**P12.** Write `flatten(nested_list)` that takes a list of lists and returns a single flat list. E.g., `flatten([[1,2],[3,4],[5]])` → `[1,2,3,4,5]`.

**P13.** Write `run_length_encode(text)` that returns a list of `(char, count)` tuples. E.g., `"aaabbc"` → `[("a",3),("b",2),("c",1)]`.

**P14.** Write a modular Caesar cipher with: `encode_char(c, shift)`, `decode_char(c, shift)`, `encode_message(message, shift)`, `decode_message(message, shift)`.

**P15.** Complete modular ATM simulation: `check_balance(account)`, `deposit(account, amount)`, `withdraw(account, amount)` (return error message if insufficient funds), `transaction_menu(account)`, `main()`.

<details>
<summary>✅ Answer for P15 (starter)</summary>

```python
def check_balance(account):
    return account["balance"]

def deposit(account, amount):
    if amount <= 0:
        return "Invalid amount"
    account["balance"] += amount
    return f"Deposited ${amount:.2f}. New balance: ${account['balance']:.2f}"

def withdraw(account, amount):
    if amount <= 0:
        return "Invalid amount"
    if amount > account["balance"]:
        return "Insufficient funds"
    account["balance"] -= amount
    return f"Withdrew ${amount:.2f}. New balance: ${account['balance']:.2f}"

def transaction_menu(account):
    while True:
        print("\n1. Check Balance  2. Deposit  3. Withdraw  4. Exit")
        choice = input("Choose: ")
        if choice == "1":
            print(f"Balance: ${check_balance(account):.2f}")
        elif choice == "2":
            amt = float(input("Amount: "))
            print(deposit(account, amt))
        elif choice == "3":
            amt = float(input("Amount: "))
            print(withdraw(account, amt))
        elif choice == "4":
            print("Goodbye!")
            break

def main():
    account = {"name": "Student", "balance": 500.00}
    print(f"Welcome, {account['name']}!")
    transaction_menu(account)

main()
```
</details>

---