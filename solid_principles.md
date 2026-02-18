# SOLID Principles in Object-Oriented Programming

SOLID is a set of five design principles that help in writing clean,
maintainable, and scalable code.

S - Single Responsibility Principle\
O - Open/Closed Principle\
L - Liskov Substitution Principle\
I - Interface Segregation Principle\
D - Dependency Inversion Principle

------------------------------------------------------------------------

## 1. Single Responsibility Principle (SRP)

A class should have only one reason to change. This means a class should
do only one job.

### Wrong Example

``` python
class Report:
    def generate(self):
        return "Report content"

    def save_to_file(self):
        print("Saving report to file")
```

This class has two responsibilities: - Generating report - Saving report

### Correct Example

``` python
class Report:
    def generate(self):
        return "Report content"

class ReportSaver:
    def save_to_file(self, content):
        print("Saving:", content)

report = Report()
content = report.generate()

saver = ReportSaver()
saver.save_to_file(content)
```

Now each class has only one responsibility.

------------------------------------------------------------------------

## 2. Open/Closed Principle (OCP)

A class should be open for extension but closed for modification. You
should be able to add new functionality without changing existing code.

### Wrong Example

``` python
class Discount:
    def calculate(self, customer_type, amount):
        if customer_type == "regular":
            return amount * 0.1
        elif customer_type == "premium":
            return amount * 0.2
```

If a new customer type comes, we must modify this class.

### Correct Example

``` python
class Discount:
    def calculate(self, amount):
        pass

class RegularDiscount(Discount):
    def calculate(self, amount):
        return amount * 0.1

class PremiumDiscount(Discount):
    def calculate(self, amount):
        return amount * 0.2

def get_discount(discount, amount):
    return discount.calculate(amount)

print(get_discount(RegularDiscount(), 1000))
```

Now we can add new discount types without changing existing code.

------------------------------------------------------------------------

## 3. Liskov Substitution Principle (LSP)

Child classes should be able to replace parent classes without breaking
the program.

### Wrong Example

``` python
class Bird:
    def fly(self):
        print("Flying")

class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly")
```

Penguin cannot correctly replace Bird because it breaks behavior.

### Correct Example

``` python
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        print("Flying")

class Penguin(Bird):
    def swim(self):
        print("Swimming")
```

Now each class behaves correctly without breaking expectations.

------------------------------------------------------------------------

## 4. Interface Segregation Principle (ISP)

A class should not be forced to implement methods it does not use.

### Wrong Example

``` python
class Worker:
    def work(self):
        pass

    def eat(self):
        pass

class Robot(Worker):
    def work(self):
        print("Working")

    def eat(self):
        raise Exception("Robots do not eat")
```

Robot is forced to implement eat.

### Correct Example

``` python
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Human(Workable, Eatable):
    def work(self):
        print("Working")

    def eat(self):
        print("Eating")

class Robot(Workable):
    def work(self):
        print("Working")
```

Now classes only implement what they need.

------------------------------------------------------------------------

## 5. Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should
depend on abstractions.

### Wrong Example

``` python
class Keyboard:
    def type(self):
        print("Typing")

class Computer:
    def __init__(self):
        self.keyboard = Keyboard()

    def use(self):
        self.keyboard.type()
```

Computer directly depends on Keyboard.

### Correct Example

``` python
class InputDevice:
    def type(self):
        pass

class Keyboard(InputDevice):
    def type(self):
        print("Typing")

class Computer:
    def __init__(self, device):
        self.device = device

    def use(self):
        self.device.type()

keyboard = Keyboard()
computer = Computer(keyboard)
computer.use()
```

Now Computer depends on abstraction, not a specific device.

------------------------------------------------------------------------

# Conclusion

Single Responsibility Principle: One class, one job.

Open/Closed Principle: Extend behavior without modifying existing code.

Liskov Substitution Principle: Child classes must behave correctly when
used as parent type.

Interface Segregation Principle: Do not force classes to implement
unused methods.

Dependency Inversion Principle: Depend on abstractions, not concrete
classes.
