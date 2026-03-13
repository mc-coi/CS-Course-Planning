## Assessment Prep — Q&A

**Q1: What are the three types of errors in Python?**
Syntax errors (code breaks Python's rules — won't run), runtime errors (valid code crashes during execution — e.g., `ZeroDivisionError`), and logic errors (code runs but produces wrong answers).

**Q2: What is the purpose of the `finally` block?**
The `finally` block always runs regardless of whether an exception occurred. It's used for cleanup — closing files, releasing resources, printing a completion message.

**Q3: What's wrong with `except:`?**
A bare `except:` catches every possible exception, including keyboard interrupts and system exits. This can hide real bugs and make debugging impossible. Always specify the exception type: `except ValueError:`.

**Q4: What are the differences between file modes `"w"`, `"a"`, and `"r"`?**
`"w"` writes/overwrites the file (erases existing content). `"a"` appends to the end. `"r"` reads the file (error if it doesn't exist).

**Q5: Why do we use `with open() as f:` instead of just `open()`?**
The `with` statement automatically closes the file when the block ends — even if an exception occurs. Without it, you must manually call `f.close()` and remember to do so even after errors.

**Q6: What is a docstring and how is it different from a comment?**
A docstring is a string literal (using `"""..."""`) placed immediately after a `def` statement. It becomes part of the function and is accessible via `help()` and `func.__doc__`. A regular comment (`#`) is discarded by Python and can't be accessed programmatically.

**Q7: What does `.strip()` do when reading file lines?**
It removes leading and trailing whitespace, including the `\n` newline character at the end of each line. Without it, lines would include the invisible newline.

**Q8: What is the `else` clause in a `try/except` block?**
The `else` block runs only if the `try` block completed without raising any exceptions. It separates "success" code from "error" code.

**Q9: How do you raise your own exception?**
Use the `raise` keyword: `raise ValueError("message here")`. This allows you to enforce rules in your functions.

**Q10: What good comments look like vs. bad:**
Bad: `x += 1  # add 1 to x` (states the obvious)
Good: `attempts += 1  # track login attempts for lockout logic` (explains why)

---