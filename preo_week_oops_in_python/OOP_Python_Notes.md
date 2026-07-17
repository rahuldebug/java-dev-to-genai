# Object-Oriented Programming in Python
## Corey Schafer Style Notes

---

## **1. Classes and Objects**

### **What is a Class?**
A class is a blueprint for creating objects. It defines attributes (data) and methods (functions).

```python
class Dog:
    # Class variable (shared by all instances)
    species = "Canis familiaris"
    
    def __init__(self, name, age):
        # Instance variables (unique to each object)
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} says Woof!"

# Create instances (objects)
dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

print(dog1.name)  # Buddy
print(dog1.bark())  # Buddy says Woof!
```

### **__init__ Method (Constructor)**
- Called automatically when you create an instance
- `self` refers to the specific instance
- Initialize instance variables here

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Rahul", 28)
```

### **self Parameter**
- `self` is a reference to the current instance
- Always the first parameter in instance methods
- Allows you to access and modify instance variables

```python
class Car:
    def __init__(self, brand):
        self.brand = brand
    
    def display(self):
        print(f"Brand: {self.brand}")  # self.brand accesses the instance variable

car = Car("Tesla")
car.display()  # Brand: Tesla
```

---

## **2. Instance vs Class Variables**

### **Instance Variables**
- Unique to each object
- Defined in `__init__` or as `self.variable`
- Each instance has its own copy

```python
class Student:
    def __init__(self, name, grade):
        self.name = name  # Instance variable
        self.grade = grade

s1 = Student("Alice", "A")
s2 = Student("Bob", "B")
# s1.name and s2.name are separate
```

### **Class Variables**
- Shared by all instances
- Defined in the class body, outside methods
- Same value for all objects

```python
class Employee:
    company_name = "TechCorp"  # Class variable
    
    def __init__(self, name):
        self.name = name  # Instance variable

emp1 = Employee("Rahul")
emp2 = Employee("Priya")

print(emp1.company_name)  # TechCorp
print(emp2.company_name)  # TechCorp (same value)
print(Employee.company_name)  # TechCorp (access via class)
```

---

## **3. Methods**

### **Instance Methods**
- Functions defined inside a class
- Take `self` as first parameter
- Can access and modify instance variables

```python
class Calculator:
    def __init__(self, initial=0):
        self.value = initial
    
    def add(self, x):
        self.value += x
        return self.value
    
    def subtract(self, x):
        self.value -= x
        return self.value

calc = Calculator(10)
print(calc.add(5))  # 15
print(calc.subtract(3))  # 12
```

### **Class Methods (@classmethod)**
- Take `cls` as first parameter instead of `self`
- Can access and modify class variables
- Called on the class itself

```python
class Temperature:
    scale = "Celsius"
    
    @classmethod
    def get_scale(cls):
        return cls.scale
    
    @classmethod
    def set_scale(cls, new_scale):
        cls.scale = new_scale

print(Temperature.get_scale())  # Celsius
Temperature.set_scale("Fahrenheit")
print(Temperature.get_scale())  # Fahrenheit
```

### **Static Methods (@staticmethod)**
- No `self` or `cls` parameter
- Can't access instance or class variables
- Utility functions that belong to the class logically

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def multiply(a, b):
        return a * b

print(Math.add(5, 3))  # 8
print(Math.multiply(4, 2))  # 8
```

---

## **4. Inheritance**

### **Basic Inheritance**
A child class inherits attributes and methods from a parent class.

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound"

class Dog(Animal):  # Dog inherits from Animal
    def speak(self):
        return f"{self.name} says Woof!"

dog = Dog("Buddy")
print(dog.speak())  # Buddy says Woof!
```

### **super() Function**
- Calls methods from the parent class
- Useful when overriding methods

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand
    
    def display(self):
        print(f"Brand: {self.brand}")

class Car(Vehicle):
    def __init__(self, brand, model):
        super().__init__(brand)  # Call parent's __init__
        self.model = model
    
    def display(self):
        super().display()  # Call parent's display
        print(f"Model: {self.model}")

car = Car("Tesla", "Model 3")
car.display()
# Output:
# Brand: Tesla
# Model: Model 3
```

### **Method Overriding**
Child class provides its own implementation of a parent method.

```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width

circle = Circle(5)
print(circle.area())  # 78.5

rect = Rectangle(4, 6)
print(rect.area())  # 24
```

---

## **5. Encapsulation (Privacy)**

### **Private Attributes**
Use `_` (single underscore) for "protected" or `__` (double underscore) for "private".

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
    
    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
# account.__balance  # Would raise AttributeError
```

### **Properties (@property)**
Use `@property` to access attributes like they're variables, but run code behind the scenes.

```python
class Person:
    def __init__(self, name, age):
        self._name = name  # Protected
        self._age = age
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if value < 0:
            print("Age can't be negative!")
        else:
            self._age = value

person = Person("Rahul", 28)
print(person.age)  # 28 (getter called)
person.age = 29  # setter called
person.age = -5  # Age can't be negative!
```

---

## **6. Polymorphism**

### **Method Overriding (Duck Typing)**
Different classes with the same method name, but different implementations.

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Bird:
    def speak(self):
        return "Tweet!"

animals = [Dog(), Cat(), Bird()]

for animal in animals:
    print(animal.speak())
# Output:
# Woof!
# Meow!
# Tweet!
```

