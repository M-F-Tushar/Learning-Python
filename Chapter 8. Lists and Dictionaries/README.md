# Chapter 8: Lists and Dictionaries - Complete Guide

## Introduction

This chapter covers Python's two most flexible collection object types:
- **Lists**: Ordered collections of arbitrary objects
- **Dictionaries**: Key-based collections of arbitrary objects

Both are remarkably flexible, can be changed in place, grow and shrink on demand, and contain any other kind of object.

---

## Part 1: Lists

### 1.1 List Properties

Python lists are:

1. **Ordered collections of arbitrary objects**
   - Maintain left-to-right positional ordering
   - Can treat items as groups

2. **Accessed by offset**
   - Use indexing like strings
   - Support slicing and concatenation

3. **Variable-length, heterogeneous, and arbitrarily nestable**
   - Can grow and shrink in place
   - Can contain any sort of object
   - Support arbitrary nesting (lists of lists of lists)

4. **Of the category "mutable sequence"**
   - Can be changed in place
   - Support all sequence operations (indexing, slicing, concatenation)
   - Support operations strings don't (deletion, expansion, index assignment)

5. **Arrays of object references**
   - Contain references to other objects (not copies)
   - Similar to arrays of pointers in other languages

### 1.2 Common List Operations

| Operation | Interpretation | Example |
|-----------|----------------|---------|
| `L = []` | Empty list | `[]` |
| `L = [123, 'abc', 1.23, {}]` | Four items: indexes 0..3 | `[123, 'abc', 1.23, {}]` |
| `L = ['Pat', 40.0, ['dev', 'mgr']]` | Nested sublists | `['Pat', 40.0, ['dev', 'mgr']]` |
| `L = list('code')` | List of iterable's items | `['c', 'o', 'd', 'e']` |
| `L = list(range(-4, 4))` | List of successive integers | `[-4, -3, -2, -1, 0, 1, 2, 3]` |
| `L[i]` | Index | Access item at position i |
| `L[i][j]` | Index of index | Access nested item |
| `L[i:j]` | Slice | Extract section |
| `len(L)` | Length | Number of items |
| `L1 + L2` | Concatenate | Join two lists |
| `L * 3` | Repeat | Repeat list 3 times |
| `3 in L` | Membership | Test if 3 is in list |
| `for x in L: print(x)` | Iteration | Loop through items |

### 1.3 List Methods

#### Growing Methods
- `L.append(4)` - Add single item to end
- `L.extend([5, 6, 7])` - Add multiple items to end
- `L.insert(i, X)` - Insert item at position i

#### Searching Methods
- `L.index(X)` - Find index of item X
- `L.count(X)` - Count occurrences of X

#### Sorting/Reversing Methods
- `L.sort()` - Sort in place
- `L.reverse()` - Reverse in place
- `L.copy()` - Make a copy
- `L.clear()` - Remove all items

#### Shrinking Methods
- `L.pop(i)` - Remove and return item at position i
- `L.remove(X)` - Remove first occurrence of X
- `del L[i]` - Delete item at position i
- `del L[i:j]` - Delete slice
- `L[i:j] = []` - Delete slice via assignment

### 1.4 Lists in Action - Examples

#### Basic List Operations

```python
# Length, concatenation, repetition
>>> len([1, 2, 3])
3
>>> [1, 2, 3] + [4, 5, 6]
[1, 2, 3, 4, 5, 6]
>>> ['Py!'] * 4
['Py!', 'Py!', 'Py!', 'Py!']
```

**Explanation**: 
- `len()` returns number of items
- `+` concatenates lists (both sides must be lists)
- `*` repeats the list content

#### Type Conversion Examples

```python
# Converting between strings and lists
>>> str([1, 2]) + '34'
'[1, 2]34'
>>> [1, 2] + list('34')
[1, 2, '3', '4']
```

**Explanation**: 
- First example converts list to string, then concatenates
- Second example converts string to list, then concatenates lists

#### List Comparisons

```python
>>> L = [1, [2, 3], 4]
>>> (L == [1, [2, 3], 4]), (L > [1, [2, 2], 4])
(True, True)
```

**Explanation**: Lists compare element by element from left to right. The nested `3` is greater than nested `2`, making the second comparison `True`.

#### Indexing and Slicing

```python
>>> L = ['hack', 'Hack', 'HACK!']
>>> L[2]          # Offset starts at 0
'HACK!'
>>> L[-2]         # Negative: count from end
'Hack'
>>> L[1:]         # Slicing from position 1 to end
['Hack', 'HACK!']
```

**Explanation**: 
- `L[2]` gets third item (0-indexed)
- `L[-2]` gets second-to-last item
- `L[1:]` gets all items from position 1 onwards

#### Matrix Representation

```python
>>> matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> matrix[1]      # Get entire row
[4, 5, 6]
>>> matrix[1][1]   # Get specific element
5
>>> matrix[2][0]   # Row 2, column 0
7
```

**Explanation**: This creates a 3×3 matrix using nested lists. First index gets the row, second index gets the column within that row.

#### Multi-line List Syntax

```python
>>> matrix = [[1, 2, 3],
...           [4, 5, 6],
...           [7, 8, 9]]
>>> matrix[1][1]
5
```

