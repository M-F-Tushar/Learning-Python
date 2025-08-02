# Chapter 11: Assignments, Expressions, and Prints

## Overview
This chapter covers the fundamental building blocks of Python programming: assignment statements, expression statements, and print operations. While these concepts are relatively simple, they include optional variations that become essential for realistic Python programming.

---

## 1. Assignments

### 1.1 Key Properties of Python Assignments

**1. Assignments create object references**
- Python assignments store references to objects, not copies
- Variables are more like pointers than data storage areas

**2. Names are created when first assigned**
- No need to predeclare variables
- Some data structure slots are also created when assigned (dictionary entries, object attributes)

**3. Names must be assigned before being referenced**
- Python raises an exception for unassigned names
- This prevents typos and ambiguous default values

**4. Some operations perform assignments implicitly**
- Module imports, function definitions, class definitions
- For loop variables, function arguments
- All follow the same assignment rules

### 1.2 Assignment Syntax Forms

| Operation | Interpretation | Example |
|-----------|----------------|---------|
| `target = 'Hack'` | Basic assignment | `x = 5` |
| `code, hack = 'py', 'PY'` | Tuple assignment | `a, b = 1, 2` |
| `[code, hack] = ['py', 'PY']` | List assignment | `[x, y] = [3, 4]` |
| `a, b, c, d = 'hack'` | Sequence assignment | `w, x, y, z = "test"` |
| `a, *b = 'hack'` | Extended-unpacking assignment | `first, *rest = [1,2,3,4]` |
| `code = hack = 'python'` | Multiple-target assignment | `x = y = z = 0` |
| `code += 1, hack *= 2` | Augmented assignments | `count += 1` |
| `(python := 3.12) + 0.01` | Named assignment expression | `if (n := len(data)) > 10:` |

---

## 2. Basic Assignments

### 2.1 Assignment Targets

```python
# Name target
L = [1, 2]

# Index target  
L[0] = 3

# Slice target
L[-1:] = [4, 5]

print(L)  # Output: [3, 4, 5]

# Attribute target (for classes)
# object.attr = L
```

**Explanation**: Python supports four types of assignment targets: names (variables), indexes, slices, and attributes. Each can be used in any form of assignment.

---

## 3. Sequence Assignments

### 3.1 Tuple and List Assignment

```python
# Basic assignments
first = 1
second = 2

# Tuple assignment (parentheses optional)
A, B = first, second
print(A, B)  # Output: (1, 2)

# List assignment
[C, D] = [first, second]
print(C, D)  # Output: (1, 2)
```

### 3.2 Variable Swapping Trick

```python
first = 1
second = 2

# Swap variables using tuple assignment
first, second = second, first
print(first, second)  # Output: (2, 1)
```

**Explanation**: Python creates a temporary tuple that saves the original values, making variable swapping elegant without explicit temporary variables.

### 3.3 Generalized Sequence Assignment

```python
# Assign tuple to list variables
[a, b, c] = (1, 2, 3)
print(a, c)  # Output: (1, 3)

# Assign string to tuple variables
(a, b, c) = 'ABC'
print(a, c)  # Output: ('A', 'C')

# Any iterable works
string = 'TEXT'
a, b, c, d = string
print(a, b, c, d)  # Output: ('T', 'E', 'X', 'T')
```

### 3.4 Advanced Sequence Assignment Patterns

**Length Mismatch Handling:**
```python
string = 'ABC'
# This would cause an error:
# a, b = string  # ValueError: too many values to unpack

# Solutions using slicing:
a, b, c = string[0], string[1], string[2:]
print(a, b, c)  # Output: ('A', 'B', 'C')

a, b = string[:2]
c = string[2:]
print(a, b, c)  # Output: ('A', 'B', 'C')
```

