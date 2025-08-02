# Chapter 9: Tuples, Files, and Everything Else

## Chapter Overview
This chapter completes the exploration of Python's core object types by examining:
- **Tuples**: Immutable collections of objects
- **Files**: Interface to external files on your computer
- **Object properties**: Common characteristics shared by all core types
- **Common pitfalls**: Issues that trap new Python users

---

## Part 1: Tuples

### What are Tuples?
Tuples are **immutable sequences** that construct simple groups of objects. They work like lists but with key differences:

#### Key Characteristics:
1. **Ordered collections** of arbitrary objects (maintain left-to-right order)
2. **Accessed by offset** (like strings and lists)
3. **Immutable sequence** category (cannot be changed in place)
4. **Fixed-length, heterogeneous, and arbitrarily nestable**
5. **Arrays of object references** (store access points to other objects)

### Tuple Operations Table

| Operation | Interpretation |
|-----------|----------------|
| `()` | An empty tuple |
| `T = (0,)` | A one-item tuple (note the comma) |
| `T = (0, 'Py', 1.2, 3)` | A four-item tuple |
| `T = 0, 'Py', 1.2, 3` | Another four-item tuple (parentheses optional) |
| `T = ('Pat', ('dev', 'mgr'))` | Nested tuples |
| `T = tuple('hack')` | Tuple from iterable |
| `T[i]`, `T[i][j]`, `T[i:j]` | Index, nested index, slice |
| `len(T)` | Length |
| `T1 + T2`, `T * 3` | Concatenate, repeat |
| `T1 > T2`, `T1 == T2` | Comparisons |
| `'code' in T` | Membership test |
| `for x in T: print(x)` | Iteration |
| `T.index('Py')`, `T.count('Py')` | Methods: search, count |

### Tuples in Action - Examples

#### Basic Operations
```python
# Concatenation and repetition
>>> (1, 2) + (3, 4)
(1, 2, 3, 4)

>>> (1, 2) * 4
(1, 2, 1, 2, 1, 2, 1, 2)

# Indexing and slicing
>>> T = (1, 2, 3, 4)
>>> T[0], T[1:3]
(1, (2, 3))

# Comparisons
>>> T == (1, 2, 3, 4), T > (1, 2, 3, 3), T > (1,)
(True, True, True)

# Iterable unpacking
>>> L = ['code', 'hack']
>>> (*L, 1, 2, *(3, 4))
('code', 'hack', 1, 2, 3, 4)
```

### Tuple Syntax Peculiarities

#### Single-Item Tuples
**Problem**: Parentheses can enclose expressions, so how does Python know when you want a tuple?

**Solution**: Use a trailing comma for single-item tuples:

```python
>>> x = (40)    # This is an integer!
>>> x
40

>>> y = (40,)   # This is a tuple containing one item
>>> y
(40,)
```

#### Optional Parentheses
Python allows omitting parentheses in unambiguous contexts:

```python
>>> 1, 2, 3, 4  # Tuple without parentheses
(1, 2, 3, 4)

# Sequence assignment uses this feature
>>> a, b, c = 1, 2, 3  # Both sides are tuples
>>> a, b, c
(1, 2, 3)
```

**Best Practice**: Use parentheses for clarity, especially in:
- Function calls
- Nested expressions
- When embedded in other literals

### Conversions, Methods, and Immutability

#### Converting and Sorting Tuples
Since tuples are immutable, you can't sort them directly:

```python
>>> T = ('cc', 'aa', 'dd', 'bb')

# Method 1: Convert to list, sort, convert back
>>> tmp = list(T)        # Make a list
>>> tmp.sort()           # Sort the list
>>> tmp
['aa', 'bb', 'cc', 'dd']
>>> T = tuple(tmp)       # Make a tuple again
>>> T
('aa', 'bb', 'cc', 'dd')

# Method 2: Use sorted() built-in
>>> sorted(T, reverse=True)
['dd', 'cc', 'bb', 'aa']
```

