# Chapter 4: Introducing Python Objects - Complete Guide

## Table of Contents
1. [Introduction](#introduction)
2. [The Python Conceptual Hierarchy](#the-python-conceptual-hierarchy)
3. [Why Use Built-in Objects?](#why-use-built-in-objects)
4. [Python's Core Object Types](#pythons-core-object-types)
5. [Numbers](#numbers)
6. [Strings](#strings)
7. [Lists](#lists)
8. [Dictionaries](#dictionaries)
9. [Tuples](#tuples)
10. [Files](#files)
11. [Other Object Types](#other-object-types)
12. [User-Defined Objects](#user-defined-objects)
13. [Chapter Summary](#chapter-summary)
14. [Test Your Knowledge](#test-your-knowledge)

---

## Introduction

In Python, we do things with stuff. "Things" are operations (like addition and concatenation), and "stuff" refers to the objects on which we perform those operations. Everything in Python is an object - even simple numbers qualify with values (e.g., 99) and supported operations (+, -, etc.).

**Key Concept**: Objects are essentially pieces of memory with values and associated operations. This chapter provides a survey of Python's built-in object types.

---

## The Python Conceptual Hierarchy

Python programs can be decomposed into four levels:

1. **Programs** are composed of **modules**
2. **Modules** contain **statements**  
3. **Statements** contain **expressions**
4. **Expressions** create and process **objects**

This hierarchy shows that objects are at the foundation of Python programming.

### Traditional Programming Concepts vs Python
- Traditional: sequence ("Do this, then that"), selection ("Do this if that is true"), repetition ("Do this many times")
- Python: The unifying principle is **objects and what we can do with them**

---

## Why Use Built-in Objects?

### Four Key Advantages

1. **Easy to Write**: Built-in objects provide powerful tools like collections (lists) and search tables (dictionaries) for free
2. **Components of Extensions**: Custom objects are often built on top of built-in objects (e.g., a stack implemented as a class managing a built-in list)
3. **More Efficient**: Built-in objects use optimized algorithms, often implemented in C for speed
4. **Standard Part of Language**: Built-ins are always the same across Python installations, unlike proprietary toolkits

**Bottom Line**: Built-in objects make programming easier, more powerful, and more accessible than creating from scratch.

---

## Python's Core Object Types

### Complete Object Types Table

| Object Type | Example Literals/Creation | Description |
|-------------|---------------------------|-------------|
| **Numbers** | `1234`, `3.1415`, `0b111`, `1_234`, `3+4j`, `Decimal`, `Fraction` | Numeric values |
| **Strings** | `'code'`, `"app's"`, `b'a\x01c'`, `'h\u00c4ck'`, `'hÄck'` | Text and byte sequences |
| **Lists** | `[1, [2, 'three'], 4.5]`, `list(range(10))` | Ordered, mutable collections |
| **Dictionaries** | `{'job': 'dev', 'years': 40}`, `dict(hours=10)` | Key-value mappings |
| **Tuples** | `(1, 'app', 4, 'U')`, `tuple('hack')`, `namedtuple` | Immutable sequences |
| **Files** | `open('docs.txt')`, `open(r'C:\data.bin', 'wb')` | File I/O objects |
| **Sets** | `set('abc')`, `{'a', 'b', 'c'}` | Unordered unique collections |
| **Other Core** | `True`, `False`, `None`, `type` | Booleans and special objects |
| **Program Units** | Functions, modules, classes | Code organization objects |
| **Implementation** | Compiled code, stack tracebacks | Internal Python objects |

### Key Properties
- **Dynamically Typed**: Python tracks object types automatically (no declarations needed)
- **Strongly Typed**: You can only perform operations valid for an object's type
- **Object Generation**: Expression syntax determines object types (e.g., `'text'` creates string, `[1,2,3]` creates list)

---

## Numbers

### Basic Number Types
- **Integers**: No fractional part (`123`, `1_234_567`)
- **Floating-point**: Have fractional part (`1.5`, `3.14159`)
- **Complex**: With imaginary parts (`3+4j`)
- **Decimal**: Flexible precision
- **Rational**: Numerator and denominator
- **Sets**: Full-featured mathematical sets

### Basic Operations Examples

```python
# Integer addition
>>> 123 + 222
345

# Floating-point multiplication  
>>> 1.5 * 4
6.0

# Number formatting with separators, hex, binary
>>> 1_234_567, 0x15, bin(21)
(1234567, 21, '0b10101')

# Exponentiation - Python handles large numbers automatically
>>> 2 ** 100
1267650600228229401496703205376

# Counting digits in a large number
>>> len(str(2 ** 12345))  # Nearly 4K digits!
3717
```

### Advanced Numeric Modules

```python
# Math module
>>> import math
>>> math.pi
3.141592653589793
>>> math.sqrt(85)
9.219544457292887

# Random module
>>> import random
>>> random.random()
0.7082048489415967
>>> random.choice([1, 2, 3, 4])
2
```

### Important Note: Big Numbers and Security
Python 3.11+ requires extra steps for pathologically large number conversions to avoid denial-of-service attacks. Use `sys.set_int_max_str_digits()` for numbers over 4,300 digits.

---

## Strings

Strings record textual information and arbitrary byte collections. They are **sequences** - positionally ordered collections with left-to-right order.

### Sequence Operations

#### Basic Indexing and Length
```python
>>> S = 'Code'  # 4-character string
>>> len(S)      # Length
4
>>> S[0]        # First character (index 0)
'C'
>>> S[1]        # Second character
'o'
```

#### Negative Indexing
```python
>>> S[-1]       # Last character
'e'
>>> S[-2]       # Second-to-last
'd'

# Negative indexing equivalence
>>> S[-1]
'e'
>>> S[len(S)-1]  # Same result
'e'
```

#### Slicing Operations
```python
>>> S = 'Code'
>>> S[1:3]      # Characters from index 1 up to (not including) 3
'od'

# Slicing variations
>>> S[1:]       # Everything from index 1 onward
'ode'
>>> S[:3]       # Everything up to index 3
'Cod' 
>>> S[:-1]      # Everything except last character
'Cod'
>>> S[:]        # Copy entire string
'Code'
```

**Slicing Format**: `X[I:J]` means "give me everything from offset I up to but not including offset J"

#### String Operations
```python
>>> S = 'Code'
>>> S + 'xyz'   # Concatenation
'Codexyz'
>>> S * 8       # Repetition  
'CodeCodeCodeCodeCodeCodeCodeCode'
>>> S           # Original unchanged (immutable)
'Code'
```

### Immutability

Strings cannot be changed in place after creation:

```python
>>> S = 'Code'
>>> S[0] = 'z'  # ERROR! Cannot change
TypeError: 'str' object does not support item assignment

>>> S = 'Z' + S[1:]  # But can create new string
>>> S
'Zode'
```

#### Working Around Immutability
```python
# Method 1: Convert to list, modify, rejoin
>>> S = 'Python'
>>> L = list(S)     # Expand to list
>>> L
['P', 'y', 't', 'h', 'o', 'n']
>>> L[0] = 'C'      # Change in list
>>> ''.join(L)      # Join back together
'Cython'

# Method 2: Use bytearray (for 8-bit text only)
>>> B = bytearray(b'app')
>>> B.extend(b'lication')
>>> B
bytearray(b'application')
>>> B.decode()
'application'
```

### Type-Specific Methods

String methods are functions attached to string objects, called with parentheses:

#### Search and Replace
```python
>>> S = 'Code'
>>> S.find('od')        # Find substring offset
1
>>> S.replace('od', 'abl')  # Replace all occurrences
'Cable'
>>> S                   # Original unchanged
'Code'
```

#### Text Processing Methods
```python
# Splitting
>>> line = 'aaa,bbb,ccccc,dd'
>>> line.split(',')
['aaa', 'bbb', 'ccccc', 'dd']

# Case conversion
>>> S = 'code'
>>> S.upper()
'CODE'

# Content testing
>>> S.isalpha()  # All alphabetic?
True

# Whitespace removal
>>> line = 'aaa,bbb,ccccc,dd\n'
>>> line.rstrip()  # Remove trailing whitespace
'aaa,bbb,ccccc,dd'

# Method chaining
>>> line.rstrip().split(',')
['aaa', 'bbb', 'ccccc', 'dd']
```

### String Formatting (Three Methods)

```python
>>> tool = 'Python'
>>> major = 3
>>> minor = 3

# Method 1: % formatting (original)
>>> 'Using %s version %s.%s' % (tool, major, minor)
'Using Python version 3.3'

# Method 2: .format() method (newer)  
>>> 'Using {} version {}.{}'.format(tool, major, minor)
'Using Python version 3.3'

# Method 3: f-strings (newest)
>>> f'Using {tool} version {major}.{minor + 9}'
'Using Python version 3.12'
```

#### Advanced Formatting Examples
```python
# Precision and alignment
>>> '%.2f | %+05d' % (3.14159, -62)
'3.14 | -0062'

>>> '{1:,.2f} | {0}'.format('sapp'[1:], 296999.256)
'296,999.26 | app'

>>> f'{296999.256:,.2f} | {"sapp"[1:]}'
'296,999.26 | app'
```

### Getting Help with String Methods

```python
# List all string attributes/methods
>>> S = 'Code'
>>> dir(S)
['__add__', '__class__', '__contains__', ...
 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 
 'startswith', 'strip', 'swapcase', 'title', 'translate', ...]

# Get help on specific method
>>> help(S.replace)
# Help on built-in function replace:
# replace(old, new, count=-1, /) method of builtins.str
# Return a copy with all occurrences of substring old replaced by new.
```

### Advanced String Coding

#### Escape Sequences
```python
>>> S = 'A\nB\tC'  # \n=newline, \t=tab
>>> len(S)         # Each escape is one character
5
>>> S = 'A\0B\0C'  # \0 = binary zero
>>> S              # Displayed in hex notation
'A\x00B\x00C'
```

#### Quote Variations
```python
# Single vs double quotes (same meaning)
>>> 'single quotes'
>>> "double quotes"

# Triple quotes for multiline strings
>>> msg = """
... aaaaaaaaaaaa
... bbb'''bbb""bbb  
... cccccccc
... """
>>> msg
'\naaaaaaaaaaaa\nbbb\'\'\'bbb""bbb\ncccccccc\n'

# Raw strings (no escape processing)
>>> r'C:\Users\you\code'  # No need to double backslashes
```

### Unicode Strings

Python supports full Unicode for international text:

#### Text vs Bytes
```python
# Normal str strings handle Unicode
>>> 'hÄck'
'hÄck'

# bytes strings handle raw bytes
>>> b'a\x01c'
b'a\x01c'
```

#### Character Encoding/Decoding
```python
# Text to bytes (encoding)
>>> 'Code'.encode('utf-8')
b'Code'
>>> 'Code'.encode('utf-16')  
b'\xff\xfeC\x00o\x00d\x00e\x00'

# Rich text examples
>>> hex(ord('🐍'))  # Snake emoji code point
'0x1f40d'
>>> len('🐍hÄck🏏')   # 6 characters
6
>>> len('🐍hÄck🏏'.encode('utf-8'))  # 13 bytes in UTF-8
13
```

#### Unicode Character Coding Methods
```python
# Four ways to code the same character (Ä)
>>> 'h\xc4\u00c4\U000000c4Äck'
'hÄÄÄÄck'

# Comparison: text vs bytes
>>> '\u00A3', '\u00A3'.encode('latin1'), b'\xA3'.decode('latin1')
('£', b'\xa3', '£')
```

---

## Lists

Lists are Python's most general sequence - **mutable**, ordered collections of arbitrarily typed objects with no fixed size.

### Sequence Operations

```python
>>> L = [123, 'text', 1.23]  # Mixed-type list
>>> len(L)
3

# Same indexing and slicing as strings
>>> L[0]
123
>>> L[:-1]  
[123, 'text']
>>> L + [4, 5, 6]
[123, 'text', 1.23, 4, 5, 6]
>>> L * 2
[123, 'text', 1.23, 123, 'text', 1.23]
>>> L  # Original unchanged
[123, 'text', 1.23]
```

### Type-Specific Operations (Mutability)

#### Growing and Shrinking Lists
```python
# Adding elements
>>> L.append('Py')    # Add to end
>>> L
[123, 'text', 1.23, 'Py']

# Removing elements  
>>> L.pop(2)          # Remove and return item at index 2
1.23
>>> L
[123, 'text', 'Py']

# Alternative removal
>>> del L[2]          # Delete item at index 2
>>> L
[123, 'text']
```

#### More List Methods
```python
>>> M = ['bb', 'aa', 'cc']

# Sorting (in-place modification)
>>> M.sort()
>>> M
['aa', 'bb', 'cc']

# Reversing (in-place modification)
>>> M.reverse() 
>>> M
['cc', 'bb', 'aa']

# Other useful methods:
# M.insert(i, x)    # Insert x at position i  
# M.remove(x)       # Remove first occurrence of x
# M.extend(iterable) # Add all items from iterable to end
```

### Bounds Checking

Python prevents accessing non-existent list items:

```python
>>> L = [123, 'text', 'Py']
>>> L[99]        # ERROR!
IndexError: list index out of range
>>> L[99] = 1    # ERROR!  
IndexError: list assignment index out of range
```

To grow a list, use methods like `append()` rather than indexing beyond bounds.

### Nesting

Lists support arbitrary nesting - lists within lists to any depth:

#### Matrix Example
```python
>>> M = [[1, 2, 3],    # 3x3 matrix as nested lists
...      [4, 5, 6],    # Indentation optional
...      [7, 8, 9]]
>>> M
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Accessing nested elements
>>> M[1]        # Get entire row 2
[4, 5, 6]
>>> M[1][2]     # Get row 2, column 3
6
```

### List Comprehensions

Advanced feature for building lists by applying expressions to sequences:

#### Basic Comprehensions
```python
>>> M = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Extract column 2
>>> col2 = [row[1] for row in M]
>>> col2
[2, 5, 8]

# Transform while extracting
>>> [row[1] + 1 for row in M]
[3, 6, 9]

# Filter with conditions
>>> [row[1] for row in M if row[1] % 2 == 0]
[2, 8]
```

#### Working with Other Iterables
```python
# Diagonal extraction
>>> diag = [M[i][i] for i in [0, 1, 2]]
>>> diag  
[1, 5, 9]

# String processing
>>> doubles = [c * 2 for c in 'hack']
>>> doubles
['hh', 'aa', 'cc', 'kk']

# Using range()
>>> list(range(4))
[0, 1, 2, 3]
>>> list(range(-6, 7, 2))  # start, stop, step
[-6, -4, -2, 0, 2, 4, 6]

# Multiple values per iteration
>>> [[x ** 2, x ** 3] for x in range(4)]
[[0, 0], [1, 1], [4, 8], [9, 27]]
```

#### Generator Expressions
```python
# Parentheses create generators (produce on demand)
>>> M = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> G = (sum(row) for row in M)
>>> next(G)  # Get next result
6
>>> next(G)
15
>>> next(G)
24
```

#### Set and Dictionary Comprehensions
```python
# Set comprehension
>>> {sum(row) for row in M}
{24, 6, 15}

# Dictionary comprehension  
>>> {i: sum(M[i]) for i in range(3)}
{0: 6, 1: 15, 2: 24}
```

---

## Dictionaries

Dictionaries are **mappings** (not sequences) - they store objects by key instead of position. They're mutable and maintain insertion order (Python 3.7+).

### Mapping Operations

#### Creating and Accessing Dictionaries
```python
# Literal creation
>>> D = {'name': 'Pat', 'job': 'dev', 'age': 40}

# Access by key
>>> D['name']
'Pat'

# Modify values
>>> D['job'] = 'mgr'
>>> D
{'name': 'Pat', 'job': 'mgr', 'age': 40}
```

#### Building Dictionaries Dynamically
```python
# Start empty and add keys
>>> D = {}
>>> D['name'] = 'Pat'  # Creates new key
>>> D['job'] = 'dev'
>>> D['age'] = 40
>>> D
{'name': 'Pat', 'job': 'dev', 'age': 40}
```

#### Alternative Construction Methods
```python
# Using dict() with keyword arguments
>>> pat1 = dict(name='Pat', job='dev', age=40)
>>> pat1
{'name': 'Pat', 'job': 'dev', 'age': 40}

# Using dict() with zip()
>>> pat2 = dict(zip(['name', 'job', 'age'], ['Pat', 'dev', 40]))
>>> pat2  
{'name': 'Pat', 'job': 'dev', 'age': 40}
```

### Nesting Revisited

Complex data structures using nested dictionaries and lists:

```python
>>> rec = {'name': {'first': 'Pat', 'last': 'Smith'},
...        'jobs': ['dev', 'mgr'], 
...        'age': 40.5}

# Accessing nested data
>>> rec['name']
{'first': 'Pat', 'last': 'Smith'}
>>> rec['name']['last']
'Smith'
>>> rec['jobs']
['dev', 'mgr']
>>> rec['jobs'][-1]
'mgr'

# Modifying nested structures
>>> rec['jobs'].append('janitor')
>>> rec
{'name': {'first': 'Pat', 'last': 'Smith'}, 
 'jobs': ['dev', 'mgr', 'janitor'], 'age': 40.5}
```

#### Memory Management
```python
# Python automatically manages memory
>>> rec = 0  # Previous dictionary is garbage collected
```

### Missing Keys: if Tests

#### Handling Non-existent Keys
```python
>>> D = {'a': 1, 'b': 2, 'c': 3}
>>> D['d'] = 4        # OK - creates new key
>>> D['e']            # ERROR!
KeyError: 'e'
```

#### Testing for Key Existence
```python
# Using 'in' operator
>>> 'e' in D
False

# if statement with proper indentation
>>> if not 'e' in D:
...     print('missing key!')
... 
missing key!

# Multiple statements in block
>>> if not 'e' in D:
...     print('missing')
...     print('no, really...')
... 
missing
no, really...
```

#### Safe Key Access Methods
```python
# Method 1: get() with default
>>> D.get('a', 'missing')    # Key exists
1
>>> D.get('e', 'missing')    # Key missing, return default
'missing'

# Method 2: Ternary if/else expression  
>>> D['e'] if 'e' in D else 0
0
```

### Item Iteration: for Loops

#### Dictionary Methods for Iteration
```python
>>> D = dict(a=1, b=2, c=3)
>>> list(D.keys())      # Get keys
['a', 'b', 'c']
>>> list(D.values())    # Get values  
[1, 2, 3]
>>> list(D.items())     # Get key-value pairs
[('a', 1), ('b', 2), ('c', 3)]
```

#### Understanding the Iteration Protocol
```python
# Methods return iterables, not lists
>>> D.keys()
dict_keys(['a', 'b', 'c'])

# Manual iteration
>>> I = iter(D.keys())
>>> next(I)
'a'
>>> next(I)
'b'
```

#### for Loop Examples
```python
# Explicit key iteration
>>> for key in D.keys():
...     print(key, '=>', D[key])
... 
a => 1
b => 2  
c => 3

# Implicit key iteration
>>> for key in D:
...     print(key, '=>', D[key])

# Key-value pair iteration with tuple unpacking
>>> for (key, value) in D.items():
...     print(key, '=>', value)
```

---

## Tuples

Tuples are **immutable sequences** - like lists but cannot be changed after creation. Used for fixed collections.

### Basic Tuple Operations

```python
>>> T = (1, 2, 3, 4)    # 4-item tuple
>>> len(T)
4

# Same sequence operations as lists/strings
>>> T + (5, 6)          # Concatenation
(1, 2, 3, 4, 5, 6)
>>> T[0], T[1:]         # Indexing, slicing
(1, (2, 3, 4))
```

### Tuple Methods (Limited)

```python
>>> T.index(4)    # Find index of value
3
>>> T.count(4)    # Count occurrences
1
```

### Immutability

```python
>>> T[0] = 2    # ERROR! Cannot modify
TypeError: 'tuple' object does not support item assignment

# Must create new tuple instead
>>> T = (2,) + T[1:]  # Note: comma needed for 1-item tuple
>>> T
(2, 2, 3, 4)
```

### Mixed Types and Nesting

```python
>>> T = 'hack', 3.0, [11, 22, 33]  # Parentheses optional
>>> T
('hack', 3.0, [11, 22, 33])
>>> T[1]
3.0
>>> T[2][1]    # Can access mutable objects inside
22
>>> T.append(4)    # ERROR! No append method
AttributeError: 'tuple' object has no attribute 'append'
```

### Why Tuples?

**Integrity Constraint**: Tuples provide protection against accidental changes
- **Lists**: Can be modified anywhere in program  
- **Tuples**: Cannot be modified - safer for important data

**Use Cases**:
- Fixed collections (calendar dates, coordinates)
- Dictionary keys (must be immutable)
- Function arguments that shouldn't change
- Data that represents a structure

---

## Files

File objects provide access to files on your computer. No literal syntax - created with `open()` function.

### Basic File Operations

#### Writing Text Files
```python
>>> f = open('data.txt', 'w')    # Open for writing
>>> f.write('Hello\n')           # Returns number of characters written
6
>>> f.write('world!\n')
7  
>>> f.close()                    # Close to flush data
```

#### Reading Text Files
```python
>>> f = open('data.txt')         # Open for reading (default mode)
>>> text = f.read()              # Read entire file
>>> text
'Hello\nworld!\n'
>>> print(text)                  # print interprets \n
Hello
world!

>>> text.split()                 # Process file content
['Hello', 'world!']
```

#### File Iteration (Best Practice)
```python
>>> for line in open('data.txt'):    # Automatic line-by-line reading
...     print(line.rstrip())         # Remove newline for clean display
... 
Hello
world!
```

### Unicode and Byte Files

#### Text vs Binary Mode
- **Text files**: Use Unicode encoding/decoding automatically
- **Binary files**: Handle raw bytes without encoding

#### Binary File Example
```python
>>> bf = open('data.bin', 'wb')         # 'b' = binary mode
>>> bf.write(b'h\xFFa\xEEc\xDDk\n')    # Write bytes
8
>>> bf.close()
>>> open('data.bin', 'rb').read()      # Read binary
b'h\xffa\xeec\xddk\n'
```

#### Explicit Encoding for Text Files
```python
# Write with explicit encoding
>>> tf = open('unidata.txt', 'w', encoding='utf-8')
>>> tf.write('🐍h\u00c4ck🏏')
6
>>> tf.close()

# Read with same encoding
>>> open('unidata.txt', 'r', encoding='utf-8').read()
'🐍hÄck🏏'

# View raw bytes
>>> open('unidata.txt', 'rb').read()
b'\xf0\x9f\x90\x8dh\xc3\x84ck\xf0\x9f\x91\x8f'
```

#### Manual Encoding/Decoding
```python
>>> 'hÄck'.encode('utf-8')      # String to bytes
b'h\xc3\x84ck'
>>> b'h\xc3\x84ck'.decode('utf-8')    # Bytes to string  
'hÄck'
```

### Other File-Like Tools

Python provides additional file-related tools:
- **Pipes**: Inter-process communication
- **FIFOs**: Named pipes
- **Sockets**: Network communication  
- **Keyed-access files**: Database-like access
- **Persistent object shelves**: Object storage
- **Database interfaces**: Relational and object-oriented

---

## Other Object Types

### Sets

Sets are unordered collections of unique, immutable objects:

```python
# Creating sets
>>> X = set('hack')              # From sequence
>>> Y = {'a', 'p', 'p'}         # Set literal (duplicates removed)
>>> X, Y
({'c', 'k', 'a', 'h'}, {'p', 'a'})

# Set operations
>>> X & Y                        # Intersection
{'a'}
>>> X | Y                        # Union
{'p', 'c', 'k', 'h', 'a'}
>>> X - Y                        # Difference
{'c', 'k', 'h'}
>>> X > Y                        # Superset test
False
```

#### Common Set Use Cases
```python
# Remove duplicates
>>> list(set([3, 1, 2, 1, 3, 1]))
[1, 2, 3]

# Find differences  
>>> set('code') - set('hack')
{'d', 'o', 'e'}

# Order-neutral equality
>>> set('code') == set('deoc')
True
```

### Booleans and None

```python
# Boolean objects
>>> 1 > 2, 1 < 2
(False, True)
>>> bool('hack')    # All nonempty objects are True
True

# None object (placeholder/absence of value)
>>> X = None
>>> print(X)
None
>>> L = [None] * 100    # Initialize list with None values
>>> L[:5]
[None, None, None, None, None]
```

### Types

The `type()` function returns an object's type:

```python
>>> L = [1, 2, 3]
>>> type(L)
<class 'list'>
>>> type(type(L))  # Even types have types!
<class 'type'>
```

#### Type Testing (Generally Discouraged)
```python
# Three ways to test types
>>> type(L) == type([])    # Compare with empty list type
True
>>> type(L) == list        # Compare with type name
True  
>>> isinstance(L, list)    # Recommended method
True
```

**Important**: Type testing is usually wrong in Python! It breaks **polymorphism** - the ability for code to work with multiple types automatically.

### Type Hinting (Optional Feature)

```python
# Optional type hints (for documentation/tools only)
>>> x: int = 1              # Hint that x should be int
>>> x = 'anything'          # But Python doesn't enforce it
```

**Key Points about Type Hinting**:
- Only for documentation and external tools (like mypy)
- Python itself doesn't use or enforce type hints
- Python remains dynamically typed
- Often contrary to Python's flexibility philosophy  
- Best deferred until you understand dynamic typing benefits

---

## User-Defined Objects  

Classes let you create new object types beyond the built-in ones:

```python
>>> class Worker:
...     # Class definition details omitted for now
...     # Will be covered in Part VI
...

# Creating and using class instances
>>> sue = Worker('Sue Jones', 60000)   # Make instances
>>> bob = Worker('Bob Smith', 50000)   
>>> sue.lastName()                     # Call methods
'Jones'
>>> bob.lastName()
'Smith'
>>> sue.giveRaise(.10)                 # Modify state
>>>