**Explanation**: Lists can span multiple lines when enclosed in brackets, making large data structures more readable.

### 1.5 Changing Lists in Place

#### Index and Slice Assignment

```python
>>> L = ['code', 'Code', 'CODE!']
>>> L[1] = 'Hack'        # Index assignment
>>> L
['code', 'Hack', 'CODE!']
>>> L[0:2] = ['write', 'Python']  # Slice assignment
>>> L
['write', 'Python', 'CODE!']
```

**Explanation**: 
- Index assignment replaces single item
- Slice assignment replaces entire section (can change list size)

#### Slice Assignment Mechanics

```python
>>> L = [1, 2, 3]
>>> L[1:2] = [4, 5]     # Replace 1 item with 2
>>> L
[1, 4, 5, 3]
>>> L[1:1] = [6, 7]     # Insert at position 1
>>> L
[1, 6, 7, 4, 5, 3]
>>> L[1:2] = []         # Delete by assigning empty list
>>> L
[1, 7, 4, 5, 3]
```

**Explanation**: 
- Slice assignment works as deletion + insertion
- Number of items inserted doesn't need to match number deleted
- Empty slice assignment inserts without deleting
- Assigning empty list deletes the slice

#### In-place Concatenation

```python
>>> L = [1]
>>> L[:0] = [2, 3, 4]    # Insert at beginning
>>> L
[2, 3, 4, 1]
>>> L[len(L):] = [5, 6, 7]  # Insert at end
>>> L
[2, 3, 4, 1, 5, 6, 7]
>>> L.extend([8, 9, 10])    # More readable way to add at end
>>> L
[2, 3, 4, 1, 5, 6, 7, 8, 9, 10]
```

**Explanation**: 
- `L[:0]` inserts at the beginning
- `L[len(L):]` inserts at the end
- `extend()` is the preferred method for adding multiple items at the end

### 1.6 List Method Examples

#### Append and Extend

```python
>>> L = ['write']
>>> L.append('Python')     # Add single item
>>> L
['write', 'Python']
>>> L.extend(['code', 'goodly'])  # Add multiple items
>>> L
['write', 'Python', 'code', 'goodly']
```

**Explanation**: 
- `append()` adds one item as-is
- `extend()` iterates through the argument and adds each item

#### Sorting

```python
>>> L = ['abc', 'ABD', 'aBe']
>>> L.sort()               # Default ASCII sort
>>> L
['ABD', 'aBe', 'abc']
>>> L = ['abc', 'ABD', 'aBe']
>>> L.sort(key=str.lower)  # Case-insensitive sort
>>> L
['abc', 'ABD', 'aBe']
>>> L = ['abc', 'ABD', 'aBe']
>>> L.sort(key=str.lower, reverse=True)  # Reverse case-insensitive
>>> L
['aBe', 'ABD', 'abc']
```

**Explanation**: 
- Default sort uses ASCII values (uppercase before lowercase)
- `key=str.lower` converts to lowercase for comparison
- `reverse=True` sorts in descending order

#### Mixed Type Sorting

```python
>>> L = [1, 'hack', 2]
>>> L.sort(key=str)        # Convert all to strings for sorting
>>> L
[1, 2, 'hack']
```

**Explanation**: Mixed types can't be compared directly, so `key=str` converts all items to strings for comparison purposes.

#### Other List Methods

```python
>>> L = [1, 2, 3, 4, 5]
>>> L.pop()               # Remove and return last item
5
>>> L
[1, 2, 3, 4]
>>> L.reverse()           # Reverse in place
>>> L
[4, 3, 2, 1]
>>> list(reversed(L))     # Reversed built-in (doesn't modify original)
[1, 2, 3, 4]
>>> L                     # Original unchanged
[4, 3, 2, 1]
```

**Explanation**: 
- `pop()` removes and returns the last item (or item at specified index)
- `reverse()` modifies the list in place
- `reversed()` returns an iterator (need `list()` to see results)

#### Stack Operations (LIFO)

```python
>>> L = []
>>> L.append(1)           # Push onto stack
>>> L.append(2)
>>> L
[1, 2]
>>> L.pop()               # Pop off stack
2
>>> L
[1]
```

**Explanation**: Using `append()` and `pop()` together creates a Last-In-First-Out (LIFO) stack structure.

#### More List Methods

```python
>>> L = ['hack', 'Py', 'code']
>>> L.index('Py')         # Find index of item
1
>>> L.insert(1, 'more')   # Insert at specific position
>>> L
['hack', 'more', 'Py', 'code']
>>> L.remove('code')      # Remove by value
>>> L
['hack', 'more', 'Py']
>>> L.pop(1)              # Remove by index
'more'
>>> L
['hack', 'Py']
>>> L.count('Py')         # Count occurrences
1
```

**Explanation**: 
- `index()` returns the position of the first occurrence
- `insert()` adds item at specified position
- `remove()` deletes first occurrence of the value
- `pop(i)` removes and returns item at position i
- `count()` returns number of occurrences

### 1.7 Iteration, Comprehensions, and Unpacking

#### Basic Iteration

```python
>>> 3 in [1, 2, 3]        # Membership test
True
>>> for x in [1, 2, 3]:   # Iteration
...     print(x, end=' ')
1 2 3
>>> list(range(5))        # Convert range to list
[0, 1, 2, 3, 4]
```