#### List Comprehensions with Tuples
```python
>>> T = (1, 2, 3, 4, 5)
>>> L = [x + 20 for x in T]  # Creates a list from tuple
>>> L
[21, 22, 23, 24, 25]

# Simulating tuple comprehension
>>> tuple(x + 20 for x in T)
(21, 22, 23, 24, 25)
```

#### Tuple Methods
Tuples have only two methods:

```python
>>> T = (1, 2, 3, 2, 4, 2)
>>> T.index(2)      # Offset of first 2
1
>>> T.index(2, 2)   # Offset after position 2
3
>>> T.count(2)      # How many 2s?
3
```

#### Immutability Rules
**Important**: Immutability applies only to the top level:

```python
>>> T = (1, [2, 3], 4)
>>> T[1] = 'mod'        # This fails - can't change tuple
TypeError: 'tuple' object does not support item assignment

>>> T[1][0] = 'mod'     # This works - can change list inside tuple
>>> T
(1, ['mod', 3], 4)
```

### Why Lists and Tuples?

#### Philosophical Differences:
- **Tuple**: Simple association of objects (like a database row)
- **List**: Data structure that changes over time

#### Practical Advantages of Tuples:
1. **Integrity**: Can't be changed through other references
2. **Dictionary keys**: Tuples can be dict keys, lists cannot
3. **Built-in operations**: Some operations require tuples (e.g., string formatting)

#### Rule of Thumb:
- Use **lists** for ordered collections that might change
- Use **tuples** for fixed associations

### Named Tuples - Records Revisited

Named tuples provide both positional and named access to record fields:

```python
# Regular tuple approach
>>> pat = ('Pat', 40.5, ['dev', 'mgr'])
>>> pat[0], pat[2]  # Access by position
('Pat', ['dev', 'mgr'])

# Dictionary approach
>>> pat = dict(name='Pat', age=40.5, jobs=['dev', 'mgr'])
>>> pat['name'], pat['jobs']  # Access by name
('Pat', ['dev', 'mgr'])

# Named tuple approach - best of both worlds
>>> from collections import namedtuple
>>> Rec = namedtuple('Rec', ['name', 'age', 'jobs'])
>>> pat = Rec('Pat', age=40.5, jobs=['dev', 'mgr'])
>>> pat
Rec(name='Pat', age=40.5, jobs=['dev', 'mgr'])

# Access by position
>>> pat[0], pat[2]
('Pat', ['dev', 'mgr'])

# Access by name
>>> pat.name, pat.jobs
('Pat', ['dev', 'mgr'])

# Convert to dictionary
>>> D = pat._asdict()
>>> D['name'], D['jobs']
('Pat', ['dev', 'mgr'])
>>> D
{'name': 'Pat', 'age': 40.5, 'jobs': ['dev', 'mgr']}
```

**Trade-offs**:
- **Pros**: Extra utility, both positional and named access
- **Cons**: Extra setup code, performance overhead

---

## Part 2: Files

### File Basics
Files provide access to external files on your computer through Python's built-in `open()` function.

### Common File Operations Table

| Operation | Interpretation |
|-----------|----------------|
| `output = open(r'C:\data', 'w')` | Create output file (Windows, write mode) |
| `input = open('/home/me/data', 'r')` | Create input file (Unix, read mode) |
| `input = open('data')` | Create input file (current directory, read default) |
| `aString = input.read()` | Read entire file into single string |
| `aString = input.read(N)` | Read up to N characters into string |
| `aString = input.readline()` | Read next line (including \n) |
| `aList = input.readlines()` | Read entire file into list of lines |
| `output.write(aString)` | Write string to file |
| `output.writelines(aList)` | Write all strings in list to file |
| `output.close()` | Manual close |
| `output.flush()` | Flush output buffer to disk |
| `anyFile.seek(N)` | Change file position to offset N |
| `for line in open('data'): use line` | File iterator (best for reading lines) |

### Opening Files

#### Basic Syntax:
```python
afile = open(filename, mode)
afile.method()
```

