# Python Strings

Strings in Python are **immutable** (cannot be changed after creation).  
All string methods return a **new string**.

---

## 1. Case Conversion Methods

### lower()
Converts string to lowercase.
```python
text = "Hello World"
print(text.lower())  # hello world
```

### upper()
Converts string to uppercase.
```python
print(text.upper())  # HELLO WORLD
```

### title()
Capitalizes first letter of each word.
```python
print("python programming".title())
# Python Programming
```

### capitalize()
Capitalizes first letter of entire string.
```
print("hello world".capitalize())
# Hello world
```

### swapcase()
Swaps lowercase to uppercase and vice versa.
```
print("PyThOn".swapcase())
# pYtHoN
```

## **2. Searching Methods**

### find()
Returns index of substring. Returns -1 if not found.
```
text = "python programming"
print(text.find("pro"))  # 7
```
### index()
Same as find() but raises error if not found.
```
print(text.index("python"))  # 0
```
###count()

Counts occurrences of substring.
```
print(text.count("m"))  # 2
```

## 3. Checking Methods (Return Boolean)**

### isalpha()
True if all characters are alphabets.
```
print("Hello".isalpha())  # True
```
### isdigit()
True if all characters are digits.
```
print("1234".isdigit())  # True
```
### isalnum()
True if alphanumeric. 
```
print("Python123".isalnum())  # True
```
### isspace()
True if string contains only spaces.
```
print("   ".isspace())  # True
```
## 4. Splitting & Joining

### split()
Splits string into list.
```
text = "apple,banana,orange"
print(text.split(","))  
# ['apple', 'banana', 'orange']
```
### join()
Joins list into string.
```
words = ['Python', 'is', 'fun']
print(" ".join(words))
# Python is fun
```

## 5. Replacing & Formatting

### replace()
Replaces substring.
```
print("I like Java".replace("Java", "Python"))
# I like Python
```
### strip()
Removes leading & trailing spaces.
```
print("  hello  ".strip())
# hello
```
### lstrip() / rstrip()
```
print("  hello".lstrip())
print("hello  ".rstrip())
```

## 6. String Formatting
### f-strings (Recommended)
```
name = "Meghana"
age = 21
print(f"My name is {name} and I am {age}")
```