**Explanation**: 
- `in` tests membership
- `for` loops iterate through each item
- `range()` creates a sequence of numbers

#### List Comprehensions

```python
>>> res = [x * 4 for x in 'code']  # List comprehension
>>> res
['cccc', 'oooo', 'dddd', 'eeee']

# Equivalent for loop
>>> res = []
>>> for x in 'code':
...     res.append(x * 4)
>>> res
['cccc', 'oooo', 'dddd', 'eeee']
```

**Explanation**: List comprehensions provide a concise way to create lists. They're often faster than equivalent for loops.

#### Advanced Comprehensions

```python
>>> [x * 4 for x in 'program' if x >= 'p']  # With filter
['pppp', 'rrrr', 'rrrr']
>>> [x + y for x in 'py' for y in '312']    # Nested loops
['p3', 'p1', 'p2', 'y3', 'y1', 'y2']
>>> list(map(abs, [-1, -2, 0, 1, 2]))       # Map function
[1, 2, 0, 1, 2]
```

**Explanation**: 
- `if` clause filters items
- Multiple `for` clauses create nested loops
- `map()` applies a function to each item

#### List Unpacking

```python
>>> L = ['code', 'hack']
>>> [L, 2, 3, L]                    # Without unpacking
[['code', 'hack'], 2, 3, ['code', 'hack']]
>>> [*L, 2, 3, *L]                  # With unpacking
['code', 'hack', 2, 3, 'code', 'hack']
>>> [*'Py', *'code', *range(3)]     # Multiple unpacking
['P', 'y', 'c', 'o', 'd', 'e', 0, 1, 2]
```

**Explanation**: 
- `*` unpacks the contents of an iterable
- Without `*`, you get the list as a single item
- With `*`, you get the individual items from the list

#### Alternative to Unpacking

```python
>>> L = ['code', 'hack']
>>> L + [2, 3] + L                  # Concatenation (equivalent result)
['code', 'hack', 2, 3, 'code', 'hack']
>>> list('Py') + list('code') + list(range(3))  # For non-lists
['P', 'y', 'c', 'o', 'd', 'e', 0, 1, 2]
```

**Explanation**: Often simple concatenation is clearer than unpacking, especially for basic cases.

### 1.8 Other List Operations

#### Deletion with del

```python
>>> L = ['hack', 'more', 'Py', 'code']
>>> del L[0]              # Delete by index
>>> L
['more', 'Py', 'code']
>>> del L[1:]             # Delete slice
>>> L
['more']
```

**Explanation**: `del` statement removes items or slices from lists.

#### Slice Assignment for Deletion

```python
>>> L = ['hack', 'more', 'Py', 'code']
>>> L[0:1] = []           # Delete by assigning empty list
>>> L
['more', 'Py', 'code']
>>> L[1:] = []
>>> L
['more']
>>> L[0] = []             # This assigns empty list, doesn't delete
>>> L
[[]]
```

**Explanation**: 
- Assigning empty list to slice deletes the slice
- Assigning empty list to single index replaces that item with an empty list

---

## Part 2: Dictionaries

### 2.1 Dictionary Properties

Python dictionaries are:

1. **Accessed by key, not offset position**
   - Sometimes called associative arrays or hashes
   - Associate values with keys for retrieval

2. **Insertion-ordered collections of arbitrary objects**
   - Keys ordered by insertion time (as of Python 3.7)
   - No positional ordering like lists

3. **Variable-length, heterogeneous, and arbitrarily nestable**
   - Can grow and shrink in place
   - Can contain objects of any type
   - Support nesting to any depth

4. **Of the category "mutable mapping"**
   - Can be changed in place by assigning to indexes
   - Don't support sequence operations (concatenation, slicing)
   - Only built-in core-type representative of mapping category

5. **Tables of object references (hash tables)**
   - Implemented as hash tables for fast retrieval
   - Store object references, not copies

### 2.2 Common Dictionary Operations

| Operation | Interpretation | Example |
|-----------|----------------|---------|
| `D = {}` | Empty dictionary | `{}` |
| `D = {'name': 'Pat', 'age': 40.0}` | Two-item dictionary | `{'name': 'Pat', 'age': 40}` |
| `D = dict(name='Bob', age=40)` | Alternative construction | Keywords |
| `D = dict([('name', 'Bob'), ('age', 40)])` | From key/value pairs | List of tuples |
| `D = dict.fromkeys(['name', 'age'])` | From keys list | All values None |
| `D['name']` | Indexing by key | Get value for key |
| `'age' in D` | Key membership | Test if key exists |
| `D.keys()` | All keys | View of keys |
| `D.values()` | All values | View of values |
| `D.items()` | All key+value tuples | View of items |
| `D.get(key, default)` | Fetch by key with default | Avoid KeyError |
| `D.pop(key, default)` | Remove by key | Return value |
| `D.update(D2)` | Merge by keys | Add/update items |
| `len(D)` | Number of entries | Count key-value pairs |
| `D[key] = 62` | Adding/changing keys | Assignment |
| `del D[key]` | Deleting entries | Remove key-value pair |