#### Arguments:
1. **filename**: May include directory path
2. **mode**: Processing mode string
   - `'r'`: Read text (default)
   - `'w'`: Write text (creates new file)
   - `'a'`: Append text to end
   - `'b'`: Binary mode (e.g., `'rb'`, `'wb'`)
   - `'+'`: Read and write (e.g., `'r+'`)

#### Path Examples:
- `'file.txt'`: Current working directory
- `'a/b/file.txt'`: Unix path
- `'a\\b\\file.txt'`: Windows path
- `r'C:\data\file.txt'`: Windows raw string

### Files in Action - Examples

#### Basic File Writing and Reading:
```python
# Writing to a file
>>> myfile = open('myfile.txt', 'w')    # Open for writing
>>> myfile.write('hello text file\n')   # Write line (returns char count)
16
>>> myfile.write('goodbye text file\n')
18
>>> myfile.close()                       # Ensure data is written

# Reading from a file
>>> myfile = open('myfile.txt')          # Open for reading (default)
>>> myfile.readline()                    # Read first line
'hello text file\n'
>>> myfile.readline()                    # Read second line
'goodbye text file\n'
>>> myfile.readline()                    # End of file returns empty string
''
```

#### Reading Entire File:
```python
# Read all at once
>>> open('myfile.txt').read()
'hello text file\ngoodbye text file\n'

# Print with newlines interpreted
>>> print(open('myfile.txt').read())
hello text file
goodbye text file
```

#### File Iterator (Best Practice):
```python
# Most efficient way to read lines
>>> for line in open('myfile.txt'):
...     print(line, end='')  # end='' avoids double spacing
...
hello text file
goodbye text file
```

#### Writing Non-String Data:
```python
# Files require strings - convert other types
>>> myfile = open('myfile2.txt', 'w')
>>> myfile.write(3.14)  # Error! Must be string
TypeError: write() argument must be str, not float

>>> myfile.write(str(3.14) + '\n')  # Convert to string
5
>>> myfile.close()
>>> open('myfile2.txt').read()
'3.14\n'
```

#### Working Directory:
```python
>>> import os
>>> os.getcwd()                    # Show current working directory
'/Users/me/code/Chapter09'
>>> os.listdir()                   # List files in current directory
['myfile2.txt', 'myfile.txt']
```

### Text vs Binary Files

#### Text Files:
- Represent content as `str` strings
- Perform Unicode encoding/decoding automatically
- Perform newline translation by default
- Use modes: `'r'`, `'w'`, `'a'`

#### Binary Files:
- Represent content as `bytes` strings
- Access file content unaltered
- No newline translation
- Use modes: `'rb'`, `'wb'`, `'ab'`

#### Binary File Example:
```python
>>> myfile = open('myfile3.bin', 'wb')           # Binary write mode
>>> myfile.write(b'\x00\x01hack\x02\x03')       # Write bytes
8
>>> myfile.close()

>>> data = open('myfile3.bin', 'rb').read()     # Binary read mode
>>> data                                         # Returns bytes object
b'\x00\x01hack\x02\x03'
>>> data[2:6]                                    # Slice bytes
b'hack'
>>> byte = data[2:6][0]                          # Get individual byte
>>> byte, chr(byte), bin(byte)                   # Byte value, character, binary
(104, 'h', '0b1101000')
```

### Storing Objects in Files

