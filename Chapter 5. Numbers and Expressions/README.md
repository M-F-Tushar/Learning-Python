# Chapter 5: Numbers and Expressions - Complete Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Numeric Object Basics](#numeric-object-basics)
3. [Numeric Literals](#numeric-literals)
4. [Built-in Numeric Tools](#built-in-numeric-tools)
5. [Python Expression Operators](#python-expression-operators)
6. [Numbers in Action](#numbers-in-action)
7. [Comparison Operators](#comparison-operators)
8. [Division Operators](#division-operators)
9. [Integer Precision](#integer-precision)
10. [Complex Numbers](#complex-numbers)
11. [Hex, Octal, and Binary](#hex-octal-and-binary)
12. [Bitwise Operations](#bitwise-operations)
13. [Underscore Separators](#underscore-separators)
14. [Other Built-in Numeric Tools](#other-built-in-numeric-tools)
15. [Other Numeric Objects](#other-numeric-objects)
16. [Quiz and Answers](#quiz-and-answers)

---

## Introduction

This chapter explores Python's numeric objects and operations. In Python, data takes the form of objects—either built-in objects that Python provides or objects we create using Python tools. Objects are the most fundamental notion in Python programming.

Numbers in Python are not a single object type, but a category of similar types that can be used to keep track of bank balances, distances, visitor counts, and any other numeric quantity.

---

## Numeric Object Basics

Python's numeric toolbox includes:

### Core Numeric Types
- **Integer and floating-point objects** - Basic whole and fractional numbers
- **Complex number objects** - For engineering and scientific applications
- **Decimal fixed-precision objects** - For exact decimal arithmetic
- **Fraction rational number objects** - For exact fractional arithmetic

### Additional Tools
- **Set objects and operations** - Mathematical set operations
- **Boolean and bitwise operations** - True/False values and bit manipulation
- **Built-in modules** - `math`, `cmath`, `random`, `statistics`
- **Third-party add-ons** - NumPy, SciPy, matplotlib, etc.

---

## Numeric Literals

### Table of Numeric Literals and Constructors

| Literal | Interpretation |
|---------|----------------|
| `1234`, `−24`, `0`, `9_999_999_999_999` | Integers (unlimited size) |
| `1.23`, `1.`, `3.14e-10`, `4E210`, `4.0e+210` | Floating-point numbers |
| `0o177`, `0x9ff`, `0b101010` | Octal, hex, and binary literals |
| `3+4j`, `3.0+4.0j`, `3J` | Complex number literals |
| `set('hack')`, `{1, 2, 3, 4}` | Sets: constructors and literals |
| `Decimal('1.0')`, `Fraction(1, 3)` | Decimal and fraction extension types |
| `bool(X)`, `True`, `False` | Boolean type and constants |

### Key Concepts

#### Integer and Floating-Point Literals
```python
# Integers - unlimited precision
>>> 999999999999999999999999999999
999999999999999999999999999999

# Floating-point with decimal point or exponent
>>> 3.14
3.14
>>> 4E210
4e+210
>>> 1.23e-10
1.23e-10
```

#### Hexadecimal, Octal, and Binary Literals
```python
# Hexadecimal (base 16) - starts with 0x or 0X
>>> 0xFF
255
>>> 0x9ff
2559

# Octal (base 8) - starts with 0o or 0O
>>> 0o177
127
>>> 0O20
16

# Binary (base 2) - starts with 0b or 0B
>>> 0b101010
42
>>> 0B1111
15
```

#### Conversion Functions
```python
# Convert integer to different base representations
>>> hex(255)
'0xff'
>>> oct(255)
'0o377'
>>> bin(255)
'0b11111111'

# Convert string representations back to integers
>>> int('255')
255
>>> int('ff', 16)  # Hex to decimal
255
>>> int('377', 8)  # Octal to decimal
255
>>> int('11111111', 2)  # Binary to decimal
255
```

#### Complex Numbers
```python
# Complex numbers with j or J suffix
>>> 3+4j
(3+4j)
>>> 1j * 1J
(-1+0j)
>>> (2+1j) * 3
(6+3j)

# Access real and imaginary parts
>>> c = 3+4j
>>> c.real
3.0
>>> c.imag
4.0
```

---

## Built-in Numeric Tools

Python provides several categories of tools for processing numbers:

### Expression Operators
- Arithmetic: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- Bitwise: `<<`, `>>`, `&`, `|`, `^`, `~`
- Comparison: `<`, `<=`, `>`, `>=`, `==`, `!=`

### Built-in Mathematical Functions
- `pow(x, y)` - Power function
- `abs(x)` - Absolute value
- `round(x, n)` - Round to n decimal places
- `int(x)` - Convert to integer
- `float(x)` - Convert to float
- `hex(x)`, `oct(x)`, `bin(x)` - Base conversions

### Utility Modules
- `math` - Mathematical functions
- `random` - Random number generation
- `statistics` - Statistical functions

---

## Python Expression Operators

### Operator Precedence Table (Highest to Lowest)

| Operators | Description |
|-----------|-------------|
| `x[i]`, `x[i:j:k]`, `x(...)`, `x.attr` | Indexing, slicing, calls, attributes |
| `**` | Exponentiation |
| `+x`, `-x`, `~x` | Unary plus, minus, bitwise NOT |
| `*`, `/`, `//`, `%`, `@` | Multiplication, division, floor division, modulus, matrix multiplication |
| `+`, `-` | Addition, subtraction |
| `<<`, `>>` | Bit shifts |
| `&` | Bitwise AND |
| `^` | Bitwise XOR |
| `\|` | Bitwise OR |
| `<`, `<=`, `>`, `>=`, `!=`, `==`, `is`, `is not`, `in`, `not in` | Comparisons, identity, membership |
| `not` | Boolean NOT |
| `and` | Boolean AND |
| `or` | Boolean OR |
| `x if y else z` | Conditional expression |
| `lambda` | Lambda expression |
| `x := y` | Assignment expression |

### Mixed Operators and Precedence

```python
# Without parentheses - multiplication first
>>> 2 + 3 * 4
14

# With parentheses - addition first
>>> (2 + 3) * 4
20

# Multiple operations
>>> 2 * 3 + 4 * 5
26  # Same as (2 * 3) + (4 * 5)
```

### Mixed Types Are Converted Up

Python automatically converts operands to the most complex type:
- Integers → Floating-point → Complex

```python
# Integer + Float = Float
>>> 40 + 3.14
43.14

# Manual conversion
>>> int(3.1415)  # Truncates
3
>>> float(3)
3.0

# Equality works across types
>>> 3 == 3.0
True
```

---

## Numbers in Action

### Variables and Basic Expressions

Variables in Python:
- Created when first assigned values
- Replaced with their values in expressions
- Must be assigned before use
- Refer to objects, no declaration needed

```python
# Create variables
>>> a = 3
>>> b = 4

# Basic arithmetic
>>> a + 1, a - 1
(4, 2)
>>> b * 3, b / 2
(12, 2.0)
>>> a % 2, b ** 2  # Modulus, power
(1, 16)

# Mixed-type conversions
>>> 2 + 4.0, 2.0 ** b
(6.0, 16.0)

# Error for undefined variables
>>> c * 2
NameError: name 'c' is not defined
```

### Operator Grouping Examples

```python
# Division has higher precedence than addition
>>> b / 2 + a  # Same as ((4 / 2) + 3)
5.0

# Parentheses force order
>>> b / (2 + a)  # Same as (4 / (2 + 3))
0.8
```

### Numeric Display Formats

```python
# Floating-point precision issues
>>> 1.1 + 2.2
3.3000000000000003

# String formatting for display
>>> num = 1.1 + 2.2
>>> f'{num:.1f}'
'3.3'
>>> '%.1f' % num
'3.3'
```

#### Display Formats: STR and REPR

```python
# repr - code-like representation
>>> repr('hack')
"'hack'"

# str - user-friendly representation
>>> str('hack')
'hack'
```

---

## Comparison Operators

### Basic Comparisons

```python
# Standard comparisons
>>> 1 < 2
True
>>> 2.0 >= 1
True
>>> 2.0 == 2.0
True
>>> 2.0 != 2.0
False
```

### Chained Comparisons

Python allows chaining multiple comparisons:

```python
>>> X = 2
>>> Y = 4
>>> Z = 6

# Chained comparison (shorthand)
>>> X < Y < Z
True

# Equivalent to
>>> X < Y and Y < Z
True

# More examples
>>> 1 < 2 < 3.0 < 4
True
>>> 1 > 2 > 3.0 > 4
False
```

### Floating-Point Equality Issues

```python
# Precision problems
>>> 1.1 + 2.2 == 3.3
False
>>> 1.1 + 2.2
3.3000000000000003

# Solutions for floating-point equality
>>> int(1.1 + 2.2) == int(3.3)
True
>>> round(1.1 + 2.2, 1) == round(3.3, 1)
True

# Using math.isclose (Python 3.5+)
>>> import math
>>> math.isclose(1.1 + 2.2, 3.3)
True
```

---

## Division Operators

Python has three division-related operators:

### True Division (/)
Always keeps remainders in floating-point results:

```python
>>> 10 / 4
2.5
>>> 10 / 4.0
2.5
```

### Floor Division (//)
Truncates fractional remainders down to floor:

```python
>>> 10 // 4
2
>>> 10 // 4.0  # Result type depends on operands
2.0

# Convert to integer if needed
>>> int(10 // 4.0)
2
```

### Modulus (%)
Returns remainder of division:

```python
>>> 10 % 3, 10 % 3.0
(1, 1.0)

# divmod gives both quotient and remainder
>>> divmod(10, 3)
(3, 1)
```

### Floor vs Truncation

Important distinction for negative numbers:

```python
>>> import math

# Floor (rounds down)
>>> math.floor(2.5)
2
>>> math.floor(-2.5)
-3

# Truncation (towards zero)
>>> math.trunc(2.5)
2
>>> math.trunc(-2.5)
-2

# Floor division examples
>>> 5 // 2, 5 // -2
(2, -3)
>>> 5 // 2.0, 5 // -2.0
(2.0, -3.0)

# True truncation if needed
>>> math.trunc(5 / -2)
-2
```

---

## Integer Precision

Python integers support unlimited size:

```python
# Large integers work seamlessly
>>> 999999999999999999999999999999 + 1
1000000000000000000000000000000

# Very large numbers
>>> 2 ** 269
948568795032094272909893509191171341133987714380954
>>> x = 2 ** 1000000  # This would be huge!
```

**Note**: While unlimited precision is convenient, very large integer math is slower than normal due to the extra work required.

---

## Complex Numbers

Complex numbers are represented as two floating-point numbers (real and imaginary parts):

```python
# Creating complex numbers
>>> 1j * 1J
(-1+0j)
>>> 2 + 1j * 3
(2+3j)
>>> (2 + 1j) * 3
(6+3j)

# Accessing parts
>>> c = 3+4j
>>> c.real, c.imag
(3.0, 4.0)

# Complex math with cmath module
>>> import cmath
>>> cmath.sqrt(-1)
1j
```

---

## Hex, Octal, and Binary

### Different Base Representations

All represent the same integer values in memory:

```python
# Same values in different bases
>>> 0x01, 0x10, 0xFF  # Hex
(1, 16, 255)
>>> 0o1, 0o20, 0o377  # Octal
(1, 16, 255)
>>> 0b1, 0b10000, 0b11111111  # Binary
(1, 16, 255)
```

### Understanding Base Conversions

```python
# Hex FF = 15*16¹ + 15*16⁰ = 255
>>> 0xFF, (15 * (16 ** 1)) + (15 * (16 ** 0))
(255, 255)

# Hex 2F = 2*16¹ + 15*16⁰ = 47
>>> 0x2F, (2 * (16 ** 1)) + (15 * (16 ** 0))
(47, 47)
```

### Base Conversion Functions

```python
# Convert to string representations
>>> oct(64), hex(64), bin(64)
('0o100', '0x40', '0b1000000')

# Convert from strings
>>> int('64'), int('100', 8), int('40', 16), int('1000000', 2)
(64, 64, 64, 64)

# With base prefixes
>>> int('0x40', 16), int('0b1000000', 2)
(64, 64)
```

### String Formatting for Bases

```python
# Old-style formatting
>>> '%o, %x, %#X' % (64, 255, 255)
'100, ff, 0XFF'

# New-style formatting
>>> '{:o}, {:b}, {:x}, {:#X}'.format(64, 64, 255, 255)
'100, 1000000, ff, 0XFF'

# f-strings
>>> f'{64:o}, {64:b}, {255:x}, {255:#X}'
'100, 1000000, ff, 0XFF'
```

---

## Bitwise Operations

Bitwise operators treat integers as strings of binary bits:

### Basic Bitwise Operations

```python
>>> x = 1  # Binary: 0001

# Left shift: move bits left
>>> x << 2  # 0001 → 0100
4

# Bitwise OR: either bit set
>>> x | 3  # 0001 | 0011 = 0011
3

# Bitwise AND: both bits set
>>> x & 3  # 0001 & 0011 = 0001
1
```

### Working with Binary Representations

```python
# Using binary literals
>>> X = 0b0001
>>> X << 2
4
>>> bin(X << 2)
'0b100'

# Bitwise operations with binary display
>>> bin(X | 0b0011)  # OR
'0b11'
>>> bin(X & 0b11)    # AND
'0b1'

# XOR operations
>>> X = 0xFF
>>> bin(X ^ 0b10101010)  # XOR
'0b1010101'
```

### Bit Length Method

```python
# Query number of bits needed
>>> X = 99
>>> bin(X), X.bit_length(), len(bin(X)) - 2
('0b1100011', 7, 7)

>>> bin(256), (256).bit_length()
('0b100000000', 9)
```

---

## Underscore Separators

Python 3.6+ allows underscores in numeric literals for readability:

### Basic Usage

```python
# Underscores are ignored in numeric values
>>> 9999999999999 == 9_999_999_999_999
True
>>> 0xFFFFFFFF == 0xFF_FF_FF_FF
True
>>> 0o777777777777 == 0o777_777_777_777
True
>>> 0b1111111111111111 == 0b1111_1111_1111_1111
True

# Works with floats and complex numbers
>>> 3.141592653589793 == 3.141_592_653_589_793
True
>>> 123456789.123456789 == 123_456_789.123_456_789
True
```

### Formatting for Display

```python
# Underscores lost after reading
>>> x = 9_999_998
>>> x
9999998

# Add back for display
>>> f'{x:,} and {x:_}'
'9,999,998 and 9_999_998'
```

### Conversion Functions Support Underscores

```python
# String conversions allow underscores
>>> int('1_234_567')
1234567
>>> float('1_2_34.567_8_90')
1234.56789
```

### Important: Commas vs Underscores

```python
# Underscores are ignored
>>> 12_345_678
12345678

# Commas create tuples!
>>> 12,345,678
(12, 345, 678)
```

---

## Other Built-in Numeric Tools

### Math Module Functions

```python
>>> import math

# Constants
>>> math.pi, math.e
(3.141592653589793, 2.718281828459045)

# Trigonometric functions
>>> math.sin(2 * math.pi / 180)
0.03489949670250097

# Square root and powers
>>> math.sqrt(144), math.sqrt(2)
(12.0, 1.4142135623730951)
>>> pow(2, 4), 2 ** 4
(16, 16)
```

### Built-in Functions

```python
# Absolute value and sum
>>> abs(-62.0), sum((1, 2, 3, 4))
(62.0, 10)

# Min and max
>>> min(3, 1, 2, 4), max(3, 1, 2, 4)
(1, 4)
```

### Rounding and Truncation

```python
# Different ways to handle decimals
>>> math.floor(2.567), math.floor(-2.567)
(2, -3)
>>> math.trunc(2.567), math.trunc(-2.567)
(2, -2)
>>> int(2.567), int(-2.567)
(2, -2)

# Round function
>>> round(2.567), round(2.567, 2), round(2567, -3)
(3, 2.57, 3000)
```

### Square Root Methods

```python
# Three ways to compute square root
>>> import math
>>> math.sqrt(144)  # Module function
12.0
>>> 144 ** .5       # Expression
12.0
>>> pow(144, .5)    # Built-in function
12.0
```

### Statistics and Random Modules

```python
# Statistics module
>>> import statistics
>>> statistics.mean([1, 2, 4, 5, 7])
3.8
>>> statistics.median([1, 2, 4, 5, 7])
4

# Random module
>>> import random
>>> random.random()  # Random float 0-1
0.5566014960423105
>>> random.randint(1, 10)  # Random integer
5
>>> random.choice(['Pizza', 'Tacos', 'Tikka'])
'Tikka'

# Shuffle lists
>>> suits = ['hearts', 'clubs', 'diamonds', 'spades']
>>> random.shuffle(suits)
>>> suits
['spades', 'hearts', 'diamonds', 'clubs']
```

---

## Other Numeric Objects

### Decimal Objects

For fixed-precision floating-point arithmetic:

#### Basic Decimal Usage

```python
# Floating-point precision problems
>>> 0.1 + 0.1 + 0.1 - 0.3
5.551115123125783e-17

# Decimal solution
>>> from decimal import Decimal
>>> Decimal('0.1') + Decimal('0.1') + Decimal('0.1') - Decimal('0.3')
Decimal('0.0')
```

#### Setting Decimal Precision

```python
>>> import decimal

# Default precision
>>> decimal.Decimal(1) / decimal.Decimal(7)
Decimal('0.1428571428571428571428571429')

# Set global precision
>>> decimal.getcontext().prec = 4
>>> decimal.Decimal(1) / decimal.Decimal(7)
Decimal('0.1429')
```

### Fraction Objects

For exact rational number arithmetic:

#### Basic Fraction Usage

```python
>>> from fractions import Fraction

# Create fractions
>>> x = Fraction(1, 3)  # 1/3
>>> y = Fraction(4, 6)  # Automatically simplified to 2/3
>>> x, y
(Fraction(1, 3), Fraction(2, 3))

# Fraction arithmetic
>>> x + y
Fraction(1, 1)
>>> x * y
Fraction(2, 9)
```

#### Fractions from Strings

```python
>>> Fraction('.25')
Fraction(1, 4)
>>> Fraction('1.25')
Fraction(5, 4)
>>> Fraction('.25') + Fraction('1.25')
Fraction(3, 2)
```

#### Numeric Accuracy Comparison

```python
# Floating-point (limited accuracy)
>>> 0.1 + 0.1 + 0.1 - 0.3
5.551115123125783e-17

# Fraction (exact)
>>> Fraction(1, 10) + Fraction(1, 10) + Fraction(1, 10) - Fraction(3, 10)
Fraction(0, 1)

# Decimal (configurable precision)
>>> Decimal('0.1') + Decimal('0.1') + Decimal('0.1') - Decimal('0.3')
Decimal('0.0')
```

### Set Objects

Mathematical sets with unique, immutable objects:

#### Creating Sets

```python
# Two ways to create sets
>>> x = set('abcde')  # From iterable
>>> y = {99, 'b', 'y', 'd', 1.2}  # Literal form
>>> x, y
({'d', 'c', 'e', 'a', 'b'}, {1.2, 99, 'y', 'd', 'b'})

# Empty set requires function call
>>> z = set()  # {} is empty dict, not set
>>> z
set()
```

#### Set Operations

```python
>>> x = set('abcd')
>>> y = set('bdxy')

# Set operations
>>> x - y        # Difference
{'a', 'c'}
>>> x | y        # Union
{'y', 'd', 'x', 'c', 'a', 'b'}
>>> x & y        # Intersection
{'d', 'b'}
>>> x ^ y        # Symmetric difference
{'y', 'x', 'c', 'a'}

# Subset/superset tests
>>> x < y, x > y
(False, False)
```

#### Set Methods

```python
>>> z = x.intersection(y)
>>> z.add('HACK')
>>> z.update(set(['X', 'Y']))
>>> z.remove('b')
>>> z
{'X', 'HACK', 'd', 'Y'}
```

#### Set Comprehensions

```python
# Set comprehension syntax
>>> {x ** 2 for x in [1, 2, 3, 4]}
{16, 1, 4, 9}

>>> {c * 4 for c in 'py3X'}
{'yyyy', '3333', 'XXXX', 'pppp'}
```

#### Practical Set Applications

```python
# Remove duplicates
>>> L = [1, 2, 1, 3, 2, 4, 5]
>>> list(set(L))
[1, 2, 3, 4, 5]

# Find differences
>>> set([1, 3, 5, 7]) - set([1, 2, 4, 5, 6])
{3, 7}

# Order-neutral equality
>>> L1, L2 = [1, 3, 5, 2, 4], [2, 5, 3, 4, 1]
>>> set(L1) == set(L2)
True

# Practical example: company roles
>>> engineers = {'pat', 'ann', 'bob', 'sue'}
>>> managers = {'sue', 'tom'}
>>> engineers & managers  # Who is both?
{'sue'}
>>> engineers | managers  # All people
{'ann', 'sue', 'pat', 'tom', 'bob'}
>>> engineers - managers  # Engineers only
{'pat', 'ann', 'bob'}
```

### Boolean Objects

Python's Boolean type is a subclass of integer:

```python
>>> type(True)
<class 'bool'>
>>> isinstance(True, int)
True

# Booleans behave like integers 1 and 0
>>> True == 1, False == 0
(True, True)
>>> True + 4
5

# But they're different objects
>>> True is 1
False
```

---

## Quiz and Answers

### Test Your Knowledge: Quiz

1. **What is the value of the expression `2 * (3 + 4)` in Python, and why?**

2. **What is the value of the expression `2 * 3 + 4` in Python, and why?**

3. **What is the value of the expression `2 + 3 * 4` in Python, and why?**

4. **What tools can you use to find a number's square root, as well as its square?**

5. **What is the type of the result of the expression `1 + 2.0 + 3`, and why?**

6. **How can you truncate and round a floating-point number?**

7. **How can you convert an integer to a floating-point number?**

8. **How would you display an integer in octal, hexadecimal, or binary notation?**

9. **How might you convert an octal, hexadecimal, or binary string to a plain integer?**

### Test Your Knowledge: Answers

1. **Answer: 14**
   - The parentheses force addition to happen first: `(3 + 4) = 7`
   - Then multiplication: `2 * 7 = 14`

2. **Answer: 10**
   - Operator precedence: multiplication before addition
   - `2 * 3 = 6`, then `6 + 4 = 10`

3. **Answer: 14**
   - Same precedence rules: multiplication first
   - `3 * 4 = 12`, then `2 + 12 = 14`

4. **Square root and square tools:**
   ```python
   import math
   # Square root
   math.sqrt(N)    # Module function
   N ** 0.5        # Exponent expression
   pow(N, 0.5)     # Built-in function
   
   # Square
   N ** 2          # Exponent expression
   pow(N, 2)       # Built-in function
   ```

5. **Answer: Float**
   - Mixed-type expressions convert to most complex type
   - Integer → Float → Complex
   - Result: `6.0` (floating-point)

6. **Truncation and rounding:**
   ```python
   # Truncate
   int(N)           # Built-in function
   math.trunc(N)    # Math module
   
   # Round
   round(N, digits) # Built-in function
   math.floor(N)    # Floor function
   ```

7. **Integer to float conversion:**
   ```python
   float(I)         # Direct conversion
   I + 0.0          # Mixed arithmetic
   I / 1            # True division always returns float
   ```

8. **Display in different bases:**
   ```python
   oct(I)           # Octal string
   hex(I)           # Hexadecimal string
   bin(I)           # Binary string
   
   # String formatting
   f'{I:o}'         # Octal
   f'{I:x}'         # Hex
   f'{I:b}'         # Binary
   ```

9. **Convert base strings to integers:**
   ```python
   int(S, base)     # Specify base (8, 16, 2)
   int('377', 8)    # Octal to decimal
   int('FF', 16)    # Hex to decimal
   int('1010', 2)   # Binary to decimal
   
   # With prefixes
   int('0o377', 8)
   int('0xFF', 16)
   int('0b1010', 2)
   ```

---

## Advanced Topics and Edge Cases

### Operator Overloading and Polymorphism

Python operators can mean different things for different types:

```python
# + means addition for numbers
>>> 2 + 3
5

# + means concatenation for strings
>>> "Hello" + " World"
'Hello World'

# + means concatenation for lists
>>> [1, 2] + [3, 4]
[1, 2, 3, 4]
```

This property is called **polymorphism** - the meaning of an operation depends on the type of objects being processed.

### Immutable Constraints in Sets

Sets can only contain immutable (hashable) objects:

```python
# These work (immutable objects)
>>> S = {1, 2, 3, "hello", (1, 2, 3)}
>>> S
{1, 2, 3, 'hello', (1, 2, 3)}

# These don't work (mutable objects)
>>> S.add([1, 2, 3])  # Lists are mutable
TypeError: unhashable type: 'list'

>>> S.add({'a': 1})   # Dicts are mutable
TypeError: unhashable type: 'dict'

# Frozen sets can be nested in sets
>>> S.add(frozenset([4, 5, 6]))
>>> S
{1, 2, 3, 'hello', (1, 2, 3), frozenset({4, 5, 6})}
```

### Number Format Edge Cases

#### Underscore Separator Rules

```python
# Valid uses
>>> 1_000_000
1000000
>>> 0xFF_FF_FF_FF
4294967295

# Invalid uses - syntax errors
>>> _123        # Can't start with underscore
>>> 123_        # Can't end with underscore
>>> 12__34      # Can't have consecutive underscores

# Arbitrary positioning (valid but not recommended)
>>> 1_2_3_4_5
12345
>>> 0x_FF       # Valid but weird
255
```

#### Floating-Point Edge Cases

```python
# Scientific notation variations
>>> 1e5, 1E5, 1e+5, 1E+5
(100000.0, 100000.0, 100000.0, 100000.0)

>>> 1e-3, 1E-3
(0.001, 0.001)

# Special float values
>>> float('inf')    # Infinity
inf
>>> float('-inf')   # Negative infinity
-inf
>>> float('nan')    # Not a Number
nan

# Testing special values
>>> import math
>>> math.isinf(float('inf'))
True
>>> math.isnan(float('nan'))
True
```

### Complex Number Advanced Usage

```python
# Complex number methods and properties
>>> c = 3+4j
>>> c.conjugate()   # Complex conjugate
(3-4j)

>>> abs(c)          # Magnitude
5.0

# Complex math module
>>> import cmath
>>> cmath.phase(c)  # Phase angle
0.9272952180016122

>>> cmath.polar(c)  # Polar coordinates
(5.0, 0.9272952180016122)

>>> cmath.rect(5.0, 0.9272952180016122)  # Back to rectangular
(3.0000000000000004+3.9999999999999996j)
```

### Decimal Advanced Features

#### Decimal Context Settings

```python
>>> from decimal import Decimal, getcontext, localcontext

# Global context
>>> getcontext().prec = 6
>>> Decimal(1) / Decimal(3)
Decimal('0.333333')

# Local context (temporary)
>>> with localcontext() as ctx:
...     ctx.prec = 2
...     print(Decimal(1) / Decimal(3))
0.33

>>> Decimal(1) / Decimal(3)  # Back to global setting
Decimal('0.333333')
```

#### Rounding Modes

```python
>>> from decimal import Decimal, ROUND_UP, ROUND_DOWN, ROUND_HALF_UP

>>> d = Decimal('2.675')
>>> d.quantize(Decimal('0.01'), rounding=ROUND_UP)
Decimal('2.68')

>>> d.quantize(Decimal('0.01'), rounding=ROUND_DOWN)
Decimal('2.67')

>>> d.quantize(Decimal('0.01'), rounding=ROUND_HALF_UP)
Decimal('2.68')
```

### Fraction Advanced Features

```python
>>> from fractions import Fraction

# Fraction from float (be careful!)
>>> Fraction(0.25)
Fraction(1, 4)

>>> Fraction(0.1)  # Floating-point precision issues
Fraction(3602879701896397, 36028797018963968)

# Better to use from_float or string
>>> Fraction.from_float(0.25)
Fraction(1, 4)

>>> Fraction('0.1')
Fraction(1, 10)

# Limiting denominator
>>> Fraction(math.pi).limit_denominator(100)
Fraction(22, 7)

>>> Fraction(math.pi).limit_denominator(1000)
Fraction(355, 113)
```

---

## Performance Considerations

### Speed Comparisons

Different numeric operations have different performance characteristics:

```python
# Square root methods (fastest to slowest, typically)
import math

# Usually fastest
math.sqrt(x)

# Usually middle
x ** 0.5

# Usually slowest
pow(x, 0.5)
```

### Memory Usage

```python
# Integer memory usage grows with size
>>> import sys
>>> sys.getsizeof(1)
28
>>> sys.getsizeof(10**10)
32
>>> sys.getsizeof(10**100)
60

# Floating-point size is fixed
>>> sys.getsizeof(1.0)
24
>>> sys.getsizeof(1e100)
24
```

---

## Common Pitfalls and Best Practices

### Floating-Point Precision

**Problem:** Floating-point arithmetic isn't always exact
```python
>>> 0.1 + 0.2 == 0.3
False
```

**Solutions:**
```python
# Use Decimal for exact decimal arithmetic
>>> from decimal import Decimal
>>> Decimal('0.1') + Decimal('0.2') == Decimal('0.3')
True

# Use math.isclose for comparisons
>>> import math
>>> math.isclose(0.1 + 0.2, 0.3)
True

# Round for display
>>> round(0.1 + 0.2, 1) == 0.3
True
```

### Integer Division Gotchas

**Python 2 vs Python 3:**
```python
# Python 3 behavior (current)
>>> 5 / 2
2.5      # Always returns float

>>> 5 // 2
2        # Floor division

# To get Python 2 behavior in Python 3, use //
```

### Chained Comparison Surprises

```python
# This might not do what you expect
>>> False == False in [False]
True

# Equivalent to: (False == False) and (False in [False])
>>> (False == False) and (False in [False])
True

# Use parentheses for clarity
>>> (False == False) in [False]
False
```

### Boolean Arithmetic

```python
# Booleans are integers
>>> True + True
2
>>> False * 5
0

# This can be useful for counting
>>> sum([True, False, True, True, False])
3  # Counts True values
```

---

## Numeric Extensions and Third-Party Libraries

### Popular Numeric Libraries

1. **NumPy** - Numerical computing with arrays
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
print(arr * 2)  # [2 4 6 8 10]
```

2. **SciPy** - Scientific computing
```python
from scipy import stats
print(stats.norm.cdf(1.96))  # ~0.975
```

3. **Pandas** - Data analysis and manipulation
```python
import pandas as pd
df = pd.DataFrame({'numbers': [1, 2, 3, 4, 5]})
print(df.describe())
```

4. **Matplotlib** - Plotting and visualization
```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
plt.show()
```

5. **SymPy** - Symbolic mathematics
```python
from sympy import symbols, solve
x = symbols('x')
solve(x**2 - 4, x)  # [-2, 2]
```

---

## Practical Examples and Use Cases

### Financial Calculations

```python
from decimal import Decimal, ROUND_HALF_UP

# Money calculations should use Decimal
price = Decimal('19.99')
tax_rate = Decimal('0.08')
tax = price * tax_rate
tax = tax.quantize(Decimal('0.01'), rounding=ROUND_HALF_UP)
total = price + tax

print(f"Price: ${price}")      # Price: $19.99
print(f"Tax: ${tax}")          # Tax: $1.60
print(f"Total: ${total}")      # Total: $21.59
```

### Scientific Calculations

```python
import math
import cmath

# Physics: wave interference
def wave_amplitude(A1, A2, phase_diff):
    """Calculate resultant amplitude of two waves"""
    # Convert to complex representation
    wave1 = A1 + 0j
    wave2 = A2 * cmath.exp(1j * phase_diff)
    
    resultant = wave1 + wave2
    return abs(resultant)

# Example: two waves with amplitudes 3 and 4, phase difference π/3
amplitude = wave_amplitude(3, 4, math.pi/3)
print(f"Resultant amplitude: {amplitude:.2f}")
```

### Data Analysis

```python
import statistics
import random

# Generate sample data
data = [random.gauss(100, 15) for _ in range(1000)]

# Statistical analysis
mean = statistics.mean(data)
median = statistics.median(data)
stdev = statistics.stdev(data)
mode_val = statistics.mode([round(x) for x in data])

print(f"Mean: {mean:.2f}")
print(f"Median: {median:.2f}")
print(f"Standard Deviation: {stdev:.2f}")
print(f"Mode: {mode_val}")
```

### Cryptography and Security

```python
import random
import math

def generate_prime_candidate(length):
    """Generate a prime candidate of specified bit length"""
    # Generate random odd number
    p = random.getrandbits(length)
    p |= (1 << length - 1) | 1  # Set MSB and LSB
    return p

def is_prime(n, k=10):
    """Miller-Rabin primality test"""
    if n < 2:
        return False
    
    # Handle small primes
    small_primes = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
    if n in small_primes:
        return True
    if any(n % p == 0 for p in small_primes):
        return False
    
    # Write n-1 as 2^r * d
    r = 0
    d = n - 1
    while d % 2 == 0:
        r += 1
        d //= 2
    
    # Witness loop
    for _ in range(k):
        a = random.randrange(2, n - 1)
        x = pow(a, d, n)
        
        if x == 1 or x == n - 1:
            continue
            
        for _ in range(r - 1):
            x = pow(x, 2, n)
            if x == n - 1:
                break
        else:
            return False
    
    return True

# Generate a prime number
def generate_prime(bits):
    """Generate a prime number with specified bit length"""
    while True:
        candidate = generate_prime_candidate(bits)
        if is_prime(candidate):
            return candidate

# Example: Generate a 1024-bit prime
# prime = generate_prime(1024)
# print(f"Generated prime: {prime}")
```

---

## Chapter Summary

This comprehensive chapter covered Python's complete numeric ecosystem:

### Core Concepts Mastered:
1. **Numeric Types**: integers, floats, complex numbers, decimals, fractions, sets, booleans
2. **Literals and Representations**: decimal, binary, octal, hexadecimal formats
3. **Operators and Expressions**: precedence rules, mixed-type arithmetic
4. **Built-in Tools**: math functions, conversion utilities, formatting options
5. **Advanced Features**: unlimited precision, bitwise operations, set theory

### Key Skills Developed:
- Writing numeric literals in various bases
- Understanding operator precedence and expression evaluation
- Handling floating-point precision issues
- Using specialized numeric types for exact arithmetic
- Performing set operations and mathematical computations
- Converting between number formats and bases

### Best Practices Learned:
- Use appropriate numeric types for specific use cases
- Be aware of floating-point limitations and solutions
- Leverage Python's automatic type conversions
- Choose readable formatting for large numbers
- Apply proper rounding and precision control

### Real-World Applications:
- Financial calculations with exact decimal arithmetic
- Scientific computing with complex numbers
- Data analysis with statistical functions
- Cryptographic applications with large integers
- Set operations for data filtering and analysis

The knowledge gained from this chapter provides a solid foundation for all numeric programming in Python, from simple calculations to complex scientific and financial applications.

---

## Key Takeaways

1. **Python numbers** include integers, floats, complex numbers, decimals, fractions, and sets
2. **Unlimited integer precision** allows handling arbitrarily large numbers
3. **Operator precedence** follows mathematical conventions; use parentheses for clarity
4. **Mixed-type arithmetic** automatically converts to the most complex type
5. **Multiple number bases** (binary, octal, hex) provide flexibility for different domains
6. **Bitwise operations** enable low-level bit manipulation when needed
7. **Specialized numeric types** (Decimal, Fraction) address floating-point precision issues
8. **Sets** provide mathematical set operations and are useful for removing duplicates
9. **Built-in modules** (`math`, `random`, `statistics`) extend numeric capabilities
10. **String formatting** offers multiple ways to display numbers in various formats
11. **Performance considerations** matter for intensive numeric computations
12. **Third-party libraries** (NumPy, SciPy, pandas) extend Python's numeric capabilities significantly
13. **Precision issues** require careful handling in financial and scientific applications
14. **Boolean arithmetic** can be leveraged for counting and logical operations
15. **Proper type selection** is crucial for accuracy, performance, and code clarity