### 2.3 Dictionaries in Action - Examples

#### Basic Dictionary Operations

```python
>>> D = {'hack': 1, 'Py': 2, 'code': 3}  # Make dictionary
>>> D['Py']                               # Fetch by key
2
>>> D                                     # Insertion order preserved
{'hack': 1, 'Py': 2, 'code': 3}
```

**Explanation**: 
- Dictionaries are created with `{key: value}` syntax
- Access values using `D[key]` syntax
- Keys maintain insertion order (Python 3.7+)

#### Dictionary Properties

```python
>>> len(D)                  # Number of entries
3
>>> 'code' in D            # Key membership test
True
>>> list(D.keys())         # All keys (need list() for display)
['hack', 'Py', 'code']
```

**Explanation**: 
- `len()` returns number of key-value pairs
- `in` tests for key existence
- `keys()` returns a view object (need `list()` to see all at once)

#### Changing Dictionaries in Place

```python
>>> D
{'hack': 1, 'Py': 2, 'code': 3}
>>> D['Py'] = ['app', 'dev']    # Change existing key
>>> D
{'hack': 1, 'Py': ['app', 'dev'], 'code': 3}
>>> del D['code']               # Delete entry
>>> D
{'hack': 1, 'Py': ['app', 'dev']}
>>> D['years'] = 32            # Add new entry
>>> D
{'hack': 1, 'Py': ['app', 'dev'], 'years': 32}
>>> D['Py'][0] = 'program'     # Change nested object
>>> D
{'hack': 1, 'Py': ['program', 'dev'], 'years': 32}
```

**Explanation**: 
- Assigning to existing key changes its value
- Assigning to new key creates new entry
- `del` removes key-value pairs
- Can modify nested objects independently

#### Dictionary Methods

```python
>>> D = {'program': 1, 'script': 2, 'app': 3}
>>> list(D.keys())          # All keys
['program', 'script', 'app']
>>> list(D.values())        # All values
[1, 2, 3]
>>> list(D.items())         # All key-value pairs
[('program', 1), ('script', 2), ('app', 3)]
```

**Explanation**: All three methods return view objects that need `list()` for full display.

#### The get() Method

```python
>>> D.get('script')         # Existing key
2
>>> print(D.get('code'))    # Non-existing key
None
>>> D.get('code', 4)        # Non-existing key with default
4
```

**Explanation**: `get()` returns the value if key exists, otherwise returns default (None if not specified).

#### The update() Method

```python
>>> D
{'program': 1, 'script': 2, 'app': 3}
>>> D2 = {'code': 4, 'hack': 5, 'app': 6}  # New dictionary
>>> D.update(D2)            # Merge D2 into D
>>> D
{'program': 1, 'script': 2, 'app': 6, 'code': 4, 'hack': 5}
```

**Explanation**: `update()` adds new keys and overwrites existing ones. Note 'app' changed from 3 to 6.

#### The pop() Method

```python
>>> D.pop('app')            # Remove and return value
6
>>> D.pop('hack')           # Remove another
5
>>> D
{'program': 1, 'script': 2, 'code': 4}

# Compare with list pop
>>> L = ['aa', 'bb', 'cc', 'dd']
>>> L.pop()                 # Remove last (no argument)
'dd'
>>> L.pop(1)                # Remove by position
'bb'
>>> L
['aa', 'cc']
```

**Explanation**: 
- Dictionary `pop()` takes a key and returns its value
- List `pop()` takes an optional index (default is last item)

### 2.4 Dictionary Creation Methods

```python
# 1) Traditional literal
{'name': 'Pat', 'age': 40}

# 2) Assignment to empty dict
D = {}
D['name'] = 'Pat'
D['age'] = 40

# 3) dict() with keywords
dict(name='Pat', age=40)

# 4) dict() with key-value pairs
dict([('name', 'Pat'), ('age', 40)])
```

**Explanation**: 
- Method 1: Best when you know all data upfront
- Method 2: Best for building dictionaries dynamically
- Method 3: Less typing, but keys must be strings
- Method 4: Useful when keys/values come from sequences

#### Zipping Keys and Values

```python
>>> dict(zip(['a', 'b', 'c'], [1, 2, 3]))  # Zip keys with values
{'a': 1, 'b': 2, 'c': 3}
>>> dict.fromkeys(['a', 'b'], 0)            # Same initial value
{'a': 0, 'b': 0}
```

**Explanation**: 
- `zip()` pairs up items from two sequences
- `fromkeys()` creates dictionary with same value for all keys

#### Dictionary Unpacking

```python
>>> D = dict(a=4, c=3)
>>> {'a': 1, 'b': 2, **D}      # Unpack D into new dictionary
{'a': 4, 'b': 2, 'c': 3}      # D's values override
>>> dict(a=1, b=2) | D         # Union operator (Python 3.9+)
{'a': 4, 'b': 2, 'c': 3}
```

**Explanation**: 
- `**D` unpacks dictionary D into the literal
- `|` is the union operator (similar to `update()` but returns new dict)
- Later values override earlier ones when keys conflict

### 2.5 Dictionary Comprehensions

#### Basic Comprehension Syntax

```python
{k: v for x in iterable}  # Dictionary comprehension

# Equivalent loop
new = {}
for x in iterable:
    new[k] = v
```