#### Method 1: Manual Conversion
```python
# Writing objects to file
>>> X, Y, Z = 62, 63, 64
>>> S = 'Text'
>>> D = {'a': 1, 'b': 2}
>>> L = [1, 2, 3]
>>> F = open('datafile.txt', 'w')
>>> F.write(S + '\n')                           # Write string
>>> F.write(f'{X},{Y},{Z}\n')                   # Write formatted numbers
>>> F.write(str(L) + '$' + str(D) + '\n')       # Write objects as strings
>>> F.close()

# Reading back and inspecting
>>> chars = open('datafile.txt').read()
>>> chars
"Text\n62,63,64\n[1, 2, 3]${'a': 1, 'b': 2}\n"
>>> print(chars)
Text
62,63,64
[1, 2, 3]${'a': 1, 'b': 2}

# Parsing the data back to objects
>>> F = open('datafile.txt')
>>> line = F.readline()                         # Read string line
>>> line.rstrip()                               # Remove newline
'Text'

>>> line = F.readline()                         # Read number line
>>> parts = line.rstrip().split(',')            # Split on commas
>>> parts
['62', '63', '64']
>>> numbers = [int(P) for P in parts]           # Convert to integers
>>> numbers
[62, 63, 64]

>>> line = F.readline()                         # Read objects line
>>> parts = line.split('$')                     # Split on delimiter
>>> eval(parts[0])                              # Convert string to object
[1, 2, 3]
>>> objects = [eval(P) for P in parts]          # Convert all parts
>>> objects
[[1, 2, 3], {'a': 1, 'b': 2}]
```

#### Method 2: Using pickle Module
```python
# Storing with pickle (binary format)
>>> D = {'a': 1, 'b': 2}
>>> F = open('datafile.pkl', 'wb')              # Binary mode required
>>> import pickle
>>> pickle.dump(D, F)                           # Store object directly
>>> F.close()

# Loading with pickle
>>> F = open('datafile.pkl', 'rb')              # Binary mode for reading
>>> E = pickle.load(F)                          # Recreate object
>>> E
{'a': 1, 'b': 2}

# What pickle creates (internal format)
>>> open('datafile.pkl', 'rb').read()
b'\x80\x04\x95\x11\x00\x00\x00\x00\x00\x00\x00...'  # Binary data
```

**Pickle Benefits**:
- No manual conversion required
- Handles almost any Python object
- Efficient binary format

**Pickle Limitations**:
- Python-specific format
- Security risk with untrusted data (can execute code)

#### Method 3: Using JSON Module
```python
# Creating complex data structure
>>> who = dict(first='Pat', last='Smith')
>>> rec = dict(name=who, job=['dev', 'mgr'], age=40.5)
>>> rec
{'name': {'first': 'Pat', 'last': 'Smith'}, 'job': ['dev', 'mgr'], 'age': 40.5}

# JSON serialization in memory
>>> import json
>>> json.dumps(rec)                             # Python to JSON string
'{"name": {"first": "Pat", "last": "Smith"}, "job": ["dev", "mgr"], "age": 40.5}'
>>> S = json.dumps(rec)                         # Store JSON string
>>> O = json.loads(S)                           # JSON string to Python
>>> O == rec                                    # Same data
True

# JSON with files
>>> file = open('testjson.txt', 'w')
>>> json.dump(rec, fp=file, indent=4)           # Pretty-printed JSON
>>> file.close()
>>> print(open('testjson.txt').read())
{
    "name": {
        "first": "Pat",
        "last": "Smith"
    },
    "job": [
        "dev",
        "mgr"
    ],
    "age": 40.5
}

>>> P = json.load(open('testjson.txt'))         # Load from file
>>> P == rec                                    # Verify data
True
```

**JSON Benefits**:
- Language-neutral format
- Human-readable text
- Widely supported

**JSON Limitations**:
- Limited Python type support
- Text format (larger than pickle)

#### Method 4: Other Tools

**struct Module** (Binary data):
```python
>>> import struct
>>> data = struct.pack('i6s', 62, b'Python')   # Pack binary data
>>> data
b'>\x00\x00\x00Python'
>>> file = open('data.bin', 'wb')
>>> file.write(data)
>>> file.close()
>>> struct.unpack('i6s', open('data.bin', 'rb').read())  # Unpack
(62, b'Python')
```

**csv Module** (Comma-separated values):
```python
>>> import csv
>>> rdr = csv.reader(open('csvdata.txt'))
>>> for row in rdr: 
...     print(row)
['a', 'bbb', 'cc', 'dddd']
['11', '22', '33', '44']
```

### File Context Managers

#### The with Statement:
```python
# Automatic file closing
with open('data.txt') as myfile:
    for line in myfile:
        # use line here
        pass
# File automatically closed here, even if error occurs
```

