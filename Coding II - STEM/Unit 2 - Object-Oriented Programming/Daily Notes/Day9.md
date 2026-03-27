# Day 9: OOP Project Day — Bank Account System
**Learning Target:** I can design and implement a complete object-oriented program.

### Project Overview
Build a banking system with:
- Account class with deposit, withdraw, transfer
- CheckingAccount and SavingsAccount subclasses
- Interest calculation for savings
- Transaction history
- Account statements

### Requirements
- Use inheritance (parent Account class)
- Implement encapsulation (private balance)
- Use properties for controlled access
- Implement __str__ for account display
- Track multiple accounts

### Scaffold & Starter Code
```python
class Account:
    def __init__(self, holder, balance):
        self.holder = holder
        self._balance = balance
        self.transactions = []

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        self._balance += amount
        self.transactions.append(f"Deposit: +${amount}")

    def withdraw(self, amount):
        if amount <= self._balance:
            self._balance -= amount
            self.transactions.append(f"Withdraw: -${amount}")
        else:
            print("Insufficient funds")

    def __str__(self):
        return f"{self.holder}: ${self._balance:.2f}"

class SavingsAccount(Account):
    def __init__(self, holder, balance, interest_rate):
        super().__init__(holder, balance)
        self.interest_rate = interest_rate

    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self.deposit(interest)

# Test
account = SavingsAccount("Zach McCoy", 1000, 0.05)
account.deposit(500)
account.apply_interest()
print(account)
```

### Enhancement Ideas
- Multiple accounts per person
- Monthly statements
- Transfer between accounts
- Overdraft protection
- Loan calculations

---