**Nested Sequence Assignment:**
```python
# Nested unpacking
(a, b), c = string[:2], string[2:]
print(a, b, c)  # Output: ('T', 'E', 'XT')

# Equivalent to:
((a, b), c) = ('TE', 'XT')
print(a, b, c)  # Output: ('T', 'E', 'XT')
```

### 3.5 Common Sequence Assignment Patterns

**Enumerated Data Types:**
```python
# Initialize multiple variables with range
red, green, blue = range(3)
print(red, blue)  # Output: (0, 2)

# Show what range produces
print(list(range(3)))  # Output: [0, 1, 2]
```

**List Processing Pattern:**
```python
L = [1, 2, 3, 4]
while L:
    front, L = L[0], L[1:]  # Split front and rest
    print(front, L)

# Output:
# 1 [2, 3, 4]
# 2 [3, 4] 
# 3 [4]
# 4 []
```

---

## 4. Extended-Unpacking Assignments

### 4.1 Starred Target Syntax

```python
seq = [1, 2, 3, 4]

# First item and rest
a, *b = seq
print(a)    # Output: 1
print(b)    # Output: [2, 3, 4]

# Rest and last item
*a, b = seq
print(a)    # Output: [1, 2, 3]
print(b)    # Output: 4

# First, middle, and last
a, *b, c = seq
print(a)    # Output: 1
print(b)    # Output: [2, 3]
print(c)    # Output: 4
```

### 4.2 Extended Unpacking with Different Types

```python
# With strings
a, *b = 'hack'
print(a, b)  # Output: ('h', ['a', 'c', 'k'])

a, *b, c = 'hack'
print(a, b, c)  # Output: ('h', ['a', 'c'], 'k')

# With range objects
a, *b, c = range(4)
print(a, b, c)  # Output: (0, [1, 2], 3)
```

### 4.3 Comparison with Slicing

```python
S = 'hack'

# Using slicing
a, b, c = S[0], S[1:-1], S[-1]
print(a, b, c)  # Output: ('h', 'ac', 'k')

# Using extended unpacking
a, *b, c = S
print(a, b, c)  # Output: ('h', ['a', 'c'], 'k')
```

**Key Difference**: Extended unpacking always returns a list for starred items, while slicing returns the same type as the original sequence.

### 4.4 Boundary Cases

```python
seq = [1, 2, 3, 4]

# Starred target matches single item
a, b, c, *d = seq
print(a, b, c, d)  # Output: 1 2 3 [4]

# Starred target matches nothing
a, b, c, d, *e = seq
print(a, b, c, d, e)  # Output: 1 2 3 4 []

# Empty list regardless of position
a, b, *e, c, d = seq
print(a, b, c, d, e)  # Output: 1 2 3 4 []
```

### 4.5 Error Cases

```python
# Multiple starred targets (ERROR)
# a, *b, c, *d = seq  # SyntaxError

# Too few values, no star (ERROR)  
# a, b = seq  # ValueError

# Starred target not in sequence (ERROR)
# *a = seq  # SyntaxError

# Correct single-item tuple form
*a, = seq
print(a)  # Output: [1, 2, 3, 4]
```

### 4.6 Practical Applications

**Simplified List Processing:**
```python
L = [1, 2, 3, 4]
while L:
    front, *L = L  # Get first and rest
    print(front, L)

# Output:
# 1 [2, 3, 4]
# 2 [3, 4]
# 3 [4] 
# 4 []
```

**Common Splitting Patterns:**
```python
seq = [1, 2, 3, 4]

# First, rest pattern
a, *b = seq
print(f"First: {a}, Rest: {b}")  # First: 1, Rest: [2, 3, 4]

# Rest, last pattern  
*a, b = seq
print(f"Rest: {a}, Last: {b}")   # Rest: [1, 2, 3], Last: 4
```

---

## 5. Multiple-Target Assignments

### 5.1 Basic Multiple Assignment

```python
# Assign same value to multiple variables
a = b = c = 'code'
print(a, b, c)  # Output: ('code', 'code', 'code')

# Equivalent to:
c = 'code'
b = c  
a = b
```

