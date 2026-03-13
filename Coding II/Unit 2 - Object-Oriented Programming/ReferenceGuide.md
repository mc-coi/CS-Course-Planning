# Vocabulary & Quick Reference

**Key Terms:**
- **Class:** Blueprint for creating objects
- **Object/Instance:** Individual example of a class
- **Attribute:** Variable belonging to an object
- **Method:** Function belonging to an object
- **self:** Reference to the current object
- **__init__:** Constructor method that initializes objects
- **Inheritance:** Child class inherits from parent class
- **Encapsulation:** Hiding internal details
- **Polymorphism:** Same method name, different implementations
- **Dunder method:** Special method like __str__ or __init__

**Key Syntax:**
```python
class ClassName:
    def __init__(self, param):
        self.attribute = param

    def method(self):
        return self.attribute

class Child(Parent):
    def __init__(self, param):
        super().__init__(param)

@property
def attribute(self):
    return self._attribute
```