#### Manual try/finally:
```python
# More verbose but equivalent
myfile = open('data.txt')
try:
    for line in myfile:
        # use line here
        pass
finally:
    myfile.close()  # Always executes
```

**Benefits of Context Managers**:
- Guaranteed resource cleanup
- Works in all Python implementations
- Handles exceptions properly

---

## Part 3: Core Types Review and Summary

### Object Classifications

| Object Type | Category | Mutable? |
|-------------|----------|----------|
| Numbers | Numeric | No |
| Strings | Sequence | No |
| Lists | Sequence | Yes |
| Dictionaries | Mapping | Yes |
| Tuples | Sequence | No |
| Files | Extension | N/A |
| Sets | Set | Yes |
| Frozenset | Set | No |
| bytearray | Sequence | Yes |

### Key Principles:

1. **Category Operations**: Objects share operations by category
   - Sequences: concatenation, indexing, slicing
   - Mappings: key-based access
   - Numbers: arithmetic operations

2. **Mutability**: Only mutable objects can be changed in place
   - Mutable: lists, dictionaries, sets
   - Immutable: numbers, strings, tuples

3. **Nesting**: Compound objects can contain any other objects
   - Lists, dictionaries, tuples support arbitrary nesting
   - Sets contain only immutable objects

### Object Flexibility Examples

#### Complex Nested Structure:
```python
>>> L = ['abc', [(1, 2), ([3], 4)], 5]
>>> L[1]                    # Second item
[(1, 2), ([3], 4)]
>>> L[1][1]                 # Second item of second item  
([3], 4)
>>> L[1][1][0]              # First item of that tuple
[3]
>>> L[1][1][0][0]           # First item of that list
3
```

### References vs Copies

#### Shared References Problem:
```python
>>> X = [1, 2, 3]
>>> L = ['a', X, 'b']       # L contains reference to X
>>> D = {'x': X, 'y': 2}    # D also contains reference to X

>>> X[1] = 'surprise'       # Change affects all references
>>> L
['a', [1, 'surprise', 3], 'b']
>>> D  
{'x': [1, 'surprise', 3], 'y': 2}
```

#### Making Copies:
```python
# Various copy methods
>>> L = [1, 2, 3]
>>> D = {'a': 1, 'b': 2}

>>> A = L[:]                # Slice copy
>>> B = D.copy()            # Method copy
>>> C = list(L)             # Constructor copy
>>> E = dict(D)             # Constructor copy

# Changes to copies don't affect originals
>>> A[1] = 'Py'
>>> B['c'] = 'code'
>>> L, D                    # Originals unchanged
([1, 2, 3], {'a': 1, 'b': 2})
>>> A, B                    # Copies changed
([1, 'Py', 3], {'a': 1, 'b': 2, 'c': 'code'})
```

#### Deep Copies:
```python
# For nested structures
>>> import copy
>>> X = [[1, 2], [3, 4]]
>>> Y = copy.deepcopy(X)    # Copy all levels
```

### Comparisons, Equality, and Truth

#### Equality vs Identity:
```python
>>> L1 = [1, ('a', 3)]
>>> L2 = [1, ('a', 3)]  
>>> L1 == L2, L1 is L2      # Same value? Same object?
(True, False)               # Same value, different objects

# String caching optimization
>>> S1 = 'text'
>>> S2 = 'text'
>>> S1 == S2, S1 is S2      # Both true due to caching
(True, True)

>>> S1 = 'a longer string'
>>> S2 = 'a longer string'  
>>> S1 == S2, S1 is S2      # Normal behavior
(True, False)
```

#### Recursive Comparisons:
```python
>>> L1 = [1, ('a', 3)]      # Nested structures
>>> L2 = [1, ('a', 2)]
>>> L1 < L2, L1 == L2, L1 > L2
(False, False, True)        # L1 > L2 because 3 > 2
```

#### Truth Values:

| Object | Value |
|--------|-------|
| 'text' | True |
| '' | False |
| [1, 2] | True |
| [] | False |
| {'a': 1} | True |
| {} | False |
| 1 | True |
| 0.0 | False |
| None | False |

