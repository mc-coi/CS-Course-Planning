# Day 16: Polymorphism in Practice
**Learning Target:** I can design flexible systems using polymorphism and understand real-world application patterns.

### Key Concepts

**Liskov Substitution Principle (LSP):** A child class should be usable anywhere the parent class is used.

**Flexible Interfaces:** Designing classes so they can work with many different types.

**Runtime Behavior:** Objects determine behavior at runtime based on their actual type, not declared type.

**Extensibility:** Adding new types without changing existing code (Open/Closed Principle).

### Code Examples

```python
# Database connection polymorphism
class Database:
    def connect(self):
        pass

    def query(self, sql):
        pass

    def disconnect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        print("Connecting to MySQL...")

    def query(self, sql):
        print(f"Executing MySQL query: {sql}")

    def disconnect(self):
        print("Disconnecting from MySQL...")

class PostgresDatabase(Database):
    def connect(self):
        print("Connecting to PostgreSQL...")

    def query(self, sql):
        print(f"Executing PostgreSQL query: {sql}")

    def disconnect(self):
        print("Disconnecting from PostgreSQL...")

class SQLiteDatabase(Database):
    def connect(self):
        print("Connecting to SQLite...")

    def query(self, sql):
        print(f"Executing SQLite query: {sql}")

    def disconnect(self):
        print("Disconnecting from SQLite...")

# Application works with any database
class Application:
    def __init__(self, database):
        self.database = database

    def run(self):
        self.database.connect()
        self.database.query("SELECT * FROM users")
        self.database.disconnect()

# Use different databases without changing Application
app1 = Application(MySQLDatabase())
app1.run()
print()

app2 = Application(PostgresDatabase())
app2.run()
print()

app3 = Application(SQLiteDatabase())
app3.run()

# Notification system polymorphism
class Notifier:
    def send(self, recipient, message):
        pass

class EmailNotifier(Notifier):
    def send(self, recipient, message):
        print(f"Sending email to {recipient}: {message}")

class SMSNotifier(Notifier):
    def send(self, recipient, message):
        print(f"Sending SMS to {recipient}: {message}")

class PushNotifier(Notifier):
    def send(self, recipient, message):
        print(f"Sending push notification to {recipient}: {message}")

class SlackNotifier(Notifier):
    def send(self, recipient, message):
        print(f"Sending Slack message to {recipient}: {message}")

# System that sends notifications via any channel
class NotificationService:
    def __init__(self, notifiers):
        self.notifiers = notifiers

    def notify_all(self, recipient, message):
        for notifier in self.notifiers:
            notifier.send(recipient, message)

# Add any new notifier without changing NotificationService
service = NotificationService([
    EmailNotifier(),
    SMSNotifier(),
    PushNotifier()
])

service.notify_all("john@example.com", "Hello!")

# Processing pipeline polymorphism
class Processor:
    def process(self, data):
        return data

class UppercaseProcessor(Processor):
    def process(self, data):
        return data.upper()

class ReverseProcessor(Processor):
    def process(self, data):
        return data[::-1]

class RemoveSpacesProcessor(Processor):
    def process(self, data):
        return data.replace(" ", "")

class Pipeline:
    def __init__(self, processors):
        self.processors = processors

    def execute(self, data):
        for processor in self.processors:
            data = processor.process(data)
            print(f"After {processor.__class__.__name__}: {data}")
        return data

pipeline = Pipeline([
    UppercaseProcessor(),
    RemoveSpacesProcessor(),
    ReverseProcessor()
])

result = pipeline.execute("hello world")
print(f"Final result: {result}")

# Factory pattern with polymorphism
class ReportGenerator:
    def generate(self):
        pass

class PDFReport(ReportGenerator):
    def generate(self):
        return "Generating PDF report..."

class HTMLReport(ReportGenerator):
    def generate(self):
        return "Generating HTML report..."

class CSVReport(ReportGenerator):
    def generate(self):
        return "Generating CSV report..."

class ReportFactory:
    @staticmethod
    def create(report_type):
        if report_type == "pdf":
            return PDFReport()
        elif report_type == "html":
            return HTMLReport()
        elif report_type == "csv":
            return CSVReport()

# Use factory to create reports polymorphically
for report_type in ["pdf", "html", "csv"]:
    report = ReportFactory.create(report_type)
    print(report.generate())

# Animal feeding system
class Animal:
    def eat(self, food):
        pass

class Herbivore(Animal):
    def eat(self, food):
        if food == "grass":
            print("Eating grass...")
        else:
            print("I only eat plants!")

class Carnivore(Animal):
    def eat(self, food):
        if food == "meat":
            print("Eating meat...")
        else:
            print("I only eat meat!")

class Omnivore(Animal):
    def eat(self, food):
        print(f"Eating {food}...")

class Zoo:
    def __init__(self, animals):
        self.animals = animals

    def feed_all(self, foods):
        for i, animal in enumerate(self.animals):
            food = foods[i % len(foods)]
            animal.eat(food)

zoo = Zoo([
    Herbivore(),
    Carnivore(),
    Omnivore(),
    Herbivore()
])

zoo.feed_all(["grass", "meat", "everything"])

# Storage system polymorphism
class Storage:
    def save(self, data):
        pass

    def load(self):
        pass

class FileStorage(Storage):
    def save(self, data):
        print(f"Saving to file: {data}")

    def load(self):
        return "Data from file"

class DatabaseStorage(Storage):
    def save(self, data):
        print(f"Saving to database: {data}")

    def load(self):
        return "Data from database"

class CloudStorage(Storage):
    def save(self, data):
        print(f"Saving to cloud: {data}")

    def load(self):
        return "Data from cloud"

class Application:
    def __init__(self, storage):
        self.storage = storage

    def backup(self, data):
        self.storage.save(data)

    def restore(self):
        return self.storage.load()

# Switch storage backends without changing Application
file_app = Application(FileStorage())
file_app.backup("user data")

db_app = Application(DatabaseStorage())
db_app.backup("user data")

cloud_app = Application(CloudStorage())
cloud_app.backup("user data")

# Shape drawing with different renderers
class Shape:
    def render(self, renderer):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def render(self, renderer):
        renderer.draw_circle(self.radius)

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def render(self, renderer):
        renderer.draw_rectangle(self.width, self.height)

class Renderer:
    def draw_circle(self, radius):
        pass

    def draw_rectangle(self, width, height):
        pass

class ConsoleRenderer(Renderer):
    def draw_circle(self, radius):
        print(f"Drawing circle with radius {radius} to console")

    def draw_rectangle(self, width, height):
        print(f"Drawing rectangle {width}x{height} to console")

class GraphicsRenderer(Renderer):
    def draw_circle(self, radius):
        print(f"Drawing circle with radius {radius} using graphics")

    def draw_rectangle(self, width, height):
        print(f"Drawing rectangle {width}x{height} using graphics")

# Render shapes with different renderers
shapes = [Circle(5), Rectangle(10, 20)]
console_renderer = ConsoleRenderer()
graphics_renderer = GraphicsRenderer()

print("Console rendering:")
for shape in shapes:
    shape.render(console_renderer)

print("\nGraphics rendering:")
for shape in shapes:
    shape.render(graphics_renderer)
```

