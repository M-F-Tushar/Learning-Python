# Chapter 12: if and match Selections - Complete Guide

## Overview
This chapter covers Python's two main selection statements:
- **if/elif/else**: The primary selection tool for arbitrary logic
- **match/case**: A tool for multiple-choice selections with pattern matching

## Table of Contents
1. [if Statements](#if-statements)
2. [Multiple-Choice Selections](#multiple-choice-selections)
3. [match Statements](#match-statements)
4. [Python Syntax Rules](#python-syntax-rules)
5. [Truth Values and Boolean Operations](#truth-values-and-boolean-operations)
6. [Ternary if/else Expression](#ternary-ifelse-expression)

---

## if Statements

### General Format
```python
if test1:          # Main if test
    statements1    # Associated block
elif test2:        # Optional elif test(s)
    statements2    # Associated block
else:              # Optional else default
    statements3    # Associated block
```

### Basic Examples

#### Simple if Statement
```python
# Basic true condition
if 1:
    print('true')
# Output: true
```

#### if-else Statement
```python
# Handling false condition
if not 1:
    print('true')
else:
    print('false')
# Output: false
```

#### Complete if-elif-else Example
```python
# Mobile OS roots example
os, mode = 'Windows', 'mobile'

if os in ['iOS', 'iPhoneOS']:
    print('macOS')
elif mode == 'mobile' and os != 'Windows':
    print('Linux')
else:
    print('unknown?')
# Output: unknown?
```

### Nested if Statements
```python
# Nested logic for mobile systems
os, mode = 'Android', 'mobile'

if mode == 'mobile':
    if os == 'Android':
        print('Linux')
    elif os != 'Windows':
        print('macOS')
# Output: Linux
```

---

## Multiple-Choice Selections

### Dictionary-Based Selection

#### Basic Dictionary Selection
```python
# Using dictionary as a switch statement
choice = 'Windows'
result = {'macos': 2001, 'Linux': 1991, 'Windows': 1985}[choice]
print(result)
# Output: 1985
```

#### Equivalent if Statement
```python
# Traditional if-elif approach
choice = 'Windows'
if choice == 'macos':
    print(2001)
elif choice == 'Linux':
    print(1991)
elif choice == 'Windows':
    print(1985)
else:
    print('Bad choice')
# Output: 1985
```

### Handling Defaults in Dictionary Selection

#### Using get() Method
```python
branch = dict(macos=2001, Linux=1991, Windows=1985)
print(branch.get('Windows', 'Bad choice'))    # Output: 1985
print(branch.get('Solaris', 'Bad choice'))    # Output: Bad choice
```

#### Using in Membership Test
```python
choice = 'AmigaOS'
if choice in branch:
    print(branch[choice])
else:
    print('Bad choice')
# Output: Bad choice
```

#### Using try-except
```python
choice = 'GEM'
try:
    print(branch[choice])
except KeyError:
    print('Bad choice')
# Output: Bad choice
```

### Dictionary with Functions (Advanced)
```python
# Dictionary containing functions for complex actions
def action():
    return "Action executed"

def default():
    return "Default action"

branch = {
    'Android': lambda: "Android selected",
    'iOS': action,
    'Symbian OS': lambda: "Symbian selected"
}

choice = 'Android'
result = branch.get(choice, default)()
print(result)
# Output: Android selected
```

---

## match Statements

### Basic match Usage

#### Simple match Example
```python
# Traffic light example
state = 'go'  # Try 'go', 'stop', or other values

match state:
    case 'go':
        print('green')
    case 'stop':
        print('red')
    case _:  # Default case
        print('yellow')
# Output: green
```

#### Multiple Values in case
```python
# Matching multiple values with OR (|)
state = 'proceed'

match state:
    case 'go' | 'proceed' | 'start':
        print('green')
        print('means go')
    case 'stop' | 'halt' as what:
        print('red')
        print('means', what)
    case other:
        print('catchall', other)
# Output:
# green
# means go
```

### Practical match vs if Example
```python
# Categorizing statements
for stmt in ['if', 'while', 'try']:
    match stmt:
        case 'if' | 'match':
            print('logic')
        case 'for' | 'while' as which:
            print('loop')
        case other:
            print('tbd')

# Variables assigned during match persist
print(f"which: {which}, other: {other}")

# Output:
# logic
# loop  
# tbd
# which: while, other: try
```

#### Equivalent if Statement
```python
# Same logic using if statements
for stmt in ['if', 'while', 'try']:
    if stmt in ['if', 'match']:
        print('logic')
    elif stmt in ['for', 'while']:
        which = stmt
        print('loop')
    else:
        other = stmt
        print('tbd')
```

### Advanced match Patterns

#### Pattern Types Overview
- **Literal patterns**: `X` matches the same value
- **Wildcard patterns**: `_` matches anything (not assigned)
- **Capture patterns**: variable `X` matches anything and assigns to X
- **Or patterns**: `X | Y | Z` matches any of the patterns
- **As patterns**: `X as Y` matches pattern X and assigns to Y

#### Complex Pattern Examples
```python
# Various pattern types demonstration
state = [1, 2, 3]  # Try different values

match state:
    case 1 | 2 | 3 as what:        # Literal + capture
        print('number', what)
    case [1, 2, what]:             # Sequence pattern
        print('list', what)
    case [0, *what]:               # Sequence with star
        print('list starting with 0', what)
    case {'a': 1, 'b': 2, 'c': what}:  # Mapping pattern
        print('dict', what)
    case {'a': 0, **what}:         # Mapping with double star
        print('dict starting with a:0', what)
    case (1, 2, what):             # Tuple pattern
        print('tuple', what)
    case (0, *what):               # Tuple with star
        print('tuple starting with 0', what)
    case _ as what:                # Wildcard with capture
        print('other', what)

# Output: list 3
```

#### Guard Expressions
```python
# Using if guards in patterns
state = ((1, 2), 3)
guard1 = True

match state:
    case ((a, 2), b) if guard1:    # Pattern + guard condition
        print(f'case1 {a=} {b=}')
    case (a, 3) as what:
        print(f'case2 {a=} {what=}')
    case [a, (3 | 4)] as what if guard1:
        print(f'case3 {a=} {what=}')

# Output: case1 a=1 b=3
```

---

## Python Syntax Rules

### Block Structure and Indentation

#### Indentation Rules
- All statements at the same indentation level belong to the same block
- Nested blocks are indented further to the right
- Python uses indentation instead of braces `{}` to define blocks
- Consistent indentation is required (4 spaces or 1 tab commonly used)

#### Example of Proper Indentation
```python
x = 1
if x:
    y = 2                # 4 spaces indent
    if y:
        print('block2')  # 8 spaces indent
    print('block1')      # 4 spaces indent
print('block0')          # 0 spaces indent
```

#### Common Indentation Errors
```python
# ❌ INCORRECT - Inconsistent indentation
x = 'Hack'
if 'tho' in 'python':
    print(x * 8)
      x += 'More!'       # Error: unexpected indent
    if x.endswith('re!'):
        x *= 2
   print(x)              # Error: inconsistent indent

# ✅ CORRECT - Consistent indentation
x = 'Hack'
if 'tho' in 'python':
    print(x * 8)         # Prints: HackHackHackHackHackHackHackHack
    x += 'More!'
    if x.endswith('re!'):
        x *= 2
    print(x)             # Prints: HackMore!HackMore!
```

### Statement Continuation

#### Using Parentheses (Recommended)
```python
# List spanning multiple lines
L = ['app',
     'script',
     'program']

# Conditional spanning multiple lines
if (a == b and c == d and
    d == e and e == f):
    print('conditions met')
```

#### Using Backslashes (Discouraged)
```python
# Works but not recommended
if a == b and c == d and \
   d == e and f == g:
    print('old school')
```

#### Multiple Statements on One Line
```python
# Using semicolons (generally discouraged)
x = 1; y = 2; print(x)  # Output: 1
```

#### String Continuation
```python
# Triple-quoted strings
S = """
aaaa
bbbb
cccc"""

# Implicit string concatenation
S = ('aaaa'
     'bbbb'    # Comments ignored here
     'cccc')

# f-string continuation
S = (f'{'a' * 4}'      # Also makes 'aaaabbbbcccc'
     f'{'b' * 4}'      # Use f'' on each f-string line
     r'cccc')          # And ditto for r'' raw strings
```

---

## Truth Values and Boolean Operations

### Truth Value Rules
1. **All objects have an inherent Boolean value**
2. **True values**: Any nonzero number, nonempty object
3. **False values**: Zero numbers, empty objects, `None`

#### Examples of Truth Values
```python
# True values
print(bool(1))        # True
print(bool(-1))       # True
print(bool('hello'))  # True
print(bool([1, 2]))   # True

# False values
print(bool(0))        # False
print(bool(''))       # False
print(bool([]))       # False
print(bool(None))     # False
```

### Boolean Operators

#### and Operator
```python
# Returns first false operand, or last operand if all true
print(2 and 3)        # 3 (both true, return last)
print(3 and 2)        # 2 (both true, return last)
print([] and {})      # [] (first is false, return it)
print(3 and [])       # [] (first true, second false, return second)
```

#### or Operator
```python
# Returns first true operand, or last operand if all false
print(2 or 3)         # 2 (first is true, return it)
print(3 or 2)         # 3 (first is true, return it)
print([] or 3)        # 3 (first false, return second)
print([] or {})       # {} (both false, return last)
```

#### Practical Boolean Usage
```python
# Setting defaults using or
name = input_name or 'Anonymous'

# Validation using and
valid_user = username and password and user_exists(username)
```

### Comparison Operators
```python
# Basic comparisons return True/False
print(2 < 3)          # True
print(3 < 2)          # False
print(2 == 2)         # True
print('a' in 'abc')   # True
```

---

## Ternary if/else Expression

### Basic Syntax
```python
# Ternary expression format
A = Y if X else Z

# Equivalent if statement
if X:
    A = Y
else:
    A = Z
```

### Practical Examples
```python
# Simple example
tone = 'formal'
greeting = 'Good day' if tone == 'formal' else 'Hey'
print(greeting)  # Output: Good day

tone = 'informal'
greeting = 'Good day' if tone == 'formal' else 'Hey'
print(greeting)  # Output: Hey

# Nested in function calls
print('PASS' if score >= 60 else 'FAIL')

# Multiple ternary expressions
status = 'high' if score >= 90 else 'medium' if score >= 60 else 'low'
```

### Alternative Boolean Expressions
```python
# Using and/or (less readable)
A = ((X and Y) or Z)  # Works if Y is always truthy

# Using list indexing (not recommended)
A = [Z, Y][bool(X)]   # Always evaluates both Z and Y

# Examples showing differences
tone = 'formal'
print(['hack', 'code'][tone == 'formal'])  # code
print(['hack', 'code'][bool('formal')])    # code (different logic)
```

---

## Key Takeaways

### When to Use Each Construct

1. **if/elif/else**: 
   - General-purpose logic
   - Complex conditions
   - When you need full statement blocks

2. **Dictionary selection**:
   - Simple value mapping
   - Dynamic choices (data-driven)
   - When choices can be computed at runtime

3. **match/case**:
   - Multiple-choice selection
   - Pattern matching needs
   - When structure matching is beneficial

4. **Ternary expression**:
   - Simple conditional assignments
   - When embedding in larger expressions
   - Keep it simple and readable

### Best Practices

1. **Favor readability** over cleverness
2. **Use consistent indentation** (4 spaces recommended)
3. **Avoid mixing tabs and spaces**
4. **Keep ternary expressions simple**
5. **Use parentheses for line continuation** instead of backslashes
6. **Choose the right tool** for the job (if vs match vs dictionary)

### Common Pitfalls

1. **Inconsistent indentation** causes syntax errors
2. **Missing colons** after if/elif/else/case headers
3. **Forgetting the underscore** in match default cases
4. **Overcomplicating ternary expressions**
5. **Using match for simple true/false logic** (use if instead)

---

## Summary

Python's selection statements provide flexible ways to control program flow:
- **if statements** handle arbitrary logic with clear, readable syntax
- **match statements** excel at multiple-choice selections with pattern matching
- **Dictionary selection** offers dynamic, data-driven choices
- **Ternary expressions** provide concise conditional assignments

The key is choosing the right tool for each situation while maintaining code readability and following Python's syntax conventions.