### 5.2 Shared References with Immutable Objects

```python
# Safe with immutable objects
a = b = 0
b = b + 1
print(a, b)  # Output: (0, 1)
```

**Explanation**: Since numbers are immutable, changing `b` creates a new object, leaving `a` unchanged.

### 5.3 Shared References with Mutable Objects (Caution!)

```python
# Problematic with mutable objects
a = b = []
b.append(42)
print(a, b)  # Output: ([42], [42])
```

**Problem**: Both variables reference the same list object, so modifying through one affects both.

**Solutions:**
```python
# Create separate objects
a = []
b = []
b.append(42)
print(a, b)  # Output: ([], [42])

# Or use tuple assignment
a, b = [], []
b.append(42) 
print(a, b)  # Output: ([], [42])
```

---

## 6. Augmented Assignments

### 6.1 Augmented Assignment Operators

| Operator | Equivalent | Description |
|----------|------------|-------------|
| `X += Y` | `X = X + Y` | Addition |
| `X -= Y` | `X = X - Y` | Subtraction |
| `X *= Y` | `X = X * Y` | Multiplication |
| `X /= Y` | `X = X / Y` | Division |
| `X //= Y` | `X = X // Y` | Floor division |
| `X %= Y` | `X = X % Y` | Modulus |
| `X **= Y` | `X = X ** Y` | Exponentiation |
| `X >>= Y` | `X = X >> Y` | Right shift |
| `X <<= Y` | `X = X << Y` | Left shift |
| `X &= Y` | `X = X & Y` | Bitwise AND |
| `X |= Y` | `X = X | Y` | Bitwise OR |
| `X ^= Y` | `X = X ^ Y` | Bitwise XOR |

### 6.2 Basic Examples

```python
# Numeric operations
x = 1
x += 1  # Same as x = x + 1
print(x)  # Output: 2

# String concatenation
S = 'hack'
S += 'HACK'  # Same as S = S + 'HACK'
print(S)  # Output: 'hackHACK'
```

### 6.3 Advantages of Augmented Assignment

**1. Less typing**
**2. Left side evaluated only once**
**3. Automatic optimization for mutable objects**

### 6.4 In-Place Operations for Lists

```python
# Manual concatenation vs in-place methods
L = [1, 2]

# Concatenation (creates new object)
L = L + [3]
print(L)  # Output: [1, 2, 3]

# In-place method (modifies existing object)
L.append(4)
print(L)  # Output: [1, 2, 3, 4]

# Multiple items
L = L + [5, 6]    # Concatenation
L.extend([7, 8])  # In-place extension
print(L)  # Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

### 6.5 Augmented Assignment Optimization

```python
# += automatically uses extend for lists
L = [1, 2, 3, 4, 5, 6, 7, 8]
L += [9, 10]  # Mapped to L.extend([9, 10])
print(L)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 6.6 Differences Between += and +

```python
# += allows arbitrary sequences (like extend)
L = []
L += 'hack'  # Works: adds individual characters
print(L)  # Output: ['h', 'a', 'c', 'k']

# + requires same type
L = []
# L = L + 'code'  # TypeError: can't concatenate list and str
```

### 6.7 Index and Slice Targets

```python
# Augmented assignment with indexing
L = [1, 2]
L[0] += 10  # Change an item only
print(L)  # Output: [11, 2]

# Augmented assignment with slicing
L[-1:] += [3, 4]  # Change a section
print(L)  # Output: [11, 2, 3, 4]
```

### 6.8 Shared References with Augmented Assignment

```python
# Concatenation creates new object
L = [1, 2]
M = L
L = L + [3, 4]  # L gets new object
print(L, M)  # Output: ([1, 2, 3, 4], [1, 2])

# += modifies in-place
L = [1, 2] 
M = L
L += [3, 4]  # L modified in-place
print(L, M)  # Output: ([1, 2, 3, 4], [1, 2, 3, 4])
```