### Guided Practice

**Activity: Create a Payment Processing System**

Follow these steps:

1. Create `PaymentProcessor` base class with `process(amount)` method
2. Create `CreditCardProcessor`, `PayPalProcessor`, `CryptoCProcessor` children
3. Create an `Order` class that accepts any processor
4. Show polymorphism by processing same order with different methods

**Solution:**
```python
class PaymentProcessor:
    def process(self, amount):
        return False

class CreditCardProcessor(PaymentProcessor):
    def __init__(self, card_number):
        self.card_number = card_number

    def process(self, amount):
        print(f"Processing ${amount} with card {self.card_number[-4:]}")
        return True

class PayPalProcessor(PaymentProcessor):
    def __init__(self, email):
        self.email = email

    def process(self, amount):
        print(f"Processing ${amount} with PayPal ({self.email})")
        return True

class BitcoinProcessor(PaymentProcessor):
    def __init__(self, address):
        self.address = address

    def process(self, amount):
        btc_amount = amount / 50000  # Rough conversion
        print(f"Processing {btc_amount:.4f} BTC to {self.address}")
        return True

class Order:
    def __init__(self, items_cost):
        self.items_cost = items_cost

    def checkout(self, processor):
        if processor.process(self.items_cost):
            print(f"Order complete! Total: ${self.items_cost}\n")
        else:
            print("Payment failed\n")

order = Order(99.99)
order.checkout(CreditCardProcessor("1234567890123456"))
order.checkout(PayPalProcessor("user@example.com"))
order.checkout(BitcoinProcessor("1A1z7agoat"))
```

### Practice Problems

**Problem 1 — Beginner:** Create a `Logger` interface with log() method. Implement ConsoleLogger, FileLogger. Show polymorphism with different loggers.

**Problem 2 — Intermediate:** Create a compression system with different compression algorithms (ZIP, GZIP, RAR) that all implement compress().

**Problem 3 — Challenge:** Create an authentication system where different auth methods (username/password, OAuth, biometric) all work polymorphically.

<details>
<summary>💡 Hints</summary>

**Hint 1:** The key to polymorphism is that client code calls methods without knowing the exact type.

**Hint 2:** Design base classes with clear contracts (methods that must be implemented).

**Hint 3:** New implementations can be added without modifying existing code.

</details>

<details>
<summary>✅ Sample Answers</summary>

```python
# Problem 1
class Logger:
    def log(self, message):
        pass

class ConsoleLogger(Logger):
    def log(self, message):
        print(f"[CONSOLE] {message}")

class FileLogger(Logger):
    def __init__(self, filename):
        self.filename = filename

    def log(self, message):
        print(f"[FILE] Writing to {self.filename}: {message}")

loggers = [ConsoleLogger(), FileLogger("app.log")]
for logger in loggers:
    logger.log("System event")

# Problem 2
class Compressor:
    def compress(self, data):
        pass

class ZIPCompressor(Compressor):
    def compress(self, data):
        print(f"Compressing {data} with ZIP")

class GZIPCompressor(Compressor):
    def compress(self, data):
        print(f"Compressing {data} with GZIP")

class RARCompressor(Compressor):
    def compress(self, data):
        print(f"Compressing {data} with RAR")

file = "largefile.txt"
for compressor in [ZIPCompressor(), GZIPCompressor(), RARCompressor()]:
    compressor.compress(file)

# Problem 3
class AuthMethod:
    def authenticate(self, credentials):
        return False

class UsernamePassword(AuthMethod):
    def authenticate(self, credentials):
        if credentials["username"] == "admin" and credentials["password"] == "pass":
            print("Authenticated via username/password")
            return True
        return False

class OAuth(AuthMethod):
    def authenticate(self, credentials):
        if "token" in credentials:
            print("Authenticated via OAuth")
            return True
        return False

class Biometric(AuthMethod):
    def authenticate(self, credentials):
        if "fingerprint" in credentials:
            print("Authenticated via biometric")
            return True
        return False

auth_methods = [
    UsernamePassword(),
    OAuth(),
    Biometric()
]

credentials = [
    {"username": "admin", "password": "pass"},
    {"token": "abc123"},
    {"fingerprint": "scan123"}
]

for method, cred in zip(auth_methods, credentials):
    method.authenticate(cred)
```

</details>