#### The None Object:
```python
# Preallocating list with None
>>> size = 50
>>> L = [None] * size       # Create list of Nones
>>> L[size - 1] = 'OK'      # Now can assign to any position
>>> L[-10:]                 # Last 10 items
[None, None, None, None, None, None, None, None, None, 'OK']
```

#### Boolean Type:
```python
>>> bool(1)                 # Convert to Boolean
True
>>> bool('text')
True  
>>> bool({})
False
```

---

## Part 4: Common Gotchas and Pitfalls

### 1. Assignment Creates References, Not Copies

**Problem**:
```python
>>> L = [1, 2, 3]
>>> M = ['X', L, 'Y']       # M contains reference to L
>>> L[1] = 0                # Change L affects M
>>> M
['X', [1, 0, 3], 'Y']      # M changed too!
```

**Solution**:
```python
>>> L = [1, 2, 3]
>>> M = ['X', L[:], 'Y']    # M contains copy of L
>>> L[1] = 0                # Change L doesn't affect M
>>> M
['X', [1, 2, 3], 'Y']      # M unchanged
```

### 2. Repetition Adds One Level Deep

**Problem**:
```python
>>> L = [4, 5, 6]
>>> Y = [L] * 4             # Creates 4 references to same list
>>> Y
[[4, 5, 6], [4, 5, 6], [4, 5, 6], [4, 5, 6]]
>>> L[1] = 0                # Change affects all references
>>> Y
[[4, 0, 6], [4, 0, 6], [4, 0, 6], [4, 0, 6]]
```

**Solutions**:
```python
# Solution 1: Copy the list first
>>> L = [4, 5, 6]
>>> Y = [list(L)] * 4       # Still shares one copy
>>> L[1] = 0                # Affects Y but original L is copied
>>> Y
[[4, 5, 6], [4, 5, 6], [4, 5, 6], [4, 5, 6]]

# Solution 2: Create unique copies
>>> L = [4, 5, 6]
>>> Y = [list(L) for i in range(4)]  # Each is unique copy
>>> Y[0][1] = 99            # Only affects first copy
>>> Y
[[4, 99, 6], [4, 5, 6], [4, 5, 6], [4, 5, 6]]
```

### 3. Beware of Cyclic Data Structures

**Problem**:
```python
>>> L = ['stuff']
>>> L.append(L)             # L references itself
>>> L
['stuff', [...]]            # [...] indicates cycle
```

**Issues**:
- Can cause infinite loops in traversal code
- Need special handling in recursive algorithms

**Solution**: 
- Avoid cycles unless necessary
- Use visited sets to detect cycles in traversal code

### 4. Immutable Types Can't Be Changed in Place

**Problem**:
```python
>>> T = (1, 2, 3)
>>> T[2] = 4                # Error! Tuples are immutable
TypeError: 'tuple' object does not support item assignment
```

**Solution**:
```python
>>> T = (1, 2, 3) 
>>> T = T[:2] + (4,)        # Create new tuple
>>> T
(1, 2, 4)
```

---

## Chapter Summary

This chapter covered:

1. **Tuples**: Immutable sequences with limited methods but important use cases
   - Syntax peculiarities (commas, parentheses)
   - When to use vs lists
   - Named tuples for record-like data

2. **Files**: Interface to external storage
   - Text vs binary modes
   - Various storage formats (pickle, JSON, CSV, struct)
   - Context managers for automatic cleanup

3. **Object Properties**: Common characteristics of all core types
   - Mutability and categories
   - References vs copies
   - Comparisons and truth values

4. **Common Pitfalls**: Issues that trap new users
   - Shared references
   - Repetition behavior
   - Cyclic structures
   - Immutability constraints

**Key Takeaways**:
- Understand the difference between references and copies
- Choose appropriate data types for your use case
- Be aware of mutability implications
- Use proper file handling techniques
- Recognize and avoid common gotchas

The next part of the book shifts focus to Python statements and control flow, building on the object knowledge gained in this part.
