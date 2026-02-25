# Python Decorators

## Introduction

A decorator is a function that modifies the behavior of another function
without changing its actual code.

------------------------------------------------------------------------

## Basic Example
```python 
def my_decorator(func):
    def wrapper():
        print("Before function runs")
        func()
        print("After function runs")
    return wrapper

Now use it:

def say_hello():
    print("Hello!")

say_hello = my_decorator(say_hello)
say_hello()
```
------------------------------------------------------------------------
## Output
Before function runs

Hello!

After function runs

------------------------------------------------------------------------

- using @decorator
``` python
def decorator_function(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@decorator_fucntion
def greet():
    print("Hello")

greet()
```

------------------------------------------------------------------------

## Output

Before function call 

Hello 

After function call

------------------------------------------------------------------------

## Why Use Decorators?

-   Logging
-   Authentication
-   Authorization
-   Performance measurement

------------------------------------------------------------------------

## Example: Measuring Execution Time

``` python
import time

def timer(func):
    def wrapper():
        start = time.time()
        func()
        end = time.time()
        print("Execution Time:", end - start)
    return wrapper

@timer
def slow_function():
    time.sleep(2)

slow_function()
```
