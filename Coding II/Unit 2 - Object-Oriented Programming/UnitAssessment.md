# Unit Assessment Prep

**Review Questions:**

1. What is the difference between a class and an object?
2. What does __init__ do and why do methods need `self`?
3. Explain the difference between instance and class variables.
4. How do you implement encapsulation?
5. What is inheritance and why use it?
6. Explain method overriding with an example.
7. What is polymorphism?
8. List 3 dunder methods and their purposes.
9. When would you use @property instead of a regular method?
10. How do you call a parent method from a child class?

**Answers:**

1. A class is a blueprint; an object is an instance created from that blueprint.
2. __init__ initializes objects. self refers to the specific object being created/used.
3. Instance variables are unique to each object; class variables are shared by all instances.
4. Use private attributes (_name) and @property for controlled access.
5. Inheritance allows child classes to reuse code from parent classes, reducing repetition.
6. Method overriding replaces a parent method with a child version. Example: Animal.speak() → Dog.speak().
7. Polymorphism allows different classes to have the same method name with different behaviors.
8. __str__ (user-friendly display), __len__ (support len()), __eq__ (support ==).
9. When you need validation or transformation when getting/setting a value.
10. Use super().method_name().
