# Assessment Prep — Q&A

**Q1: What is the difference between a parameter and an argument?**
A parameter is the variable name in the `def` line. An argument is the actual value you pass when calling the function.

**Q2: What does a function return if there is no `return` statement?**
It returns `None`.

**Q3: Why is this code wrong? `def f(default=5, required): ...`**
Default parameters must come *after* required parameters. Should be: `def f(required, default=5):`.

**Q4: What is variable scope?**
Scope is where a variable is accessible. Local variables exist only inside their function. Global variables exist throughout the entire file.

**Q5: What's the output?**
```python
x = 10
def change():
    x = 99
change()
print(x)
```
Output: `10`. The `x = 99` inside `change()` creates a new *local* variable — the global `x` is untouched.

**Q6: How do you return multiple values?**
Separate them with commas: `return a, b, c`. Python automatically packages them as a tuple. Unpack with: `x, y, z = my_func()`.

**Q7: What does "single responsibility" mean?**
Each function should do exactly one thing. A function that validates input, calculates a result, and prints a report has too many responsibilities — split it into three functions.

**Q8: What's wrong here?**
```python
def double(n):
    print(n * 2)
x = double(5)
print(x + 1)
```
`double` prints but doesn't return, so `x` is `None`. `None + 1` causes a `TypeError`. Fix: use `return n * 2`.

**Q9: What is modular design and why does it matter?**
Modular design breaks programs into small, single-purpose functions. Benefits: easier to read, test, debug, reuse, and update code.

**Q10: When should you use the `global` keyword?**
Rarely. Only when a function truly needs to modify a global state. Usually better to pass values as parameters and return new values.

---