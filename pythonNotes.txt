PYTHON

 Python source files are treated as encoded in UTF-8. In that encoding, characters of most languages in the world can be used simultaneously in string literals, identifiers and comments — although the standard library only uses ASCII characters for identifiers, a convention that any portable code should follow.

INTERPRESTED LANGUAGE:==============
Compiled languages (e.g., C++, Rust) use a compiler to translate entire source code into machine-executable binaries before running, offering fast performance and platform-specific execution. Interpreted languages (e.g., Python, JavaScript) use an interpreter to read and execute code line-by-line, providing higher flexibility, platform independence, and easier debugging, but generally slower runtime speed.


INSTALLATION ====================
sudo apt install python
sudo apt update
python3 verison 

PACKAGE MANAGER >>>>>>>>>>>PIP=================
"Pip" usually refers to the standard package manager for Python, used to install and manage software packages from the Python Package Index (PyPI)
sudo apt install python3-pip -y
pip3 --version
Example : pip install <package>      => pip install requests " : Download requests library and make it available for my Python code
pip uninstall <package>    =>  pip uninstall requests   : Removes a package
pip list    =>  Shows all installed packages
pip freeze   =>  requests==2.31.0            urllib3==2.0.7                   Shows installed packages in a reproducible format,output is machine-readable, not human-friendly.
requirements.txt    =>      A file that lists project dependencies

VIRTUAL ENV=================
virtualenv = an isolated Python world for each project
Suppose:
Project A needs Django 2.2
Project B needs Django 4.0
System Python
│
├── ProjectA
│   └── venv (Django 2.2)
│
├── ProjectB
│   └── venv (Django 4.0)

========Commands you MUST remember==========
virtualenv venv
source venv/bin/activate
deactivate

What is pylint?
pylint = strict Python teacher
It checks:
coding style
bad variable names
unused variables
logic mistakes
unreadable code


What Linux is saying:
“Don’t touch system Python with pip. You might break the OS.”
Ubuntu uses Python internally for: package manager, system tools ,updates
So Ubuntu blocks:
pip3 install virtualenv
pip3 install requests       at system level.

INSTALL VIRTUALENV===========
apt intall python.12-venv to install virtual environment
python3 -m venv myenv           => reate a virtual environment
source myenv/bin/activate           => activate it , (myenv) will be in terminal if activated
pip install requests             =>  requests library is a popular third-party library for handling HTTP communication
pip install pylint                  => static code analysis tool used to check Python code for errors, enforce coding standards 

which pip       => gives version of pip

first install python and pip 
then install venv and create a venv
then activate it
install packages like requests and pylint
pip freeze > requirements.txt ==>> generates req file where all the required packages are listed



MEMORY MANAGEMENT ================

How Memory Works in Python
Python uses:
🔹 Private Heap Memory
🔹 Managed by Python Memory Manager
🔹 Automatic allocation & deallocation
You don’t manually free memory like in C.
STACK VS HEAP=============
🗂 Stack
Stores: function calls, local variables
Works in LIFO order
Fast memory
🏢 Heap
Stores: objects (lists, dicts, class objects, etc.)
Dynamically allocated
Managed automatically
Example:
x = 10
x → stored in stack (reference)
10 → stored in heap
GARBAGE COLLECTION============
=> an automatic memory management system that reclaims memory from objects that are no longer in use, allowing developers to focus on coding without manual memory allocation and deallocation. GC uses either reference counting or circular references.
=> Python also has Garbage Collector for handling:
=> CIRCULAR REFERENCES
Example:
class A:
    pass
a = A()
a.self = a
Here reference count never becomes 0
Garbage Collector handles this.
Module:
import gc
gc.collect()
REFERENCE COUNTING===========
Python uses Reference Counting as primary garbage collection method.
Each object keeps track of:
How many variables point to it
Example:
a = [1, 2, 3]
b = a
Now reference count = 2
If:
del a
Reference count = 1
When count becomes 0 → object is deleted.



DATATYPES ============
IMMUTABLE:                                      MUTABLE:                            
int                                                             list
float                                                          Dictionary
str                                                              set
tuple

print(type(s))  : Returns data type.

1. Numeric: int, float, complex
2. Sequence Type: string, list, tuple
3. Mapping Type: dict
4. Boolean: bool
5. Set Type: set, frozenset
6. Binary Types: bytes, bytearray, memoryview