**Important**: This difference matters for mutable objects when references are shared.

---

## 7. Named Assignment Expressions (`:=`)

### 7.1 Basic Syntax and Behavior

```python
# := assigns and returns the value
a = 'hack' * (b := 2)
print(a)  # Output: 'hackhack'
print(b)  # Output: 2

# Simple named assignment
result = (python := 3.12) + 0.01
print(result)  # Output: 3.13
print(python)  # Output: 3.12
```

### 7.2 Limitations of Named Assignment

```python
# Only simple names allowed (not other assignment forms)
# (python, Python := 3.12, 3.13) + 0.01  # TypeError
# (python[0] := 3.12) + 0.01             # SyntaxError  
# (python.attr := 3.12) + 0.01           # SyntaxError

# No augmented forms
# There is no :+=, :*=, etc.
```

### 7.3 Common Use Cases

**File Reading Pattern:**
```python
# Traditional approach
line = file.readline()
if line:
    print(line)

# With := (assuming file is opened)
# if line := file.readline():
#     print(line)

# Traditional while loop
line = file.readline()
while line:
    print(line)
    line = file.readline()

# With := 
# while line := file.readline():
#     print(line)
```

### 7.4 Parentheses Requirements

```python
# Comparison operations require parentheses
# if (line := file.readline()) != ignore:
#     print(line)
    
# while (line := file.readline()) != stop:
#     print(line)
```

**Why**: Without parentheses, the `!=` operator binds tighter than `:=`, changing the meaning.

### 7.5 Creative Uses

```python
# Reuse values in literals
result = [val := 'Py!', val * 2, val * 3]
print(result)  # Output: ['Py!', 'Py!Py!', 'Py!Py!Py!']

# Get last result from generator expression
powers = list(pow := 2 ** num for num in [2, 4, 8])
print(powers)  # Output: [4, 16, 256]
print(pow)     # Output: 256 (last computed value)

# In f-strings
name = "Alice"
greeting = f'Hello {(name := input("Who are you? ")) if False else name}'
print(greeting)  # Uses existing name value

# Nested assignments
result = (x := (y := (z := 1) + 1) + 1)
print(result)  # Output: 3
print(x, y, z)  # Output: (3, 2, 1)
```

### 7.6 Best Practices

- Use parentheses for clarity and to avoid operator precedence issues
- Don't overuse - clarity is better than cleverness
- Good for avoiding redundant calls in conditions
- Avoid deeply nested walrus operators

---

## 8. Variable Name Rules

### 8.1 Syntax Rules

**Valid Characters:**
- Must start with underscore `_` or letter (a-z, A-Z)
- Can contain letters, digits (0-9), or underscores
- Unicode characters allowed but not recommended

**Examples:**
```python
# Valid names
_hack = 1
hack = 2  
Hack_1 = 3

# Invalid names (would cause SyntaxError)
# 1_hack = 1    # Can't start with digit
# hack$ = 2     # Invalid character $
# @#! = 3       # Invalid characters
```

### 8.2 Case Sensitivity

```python
# These are different variables
x = 0
X = 'Hello'
print(x, X)  # Output: 0 Hello
```

### 8.3 Reserved Words

Python reserved words (cannot be used as variable names):

| Reserved Words | | | | |
|---|---|---|---|---|
| `False` | `await` | `else` | `import` | `pass` |
| `None` | `break` | `except` | `in` | `raise` |
| `True` | `class` | `finally` | `is` | `return` |
| `and` | `continue` | `for` | `lambda` | `try` |
| `as` | `def` | `from` | `nonlocal` | `while` |
| `assert` | `del` | `global` | `not` | `with` |
| `async` | `elif` | `if` | `or` | `yield` |

**Soft Reserved Words** (context-dependent):
- `match`, `case`, `_`, `type`