### **isinstance() and type()**
Check if an object is an instance of a class.

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()
print(isinstance(dog, Dog))  # True
print(isinstance(dog, Animal))  # True (inheritance)
print(type(dog))  # <class '__main__.Dog'>
```

---

## **7. Special Methods (Dunder Methods)**

### **__str__ and __repr__**
- `__str__`: Human-readable representation (for `print()`)
- `__repr__`: Official representation (for debugging)

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author
    
    def __str__(self):
        return f"{self.title} by {self.author}"
    
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}')"

book = Book("Python Basics", "Corey Schafer")
print(str(book))  # Python Basics by Corey Schafer
print(repr(book))  # Book('Python Basics', 'Corey Schafer')
```

### **__len__ and __getitem__**
Make custom objects support `len()` and indexing `[]`.

```python
class MyList:
    def __init__(self, items):
        self.items = items
    
    def __len__(self):
        return len(self.items)
    
    def __getitem__(self, index):
        return self.items[index]

my_list = MyList([1, 2, 3, 4, 5])
print(len(my_list))  # 5
print(my_list[2])  # 3
```

### **__eq__, __lt__, __gt__**
Compare objects with `==`, `<`, `>`.

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
    
    def __eq__(self, other):
        return self.gpa == other.gpa
    
    def __lt__(self, other):
        return self.gpa < other.gpa
    
    def __gt__(self, other):
        return self.gpa > other.gpa

s1 = Student("Alice", 3.8)
s2 = Student("Bob", 3.5)

print(s1 > s2)  # True
print(s1 == s2)  # False
```

### **__init__ and __del__**
- `__init__`: Called when object is created
- `__del__`: Called when object is destroyed (rarely used)

```python
class Resource:
    def __init__(self, name):
        self.name = name
        print(f"Resource {name} created")
    
    def __del__(self):
        print(f"Resource {self.name} destroyed")

res = Resource("File")
# Output: Resource File created
# (When res goes out of scope or is deleted)
# Output: Resource File destroyed
```

---

## **8. Composition vs Inheritance**

### **Inheritance ("is-a")**
Use when there's a clear hierarchical relationship.

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

class Car(Vehicle):  # Car IS-A Vehicle
    pass
```

### **Composition ("has-a")**
Use when an object contains another object as a component.

```python
class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower

class Car:
    def __init__(self, brand, engine):
        self.brand = brand
        self.engine = engine  # Car HAS-A Engine

engine = Engine(200)
car = Car("Tesla", engine)
print(car.engine.horsepower)  # 200
```

---

## **9. Class Design Best Practices**

### **Single Responsibility Principle**
Each class should have one job.

```python
# Bad: User class doing too much
class User:
    def __init__(self, name):
        self.name = name
    
    def save_to_database(self):
        pass
    
    def send_email(self):
        pass

# Good: Separate concerns
class User:
    def __init__(self, name):
        self.name = name

class UserRepository:
    def save(self, user):
        pass

class EmailService:
    def send(self, user):
        pass
```

### **DRY Principle (Don't Repeat Yourself)**
Avoid duplicating code; use inheritance or methods.

```python
# Bad: Duplicated code
class Dog:
    def __init__(self, name):
        self.name = name
        print(f"{name} created")

class Cat:
    def __init__(self, name):
        self.name = name
        print(f"{name} created")

# Good: Shared in parent class
class Animal:
    def __init__(self, name):
        self.name = name
        print(f"{name} created")

class Dog(Animal):
    pass

class Cat(Animal):
    pass
```

---

## **10. Practical Example: Bank Account System**

```python
class Account:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self._balance = balance  # Protected
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            print(f"Deposited ${amount}")
        else:
            print("Deposit amount must be positive")
    
    def withdraw(self, amount):
        if amount > 0 and amount <= self._balance:
            self._balance -= amount
            print(f"Withdrew ${amount}")
        else:
            print("Invalid withdrawal amount")
    
    @property
    def balance(self):
        return self._balance
    
    def __str__(self):
        return f"Account({self.owner}, ${self._balance})"

class SavingsAccount(Account):
    def __init__(self, owner, balance=0, interest_rate=0.02):
        super().__init__(owner, balance)
        self.interest_rate = interest_rate
    
    def apply_interest(self):
        interest = self._balance * self.interest_rate
        self.deposit(interest)

# Usage
savings = SavingsAccount("Rahul", 1000, 0.05)
savings.deposit(500)
savings.apply_interest()
print(savings)  # Account(Rahul, $1575)
```

---

## **Key Takeaways**

1. **Classes** are blueprints; **objects** are instances
2. **Inheritance** creates hierarchies; **composition** embeds objects
3. **Encapsulation** protects data with privacy levels
4. **Polymorphism** allows different behaviors for different types
5. **Special methods** make custom objects act like built-in types
6. **Design principles** make code cleaner and maintainable

---

## **Common Mistakes**

❌ **Forgetting `self` in methods**
```python
class Dog:
    def bark():  # Wrong! Missing self
        print("Woof")
```

❌ **Modifying class variables thinking they're instance variables**
```python
class Counter:
    count = 0
    
    def __init__(self):
        Counter.count += 1  # Correct
        # self.count += 1  # Wrong! Creates instance variable
```

❌ **Deep nesting of inheritance (too complex)**
```python
# Bad: Too many levels
class A: pass
class B(A): pass
class C(B): pass
class D(C): pass
class E(D): pass  # Hard to understand
```

✅ **Keep it simple. Use composition when inheritance gets too deep.**

---

**End of OOP Notes**