int : numbers
n1 = 100000000000000000
print(f'{n1:,}')
output : 100,000,000,000,000,000

float : decimal numbers
complex : complex(2, 3)  = irrational
string : sequence of char
bool : true or false

NONE :
None is a special constant that represents the absence of a value or a null value. It is the sole instance of the built-in NoneType class. 

TYPE CASTING AND CONVERSION :
int() : Converts to integer.
float() : Converts to float.
complex() : Converts to complex number.
str() : Converts any value to string.
list()
tuple()
set()
dict()
ord() : Returns ASCII (Unicode) value of a character.  ord('A')   # 65
chr() : Returns character from ASCII value. chr(65)   # 'A'
bool() : Converts to True or False.               bool(0) # False       bool("") # False            bool("Hello") # True
bin() : Binary    bin(10)   # '0b1010' ====>> 0b represents that it is binary value
oct() : Octal   oct(10)   # '0o12'
hex() : Hexadecimal      hex(10)   # '0xa'
abs() : Returns absolute/positive value.     abs(-5)   # 5
round() : Rounds number.    round(3.6)   # 4
id() : Returns memory address.    id(x)



OPERATORS===============

=>  is vs == (Memory Concept)
== → compares values
is → compares memory location

ARITHETIC OPERATORS

Used for mathematical calculations.