### 8.4 Naming Conventions

**Built-in Patterns:**
```python
# Single underscore: not imported by "from module import *"
_internal = "private"

# Double underscores: system-defined names  
__name__ = "special"

# Leading double underscore: class name mangling
class MyClass:
    __private = "mangled"

# Single underscore: last expression result in REPL
# Also wildcard in match statements
```

**Style Conventions:**
```python
# Acceptable styles
camelCase = "someVariable"
snake_case = "some_variable" 
PascalCase = "SomeClass"  # Usually for classes

# Module and variable naming
my_module = "lowercase"
MyClass = "CapitalizedWords"
```

### 8.5 Names vs Objects

```python
# Names have no type, objects do
x = 0           # x references integer
x = 'Hello'     # x references string  
x = [1, 2, 3]   # x references list

# This flexibility is a Python advantage
```

---

## 9. Expression Statements

Expression statements are expressions used as statements (usually on their own lines).

### 9.1 Common Uses

**Function and Method Calls:**
```python
# Functions that work via side effects
print('Hello World')  # Displays output
list.append(42)      # Modifies list
file.close()         # Closes file

# Method calls
my_string.upper()    # Returns result (usually assigned)
my_list.sort()       # Modifies list in place
```

**Interactive Prompt:**
```python
# At Python REPL, expressions are automatically printed
>>> 'hello world'
'hello world'

>>> 2 + 2
4
```

### 9.2 Expression vs Statement Forms

| Operation | Interpretation |
|-----------|----------------|
| `hack('Py', 3.12)` | Function call |
| `code.hack('Py')` | Method call |
| `hack` | Print in REPL |
| `print(a, b, c, sep='')` | Print function call |
| `yield x ** 2` | Generator yield |
| `await producer()` | Coroutine await |

### 9.3 Important Distinction

```python
# print returns None but displays output
x = print('code')
print(x)  # Output: None

# Statements cannot be used as expressions  
# if x = 5:  # SyntaxError - assignment is not expression
# Use := for assignment in expressions
if (x := 5) > 3:
    print("x is", x)
```

### 9.4 Common Mistakes with In-Place Methods

```python
# WRONG - in-place methods return None
L = [1, 2]
L = L.append(3)  # L becomes None!
print(L)         # Output: None

# CORRECT - use as expression statement
L = [1, 2]
L.append(3)      # Modifies L in place
print(L)         # Output: [1, 2, 3]
```

**Remember**: Methods like `append()`, `sort()`, `reverse()` modify objects in-place and return `None`.

---

## 10. Print Operations

### 10.1 Print as File Interface

Print provides a programmer-friendly interface to the standard output stream:

- **File object methods**: Write strings to files
- **Print operations**: Write objects to stdout with automatic formatting
- **Standard output stream**: Default destination for program text output

### 10.2 Print Function Syntax

```python
print([object, ...][, sep=' '][, end='\n'][, file=sys.stdout][, flush=False])
```

**Parameters:**
- `object`: Items to print (any number)
- `sep`: String between objects (default: space)
- `end`: String at end (default: newline)
- `file`: Output destination (default: stdout) 
- `flush`: Force immediate output (default: False)

### 10.3 Basic Print Examples

```python
# Basic printing
print()  # Empty line
x, y, z = 'python', 3.12, ['lp6e']
print(x, y, z)  # Output: python 3.12 ['lp6e']

# Custom separators
print(x, y, z, sep='')        # Output: python3.12['lp6e']
print(x, y, z, sep=', ')      # Output: python, 3.12, ['lp6e']

# Custom endings
print(x, y, z, end='')        # No newline
print(x, y, z, end='!\n')     # Custom ending

# Combine options
print(x, y, z, sep='...', end='!\n')  # Output: python...3.12...['lp6e']!
```

### 10.4 File Output

