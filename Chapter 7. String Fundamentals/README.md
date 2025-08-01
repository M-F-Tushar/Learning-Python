# Python String Fundamentals - Complete Guide

## Table of Contents
1. [Introduction](#introduction)
2. [String Object Basics](#string-object-basics)
3. [String Literals](#string-literals)
4. [String Operations](#string-operations)
5. [String Methods](#string-methods)
6. [String Formatting](#string-formatting)
7. [General Type Categories](#general-type-categories)
8. [Quiz and Answers](#quiz-and-answers)

---

## Introduction

Strings are Python's primary tool for storing and representing text and byte-based information. They are **immutable sequences** - meaning:
- Characters have a left-to-right positional order
- Cannot be changed in place
- First representative of the sequence class (others include lists and tuples)

### What Strings Represent
- Symbols and words (names, text)
- File contents loaded into memory
- Internet addresses
- Python source code
- Raw bytes for media files and network transfers
- Unicode text (encoded and decoded forms)

---

## String Object Basics

### Key Characteristics
- **Immutable sequences**: Cannot be changed in place
- **Higher-level than C arrays**: Come with powerful processing tools
- **No distinct character type**: Use one-character strings instead
- **Sequences support**: indexing, slicing, concatenation, iteration

### Common String Operations Preview

| Operation | Example | Description |
|-----------|---------|-------------|
| Empty string | `S = ''` | Create empty string |
| Double quotes | `S = "app's"` | Same as single quotes |
| Escape sequences | `S = 'c\no\td\x00e'` | Special characters |
| Triple quotes | `S = """multiline..."""` | Block strings |
| Raw strings | `S = r'\temp\data.txt'` | Ignore escapes |
| Concatenation | `S1 + S2` | Combine strings |
| Repetition | `S * 3` | Repeat string |
| Indexing | `S[i]` | Get character at position |
| Slicing | `S[i:j]` | Extract substring |
| Length | `len(S)` | Number of characters |

---

## String Literals

### 1. Single and Double Quotes

Both single (`'`) and double (`"`) quotes work identically:

```python
>>> 'python', "python"
('python', 'python')

# Embed quotes of the other type
>>> 'python"s', "python's"
('python"s', "python's")

# Automatic concatenation of adjacent literals
>>> title = "Learning " 'Python' " 6E"
>>> title
'Learning Python 6E'
```

**Key Points:**
- Quotes must match and be straight (not slanted)
- Allows embedding opposite quote type without escaping
- Adjacent string literals automatically concatenate

### 2. Escape Sequences

Backslashes introduce special character codes:

```python
>>> s = 'a\nb\tc'  # newline and tab
>>> s
'a\nb\tc'
>>> print(s)
a
b	c
>>> len(s)  # Only 5 characters total
5
```

#### Complete Escape Sequence Table

| Escape | Meaning | Example |
|--------|---------|---------|
| `\\` | Backslash | `'\\'` → `\` |
| `\'` | Single quote | `'\''` → `'` |
| `\"` | Double quote | `'\"'` → `"` |
| `\n` | Newline | `'a\nb'` → `a` + newline + `b` |
| `\r` | Carriage return | Windows line endings |
| `\t` | Horizontal tab | `'a\tb'` → `a` + tab + `b` |
| `\v` | Vertical tab | Rarely used |
| `\a` | Bell | System beep (where supported) |
| `\b` | Backspace | Delete previous character |
| `\f` | Formfeed | Page break |
| `\xhh` | Hex value | `'\x41'` → `A` (hex 41 = 65) |
| `\ooo` | Octal value | `'\101'` → `A` (octal 101 = 65) |
| `\0` | Null character | Binary zero |
| `\uhhhh` | Unicode 16-bit | `'\u0041'` → `A` |
| `\Uhhhhhhhh` | Unicode 32-bit | `'\U00000041'` → `A` |

#### Advanced Escape Examples

```python
# Absolute values as characters
>>> s = 'a\0b\0c'  # Contains null characters
>>> s
'a\x00b\x00c'
>>> len(s)
5

# All escape codes
>>> s = '\001\002\x03'  # Octal and hex
>>> s
'\x01\x02\x03'
>>> len(s)
3

# Mixed characters and escapes
>>> S = 'H\tA\nC\x00K'
>>> len(S)
7
>>> print(S)
H	A
CK
```

### 3. Raw Strings

Prefix `r` or `R` turns off escape mechanism:

```python
# Problem with regular strings
>>> myfile = open('C:\new\text.dat', 'w')  # \n and \t interpreted!

# Solution 1: Raw strings
>>> myfile = open(r'C:\new\text.dat', 'w')  # Backslashes literal

# Solution 2: Double backslashes
>>> myfile = open('C:\\new\\text.dat', 'w')  # Escape the backslashes

# Demonstration
>>> path = r'C:\new\text.dat'
>>> path
'C:\\new\\text.dat'  # Python shows escaped version
>>> print(path)
C:\new\text.dat      # But actually contains single backslashes
>>> len(path)
15
```

**Raw String Limitation:**
```python
# Cannot end with single backslash
>>> r'path\'    # SyntaxError!
>>> r'path\\'[:-1]    # Workaround: slice off last character
>>> r'path' + '\\'   # Workaround: concatenate
>>> 'path\\'         # Workaround: use regular string
```

### 4. Triple Quotes (Block Strings)

Use `"""` or `'''` for multiline strings:

```python
>>> quip = """Python strings
... sure have
... a lot of options"""
>>> quip
'Python strings\n sure have\na lot of options'
>>> print(quip)
Python strings
 sure have
a lot of options
```

**Uses for Triple Quotes:**
- Multiline text in programs
- Embedding HTML, XML, JSON, YAML
- Documentation strings (docstrings)
- Temporarily disabling code blocks

**Important:** Comments inside triple quotes become part of the string:
```python
# Wrong way
>>> menu = """
... Open  # This comment is IN the string!
... Save  # This too!
... """

# Right way
>>> menu = (
...     'Open\n'  # Comments here are ignored
...     'Save\n'  # Newlines must be explicit
... )
```

---

## String Operations

### Basic Operations

```python
# Length
>>> len('abc')
3

# Concatenation
>>> 'abc' + 'def'
'abcdef'

# Repetition
>>> 'Py!' * 4
'Py!Py!Py!Py!'

# Practical repetition use
>>> print('-' * 80)  # 80 dashes
--------------------------------------------------------------------------------
```

### Iteration and Membership

```python
>>> myjob = 'hacker'

# Iterate through characters
>>> for c in myjob:
...     print(c, end=' ')
h a c k e r

# Test membership
>>> 'k' in myjob
True
>>> 'z' in myjob
False
>>> 'HACK' in 'abcHACKdef'  # Substring search
True
```

### Indexing and Slicing

#### Indexing Basics
```python
>>> S = 'code'
>>> S[0]    # First character
'c'
>>> S[-1]   # Last character
'e'
>>> S[-2]   # Second from end
'd'
```

#### Slicing Syntax: `S[start:end:step]`

```python
>>> S = 'code'
>>> S[1:3]    # Characters 1 and 2 (end not included)
'od'
>>> S[1:]     # From position 1 to end
'ode'
>>> S[:3]     # From start to position 3 (not included)
'cod'
>>> S[:-1]    # All but last character
'cod'
>>> S[:]      # Complete copy
'code'
```

#### Advanced Slicing with Steps

```python
>>> S = 'abcdefghijklmnop'
>>> S[1:10:2]    # Every other character from 1 to 10
'bdfhj'
>>> S[::2]       # Every other character from start to end
'acegikmo'
>>> S[::-1]      # Reverse the string
'ponmlkjihgfedcba'
>>> S[5:1:-1]    # Reverse slice from 5 to 1
'fdec'
```

#### Slice Object Equivalence
```python
>>> 'code'[1:3]
'od'
>>> 'code'[slice(1, 3)]  # Same result using slice object
'od'
```

### Practical Slicing Applications

#### Command Line Arguments
```python
# File: echo.py
import sys
print(sys.argv)

# $ python echo.py -a -b -c
# ['echo.py', '-a', '-b', '-c']

# Get arguments without program name
args = sys.argv[1:]  # ['−a', '−b', '−c']
```

#### Cleaning Input Lines
```python
# Remove newline from end of line
line = "Hello World\n"
clean_line = line[:-1]  # "Hello World"

# Better approach using strip method
clean_line = line.rstrip()  # Handles missing newlines gracefully
```

### String Conversion Tools

#### Type Conversion
```python
# String to number
>>> int('62')
62
>>> float('1.5')
1.5

# Number to string
>>> str(62)
'62'

# Mixed operations require conversion
>>> S = '62'
>>> I = 1
>>> int(S) + I      # Addition: 63
63
>>> S + str(I)      # Concatenation: '621'
'621'

# Using eval (less safe, more powerful)
>>> eval('2 + 3')
5
```

#### Character Code Conversions
```python
# Character to ASCII code
>>> ord('h')
104
>>> ord('A')
65

# ASCII code to character
>>> chr(104)
'h'
>>> chr(65)
'A'

# Process all characters in string
>>> for c in 'hack':
...     print(c, ord(c))
h 104
a 97
c 99
k 107

# Character arithmetic
>>> S = '5'
>>> S = chr(ord(S) + 1)
>>> S
'6'
```

#### String Comparisons
Strings compare lexicographically (by character codes):

```python
>>> 'hack' == 'hack'
True
>>> 'hact' > 'hack'    # 't' > 'k'
True  
>>> 'hacker' > 'hack'  # Longer string wins when prefixes equal
True
```

### Modifying Strings (Creating New Ones)

Since strings are immutable, "changes" create new strings:

```python
# Concatenation approach
>>> S = 'text'
>>> S = S + 'ual!'
>>> S
'textual!'

# Slicing and concatenation
>>> S = 'text'
>>> S = S[:4] + ' processing' + S[-1:]
>>> S
'text processing!'

# Using methods (covered next)
>>> S = 'text'
>>> S = S.replace('ex', 'hough')
>>> S
'thought'
```

---

## String Methods

### Method Call Syntax

**Format:** `object.method(arguments)`

```python
>>> S = 'hack'
>>> result = S.find('ac')  # Find substring, returns position
>>> result
1
```

### All String Methods (Python 3.12)

#### Case Conversion Methods
```python
>>> S = 'Hello World'
>>> S.upper()
'HELLO WORLD'
>>> S.lower()
'hello world'
>>> S.capitalize()
'Hello world'
>>> S.title()
'Hello World'
>>> S.swapcase()
'hELLO wORLD'
>>> S.casefold()  # Aggressive lowercase for comparisons
'hello world'
```

#### Search and Replace Methods
```python
>>> S = 'hello world hello'
>>> S.find('llo')      # First occurrence
2
>>> S.rfind('llo')     # Last occurrence
14
>>> S.index('llo')     # Like find, but raises error if not found
2
>>> S.count('l')       # Count occurrences
6
>>> S.replace('hello', 'hi')
'hi world hi'
>>> S.replace('l', 'L', 2)  # Replace only first 2 occurrences
'heLLo world hello'
```

#### Content Testing Methods
```python
>>> '123'.isdigit()
True
>>> 'abc'.isalpha()
True
>>> 'abc123'.isalnum()
True
>>> 'Hello World'.istitle()
True
>>> 'HELLO'.isupper()
True
>>> 'hello'.islower()
True
>>> '   '.isspace()
True
>>> 'hello123'.isascii()
True
>>> 'hello_world'.isidentifier()  # Valid Python identifier?
True
```

#### Whitespace and Formatting Methods
```python
>>> S = '   hello world   \n'
>>> S.strip()          # Remove whitespace from both ends
'hello world'
>>> S.lstrip()         # Remove from left
'hello world   \n'
>>> S.rstrip()         # Remove from right
'   hello world'
>>> S.strip('h ')      # Remove specific characters
'ello world'

# Justification and padding
>>> 'hello'.center(10)
'  hello   '
>>> 'hello'.ljust(10, '-')
'hello-----'
>>> 'hello'.rjust(10, '0')
'00000hello'
>>> '42'.zfill(5)      # Zero-fill for numbers
'00042'
```

#### Splitting and Joining Methods
```python
# Splitting strings
>>> 'one two three'.split()     # Split on whitespace
['one', 'two', 'three']
>>> 'one,two,three'.split(',')  # Split on delimiter
['one', 'two', 'three']
>>> 'one-two-three'.split('-', 1)  # Limit splits
['one', 'two-three']

# Splitting lines
>>> 'line1\nline2\nline3'.splitlines()
['line1', 'line2', 'line3']

# Joining strings
>>> ' '.join(['one', 'two', 'three'])
'one two three'
>>> ','.join(['a', 'b', 'c'])
'a,b,c'
>>> ''.join(['h', 'e', 'l', 'l', 'o'])  # Rejoin characters
'hello'
```

#### Start/End Testing Methods
```python
>>> 'hello.py'.startswith('hello')
True
>>> 'hello.py'.endswith('.py')
True
>>> 'hello.py'.endswith(('.py', '.pyx'))  # Multiple options
True
```

#### Prefix/Suffix Removal (Python 3.9+)
```python
>>> 'hello_world'.removeprefix('hello_')
'world'
>>> 'hello.py'.removesuffix('.py')
'hello'
```

### Advanced String Processing

#### Converting Between Mutable and Immutable
```python
# Convert string to list for multiple modifications
>>> S = 'text'
>>> L = list(S)
>>> L
['t', 'e', 'x', 't']
>>> L[0] = 'h'
>>> L[3] = '!'
>>> L
['h', 'e', 'x', '!']
>>> S = ''.join(L)  # Convert back to string
>>> S
'hex!'
```

#### Text Parsing Examples

**Fixed-Position Parsing:**
```python
>>> line = 'aaa bbb ccc'
>>> col1 = line[:3]      # 'aaa'
>>> col2 = line[4:8]     # 'bbb '
>>> col3 = line[-3:]     # 'ccc'
```

**Delimiter-Based Parsing:**
```python
>>> line = 'aaa bbb ccc'
>>> cols = line.split()
>>> cols
['aaa', 'bbb', 'ccc']

>>> line = 'Python,3.12,scripting,33'
>>> data = line.split(',')
>>> data
['Python', '3.12', 'scripting', '33']

>>> line = 'youPYarePYaPYstringPYcoder'
>>> parts = line.split('PY')
>>> parts
['you', 'are', 'a', 'string', 'coder']
```

#### Complete Method Example
```python
>>> line = "Python's strings are awesome!\n"
>>> line.rstrip()                    # Remove trailing whitespace
"Python's strings are awesome!"
>>> line.upper()                     # Convert to uppercase
"PYTHON'S STRINGS ARE AWESOME!\n"
>>> line.isalpha()                   # Test if all alphabetic
False
>>> line.endswith('awesome!\n')      # Test suffix
True
>>> line.startswith('Python')        # Test prefix
True

# Alternative approaches
>>> line.find('awesome') != -1       # Search method
True
>>> 'awesome' in line                # Membership operator
True
>>> sub = 'awesome!\n'
>>> line.endswith(sub)               # Method approach
True
>>> line[-len(sub):] == sub          # Slicing approach
True
```

---

## String Formatting

Python has **three** major string formatting approaches:

1. **Formatting Expression** (`%` operator) - Original
2. **Formatting Method** (`.format()`) - Python 3.0+
3. **F-String Literal** (`f''`) - Python 3.6+

### 1. Formatting Expression (`%` operator)

#### Basic Syntax
```python
# Single value
>>> 'Hello %s!' % 'world'
'Hello world!'

# Multiple values (requires tuple)
>>> 'There are %d ways to %s!' % (3, 'format')
'There are 3 ways to format!'

# Variable usage
>>> option = 'expression'
>>> 'Meet the formatting %s!' % option
'Meet the formatting expression!'
```

#### Type Codes

| Code | Meaning | Example |
|------|---------|---------|
| `%s` | String (any object) | `'%s' % 42` → `'42'` |
| `%d` | Decimal integer | `'%d' % 42.8` → `'42'` |
| `%i` | Integer (same as d) | `'%i' % 42` → `'42'` |
| `%o` | Octal | `'%o' % 8` → `'10'` |
| `%x` | Hex (lowercase) | `'%x' % 255` → `'ff'` |
| `%X` | Hex (uppercase) | `'%X' % 255` → `'FF'` |
| `%e` | Exponential (lowercase) | `'%e' % 1000` → `'1.000000e+03'` |
| `%E` | Exponential (uppercase) | `'%E' % 1000` → `'1.000000E+03'` |
| `%f` | Floating point | `'%f' % 1.23` → `'1.230000'` |
| `%g` | General format | `'%g' % 1.23` → `'1.23'` |
| `%%` | Literal % | `'100%%' % ()` → `'100%'` |

#### Advanced Formatting
```python
# Field width and precision
>>> x = 1234
>>> 'integers: ...%d...%-6d...%06d' % (x, x, x)
'integers: ...1234...1234 ...001234'

# Floating point formatting
>>> x = 1.23456789
>>> '%e | %f | %g' % (x, x, x)
'1.234568e+00 | 1.234568 | 1.23457'
>>> '%-6.2f | %05.2f | %+06.1f' % (x, x, x)
'1.23   | 01.23 | +001.2'

# Dynamic width and precision
>>> '%f, %.2f, %.*f' % (1/3.0, 1/3.0, 4, 1/3.0)
'0.333333, 0.33, 0.3333'
```

#### Dictionary-Based Formatting
```python
>>> '%(qty)s more %(tool)s' % {'qty': 1, 'tool': 'formatter'}
'1 more formatter'

# Template usage
>>> reply = """
... Hello %(name)s!
... Welcome to %(year)s
... """
>>> values = {'name': 'Pat', 'year': 2024}
>>> print(reply % values)

Hello Pat!
Welcome to 2024

# Using vars() function
>>> name = 'Pat'
>>> year = 2024
>>> '%(name)s from %(year)s' % vars()
'Pat from 2024'
```

### 2. Formatting Method (`.format()`)

#### Basic Syntax
```python
# Positional (automatic)
>>> '{}, {}, and {}'.format('expr', 'method', 'fstring')
'expr, method, and fstring'

# Positional (explicit)
>>> '{0}, {1}, and {2}'.format('expr', 'method', 'fstring')
'expr, method, and fstring'

# Keyword arguments
>>> '{first}, {second}, and {third}'.format(first='expr', second='method', third='fstring')
'expr, method, and fstring'

# Mixed
>>> '{first}, {0}, and {third}'.format('method', first='expr', third='fstring')
'expr, method, and fstring'
```

#### Accessing Attributes and Items
```python
import sys
>>> 'This {1[kind]} runs {0.platform}'.format(sys, {'kind': 'laptop'})
'This laptop runs darwin'

>>> somelist = ['H', 'A', 'C', 'K']
>>> 'zero={0[0]}, two={0[2]}'.format(somelist)
'zero=H, two=C'
```

#### Advanced Formatting Options
```python
# Field width and alignment
>>> '{0:10} = {1:10}'.format('text', 123.4567)
'text       =   123.4567'
>>> '{0:>10} = {1:<10}'.format('text', 123.4567)
'      text = 123.4567  '
>>> '{0:^10}'.format('text')  # Center alignment
'   text   '

# Number formatting
>>> '{:e}, {:.3e}, {:g}'.format(3.14159, 3.14159, 3.14159)
'3.141590e+00, 3.142e+00, 3.14159'
>>> '{:f}, {:.2f}, {:06.2f}'.format(3.14159, 3.14159, 3.14159)
'3.141590, 3.14, 003.14'

# Different number bases
>>> '{:X}, {:o}, {:b}'.format(255, 255, 255)
'FF, 377, 11111111'

# Thousands separators
>>> '{:,.2f}'.format(12345.678)
'12,345.68'
>>> '{:_}'.format(1234567)
'1_234_567'
```

#### Dynamic Formatting
```python
# Dynamic width and precision
>>> '{:.4f}'.format(1/3.0)
'0.3333'
>>> '{0:.{1}f}'.format(1/3.0, 4)
'0.3333'

# All dynamic components
>>> '{0:{1}{2}{3}{4}{5}.{6}{7}}'.format(1234.564, '0', '<', '+', '12', ',', '2', 'f')
'+1,234.56000'
```

### 3. F-String Formatting Literal

#### Basic Syntax
```python
>>> what = 'coding'
>>> tool = 'Python'
>>> f'Learning {what} in {tool}'
'Learning coding in Python'

# Expressions inside braces
>>> f'Learning {what.upper() + "!"} in {tool + str(3.12)}'
'Learning CODING! in Python3.12'
```

#### Advanced F-String Features
```python
# Number formatting
>>> a = 3.14156
>>> b = 1_234_567
>>> f'{a:.2f} and {b:09}'
'3.14 and 001234567'
>>> f'{a * 1000:,.2f} and {b:,} and {b:_}'
'3,141.56 and 1,234,567 and 1_234_567'

# Different bases
>>> f'{b:_X} and {b:_o} and {b // 64:_b}'
'12_D687 and 455_3207 and 100_1011_0101_1010'

# Debug format (Python 3.8+)
>>> f'{a=:.2f} and {b=:,}'
'a=3.14 and b=1,234,567'
```

#### String Format Flags
```python
>>> c = 'h\xc4ck'  # Contains non-ASCII character
>>> f'{c!s} and {c!r} and {c!a}'
"hÄck and 'hÄck' and 'h\\xc4ck'"
```

#### Dynamic Formatting with F-Strings
```python
>>> width = 8
>>> f'{a:.{width}f} and {c:0>{width}}'
'3.14156000 and 0000hÄck'

# Nested expressions
>>> f'{a=:.{width}f} and {c * 2:0>{width * 3}}'
'a=3.14156000 and 0000000000000000hÄckhÄck'
```

#### F-String Considerations
```python
# Template usage requires variables in scope
>>> values = {'tool': 'Python', 'role': 'scripting'}
>>> f'Use {values["tool"]} for {values["role"]}.'
'Use Python for scripting.'

# Better approach: extract to variables
>>> tool = values['tool']
>>> role = values['role']
>>> f'Use {tool} for {role}.'
'Use Python for scripting.'

# External templates need eval() (security risk)
>>> template = "f'Use {tool} for {role}.'"
>>> eval(template)
'Use Python for scripting.'
```

### Comparison Summary

| Feature | Expression (`%`) | Method (`.format()`) | F-String (`f''`) |
|---------|------------------|---------------------|------------------|
| **Syntax** | `'%s %d' % (str, num)` | `'{} {}'.format(str, num)` | `f'{str} {num}'` |
| **Readability** | Compact | Explicit | Most readable |
| **Performance** | Fastest | Slower | Fast |
| **Templates** | Dictionary support | Argument support | Variables only |
| **Expressions** | Limited | Limited | Full Python |
| **Since** | Python 1.0 | Python 3.0 | Python 3.6 |

---

## General Type Categories

### Python Type Categories

Python organizes types into major categories that share operations:

#### 1. Numbers
- **Types:** `int`, `float`, `complex`, `decimal.Decimal`, `fractions.Fraction`
- **Operations:** `+`, `-`, `*`, `/`, `//`, `%`, `**`
- **Immutable:** Cannot change in place

#### 2. Sequences  
- **Types:** `str`, `list`, `tuple`, `bytes`, `bytearray`
- **Operations:** indexing (`[i]`), slicing (`[i:j]`), concatenation (`+`), repetition (`*`), `len()`, `in`
- **Ordered:** Have positional order (left-to-right)

#### 3. Mappings
- **Types:** `dict`, `collections.OrderedDict`, etc.
- **Operations:** key indexing (`[key]`), `len()`, `in`
- **Key-based:** Access by key, not position

### Mutability Classification

#### Immutable Types
**Cannot be changed in place:**
- Numbers (`int`, `float`, `complex`)
- Strings (`str`)
- Tuples (`tuple`)
- Frozen sets (`frozenset`)
- Bytes (`bytes`)

```python
>>> s = 'hello'
>>> s[0] = 'H'  # Error! Strings are immutable
TypeError: 'str' object does not support item assignment
```

#### Mutable Types
**Can be changed in place:**
- Lists (`list`)
- Dictionaries (`dict`)
- Sets (`set`)
- Byte arrays (`bytearray`)

```python
>>> L = [1, 2, 3]
>>> L[0] = 'changed'  # OK! Lists are mutable
>>> L
['changed', 2, 3]
```

### Shared Operations by Category

#### Sequence Operations (work on all sequences)
```python
# These work the same on strings, lists, tuples:
>>> 'abc' + 'def'           # String concatenation
'abcdef'
>>> [1, 2] + [3, 4]         # List concatenation  
[1, 2, 3, 4]
>>> (1, 2) + (3, 4)         # Tuple concatenation
(1, 2, 3, 4)

>>> 'hi' * 3               # String repetition
'hihihi'
>>> [1, 2] * 3             # List repetition
[1, 2, 1, 2, 1, 2]

>>> len('abc')             # Length
3
>>> len([1, 2, 3])
3
```

---

## Quiz and Answers

### Quiz Questions

1. **Can the string find method be used to search a list?**

2. **Can a string slice expression be used on a list?**

3. **How would you convert a character to its ASCII integer code? How would you convert the other way, from an integer code to a character?**

4. **How might you go about changing a string in Python?**

5. **Given a string S with the value `'c,od,e'`, name two ways to extract the two characters in the middle.**

6. **How many characters are there in the string `"a\nb\x1f\000d"`?**

7. **Write an expression, method call, and f-string to format 'Python' and 3.12 at a string's beginning and end.**

### Quiz Answers

1. **String find method on lists:**
   
   **No**, because methods are type-specific and only work on their designated object type. The `find()` method only works on strings.
   
   ```python
   >>> 'hello'.find('ll')    # Works - returns 2
   2
   >>> [1, 2, 3].find(2)     # Error!
   AttributeError: 'list' object has no attribute 'find'
   
   # However, the 'in' operator works on both:
   >>> 'll' in 'hello'       # String membership
   True
   >>> 2 in [1, 2, 3]        # List membership
   True
   ```

2. **String slice expression on lists:**
   
   **Yes!** Unlike methods, expressions are generic and work across multiple types. Slicing is a sequence operation that works on any sequence type.
   
   ```python
   >>> 'hello'[1:4]          # String slicing
   'ell'
   >>> [1, 2, 3, 4, 5][1:4]  # List slicing
   [2, 3, 4]
   >>> (1, 2, 3, 4, 5)[1:4]  # Tuple slicing
   (2, 3, 4)
   ```
   
   The only difference is the type of object returned - slicing a list returns a new list, slicing a string returns a new string.

3. **Character/ASCII code conversion:**
   
   Use `ord()` to convert character to integer code, and `chr()` to convert integer code to character:
   
   ```python
   # Character to ASCII code
   >>> ord('A')
   65
   >>> ord('a')
   97
   >>> ord('5')
   53
   
   # ASCII code to character
   >>> chr(65)
   'A'
   >>> chr(97)
   'a'
   >>> chr(53)
   '5'
   
   # Practical example - character arithmetic
   >>> char = 'A'
   >>> next_char = chr(ord(char) + 1)
   >>> next_char
   'B'
   
   # Process string characters
   >>> word = 'Hello'
   >>> for char in word:
   ...     print(f"'{char}' = {ord(char)}")
   'H' = 72
   'e' = 101
   'l' = 108
   'l' = 108
   'o' = 111
   ```
   
   **Note:** These are Unicode code points, which include ASCII as a subset for basic characters.

4. **Changing strings in Python:**
   
   Strings are **immutable**, so you can't change them directly. Instead, create a new string and assign it back:
   
   ```python
   # Method 1: Concatenation
   >>> S = 'Hello'
   >>> S = S + ' World'  # Creates new string
   >>> S
   'Hello World'
   
   # Method 2: Slicing and concatenation
   >>> S = 'Hello World'
   >>> S = S[:6] + 'Python'  # Replace 'World' with 'Python'
   >>> S
   'Hello Python'
   
   # Method 3: String methods
   >>> S = 'Hello World'
   >>> S = S.replace('World', 'Python')
   >>> S
   'Hello Python'
   
   # Method 4: String formatting
   >>> template = 'Hello {}'
   >>> S = template.format('Python')
   >>> S
   'Hello Python'
   
   # Method 5: F-strings
   >>> name = 'Python'
   >>> S = f'Hello {name}'
   >>> S
   'Hello Python'
   
   # For many changes, convert to list, modify, then join back
   >>> S = 'Hello'
   >>> L = list(S)           # ['H', 'e', 'l', 'l', 'o']
   >>> L[0] = 'h'            # Modify in place
   >>> L.append('!')
   >>> S = ''.join(L)        # Convert back to string
   >>> S
   'hello!'
   ```

5. **Extract middle characters from `'c,od,e'`:**
   
   The middle characters are 'od' (positions 2 and 3). Two approaches:
   
   ```python
   >>> S = 'c,od,e'
   
   # Method 1: Slicing
   >>> S[2:4]
   'od'
   
   # Method 2: Split and index
   >>> S.split(',')[1]
   'od'
   
   # Verification - let's see the string breakdown:
   >>> S = 'c,od,e'
   >>> for i, char in enumerate(S):
   ...     print(f"Index {i}: '{char}'")
   Index 0: 'c'
   Index 1: ','
   Index 2: 'o'
   Index 3: 'd'
   Index 4: ','
   Index 5: 'e'
   
   # Split breakdown:
   >>> S.split(',')
   ['c', 'od', 'e']  # Index 1 gives us 'od'
   ```

6. **Character count in `"a\nb\x1f\000d"`:**
   
   **Six characters total.** Let's break it down:
   
   ```python
   >>> S = "a\nb\x1f\000d"
   >>> len(S)
   6
   
   # Character breakdown:
   >>> for i, char in enumerate(S):
   ...     print(f"Index {i}: {repr(char)} (ord: {ord(char)})")
   Index 0: 'a' (ord: 97)
   Index 1: '\n' (ord: 10)     # Newline character
   Index 2: 'b' (ord: 98)
   Index 3: '\x1f' (ord: 31)   # Hex escape - control character
   Index 4: '\x00' (ord: 0)    # Octal escape - null character
   Index 5: 'd' (ord: 100)
   
   # Visual representation:
   >>> print(repr(S))
   'a\nb\x1f\x00d'
   
   # What it looks like when printed (non-printables may not show):
   >>> print(S)
   a
   bd
   ```
   
   The string contains: `a`, newline, `b`, hex character 1F (unit separator), null character, `d`.

7. **Format 'Python' and 3.12 at beginning and end:**
   
   ```python
   # Method 1: Formatting Expression (%)
   >>> '%s version %g' % ('Python', 3.12)
   'Python version 3.12'
   >>> 'Language: %s, Version: %.2f' % ('Python', 3.12)
   'Language: Python, Version: 3.12'
   
   # Method 2: Format Method (.format())
   >>> '{} version {}'.format('Python', 3.12)
   'Python version 3.12'
   >>> 'Language: {0}, Version: {1:.2f}'.format('Python', 3.12)
   'Language: Python, Version: 3.12'
   >>> 'Language: {lang}, Version: {ver:.2f}'.format(lang='Python', ver=3.12)
   'Language: Python, Version: 3.12'
   
   # Method 3: F-String Literal (f'')
   >>> lang = 'Python'
   >>> version = 3.12
   >>> f'{lang} version {version}'
   'Python version 3.12'
   >>> f'Language: {lang}, Version: {version:.2f}'
   'Language: Python, Version: 3.12'
   
   # More complex formatting examples:
   >>> f'{lang:>10} v{version:<6.2f}'  # Right-align lang, left-align version
   '    Python v3.12  '
   >>> f'{lang.upper()}: {version:.1f}'  # Method call in f-string
   'PYTHON: 3.1'
   ```

---

## Additional Practice Exercises

### Exercise 1: String Manipulation
```python
# Given this string, perform various operations:
text = "  Python Programming is Fun!  "

# 1. Remove whitespace
clean_text = text.strip()
print(f"Cleaned: '{clean_text}'")

# 2. Convert to different cases
print(f"Upper: {clean_text.upper()}")
print(f"Lower: {clean_text.lower()}")
print(f"Title: {clean_text.title()}")

# 3. Replace words
modified = clean_text.replace("Fun", "Awesome")
print(f"Modified: {modified}")

# 4. Split into words
words = clean_text.split()
print(f"Words: {words}")
print(f"Word count: {len(words)}")

# 5. Extract specific parts
language = clean_text.split()[0]  # First word
activity = clean_text.split()[1]  # Second word
print(f"Language: {language}, Activity: {activity}")
```

### Exercise 2: String Analysis
```python
def analyze_string(s):
    """Comprehensive string analysis"""
    print(f"Analyzing: '{s}'")
    print(f"Length: {len(s)}")
    print(f"Character breakdown:")
    
    for i, char in enumerate(s):
        print(f"  {i:2d}: '{char}' (ord: {ord(char):3d}) {get_char_type(char)}")
    
    print(f"Uppercase count: {sum(1 for c in s if c.isupper())}")
    print(f"Lowercase count: {sum(1 for c in s if c.islower())}")
    print(f"Digit count: {sum(1 for c in s if c.isdigit())}")
    print(f"Space count: {sum(1 for c in s if c.isspace())}")
    print()

def get_char_type(char):
    """Return character type description"""
    if char.isalpha():
        return "letter"
    elif char.isdigit():
        return "digit"
    elif char.isspace():
        return "whitespace"
    else:
        return "other"

# Test the analyzer
analyze_string("Hello World 123!")
analyze_string("Python\n3.12\t")
```

### Exercise 3: Format Practice
```python
# Data to format
products = [
    ("Python Book", 29.99, 5),
    ("Java Guide", 34.50, 2), 
    ("C++ Manual", 39.95, 8)
]

print("Product Inventory Report")
print("=" * 50)

# Using different formatting methods
for i, (name, price, qty) in enumerate(products, 1):
    # Method 1: % formatting
    line1 = "%d. %-15s $%6.2f (Qty: %2d)" % (i, name, price, qty)
    
    # Method 2: .format() method
    line2 = "{}. {:15s} ${:6.2f} (Qty: {:2d})".format(i, name, price, qty)
    
    # Method 3: f-string
    line3 = f"{i}. {name:15s} ${price:6.2f} (Qty: {qty:2d})"
    
    print("% method:", line1)
    print(".format(): ", line2)
    print("f-string:  ", line3)
    print()

# Calculate totals using f-strings
total_value = sum(price * qty for name, price, qty in products)
total_items = sum(qty for name, price, qty in products)

print(f"Summary:")
print(f"Total Items: {total_items:,}")
print(f"Total Value: ${total_value:,.2f}")
```

### Exercise 4: Text Processing Pipeline
```python
def process_text(text):
    """Complete text processing pipeline"""
    print(f"Original: '{text}'")
    
    # Step 1: Clean whitespace
    cleaned = text.strip()
    print(f"Cleaned: '{cleaned}'")
    
    # Step 2: Normalize case
    normalized = cleaned.lower()
    print(f"Normalized: '{normalized}'")
    
    # Step 3: Replace problematic characters
    processed = normalized.replace(',', ' ').replace('.', ' ').replace('!', '')
    print(f"Processed: '{processed}'")
    
    # Step 4: Split into words
    words = processed.split()
    print(f"Words: {words}")
    
    # Step 5: Filter and analyze
    long_words = [word for word in words if len(word) > 4]
    print(f"Long words (>4 chars): {long_words}")
    
    # Step 6: Reconstruct
    result = ' '.join(words)
    print(f"Final result: '{result}'")
    
    return result

# Test the pipeline
sample_text = "  Hello, World! Python Programming is Amazing.  "
processed = process_text(sample_text)
```

### Exercise 5: Advanced Slicing Practice
```python
def demonstrate_slicing():
    """Comprehensive slicing examples"""
    text = "Python Programming"
    print(f"Working with: '{text}' (length: {len(text)})")
    print()
    
    # Basic slicing
    print("Basic Slicing:")
    print(f"text[0:6]     = '{text[0:6]}'     # First 6 characters")
    print(f"text[7:]      = '{text[7:]}'      # From position 7 to end")
    print(f"text[:6]      = '{text[:6]}'      # Start to position 6")
    print(f"text[-11:]    = '{text[-11:]}'    # Last 11 characters")
    print(f"text[:-11]    = '{text[:-11]}'    # All but last 11")
    print()
    
    # Step slicing
    print("Step Slicing:")
    print(f"text[::2]     = '{text[::2]}'     # Every other character")
    print(f"text[1::2]    = '{text[1::2]}'    # Every other, starting at 1")
    print(f"text[::-1]    = '{text[::-1]}'    # Reverse entire string")
    print(f"text[::-2]    = '{text[::-2]}'    # Reverse, every other")
    print()
    
    # Complex slicing
    print("Complex Slicing:")
    print(f"text[7::-1]   = '{text[7::-1]}'   # From pos 7 to start, reversed")
    print(f"text[:-8:-1]  = '{text[:-8:-1]}'  # Last 7 chars, reversed")
    print(f"text[6:12:2]  = '{text[6:12:2]}'  # Positions 6-11, every other")
    print()

demonstrate_slicing()
```

---

## Key Takeaways

### Essential Concepts

1. **Strings are immutable sequences** - cannot be changed in place, but you can create new strings
2. **Multiple literal forms** - single/double quotes, triple quotes, raw strings, escape sequences
3. **Rich operation set** - indexing, slicing, concatenation, repetition, membership testing
4. **Comprehensive method library** - 40+ methods for searching, replacing, formatting, testing
5. **Three formatting approaches** - expression (`%`), method (`.format()`), and f-strings (`f''`)
6. **Type categories matter** - sequences share operations, immutable vs mutable affects usage

### Best Practices

1. **Use f-strings for new code** - most readable and performant for inline formatting
2. **Choose quote style consistently** - prefer single quotes unless embedding single quotes
3. **Use raw strings for paths/regex** - avoid escape sequence issues
4. **Leverage string methods** - more readable than manual character processing
5. **Remember immutability** - assign results of string operations to variables
6. **Use appropriate formatting** - match the tool to the use case

### Common Pitfalls

1. **Forgetting tuple for multiple % values** - `'%s %s' % (a, b)` not `'%s %s' % a, b`
2. **Modifying strings in place** - remember to assign results back
3. **Confusing slice bounds** - end index is exclusive
4. **Raw string limitations** - cannot end with single backslash
5. **F-string scope issues** - variables must be in scope where f-string is evaluated

This comprehensive guide covers all the essential aspects of Python strings from basic literals to advanced formatting techniques. Practice with the provided exercises to reinforce your understanding!