+	    Addition	                    5 + 2 → 7
-	    Subtraction	            5 - 2 → 3
*	    Multiplication	        5 * 2 → 10
/	    Division	                    5 / 2 → 2.5
//	    Floor Division	        5 // 2 → 2
%	    Modulus                 	5 % 2 → 1
**	Power	                        5 ** 2 → 25
Example:
a = 10
b = 3
print(a + b)
print(a // b)
print(a ** b)

COMPARISON / RELATIONAL OPERATORS

Used to compare two values.
Returns True or False.

==	    Equal
!=	    Not equal
>	        Greater than
<	        Less than
>=	    Greater than or equal
<=	    Less than or equal
Example:
x = 5
y = 10
print(x == y)   # False
print(x < y)    # True


LOGICAL OPERATORS

Used to combine conditions.

and	    True if both are True
or	        True if at least one is True
not	    Reverses result
Example:
a = 5
print(a > 0 and a < 10)  # True
print(not(a > 0))        # False


ASSIGNMENT OPERATORS 

Used to assign values.

=	x = 5	Assign
+=	x += 3	x = x + 3
-=	x -= 3	x = x - 3
*=	x *= 2	x = x * 2
/=	x /= 2	x = x / 2
//=	x //= 2	Floor divide assign
%=	x %= 2	Modulus assign
**=	x **= 2	Power assign
Example:
x = 10
x += 5
print(x)   # 15


MEMBERSHIP OPERATORS

Used to check presence in sequence.

in	            Present
not in	    Not present
Example:
nums = [1, 2, 3]
print(2 in nums)      # True
print(5 not in nums)  # True


IDENTITY OPERATOR

Used to compare memory location.

is	               Same object i.e., address is same
is not	       Different object 

Example:
a = [1,2]
b = [1,2]
c = a
print(a == b)  # True (values same)   
print(a is b)  # False (different memory)
print(a is c)  # True


BTWISE OEPRATOR

Used for binary operations.

&	        AND
`	        `
^	        XOR
~	        NOT
<<	    Left shift
>>	    Right shift

Example:
a = 5   # 101
b = 3   # 011
print(a & b)  # 1
print(a | b)  # 7


========CONTROL FLOW==========
1. CONDITIONAL STATEMENTS
Conditional Statements (Decision Making)
🔹 if Statement
Executes block if condition is True.
age = 18
if age >= 18:
    print("Eligible to vote")

🔹 if-else Statement
num = 5
if num % 2 == 0:
    print("Even")
else:
    print("Odd")

🔹 if-elif-else Statement
Used for multiple conditions.
marks = 85
if marks >= 90:
    print("Grade A")
elif marks >= 75:
    print("Grade B")
else:
    print("Grade C")

🔹 Nested if
x = 10
if x > 0:
    if x < 20:
        print("Between 0 and 20")


2. LOOPS
Used to repeat code.
🔹 for Loop
Used to iterate over sequences.
for i in range(5):
    print(i)
Iterating through list:
nums = [1,2,3]
for n in nums:
    print(n)

🔹 while Loop
Executes while condition is True.
count = 1
while count <= 5:
    print(count)
    count += 1
⚠ Be careful of infinite loops.

3. LOOP CONTROL STATEMENTS
🔹 break
Stops loop completely.
for i in range(5):
    if i == 3:
        break
    print(i)

🔹 continue
Skips current iteration.
for i in range(5):
    if i == 2:
        continue
    print(i)

🔹 pass
Does nothing (placeholder).
if True:
    pass

4. ELSE WITH LOOPS
Python allows else with loops.
🔹 for-else
for i in range(3):
    print(i)
else:
    print("Loop finished")
⚠ else runs only if loop is NOT stopped by break.

🔹 while-else
x = 0
while x < 3:
    print(x)
    x += 1
else:
    print("Done")

5. MATCH CASE
Similar to switch statement.
day = 1
match day:
    case 1:
        print("Monday")
    case 2:
        print("Tuesday")
    case _:
        print("Invalid")

6.  TERNARY OPERATOR (Short if-else)
x = 10
result = "Even" if x % 2 == 0 else "Odd"

7. BUILT-IN FUNCTIONS WITH LOOPS
=> enumerate(): enumerate() adds a counter (index) to an iterable.
bad example :
names = ["Meghana", "Riya", "Anu"]
for i in range(len(names)):
    print(i, names[i])

with enumerate():
fruits = ["Apple", "Banana", "Mango"]
for i, fruit in enumerate(fruits):
    print(i, fruit)

custom start with enumerate():
for i, fruit in enumerate(fruits, start=1):
    print(i, fruit)

=> zip(): zip() combines multiple iterables element-wise.

names = ["Meghana", "Riya", "Anu"]
marks = [90, 85, 88]
for name, mark in zip(names, marks):
    print(name, mark)

If lists are different lengths:
a = [1,2,3]
b = [4,5]
for x, y in zip(a, b):
    print(x, y)

Unzipping with zip()
pairs = [(1,2), (3,4), (5,6)]
x, y = zip(*pairs)
print(x)  # (1,3,5)
print(y)  # (2,4,6)


==========FUNCTIONS===========
A function is a reusable block of code used to perform a specific task.
EXAMPLE :
def greet(name):
    return "Hello " + name
print(greet("Meghana"))   output : Hello Meghana

TYPES : built-in and user-defined=========

FUNCTION PARAMETERS=========

1. Positional Arguments
Order matters.
def add(a, b):
    return a + b
add(2, 3)

2. Keyword Arguments
Order doesn’t matter.
add(a=5, b=10)

3. Default Arguments
Provide default value.
def greet(name="Guest"):
    print("Hello", name)
greet()

4. Variable-Length Arguments
==>> *args → Multiple positional arguments
def total(*numbers):
    return sum(numbers)
total(1,2,3,4)
==>> **kwargs → Multiple keyword arguments
def details(**info):
    print(info)
details(name="Meghana", age=21)

RETURN=========
Multiple Return Values
def calc(a, b):
    return a+b, a-b
x, y = calc(5, 2)

LAMBDA FUNCTION=========
small anonymous function that can take any no.of arguments but can have only one expression
SYNTAX   :     lambda aruments : expression
 sum  = lambda n1 , n2 : n1+n2
print(sum) ===> gives sum of n1 and n2
===>> Used with:        map()           filter()       reduce()        sorted()
exmaple :
1. nums = [1, 2, 3, 4]
result = list(map(lambda x: x*x, nums))
print(result)

2. nums = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)

3. from functools import reduce
nums = [1, 2, 3, 4]
total = reduce(lambda x, y: x + y, nums)
print(total)

4. names = ["Meghana", "Riya", "Anu"]
result = sorted(names, key=lambda x: len(x))
print(result)

RECURSION=========
Function calling itself.
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n-1)

SCOPE OF VARIABLE AND GLOBAL=========
Scope of Variables
🔹 Local Variable
Defined inside function.
🔹 Global Variable
Defined outside function.
x = 10
def show():
    print(x)
