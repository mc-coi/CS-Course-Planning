# Unit Assessment Prep

**Review Questions:**

1. What are the three main file modes in Python?
2. Why use the `with` statement for files?
3. What's the difference between `read()` and `readlines()`?
4. How do you read a CSV file?
5. What's JSON used for?
6. Explain try/except/else/finally.
7. What are custom exceptions?
8. How do you calculate mean and median?
9. When should you use `DictReader` vs `reader`?
10. How do you handle missing data?

**Answers:**

1. `'r'` (read), `'w'` (write/overwrite), `'a'` (append)
2. It automatically closes the file, even if errors occur
3. `read()` returns entire string; `readlines()` returns list of lines
4. `csv.reader()` or `csv.DictReader()` from csv module
5. Lightweight format for storing/exchanging structured data
6. try runs code, except catches errors, else runs if no error, finally always runs
7. Custom classes inheriting from Exception for application-specific errors
8. Mean: sum/count; Median: middle value of sorted data
9. DictReader when you want dict access (column names); reader for list access
10. Use defaults, skip rows, validate before use

---
