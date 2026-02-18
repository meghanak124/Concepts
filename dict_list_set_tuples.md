# Python Data Structures: Lists, Tuples, Sets, and Dictionaries

## 1. Lists

### Definition

A list is an ordered, mutable collection of elements. Lists allow
duplicate values.

### Creating a List

``` python
numbers = [1, 2, 3, 4]
mixed = [1, "hello", 3.5, True]
```

### Key Characteristics

-   Ordered
-   Mutable (can modify after creation)
-   Allows duplicates
-   Indexed (starts from 0)

### Common List Methods

``` python
lst.append(x)       # Add element at end
lst.insert(i, x)    # Insert at position
lst.remove(x)       # Remove first occurrence
lst.pop()           # Remove last element
lst.sort()          # Sort list
lst.reverse()       # Reverse list
len(lst)            # Length
```

### Example

``` python
nums = [10, 20, 30]
nums.append(40)
nums[0] = 5
```

------------------------------------------------------------------------

## 2. Tuples

### Definition

A tuple is an ordered, immutable collection of elements.

### Creating a Tuple

``` python
t = (1, 2, 3)
single = (5,)  # Single element tuple
```

### Key Characteristics

-   Ordered
-   Immutable (cannot modify)
-   Allows duplicates
-   Indexed

### Tuple Methods

``` python
t.count(x)     # Count occurrences
t.index(x)     # Find index
```

### When to Use Tuples

-   When data should not change
-   Faster than lists
-   Can be used as dictionary keys

------------------------------------------------------------------------

## 3. Sets

### Definition

A set is an unordered collection of unique elements.

### Creating a Set

``` python
s = {1, 2, 3}
empty_set = set()
```

### Key Characteristics

-   Unordered
-   Mutable
-   No duplicates
-   Not indexed

### Common Set Methods

``` python
s.add(x)           # Add element
s.remove(x)        # Remove element
s.discard(x)       # Remove safely
s.union(other)     # Union
s.intersection(o)  # Intersection
s.difference(o)    # Difference
```

### Example

``` python
a = {1, 2, 3}
b = {3, 4, 5}
a.union(b)
```

------------------------------------------------------------------------

## 4. Dictionaries

### Definition

A dictionary is an unordered, mutable collection of key-value pairs.

### Creating a Dictionary

``` python
student = {
    "name": "Meghana",
    "age": 22,
    "grade": "A"
}
```

### Key Characteristics

-   Key-value pairs
-   Keys must be unique
-   Mutable
-   Fast lookup using keys

### Common Dictionary Methods

``` python
d.keys()          # All keys
d.values()        # All values
d.items()         # Key-value pairs
d.get(key)        # Safe access
d.update(other)   # Update dictionary
d.pop(key)        # Remove key
```

### Example

``` python
student["age"] = 23
student["city"] = "Hyderabad"
```

------------------------------------------------------------------------

## Comparison Table

  Feature      List   Tuple   Set   Dictionary
  ------------ ------ ------- ----- ------------
  Ordered      Yes    Yes     No    No
  Mutable      Yes    No      Yes   Yes
  Duplicates   Yes    Yes     No    Keys: No
  Indexed      Yes    Yes     No    By keys