🔹 global Keyword
x = 5
def change():
    global x
    x = 20 
    print(x)
change()    => prints 20    
print(x)  => prints 20

DOCSTRINGS=========
Used to document functions.
def add(a, b):
    """Returns sum of two numbers"""
    return a + b
help(add)

NESTED FUNCTIONS=========
Function inside another function.
def outer():
    def inner():
        print("Inside")
    inner()

DECORATORS:================
A decorator is a function that takes another function and extends or modifies its behavior without changing its actual code.
1. first-class functions 
2. closure : A closure is a function object that remembers values from its enclosing scope even if that outer function has finished executing.
3. local variable
4. inner function
5. inner variable
6. free variable

Closures=========
Function remembering outer variable.
def outer(x):  => first class function
    def inner():   => remembers x=10 which is argument of outer function
        print(x)
    return inner
func = outer(10)
func()

Decorator example :
def decorator_function(original_function):
    def wrapper():
        print("Before execution")
        original_function()
        print("After execution")
    return wrapper

#WITHOUT DECORATORS
def display():
    print("Hello!")
decorated = decorator_function(display)
decorated()

#WITH DECORATORS
@decorator_function
def display():
    print("Hello!")
display()


# nonlocal 
nonlocal is used inside nested functions

def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20   
        print("Inner:", x)
    print("Outer:", x) => 10
    inner()
    print("Outer:", x) => once inner is invoked, x will be 20 every where

outer()


ANNOTATIONS (TYPE HINTS)
def add(a: int, b: int) -> int: => hints that output will be int type and the parameters are also int type
    return a + b 

ASSERT
Used for debugging.
It checks a condition.
If False → raises AssertionError.
🔹 Syntax
assert condition, "Error message"
🔹 Example
x = 5
assert x == 0   => without message
asset x<0 , "Assertion error"  => with message



===========EXCEPTION HANDLING============
An exception is an error that occurs during program execution.
Exception Handling Flow
Order:  try         except          else        finally

EXAMPLE :

1. basic try-except
try:
    #risky code
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

2. Handling Multiple Exceptions
try:
    num = int(input("Enter number: "))
    result = 10 / num
except ValueError:
    print("Invalid input")
except ZeroDivisionError:
    print("Cannot divide by zero")

3. Catching Multiple Exceptions Together
except (ValueError, ZeroDivisionError):
    print("Error occurred")

4. Generic Exception
An exception handler is considered "generic" when you use the base Exception class to catch everything. Printing it in this case just reveals which random error you accidentally caught. 
try:
    x = 10 / 0
except Exception as e:
    print("Error:", e)
e stores the error message.

5. else Block
Runs only if NO exception occurs.
try:
    x = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print("Success")

6. finally Block
Always executes (whether exception occurs or not).
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Error")
finally:
    print("Done")
Used for:
Closing files
Releasing resources
Cleanup operations

7. raise Keyword
Used to manually raise exception.
age = -5
if age < 0:
    raise ValueError("Age cannot be negative")

8.Custom Exceptions
You can create your own exception class.
class InvalidAgeError(Exception):
    pass
age = -1
if age < 0:
    raise InvalidAgeError("Invalid age")



"""
==============MODULES    =>  organizing or managing==============
"""
A module is a file containing Python code (functions, variables, classes) that you can reuse in other Python programs.
# file: my_module.py
def greet(name):
    return f"Hello, {name}!"
PI = 3.14159

Now you can use this module in another file:
# file: main.py
import my_module
print(my_module.greet("Meghana"))
print(my_module.PI)

TYPES : built-in , userdefined and third party 

=> Third-party Modules
Modules installed via pip, not included in standard Python.
Example: numpy, pandas, requests.

import requests  as r  => importing modules
response = r.get("https://api.github.com")
print(response.status_code)

EXAMPLE : random

# import random
# for i in range(3):
#     print(random.randint(10,20)) #=>  randome nuber between 10 and 20
# members = ['hello', 'world', 'how', 'are', 'you']
# leader = random.choice(members)
# print(leader)

#DICE
# import random
# class Dice :
#     def roll(self):
#         first = random.randint(1,6)
#         second = random.randint(1,6)
#         return first , second
# dice = Dice()
# print(dice.roll())