#### Dictionary Comprehension Examples

```python
>>> list(zip(['a', 'b', 'c'], [1, 2, 3]))  # Show zip result
[('a', 1), ('b', 2), ('c', 3)]
>>> D = dict(zip(['a', 'b', 'c'], [1, 2, 3]))
>>> D
{'a': 1, 'b': 2, 'c': 3}

# Same result with comprehension
>>> D = {k: v for (k, v) in zip(['a', 'b', 'c'], [1, 2, 3])}
>>> D
{'a': 1, 'b': 2, 'c': 3}
```

**Explanation**: Dictionary comprehensions can replace `dict()` + `zip()` combinations.

#### More Comprehension Examples

```python
>>> D = {x: x ** 2 for x in [1, 2, 3, 4]}     # Squares
>>> D
{1: 1, 2: 4, 3: 9, 4: 16}
>>> D = {c: c * 4 for c in 'HACK'}            # Character repetition
>>> D
{'H': 'HHHH', 'A': 'AAAA', 'C': 'CCCC', 'K': 'KKKK'}
>>> D = {c.lower(): (c + '!') for c in ['HACK', 'PY', 'CODE']}
>>> D
{'hack': 'HACK!', 'py': 'PY!', 'code': 'CODE!'}
```

**Explanation**: 
- Keys and values can both be expressions
- Can transform data while building the dictionary

#### Initialization Comparisons

```python
# Using fromkeys
>>> D = dict.fromkeys(['a', 'b', 'c'], 0)
>>> D
{'a': 0, 'b': 0, 'c': 0}

# Using comprehension
>>> D = {k: 0 for k in ['a', 'b', 'c']}
>>> D
{'a': 0, 'b': 0, 'c': 0}

# From string
>>> D = dict.fromkeys('code')
>>> D
{'c': None, 'o': None, 'd': None, 'e': None}
>>> D = {k: None for k in 'code'}
>>> D
{'c': None, 'o': None, 'd': None, 'e': None}
```

**Explanation**: Comprehensions provide more flexibility than `fromkeys()` for initialization.

### 2.6 Key Insertion Ordering

```python
>>> D = dict(a=1, b=2)      # Literal keys in order
>>> D['c'] = 3              # New keys always go to end
>>> D
{'a': 1, 'b': 2, 'c': 3}
>>> D.pop('b')              # Remove middle key
2
>>> D                       # Other keys maintain positions
{'a': 1, 'c': 3}
>>> D['b'] = 2              # Re-adding goes to end
>>> D
{'a': 1, 'c': 3, 'b': 2}
>>> D['c'] = 0              # Changing value doesn't move key
>>> D['d'] = 1              # New key goes to end
>>> D
{'a': 1, 'c': 0, 'b': 2, 'd': 1}
```

**Explanation**: 
- Keys maintain insertion order (Python 3.7+)
- Removing and re-adding a key puts it at the end
- Changing a value doesn't change key position

#### Dictionary as Stack

```python
>>> D.popitem()             # Remove most recently added
('d', 1)
>>> D.popitem()             # Remove next most recent
('b', 2)
>>> D
{'a': 1, 'c': 0}
```

**Explanation**: `popitem()` removes the most recently inserted key-value pair (LIFO behavior).

### 2.7 Dictionary Union Operator

```python
>>> D = dict(a=1, b=2)
>>> D | {'b': 3, 'c': 4}                    # Union returns new dict
{'a': 1, 'b': 3, 'c': 4}
>>> D | {'b': 3, 'c': 4} | dict(a=5, d=6)  # Chain unions
{'a': 5, 'b': 3, 'c': 4, 'd': 6}

# Equivalent with update (but modifies original)
>>> D
{'a': 1, 'b': 2}
>>> C = D.copy()                # Need copy to avoid modifying D
>>> C.update({'b': 3, 'c': 4})  # update modifies in place
>>> C.update(dict(a=5, d=6))
>>> C
{'a': 5, 'b': 3, 'c': 4, 'd': 6}

# Also equivalent with unpacking
>>> D
{'a': 1, 'b': 2}
>>> {**D, **{'b': 3, 'c': 4}, **dict(a=5, d=6)}
{'a': 5, 'b': 3, 'c': 4, 'd': 6}
```

**Explanation**: 
- `|` creates new dictionary (like `copy()` + `update()`)
- `update()` modifies existing dictionary
- `**` unpacking can achieve same result in literals

### 2.8 Practical Example: Books Database

```python
>>> table = {'2024': 'Learning Python, 6th Edition',
...          '2013': 'Learning Python, 5th Edition', 
...          '1999': 'Learning Python'}
>>> table['2024']
'Learning Python, 6th Edition'
>>> for year in table:
...     print(year + '\t' + table[year])
2024    Learning Python, 6th Edition
2013    Learning Python, 5th Edition
1999    Learning Python
```

**Explanation**: 
- Dictionary maps years (keys) to titles (values)
- Loop iterates through keys in insertion order
- `\t` adds tab character for formatting

#### Reverse Mapping (Value to Key)