```python
# Print to file
print(x, y, z, sep='...', file=open('data.txt', 'w'))

# Verify file contents
print(open('data.txt').read())  # Shows file contents
```

### 10.5 Advanced Formatting

```python
# When print formatting isn't enough, use string formatting
x, y, z = 'python', 3.12, ['lp6e']

# String formatting
text = '%s: %-.4f, %05d' % (x, y, int(z[0][-2:]))
print(text)  # Output: python: 3.1200, 00006

# f-strings  
print(f'{x}: {y:-0.4f}, {int(z[0][-2:]):05d}')

# Don't overuse f-strings for simple printing
a, b, c = 11, 3.14, 'hack'
print(f'{a} {b} {c}')  # Overkill
print(a, b, c)         # Better for simple cases
```

### 10.6 Stream Redirection

**Manual Redirection:**
```python
import sys

# Save original stdout
temp = sys.stdout

# Redirect to file
sys.stdout = open('log.txt', 'a')
print('lp6e was here')  # Goes to file
print(1, 2, 3)

# Restore original stdout  
sys.stdout.close()
sys.stdout = temp
print('back in the REPL')  # Goes to console
```

**Temporary Redirection:**
```python
# Better approach - temporary redirection
log = open('log.txt', 'a')
print(1, 2, 3, file=log)  # To file
print(4, 5, 6)            # To console
log.close()
```

**Error Output:**
```python
import sys

# Print to standard error
sys.stderr.write('Bad!' * 8 + '\n')
print('Bad!' * 8, file=sys.stderr)
```

### 10.7 Print vs File Write Equivalence

```python
import sys

# These are equivalent:
print(X, Y)
sys.stdout.write(str(X) + ' ' + str(Y) + '\n')

# Demonstration
X, Y = 1, 2
print(X, Y)                                          # Output: 1 2
sys.stdout.write(str(X) + ' ' + str(Y) + '\n')      # Output: 1 2
```

---

## 11. Key Takeaways and Best Practices

### 11.1 Assignment Best Practices

1. **Use sequence assignment for swapping**: `a, b = b, a`
2. **Use extended unpacking for splitting**: `first, *rest = sequence`
3. **Be careful with mutable objects in multiple assignment**: Create separate objects
4. **Use augmented assignment for efficiency**: `x += 1` vs `x = x + 1`
5. **Use named assignment sparingly**: Only when it improves readability

### 11.2 Common Pitfalls to Avoid

1. **Don't assign in-place method results**: `L.append(x)` not `L = L.append(x)`
2. **Watch out for shared references**: `a = b = []` creates shared object
3. **Remember operator precedence with `:=`**: Use parentheses for clarity
4. **Don't confuse `=` and `==`**: Assignment vs comparison

### 11.3 Print Best Practices

1. **Use print for simple output**: Don't overcomplicate with f-strings
2. **Use file parameter for temporary redirection**: Better than sys.stdout manipulation
3. **Use string formatting for complex output**: When print's options aren't enough
4. **Remember print returns None**: Don't chain print calls expecting values

### 11.4 Naming Best Practices

1. **Follow Python conventions**: snake_case for variables, PascalCase for classes
2. **Avoid reserved words**: Check the reserved word list
3. **Use meaningful names**: Code is read more than written
4. **Be consistent**: Pick a naming style and stick to it

---

## 12. Summary

This chapter covered the fundamental building blocks of Python programming:

- **Assignments**: Various forms from basic to extended unpacking
- **Expression statements**: Using expressions as standalone statements  
- **Print operations**: Flexible output with formatting and redirection options
- **Variable naming**: Rules, conventions, and best practices

These concepts form the foundation for more advanced Python programming constructs covered in subsequent chapters. Understanding these basics thoroughly will make learning more complex topics much easier.

The key insight is that while these operations appear simple, their optional forms and edge cases provide powerful tools for writing clean, efficient Python code. The examples and patterns shown here will appear frequently in real-world Python programming.
