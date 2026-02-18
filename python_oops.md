# Python Object-Oriented Programming (OOP)

## 1. What is OOP?

Object-Oriented Programming (OOP) is a programming paradigm based on the
concept of objects. Objects contain: - Data (attributes) - Behavior
(methods)

OOP helps in organizing code using classes and objects.

------------------------------------------------------------------------

## 2. Class and Object

### Class

A class is a blueprint for creating objects.

### Object

An object is an instance of a class.

### Example

``` python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, my name is {self.name}"

# Creating object
p1 = Person("Meghana", 22)
print(p1.greet())
```

------------------------------------------------------------------------

## 3. Constructor (**init**)

A constructor is a special method that runs automatically when an object
is created.

``` python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

car1 = Car("Toyota", "Corolla")
print(car1.brand)
```

------------------------------------------------------------------------

## 4. Attributes

Attributes are variables inside a class.

### Instance Attributes

Belong to each object.

### Class Attributes

Shared by all objects.

``` python
class Student:
    school_name = "ABC School"  # Class attribute

    def __init__(self, name):
        self.name = name  # Instance attribute

s1 = Student("Rahul")
s2 = Student("Anita")

print(s1.school_name)
```

------------------------------------------------------------------------

## 5. Methods

Methods are functions defined inside a class.

``` python
class Calculator:
    def add(self, a, b):
        return a + b

calc = Calculator()
print(calc.add(5, 3))
```

------------------------------------------------------------------------

## 6. Encapsulation

Encapsulation means restricting access to certain details of an object.

-   Public: normal variable
-   Protected: \_variable (convention)
-   Private: \_\_variable

``` python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private variable

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())
```

------------------------------------------------------------------------

## 7. Inheritance

Inheritance allows one class to inherit properties and methods from
another class.

``` python
class Animal:
    def speak(self):
        return "Animal sound"

class Dog(Animal):
    def speak(self):
        return "Bark"

d = Dog()
print(d.speak())
```

------------------------------------------------------------------------

## 8. Method Overriding

Method overriding happens when a child class provides a different
implementation of a method from the parent class.

``` python
class Parent:
    def show(self):
        print("Parent method")

class Child(Parent):
    def show(self):
        print("Child method")

obj = Child()
obj.show()
```

------------------------------------------------------------------------

## 9. Polymorphism

Polymorphism allows methods to have the same name but different
behavior.

``` python
class Cat:
    def sound(self):
        return "Meow"

class Cow:
    def sound(self):
        return "Moo"

def make_sound(animal):
    print(animal.sound())

make_sound(Cat())
make_sound(Cow())
```

------------------------------------------------------------------------

## 10. Abstraction

Abstraction means hiding complex implementation details and showing only
necessary features.

Python uses the abc module.

``` python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

r = Rectangle(4, 5)
print(r.area())
```

------------------------------------------------------------------------

## 11. Special (Magic) Methods

Special methods start and end with double underscores.

Common ones: - **init** - **str** - **len**

``` python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return f"Book: {self.title}"

b = Book("Python Basics")
print(b)
```

------------------------------------------------------------------------

## 12. Composition

Composition means one class contains an object of another class.

``` python
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self):
        self.engine = Engine()

    def start_car(self):
        return self.engine.start()

c = Car()
print(c.start_car())
```

------------------------------------------------------------------------

## 13. Difference Between Inheritance and Composition

Inheritance: - "is-a" relationship - Example: Dog is an Animal

Composition: - "has-a" relationship - Example: Car has an Engine

------------------------------------------------------------------------

## 14. Advantages of OOP

-   Code reusability
-   Better organization
-   Easy maintenance
-   Modularity
-   Scalability