```python
# Method 1: Restructure the dictionary
>>> table = {'Learning Python, 6th Edition': 2024,
...          'Learning Python, 5th Edition': 2013,
...          'Learning Python': 1999}
>>> table['Learning Python']
1999

# Method 2: Search through items
>>> table = {'2024': 'Learning Python, 6th Edition',
...          '2013': 'Learning Python, 5th Edition', 
...          '1999': 'Learning Python'}
>>> list(table.items())[:2]
[('2024', 'Learning Python, 6th Edition'), ('2013', 'Learning Python, 5th Edition')]
>>> [year for (year, title) in table.items() if title == 'Learning Python']
['1999']
```

**Explanation**: 
- Method 1: Reverse key-value relationship in dictionary structure
- Method 2: Search through all items to find matching value
- List comprehension with tuple unpacking finds year for given title

#### Multiple Ways to Map Values to Keys

```python
>>> K = 'Learning Python'
>>> V = 1999
>>> table[K]  # Key => Value (normal lookup)
1999

# Value => Key searches
>>> [key for (key, value) in table.items() if value == V]
['Learning Python']
>>> [key for key in table.keys() if table[key] == V]
['Learning Python']

# Dictionary inversion (if values are unique and immutable)
>>> dict(zip(table.values(), table.keys()))[V]
'Learning Python'
```

**Explanation**: 
- Normal dictionary lookup is key to value
- Reverse lookup requires searching (slower than direct lookup)
- Dictionary inversion creates new dict with swapped keys/values
- Multiple keys can have same value, but each key has only one value

### 2.9 Dictionary Usage Tips

#### Important Limitations and Rules

**1. Sequence operations don't work**
```python
>>> D = {'a': 1, 'b': 2}
>>> D + {'c': 3}  # This will fail
TypeError: unsupported operand type(s) for +: 'dict' and 'dict'
>>> D[0:2]        # This will fail
TypeError: unhashable type: 'slice'
```

**Explanation**: Dictionaries are mappings, not sequences. Concatenation and slicing don't make sense for key-based collections.

**2. Assigning to new indexes adds entries**
```python
>>> D = {'a': 1}
>>> D['b'] = 2    # Creates new entry
>>> D
{'a': 1, 'b': 2}
```

**Explanation**: Unlike lists, you can assign to any key in a dictionary. New keys create new entries.

**3. Keys need not always be strings**
```python
# Integer keys
>>> D = {}
>>> D[99] = 'hack'
>>> D[99]
'hack'
>>> D
{99: 'hack'}

# Mixed key types
>>> D = {1: 'int', 'a': 'string', (1, 2): 'tuple'}
>>> D[1]
'int'
>>> D['a'] 
'string'
>>> D[(1, 2)]
'tuple'
```

**Explanation**: Any immutable object can be a dictionary key (strings, numbers, tuples). Lists and dictionaries cannot be keys because they're mutable.

### 2.10 Advanced Dictionary Usage

#### Using Dictionaries as Flexible Lists

```python
# Regular list - must assign to existing indices
>>> L = []
>>> L[99] = 'hack'  # This fails
IndexError: list assignment index out of range

# Dictionary - can assign to any key
>>> D = {}
>>> D[99] = 'hack'  # This works
>>> D[99]
'hack'
>>> D[62] = 'code'
>>> D[30] = 'write'
>>> D
{99: 'hack', 62: 'code', 30: 'write'}
```

**Explanation**: Dictionaries with integer keys can simulate sparse arrays without allocating space for unused positions.

#### Sparse Data Structures with Tuple Keys

```python
>>> Matrix = {}
>>> Matrix[(2, 3, 4)] = 88    # 3D coordinate as key
>>> Matrix[(7, 8, 9)] = 99
>>> X = 2; Y = 3; Z = 4       # Variables for coordinates
>>> Matrix[(X, Y, Z)]
88
>>> Matrix
{(2, 3, 4): 88, (7, 8, 9): 99}

# Accessing non-existent position
>>> Matrix[(2, 3, 6)]
KeyError: (2, 3, 6)
```

**Explanation**: 
- Tuples make good keys for multidimensional coordinates
- Only stores values for positions that have data (sparse matrix)
- Accessing empty positions raises KeyError

#### Avoiding Missing-Key Errors

```python
# Method 1: get() with default
>>> Matrix.get((2, 3, 4), 0)    # Exists: return value
88
>>> Matrix.get((2, 3, 6), 0)    # Doesn't exist: return default
0

# Method 2: Test with 'in' first
>>> if (2, 3, 6) in Matrix:
...     print(Matrix[(2, 3, 6)])
... else:
...     print(0)
0

# Method 3: Try/except (preview of exception handling)
>>> try:
...     print(Matrix[(2, 3, 6)])
... except KeyError:
...     print(0)
0
```

**Explanation**: 
- `get()` is most concise for providing defaults
- `in` test prevents KeyError but requires extra code
- `try/except` is more general but also more verbose

#### Nested Dictionaries as Records

```python
# Simple record
>>> rec = {}
>>> rec['title'] = 'Learning Python, 5th Edition'
>>> rec['year'] = 2013
>>> rec['isbn'] = '9781449355739'
>>> rec['year'], rec['isbn']
(2013, '9781449355739')

# Complex nested record
>>> rec = {'title': 'Learning Python, 5th Edition',
...        'date': {'year': 2013, 'month': 'July'},
...        'isbns': ['1449355730', '9781449355739']}

# Accessing nested data
>>> rec['title']
'Learning Python, 5th Edition'
>>> rec['isbns']
['1449355730', '9781449355739']
>>> rec['isbns'][1]
'9781449355739'
>>> rec['date']['year']
2013
```