"""
==============PACKAGES    => from package import module / from package.module import funcitons==============
"""
=> A package is a folder containing modules and a special file __init__.py.

from mypackage import module1
module1.some_function() 

COMMON PACKAGES:
numpy → Numerical computations, arrays, matrices
pandas → DataFrames, CSV/Excel handling
scipy → Scientific computing, linear algebra, statistics

matplotlib → Plotting charts
seaborn → Statistical visualization (built on matplotlib)
plotly → Interactive plots

requests → HTTP requests
flask → Web apps (micro-framework)
django → Full-fledged web framework

scikit-learn → ML algorithms
tensorflow → Deep learning
pytorch → Deep learning

opencv-python → Computer vision
Pillow → Image processing
imageio → Reading/writing images & videos

os → File & directory operations
sys → System-level operations
json → JSON parsing
logging → Logging messages


=======FILE HANDLING=========
File handling is the process of reading from and writing to files in Python.
Python provides built-in functions to create, read, update, and delete files.
Files can be:
Text files (.txt) – contain readable characters
Binary files (.jpg, .png, .pdf) – contain non-readable data

2. Opening a File
Python uses the built-in open() function:
file = open("example.txt", "mode")

Mode	                Description
'r'	                        Read (default) – file must exist
'w'	                    Write – creates file or truncates existing
'a'	                        Append – adds data to the end
'x'	                        Create – creates new file, fails if exists
'b'                     	Binary mode – for non-text files (use with rb, wb, ab)
't'                         	Text mode (default) – 'rt', 'wt'
'+'                      	Update (read & write) – 'r+', 'w+', 'a+'
Example:
file = open("example.txt", "w")  # open file for writing

3. Writing to a File
write() – writes string to file
writelines() – writes list of strings
file = open("example.txt", "w")
file.write("Hello, Meghana!\n")
file.write("Python File Handling is easy.\n")
file.close()

With a list of lines:
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
file = open("example.txt", "w")
file.writelines(lines)
file.close()

4. Reading from a File
read() – reads entire file as a string
readline() – reads one line at a time
readlines() – reads all lines into a list
file = open("example.txt", "r")
content = file.read()
print(content)
file.close()

Line by line:
file = open("example.txt", "r")
for line in file:
    print(line.strip())  # removes extra newline
file.close()

5. Using with Statement===============

Automatically handles file closing:

with open("example.txt", "w") as file:
    file.write("This file will auto-close.\n")

with open("example.txt", "r") as file:
    print(file.read())
✅ Always prefer with for safety.

6. Appending to a File
with open("example.txt", "a") as file:
    file.write("This line is added at the end.\n")

7. Other Useful File Operations (os module)

import os
# Rename file
os.rename("example.txt", "new_example.txt")

# Delete file
os.remove("new_example.txt")

# Check if file exists
print(os.path.exists("new_example.txt"))  # False

8. File Cursor / Pointer

seek(offset, whence) – moves pointer

tell() – returns current pointer position

with open("example.txt", "r") as file:
    print(file.read(5))  # read first 5 characters => prints first 5 characters
    print(file.tell())   # pointer at 5 ==> prints 5
    file.seek(0)         # move to start

10. Reading Large Files

For huge files, read line by line to save memory:
with open("large_file.txt", "r") as file:
    for line in file:
        process(line)


EXAMPLE :
with open('file_path', 'r/w', encoding= 'utf8') as csvfile/any_file:
    file_data = DictReader(csvfile)

import openpyxl as xl
from openpyxl.chart import BarChart, Reference

wb = xl.load_workbook('translactions.xlsx')
sheet = wb['Sheet1']
cell1 = sheet['a1']
cell2 = sheet.cell(2,1)

for row in range(2, sheet.max_row+1) :
    cell1 = sheet.cell(row,3)


=========================
Example : GENERATING RANDOM VALUES



"""
==============PATH RELATIVE AND ABSOLUTE==============
"""

# from pathlib import Path
 
# path = Path("emails")
# print(path.mkdir())  # => creates Python Practice directory in the package and return None
# path = Path("emails")
# print(path.exists())  # True
# print(path.rmdir())   # deletes Python Practice and return None
# path = Path()
# for file in path.glob('*'):  # iterate through all the file&dir(*) in the path 
#     print(file)                 # and prints the file name




==========FILE HANDLING============