**Explanation**: 
- Dictionaries can represent structured data like records
- Nested dictionaries and lists create complex data structures
- Chain indexing operations to access deeply nested data

#### Database-like Collections

```python
# List-based database
db = []
db.append(rec)    # Add records to list
db.append(other)
db[0]['isbns']    # Access by position

# Dictionary-based database  
db = {}
db['lp5e'] = rec      # Add records with meaningful keys
db['lp6e'] = other
db['lp5e']['isbns']   # Access by key
```

**Explanation**: 
- Collections can contain dictionaries as records
- List databases use numeric indices
- Dictionary databases use meaningful string keys

### 2.11 Dictionary Views

#### Understanding View Objects

```python
>>> D = dict(program=1, script=2, app=3)
>>> D.keys()
dict_keys(['program', 'script', 'app'])
>>> D.values()
dict_values([1, 2, 3])
>>> D.items()
dict_items([('program', 1), ('script', 2), ('app', 3)])
```

**Explanation**: 
- `keys()`, `values()`, and `items()` return view objects, not lists
- Views are iterables that produce results on demand
- Views don't support list operations like indexing

#### Converting Views to Lists

```python
>>> D = dict(a=1, b=2, c=3)
>>> K = D.keys()        # Make a view object
>>> K
dict_keys(['a', 'b', 'c'])
>>> list(K)             # Force to real list
['a', 'b', 'c']
>>> V = D.values()      # Values view
>>> list(V)
[1, 2, 3]
>>> list(D.items())     # Items view to list
[('a', 1), ('b', 2), ('c', 3)]

# Views don't support list operations
>>> K[0]                # This fails
TypeError: 'dict_keys' object is not subscriptable
>>> K.sort()            # This fails  
AttributeError: 'dict_keys' object has no attribute 'sort'

# But lists do
>>> list(K)[0], list(K).sort()
('a', None)
```

**Explanation**: 
- Use `list()` to convert views when you need list operations
- Views save memory by not storing all results at once
- Views can't be indexed or sorted directly

#### Dynamic Views

```python
>>> D = {'a': 1, 'b': 2, 'c': 3}
>>> K = D.keys()
>>> V = D.values()
>>> list(K), list(V)    # Views maintain current state
(['a', 'b', 'c'], [1, 2, 3])
>>> del D['b']          # Change the dictionary
>>> D
{'a': 1, 'c': 3}
>>> list(K), list(V)    # Views reflect changes automatically
(['a', 'c'], [1, 3])
```

**Explanation**: Views automatically reflect changes made to the original dictionary after the view was created.

#### Views in Loops

```python
>>> for k in D.keys(): 
...     print(k)        # View iterator
a
c

# Usually unnecessary - dictionaries are iterable
>>> for k in D: 
...     print(k)        # Dictionary iterator (equivalent)
a
c
```

**Explanation**: 
- Views work automatically in loops
- Usually don't need to call `keys()` explicitly
- `for k in D` is equivalent to `for k in D.keys()`

### 2.12 Dictionary Views and Sets

#### Set-like Operations

```python
>>> D = {'a': 1, 'b': 2, 'c': 3}
>>> K = D.keys()
>>> V = D.values()

# Keys views support set operations
>>> K | {'x': 4}        # Union (keys with another set)
{'x', 'a', 'b', 'c'}   # Result is a set

# Values views don't support set operations
>>> V | {'x': 4}        # This fails
TypeError: unsupported operand type(s) for |: 'dict_values' and 'set'
```

**Explanation**: 
- Keys views are set-like (unique, immutable items)
- Values views are not set-like (may have duplicates)
- Set operations on views return sets, not dictionaries

#### Mixing Views with Sets and Dictionaries

```python
>>> D = {'a': 1, 'b': 2, 'c': 3}
>>> D.keys() & D.keys()         # Intersect views
{'b', 'a', 'c'}
>>> D.keys() & {'b'}            # Intersect view and set
{'b'}
>>> D.keys() & {'b': 1}         # Intersect view and dictionary
{'b'}                           # (dictionary treated as its keys)
>>> D.keys() | {'b', 'c', 'd'}  # Union view and set
{'b', 'a', 'd', 'c'}
```

**Explanation**: 
- Views can be mixed with sets and other dictionaries in set operations
- Dictionaries are treated as their keys in set operations
- Results are always sets, not dictionaries

#### Items Views and Set Operations

```python
>>> D = {'a': 1}
>>> D.items()           # Items view
dict_items([('a', 1)])
>>> D.items() | D.keys()                    # Union items and keys
{('a', 1), 'a'}
>>> D.items() | D                           # Dictionary treated as keys
{('a', 1), 'a'}
>>> D.items() | {('c', 3), ('d', 4)}       # Union with tuples
{('a', 1), ('c', 3), ('d', 4)}
>>> dict(D.items() | {('c', 3), ('d', 4)}) # Convert back to dict
{'a': 1, 'c': 3, 'd': 4}

# Items views only work if values are immutable
>>> {'a': [1, 2]}.items() | {0, 1}  # Mutable values fail
TypeError: unhashable type: 'list'
```

**Explanation**: 
- Items views support set operations if all values are immutable
- Can union items views to effectively merge dictionaries
- Mutable values (like lists) can't be in sets, so items views fail

### 2.13 Sorting Dictionary Keys

#### The Problem with View Objects

```python
>>> D = {'c': 3, 'b': 2, 'a': 1}
>>> D
{'c': 3, 'b': 2, 'a': 1}
>>> Ks = D.keys()       # Get keys view
>>> Ks.sort()           # This fails - views don't have sort()
AttributeError: 'dict_keys' object has no attribute 'sort'
```

**Explanation**: Views don't support list methods like `sort()`.

#### Solutions for Sorting

```python
# Method 1: Convert to list first
>>> Ks = list(D.keys())     # Convert to list
>>> Ks.sort()               # Sort the list
>>> for k in Ks: 
...     print(k, D[k])
a 1
b 2
c 3

# Method 2: Use sorted() on view
>>> Ks = D.keys()           # Keep as view
>>> for k in sorted(Ks): 
...     print(k, D[k])      # sorted() works on any iterable
a 1
b 2  
c 3

# Method 3: Use sorted() on dictionary directly
>>> for k in sorted(D): 
...     print(k, D[k])      # Dictionary iterator in sorted()
a 1
b 2
c 3
```

**Explanation**: 
- Method 1: Explicit conversion and sorting
- Method 2: `sorted()` works on any iterable, returns sorted list
- Method 3: Most concise - `sorted(D)` sorts the dictionary's keys

### 2.14 Dictionary Comparisons

#### Equality Comparisons

```python
>>> D1 = dict(a=1, b=2, c=3)
>>> D2 = dict(c=3, b=2, a=1)       # Different insertion order
>>> D1, D2
({'a': 1, 'b': 2, 'c': 3}, {'c': 3, 'b': 2, 'a': 1})
>>> D1 == D2, D1 != D2              # Equality ignores order
(True, False)
```

**Explanation**: Dictionary equality compares all key-value pairs and ignores insertion order.

#### Magnitude Comparisons

```python
>>> D1 = dict(a=1, b=2, c=4)       # Different values
>>> D2 = dict(c=3, b=2, a=1)
>>> D1 > D2                         # Direct comparison fails
TypeError: '>' not supported between instances of 'dict' and 'dict'

# Manual comparison of items
>>> list(D1.items()), list(D2.items())
([('a', 1), ('b', 2), ('c', 4)], [('c', 3), ('b', 2), ('a', 1)])
>>> list(D1.items()) > list(D2.items())     # Compare as lists
False
>>> D1.items() > D2.items()                 # Set comparison (not greater-than!)
False
>>> sorted(D1.items()) > sorted(D2.items()) # Sort first, then compare
True
```

**Explanation**: 
- Dictionaries don't support `>`, `<` comparisons directly
- Can compare items as lists, but need to consider insertion order
- Views support set operations, not magnitude comparisons
- Sorting items first gives consistent magnitude comparison

---

## Summary

### Lists Summary
- **Ordered, mutable sequences** that can contain any object types
- **Indexed by position** (0, 1, 2, ...) with support for negative indexing
- **Dynamic sizing** - can grow and shrink with `append()`, `extend()`, `pop()`, `remove()`, etc.
- **Rich method set** for sorting, reversing, searching, and modification
- **Support comprehensions** for concise creation: `[x*2 for x in range(5)]`
- **Slice assignment** allows in-place modification of sections
- **Can be nested** to create multidimensional structures

### Dictionaries Summary  
- **Key-based mappings** that associate values with keys for fast lookup
- **Insertion-ordered** (Python 3.7+) but not positionally indexed
- **Mutable** - can add, change, and delete key-value pairs
- **Flexible keys** - any immutable object (strings, numbers, tuples)
- **Rich method set** - `get()`, `keys()`, `values()`, `items()`, `update()`, etc.
- **Support comprehensions** for concise creation: `{k: v for k, v in pairs}`
- **Multiple creation methods** - literals, `dict()`, `fromkeys()`, etc.
- **View objects** for keys, values, and items that reflect changes dynamically

### Key Differences
| Aspect | Lists | Dictionaries |
|--------|-------|-------------|
| Access | By position (index) | By key |
| Ordering | Positional | Insertion order only |
| Keys/Indices | Must be integers in range | Any immutable object |
| Sequence Ops | Support slicing, concat | Don't support |
| Use Cases | Ordered collections | Mappings, records, lookups |

### When to Use Which
- **Use Lists** for:
  - Ordered data where position matters
  - Sequences that need slicing/concatenation  
  - Data accessed by numeric index
  - Implementing stacks, queues

- **Use Dictionaries** for:
  - Data looked up by meaningful keys
  - Records with named fields
  - Mappings and associations
  - Fast lookups by key
  - Sparse data structures

Both are fundamental Python data structures that form the backbone of most Python programs. Understanding their capabilities, methods, and appropriate use cases is essential for effective Python programming.
