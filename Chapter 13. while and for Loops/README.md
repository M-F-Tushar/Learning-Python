# Python Loops - Complete Guide (Chapter 13)

## Table of Contents
1. [Introduction to Loops](#introduction-to-loops)
2. [while Loops](#while-loops)
3. [Loop Control Statements](#loop-control-statements)
4. [for Loops](#for-loops)
5. [Loop Coding Techniques](#loop-coding-techniques)
6. [Chapter Summary](#chapter-summary)

---

## Introduction to Loops

Python provides two main looping constructs for repetitive tasks:

### **while / else**
- Most general looping statement
- Can handle repetitive tasks of all kinds

### **for / else**
- Specialized loop for stepping through iterable objects
- Designed for easy iteration over sequences

**Additional loop-related tools covered:**
- `break` and `continue` statements
- Loop `else` clause
- Built-in functions: `range`, `zip`, `enumerate`

---

## while Loops

### General Format

```python
while test:          # Loop test
    statements       # Repeated loop body
else:               # Optional else
    statements      # Run if didn't exit via break
```

**How it works:**
1. Python evaluates the test expression
2. If true, executes the loop body
3. Returns to test and repeats
4. When test becomes false, exits loop
5. If `else` clause exists and no `break` was encountered, executes `else`

### Examples

#### Example 1: Infinite Loop
```python
>>> while True:
...     print('Type Ctrl+C to stop me!')
```
**Explanation:**
- `True` is always true, creating an infinite loop
- Must use Ctrl+C to terminate
- Demonstrates basic while loop structure

#### Example 2: String Slicing Loop
```python
>>> x = 'code'
>>> while x:  # While x is not empty
...     print(x, end=' ')  # Print current string
...     x = x[1:]         # Strip first character
code ode de e
```
**Explanation:**
- Tests `x` directly (empty string is false)
- Each iteration removes first character with slicing `x[1:]`
- Loop ends when string becomes empty
- `end=' '` puts all output on same line

#### Example 3: Counter Loop
```python
>>> a = 0; b = 10
>>> while a < b:  # One way to count
...     print(a, end=' ')
...     a += 1    # Or, a = a + 1
0 1 2 3 4 5 6 7 8 9
```
**Explanation:**
- Counts from `a` (0) up to but not including `b` (10)
- `a += 1` increments counter each iteration
- Common pattern for generating object indexes

#### Example 4: Simulating "do until" Loop
```python
while True:
    # ...loop body...    # Always run loop body once
    if test: break       # Test for loop exit
```
**Explanation:**
- Python lacks "do until" construct
- This pattern ensures body runs at least once
- Uses `break` to exit when condition is met

---

## Loop Control Statements

### break, continue, pass, and Loop else

#### **break**
- Jumps out of the closest enclosing loop entirely
- Skips any remaining loop body code

#### **continue**  
- Jumps to the top of the closest enclosing loop
- Skips remaining body code for current iteration

#### **pass**
- Does nothing - empty statement placeholder
- Used when syntax requires a statement but you have nothing to do

#### **Loop else**
- Runs only if loop exits normally (without hitting `break`)
- Provides explicit syntax for "loop completed successfully" scenarios

### General Loop Format with Control Statements

```python
while test:
    statements
    if test: break      # Exit loop now, skip else
    if test: continue   # Go to test at top
else:
    statements         # Run on exit if no break
```

### Examples

#### Example 1: pass Statement
```python
>>> while True: pass  # Type Ctrl+C to stop
```
**Explanation:**
- Creates infinite loop that does nothing
- `pass` serves as placeholder where statement is required
- Body is on same line (allowed for simple statements)

**Other uses of pass:**
```python
def func1():
    pass  # Add real code here later

def func2():
    pass  # Placeholder function
```

#### Example 2: Ellipsis Alternative to pass
```python
def func1():
    ...  # Alternative to pass

>>> func1()  # Does nothing if called
>>> tbd = ...  # Alternative to both pass and None
>>> tbd
Ellipsis
```
**Explanation:**
- `...` (three dots) can replace `pass` in many contexts
- Useful for "to be implemented later" code
- Returns actual `Ellipsis` object when used as expression

#### Example 3: continue Statement
```python
x = 10
while x:
    x -= 1              # Decrement first
    if x % 2 != 0: continue  # Odd? Skip print
    print(x, end=' ')   # Even numbers only
# Output: 8 6 4 2 0
```
**Explanation:**
- Counts down from 10 to 1
- `continue` skips odd numbers
- Only even numbers get printed
- `%` is modulus operator (remainder after division)

**Alternative without continue:**
```python
x = 10
while x:
    x -= 1
    if x % 2 == 0:     # Even? Print it
        print(x, end=' ')
```

#### Example 4: break Statement - Interactive Loop
```python
>>> num = 1
>>> while True:
...     tool = input(f'{num}) What\'s your favorite language? ')
...     if tool == 'stop': break
...     print('Bravo!' if tool == 'Python' else 'Try again...')
...     num += 1

1) What's your favorite language? Java
Try again...
2) What's your favorite language? Python  
Bravo!
3) What's your favorite language? stop
```
**Explanation:**
- Infinite loop with user input
- `break` exits when user types "stop"
- Uses f-string formatting and conditional expression
- No need for nested `else` after `break`

**Alternative using named assignment (walrus operator):**
```python
>>> num = 1
>>> while (tool := input(f'{num}) What\'s your favorite language? ')) != 'stop':
...     print('Bravo!' if tool == 'Python' else 'Try again...')
...     num += 1
```

#### Example 5: Loop else - Prime Number Checker
```python
x = num // 2          # Start checking from num//2
while x > 1:
    if num % x == 0:  # Remainder is 0?
        print(num, 'has factor', x)
        break         # Exit loop
    x -= 1
else:                 # Normal exit (no break)
    print(num, 'is prime')
```
**Explanation:**
- Tests if `num` has factors other than 1 and itself
- `//` is integer division (truncates remainder)
- If factor found, `break` exits and skips `else`
- If no factors found, `else` executes (number is prime)
- `else` also runs if `x` starts ≤ 1

### Why Use Loop else?

**Traditional approach with flags:**
```python
found = False
while x and not found:
    if match(x[0]):      # Value at front
        print('Found')
        found = True
    else:
        x = x[1:]        # Slice off front
if not found:
    print('Not found')
```

**Cleaner approach with loop else:**
```python
while x:                 # Exit when empty
    if match(x[0]):
        print('Found')
        break            # Exit, go around else
    x = x[1:]
else:
    print('Not found')   # Only here if no break
```

**Benefits:**
- More concise code
- No flag variables needed
- Explicit syntax for "search failure" case
- More structured than manual flag testing

---

## for Loops

### General Format

```python
for target in object:    # Assign object items to target
    statements          # Repeated loop body
else:                   # Optional else
    statements         # Run if didn't exit via break
```

**How it works:**
1. Python assigns items from iterable object to target one by one
2. Executes loop body for each item
3. Target variable refers to current item
4. After loop, target refers to last item (unless `break` was used)

### Complete Format with Control Statements

```python
for target in object:    # Assign object items to target
    statements
    if test: break      # Exit loop now, skip else
    if test: continue   # Go to top of loop
else:
    statements         # Run on exit if no break
```

### Basic Examples

#### Example 1: Basic Usage
```python
>>> for x in ['app', 'script', 'program']:
...     print(x, end=' ')
app script program
```
**Explanation:**
- Iterates through list items from left to right
- `x` receives each item in turn
- Loop body executes once per item

#### Example 2: Sum and Product Calculations
```python
# Calculate sum
>>> sum = 0
>>> for x in [1, 2, 3, 4]:
...     sum = sum + x
>>> sum
10

# Calculate product  
>>> prod = 1
>>> for item in [1, 2, 3, 4]: 
...     prod *= item
>>> prod
24
```
**Explanation:**
- First loop accumulates sum: 0+1+2+3+4 = 10
- Second loop accumulates product: 1×1×2×3×4 = 24
- Variable names (`x`, `item`) are arbitrary

#### Example 3: Other Data Types
```python
>>> S = 'Python'
>>> T = ('web', 'num', 'app')

>>> for x in S: print(x, end=' ')  # Iterate over string
P y t h o n

>>> for x in T: print(x, end=' ')  # Iterate over tuple  
web num app
```
**Explanation:**
- `for` works on any sequence type
- Strings iterate character by character
- Tuples iterate item by item

### Tuple Assignment in for Loops

#### Example 1: Basic Tuple Unpacking
```python
>>> T = [(1, 2), (3, 4), (5, 6)]
>>> for (a, b) in T:    # Tuple assignment
...     print(a, b)
1 2
3 4  
5 6
```
**Explanation:**
- Each iteration unpacks a tuple: `(a, b) = (1, 2)`, etc.
- First iteration: `a=1, b=2`
- Second iteration: `a=3, b=4`
- Third iteration: `a=5, b=6`

**Alternative syntax (parentheses optional):**
```python
>>> for [a, b] in T: ...    # List syntax works too
>>> for a, b in T: ...      # Parentheses optional
```

#### Example 2: Dictionary Iteration
```python
>>> D = {'a': 1, 'b': 2}

# Basic key iteration
>>> for key in D:
...     print(key, '=>', D[key])  # Use dict indexing
a => 1
b => 2

# Using items() method
>>> list(D.items())
[('a', 1), ('b', 2)]

>>> for (key, value) in D.items():
...     print(key, '=>', value)   # Iterate over key-value tuples
a => 1  
b => 2
```
**Explanation:**
- `D.items()` returns key-value pairs as tuples
- Tuple assignment unpacks each `(key, value)` pair
- More efficient than indexing with `D[key]`

#### Example 3: Manual Assignment Alternative
```python
>>> T = [(1, 2), (3, 4), (5, 6)]
>>> for both in T:
...     a, b = both     # Manual assignment
...     print(a, b)
1 2
3 4
5 6
```

#### Example 4: Nested Structure Unpacking
```python
>>> ((a, b), c) = ((1, 2), 3)  # Nested sequence assignment
>>> a, b, c
(1, 2, 3)

>>> for ((a, b), c) in [((1, 2), 3), ((4, 5), 6)]:
...     print(a, b, c)
1 2 3
4 5 6

# Works with mixed types
>>> for ((a, b), c) in [([1, 2], 3), ['XY', 6]]:
...     print(a, b, c)  
1 2 3
X Y 6
```

### Extended-Unpacking Assignment in for Loops

#### Example 1: Starred Names
```python
>>> a, *b, c = (1, 2, 3, 4)
>>> a, b, c
(1, [2, 3], 4)

>>> for (a, *b, c) in [(1, 2, 3, 4), (5, 6, 7, 8)]:
...     print(a, b, c)
1 [2, 3] 4
5 [6, 7] 8
```
**Explanation:**
- `*b` collects middle items into a list
- `a` gets first item, `c` gets last item
- Useful for extracting specific columns from data

#### Example 2: Slicing Alternative
```python
>>> for all in [(1, 2, 3, 4), (5, 6, 7, 8)]:
...     a, b, c = all[0], all[1:-1], all[-1]
...     print(a, b, c)
1 (2, 3) 4
5 (6, 7) 8
```
**Explanation:**
- Achieves similar result using slicing
- Slicing returns type-specific result (tuple here)
- Starred targets always return lists

#### Example 3: Complex Unpacking (Advanced)
```python
>>> L, M = [1, 2], [3, 4]
>>> pairs = [[(5, 6), (7, 8), (9, 10)]] * 2

>>> for [(a, *X), (b, *L[0]), (c, *M[:0])] in pairs:
...     print(f'<{a=} {X=}> <{b=} {L=}> <{c=} {M=}>')
<a=5 X=[6]> <b=7 L=[[8], 2]> <c=9 M=[10, 3, 4]>
<a=5 X=[6]> <b=7 L=[[8], 2]> <c=9 M=[10, 10, 3, 4]>
```

### Nested for Loops

#### Example 1: Basic Nesting
```python
>>> for x in 'abc':     # Outer loop
...     for y in '123': # Inner loop  
...         print(x + y, end=' ')  # Combine items
a1 a2 a3 b1 b2 b3 c1 c2 c3
```
**Explanation:**
- Inner loop runs completely for each outer loop iteration
- For `x='a'`: prints `a1`, `a2`, `a3`
- For `x='b'`: prints `b1`, `b2`, `b3`  
- For `x='c'`: prints `c1`, `c2`, `c3`

#### Example 2: Search with Loop else
```python
>>> items = ['aaa', 111, (4, 5), 2.01]  # A list of objects
>>> tests = [(4, 5), 3.14]              # Keys to search for

>>> for key in tests:          # For each key
...     for item in items:     # For each item
...         if item == key:    # Check for match
...             print(key, 'was found')
...             break
...     else:
...         print(key, 'not found!')
(4, 5) was found
3.14 not found!
```
**Explanation:**
- Outer loop: iterates through search keys
- Inner loop: searches for current key in items list
- `break` exits inner loop when match found
- `else` (aligned with inner `for`) runs if no `break` occurred
- Critical: `else` belongs to inner loop, not outer `for` or `if`

#### Example 3: Simplified with 'in' Operator
```python
>>> for key in tests:      # For each key
...     if key in items:   # Let Python do the search
...         print(key, 'was found')
...     else:
...         print(key, 'not found!')
(4, 5) was found
3.14 not found!
```
**Explanation:**
- `in` operator replaces inner loop
- More concise and often faster
- Let Python do the work when possible

#### Example 4: Building Results List
```python
>>> seq1 = 'trippy'
>>> seq2 = 'python'

>>> res = []                # Start with empty list
>>> for x in seq1:          # Scan first sequence
...     if x in seq2:       # Common item?
...         res.append(x)   # Add to results
>>> res
['t', 'p', 'p', 'y']
```
**Explanation:**
- Finds common items between two sequences
- Preserves order and duplicates from first sequence
- Could be generalized into a reusable function

**Alternative approaches:**
```python
# Using set intersection (loses order, drops duplicates)
>>> list(set(seq1) & set(seq2))
['p', 'y', 't']

# Using list comprehension (next chapter topic)
>>> [x for x in seq1 if x in seq2]
['t', 'p', 'p', 'y']
```

---

## Loop Coding Techniques

### General Guidelines
1. Use `for` instead of `while` when possible (simpler, often faster)
2. Don't use `range` in `for` loops except as last resort
3. Let Python automate iteration work
4. Resist temptation to count things manually

### Counter Loops: range

#### Basic range Usage
```python
>>> list(range(5))                    # One argument: 0 to N-1
[0, 1, 2, 3, 4]

>>> list(range(2, 5))                 # Two arguments: start to stop-1  
[2, 3, 4]

>>> list(range(0, 10, 2))            # Three arguments: start, stop, step
[0, 2, 4, 6, 8]
```

#### range Properties and Limitations
```python
>>> range(5)[2]                      # Supports indexing
2
>>> range(5)[1:3]                    # Supports slicing
range(1, 3)
>>> list(range(5)) + [6, 7]         # Can concatenate with lists
[0, 1, 2, 3, 4, 6, 7]

>>> range(5) + [6, 7]                # But can't add range + list
TypeError: unsupported operand type(s) for +: 'range' and 'list'
```

#### Advanced range Examples
```python
>>> list(range(-5, 5))               # Negative ranges
[-5, -4, -3, -2, -1, 0, 1, 2, 3, 4]

>>> list(range(5, -5, -1))           # Reverse with negative step
[5, 4, 3, 2, 1, 0, -1, -2, -3, -4]
```

#### Simple Repetition
```python
>>> for i in range(3):
...     print(i, 'Pythons')
0 Pythons
1 Pythons  
2 Pythons
```
**Explanation:**
- `range(3)` produces 0, 1, 2
- Loop body executes 3 times
- `i` holds current iteration number

### Sequence Scans: while vs range vs for

#### Best Practice: Simple for Loop
```python
>>> X = 'hack'
>>> for item in X: print(item, end=' ')
h a c k
```
**Why this is best:**
- Simplest code
- Fastest execution
- Python handles iteration automatically

#### Manual Indexing with while
```python
>>> i = 0
>>> while i < len(X):
...     print(X[i], end=' ')
...     i += 1
h a c k

# Alternative with walrus operator
>>> i = -1  
>>> while (i := i + 1) < len(X):
...     print(X[i], end=' ')
h a c k
```

#### Manual Indexing with for and range
```python
>>> X = 'hack'
>>> len(X)
4
>>> list(range(len(X)))
[0, 1, 2, 3]

>>> for i in range(len(X)): 
...     print(X[i], end=' ')
h a c k
```
**Explanation:**
- `range(len(X))` generates indexes: [0, 1, 2, 3]
- Must index back into `X` to get items
- More complex than needed for simple iteration

### Sequence Shufflers: range and len

#### Example 1: Rotating String
```python
>>> S = 'hack'
>>> for i in range(len(S)):    # For repeat count
...     S = S[1:] + S[:1]      # Move front item to end
...     print(S, end=' ')
ackh ckha khac hack
```
**Explanation:**
- Each iteration: `S[1:]` (all but first) + `S[:1]` (first char)
- Iteration 1: `'ack' + 'h'` = `'ackh'`
- Iteration 2: `'ckh' + 'a'` = `'ckha'`
- etc.

#### Example 2: Non-Destructive Rotation
```python
>>> S = 'hack'
>>> for i in range(len(S)):    # For positions
...     X = S[i:] + S[:i]      # Rear part + front part
...     print(X, end=' ')
hack ackh ckha khac
```
**Explanation:**
- Creates new string each time without modifying original
- Iteration 0: `S[0:] + S[:0]` = `'hack' + ''` = `'hack'`
- Iteration 1: `S[1:] + S[:1]` = `'ack' + 'h'` = `'ackh'`
- etc.

#### Example 3: Works on Any Sequence Type
```python
>>> L = [1, 2, 3, 4]
>>> for i in range(len(L)):
...     X = L[i:] + L[:i]      # Works on any sequence
...     print(X, end=' ')
[1, 2, 3, 4] [2, 3, 4, 1] [3, 4, 1, 2] [4, 1, 2, 3]
```

### Skipping Items: range vs Slices

#### Using range to Skip Items
```python
>>> S = 'abcdefghijk'
>>> list(range(0, len(S), 2))        # Every second index
[0, 2, 4, 6, 8, 10]

>>> for i in range(0, len(S), 2): 
...     print(S[i], end=' ')
a c e g i k
```

#### Better Approach: Extended Slicing
```python
>>> S = 'abcdefghijk'
>>> for c in S[::2]:                 # Every second character
...     print(c, end=' ')
a c e g i k
```
**Advantages of slicing:**
- Much simpler to write and read
- Less code

**Advantage of range:**
- Uses less memory (no copy made)
- May matter for very large sequences

### Changing Lists: range vs Comprehensions

#### Problem: This Doesn't Work
```python
>>> L = [10, 20, 30, 40, 50]
>>> for x in L:
...     x += 1          # Changes x, not L
>>> L                   # L is unchanged
[10, 20, 30, 40, 50]
>>> x                   # x is not part of L
51
```
**Why it fails:**
- `x` refers to integer object from list
- `x += 1` makes `x` refer to new integer
- Original list objects unchanged

#### Solution 1: Using range for Indexing
```python
>>> L = [10, 20, 30, 40, 50]
>>> for i in range(len(L)):  # Add one to each item
...     L[i] += 1            # Or L[i] = L[i] + 1
>>> L
[11, 21, 31, 41, 51]
```
**Why this works:**
- `i` gets index positions: 0, 1, 2, 3, 4
- `L[i] += 1` modifies list item at position `i`
- Actually changes the list in place

#### Solution 2: Equivalent while Loop
```python
>>> i = 0
>>> while i < len(L):        # Add one more to each
...     L[i] += 1
...     i += 1
>>> L
[12, 22, 32, 42, 52]
```

#### Solution 3: List Comprehension (Preview)
```python
>>> [x + 1 for x in L]       # Create new list
[13, 23, 33, 43, 53]
```
**Differences:**
- Creates new list rather than modifying original
- Often faster than explicit loops
- Topic of next chapter

### Parallel Traversals: zip

#### Basic zip Usage
```python
>>> L1 = [1, 2, 3, 4]
>>> L2 = [5, 6, 7, 8]

>>> zip(L1, L2)                      # zip object (iterable)
<zip object at 0x026523C8>

>>> list(zip(L1, L2))                # Convert to list to see all
[(1, 5), (2, 6), (3, 7), (4, 8)]
```

#### Parallel Iteration
```python
>>> for (x, y) in zip(L1, L2):
...     print(f'{x} + {y} => {x + y}')
1 + 5 => 6
2 + 6 => 8  
3 + 7 => 10
4 + 8 => 12
```
**Explanation:**
- `zip` pairs up items from both lists
- Tuple assignment unpacks each pair
- Much cleaner than manual indexing

#### Manual Alternative (Less Preferred)
```python
>>> i = -1
>>> while (i := i + 1) < len(L1):
...     print(f'{L1[i]} + {L2[i]} => {L1[i] + L2[i]}')
1 + 5 => 6
2 + 6 => 8
3 + 7 => 10  
4 + 8 => 12
```

#### zip with Different Types
```python
>>> list(zip(range(4), 'hack'))
[(0, 'h'), (1, 'a'), (2, 'c'), (3, 'k')]
```

#### zip with Multiple Arguments
```python
>>> T1, T2, T3 = (1, 2, 3), (4, 5, 6), (7, 8, 9)
>>> list(zip(T1, T2, T3))            # 3 arguments, 3-item tuples
[(1, 4, 7), (2, 5, 8), (3, 6, 9)]

>>> list(zip(T1, T2))                # 2 arguments, 2-item tuples  
[(1, 4), (2, 5), (3, 6)]
```
**Rule:** For N arguments with M items each, zip gives M tuples of N items.

#### zip Truncation Behavior
```python
>>> S1 = 'abc'
>>> S2 = 'xyz123' 

>>> list(zip(S1, S2))                # Truncates to shortest
[('a', 'x'), ('b', 'y'), ('c', 'z')]
```
**Important:** `zip` stops when shortest sequence is exhausted.

#### Dictionary Construction with zip
```python
>>> keys = ['app', 'script', 'program']
>>> vals = [1, 3, 5]

# Method 1: Loop with zip
>>> list(zip(keys, vals))
[('app', 1), ('script', 3), ('program', 5)]

>>> D2 = {}
>>> for (k, v) in zip(keys, vals): 
...     D2[k] = v
>>> D2
{'app': 1, 'script': 3, 'program': 5}

# Method 2: dict constructor (preferred)
>>> D3 = dict(zip(keys, vals))
>>> D3
{'app': 1, 'script': 3, 'program': 5}

# Method 3: Dictionary comprehension (preview)
>>> {k: v for (k, v) in zip(keys, vals)}
{'app': 1, 'script': 3, 'program': 5}
```

### Offsets and Items: enumerate

#### Manual Counter Approach
```python
>>> S = 'hack'
>>> offset = 0
>>> for item in S:
...     print(item, 'appears at offset', offset)
...     offset += 1
h appears at offset 0
a appears at offset 1
c appears at offset 2  
k appears at offset 3
```

#### Better Approach: enumerate
```python
>>> S = 'hack'
>>> for (offset, item) in enumerate(S):
...     print(item, 'appears at offset', offset)
h appears at offset 0
a appears at offset 1
c appears at offset 2
k appears at offset 3
```
**Advantages:**
- No manual counter management
- Cleaner, less error-prone code
- Automatic iteration with position info

#### How enumerate Works
```python
>>> E = enumerate(S)
>>> E
<enumerate object at 0x10ebd7880>

>>> next(E)              # Manual iteration
(0, 'h')
>>> next(E)
(1, 'a')  
>>> next(E)
(2, 'c')
```

#### enumerate in Other Contexts
```python
# List comprehension
>>> [c * i for (i, c) in enumerate(S)]
['', 'a', 'cc', 'kkk']

# File processing  
>>> for (ix, line) in enumerate(open('data.txt')):
...     print(f'{ix}) {line.rstrip()}')
0) Testing file IO
1) Learning Python, 6E  
2) Python 3.12
```

---

## Chapter Summary

### Key Concepts Covered

#### **Loop Statements**
- **`while`**: Most general loop, controlled by test condition
- **`for`**: Specialized for iterating over sequences and iterables

#### **Loop Control**
- **`break`**: Exit loop immediately, skip `else` clause
- **`continue`**: Jump to loop start, skip rest of current iteration  
- **`pass`**: Empty placeholder statement
- **Loop `else`**: Runs only if loop exits normally (no `break`)

#### **Built-in Functions for Loops**
- **`range(start, stop, step)`**: Generates integer sequences
- **`zip(*iterables)`**: Pairs items from multiple sequences  
- **`enumerate(iterable)`**: Provides both indexes and items

#### **Best Practices**
1. Prefer `for` over `while` when iterating sequences
2. Use simple `for item in sequence` when possible
3. Reserve `range` for when you need indexes or counters
4. Use `zip` for parallel iteration over multiple sequences
5. Use `enumerate` when you need both items and their positions
6. Let Python do the iteration work automatically
7. Use loop `else` to catch "normal completion" scenarios

### **Common Patterns and Idioms**

#### **Search Pattern with Loop else**
```python
for item in collection:
    if found_what_looking_for(item):
        process_found_item(item)
        break
else:
    handle_not_found_case()
```

#### **Parallel Processing**
```python
for x, y, z in zip(list1, list2, list3):
    process_together(x, y, z)
```

#### **Indexed Iteration**
```python
for i, item in enumerate(sequence):
    process_with_index(i, item)
```

#### **Dictionary Key-Value Iteration**
```python
for key, value in dictionary.items():
    process_pair(key, value)
```

### **Performance Considerations**

#### **Memory Usage**
- `range`, `zip`, `enumerate` are iterators (generate on demand)
- Don't force to lists unless you need all items at once
- Slicing creates copies; iteration doesn't

#### **Speed Comparisons**
1. **Fastest**: Simple `for` loop over sequence
2. **Fast**: `for` with `range`, `zip`, `enumerate`
3. **Slower**: `while` loops with manual indexing
4. **Slowest**: Complex nested manual indexing

### **Detailed Examples and Exercises**

#### **Exercise 1: Prime Number Detection (Complete Analysis)**

```python
def is_prime(num):
    """
    Determine if a positive integer is prime.
    Returns True if prime, False otherwise.
    """
    if num < 2:
        return False
    
    # Check for factors from 2 to sqrt(num)
    x = num // 2
    while x > 1:
        if num % x == 0:  # Found a factor
            return False
        x -= 1
    return True  # No factors found

# Test cases
test_numbers = [1, 2, 3, 4, 5, 17, 18, 19, 20, 25]
for num in test_numbers:
    result = "prime" if is_prime(num) else "not prime"
    print(f"{num} is {result}")
```

**Output Analysis:**
```
1 is not prime     # By definition, 1 is not prime
2 is prime         # Smallest prime number
3 is prime         # No factors other than 1 and 3
4 is not prime     # 4 = 2 × 2
5 is prime         # No factors other than 1 and 5
17 is prime        # No factors found
18 is not prime    # 18 = 2 × 9, 3 × 6
19 is prime        # No factors found
20 is not prime    # 20 = 4 × 5, 2 × 10
25 is not prime    # 25 = 5 × 5
```

**Algorithm Explanation:**
- Starts checking from `num // 2` down to 2
- If any number divides evenly (`num % x == 0`), it's not prime
- Uses loop `else` pattern: if no `break` occurs, number is prime
- Edge case: numbers < 2 are not prime by definition

#### **Exercise 2: String Pattern Matching**

```python
def find_pattern_positions(text, pattern):
    """
    Find all starting positions where pattern occurs in text.
    Returns list of positions (0-based indexing).
    """
    positions = []
    text_len, pattern_len = len(text), len(pattern)
    
    for i in range(text_len - pattern_len + 1):
        # Check if pattern matches at position i
        match = True
        for j in range(pattern_len):
            if text[i + j] != pattern[j]:
                match = False
                break
        if match:
            positions.append(i)
    
    return positions

# Example usage
text = "abcabcabcabc"
pattern = "abc"
positions = find_pattern_positions(text, pattern)
print(f"Pattern '{pattern}' found at positions: {positions}")

# Demonstrate with enumeration
for i, pos in enumerate(positions):
    print(f"Match {i+1}: starts at position {pos}")
    print(f"  Text slice: '{text[pos:pos+len(pattern)]}'")
```

**Output:**
```
Pattern 'abc' found at positions: [0, 3, 6, 9]
Match 1: starts at position 0
  Text slice: 'abc'
Match 2: starts at position 3  
  Text slice: 'abc'
Match 3: starts at position 6
  Text slice: 'abc'
Match 4: starts at position 9
  Text slice: 'abc'
```

#### **Exercise 3: Data Processing with Multiple Techniques**

```python
# Sample data: student records
students = ['Alice', 'Bob', 'Charlie', 'Diana']
scores = [85, 92, 78, 96]
grades = ['B', 'A', 'C', 'A']

print("=== Method 1: Using enumerate ===")
for i, student in enumerate(students):
    print(f"{i+1}. {student}: {scores[i]} ({grades[i]})")

print("\n=== Method 2: Using zip ===")
for student, score, grade in zip(students, scores, grades):
    print(f"{student}: {score} ({grade})")

print("\n=== Method 3: Using zip with enumerate ===")
for i, (student, score, grade) in enumerate(zip(students, scores, grades)):
    print(f"#{i+1}: {student} scored {score} (grade {grade})")

print("\n=== Method 4: Creating dictionary ===")
student_data = dict(zip(students, zip(scores, grades)))
for student, (score, grade) in student_data.items():
    print(f"{student}: {score} points, grade {grade}")

# Analysis: Find students with A grades
print("\n=== Students with A grades ===")
a_students = []
for student, score, grade in zip(students, scores, grades):
    if grade == 'A':
        a_students.append((student, score))

for student, score in a_students:
    print(f"{student}: {score}")

# Calculate class statistics
total_score = sum(scores)
avg_score = total_score / len(scores)
print(f"\nClass average: {avg_score:.1f}")

# Find highest and lowest scores
max_score = max(scores)
min_score = min(scores)
print(f"Highest score: {max_score}")
print(f"Lowest score: {min_score}")
```

#### **Exercise 4: Matrix Operations**

```python
def print_matrix(matrix, title="Matrix"):
    """Pretty print a 2D matrix."""
    print(f"\n{title}:")
    for row in matrix:
        print("  ", end="")
        for item in row:
            print(f"{item:4}", end=" ")
        print()  # New line after each row

# Create sample matrices
matrix_a = [
    [1, 2, 3],
    [4, 5, 6], 
    [7, 8, 9]
]

matrix_b = [
    [9, 8, 7],
    [6, 5, 4],
    [3, 2, 1]
]

print_matrix(matrix_a, "Matrix A")
print_matrix(matrix_b, "Matrix B")

# Matrix addition using nested loops
def add_matrices(m1, m2):
    """Add two matrices of the same size."""
    result = []
    for i in range(len(m1)):
        row = []
        for j in range(len(m1[i])):
            row.append(m1[i][j] + m2[i][j])
        result.append(row)
    return result

# Alternative using zip
def add_matrices_zip(m1, m2):
    """Add matrices using zip for cleaner code."""
    result = []
    for row1, row2 in zip(m1, m2):
        new_row = []
        for val1, val2 in zip(row1, row2):
            new_row.append(val1 + val2)
        result.append(new_row)
    return result

# Demonstrate both methods
sum_matrix1 = add_matrices(matrix_a, matrix_b)
sum_matrix2 = add_matrices_zip(matrix_a, matrix_b)

print_matrix(sum_matrix1, "Sum (method 1)")
print_matrix(sum_matrix2, "Sum (method 2)")

# Matrix traversal with coordinates
print("\n=== Matrix coordinates and values ===")
for i, row in enumerate(matrix_a):
    for j, value in enumerate(row):
        print(f"Position ({i},{j}): {value}")
```

#### **Exercise 5: File Processing Simulation**

```python
# Simulate file content (in real code, you'd use: open('filename.txt'))
file_lines = [
    "# Configuration file",
    "server_name = localhost", 
    "port = 8080",
    "# Database settings",
    "db_host = 192.168.1.100",
    "db_port = 5432",
    "debug = True",
    "# End of file"
]

print("=== Processing configuration file ===")

# Method 1: Simple iteration
config = {}
for line in file_lines:
    line = line.strip()  # Remove whitespace
    if line and not line.startswith('#'):  # Skip empty lines and comments
        if '=' in line:
            key, value = line.split('=', 1)  # Split on first '=' only
            config[key.strip()] = value.strip()

print("Parsed configuration:")
for key, value in config.items():
    print(f"  {key}: {value}")

# Method 2: With line numbers using enumerate
print("\n=== Line-by-line analysis ===")
comment_lines = []
config_lines = []
blank_lines = []

for line_num, line in enumerate(file_lines, 1):  # Start counting from 1
    stripped = line.strip()
    if not stripped:
        blank_lines.append(line_num)
    elif stripped.startswith('#'):
        comment_lines.append(line_num)
    elif '=' in stripped:
        config_lines.append(line_num)
    
    print(f"Line {line_num:2}: {line}")

print(f"\nSummary:")
print(f"  Comment lines: {comment_lines}")
print(f"  Config lines:  {config_lines}")
print(f"  Blank lines:   {blank_lines}")
print(f"  Total lines:   {len(file_lines)}")
```

#### **Exercise 6: Advanced Loop Patterns**

```python
# Pattern 1: Loop with early termination
def find_first_negative(numbers):
    """Find the first negative number and its position."""
    for i, num in enumerate(numbers):
        if num < 0:
            return i, num
    return None, None  # No negative number found

# Pattern 2: Loop with multiple conditions
def process_until_condition(data, max_items=5, stop_value=None):
    """Process items until max reached or stop value found."""
    processed = []
    for i, item in enumerate(data):
        if i >= max_items:
            print(f"Stopped: reached maximum {max_items} items")
            break
        if item == stop_value:
            print(f"Stopped: found stop value '{stop_value}'")
            break
        processed.append(item * 2)  # Some processing
    else:
        print("Stopped: end of data reached")
    return processed

# Pattern 3: Nested loops with labeled breaks (using functions)
def find_in_matrix(matrix, target):
    """Find target value in 2D matrix, return coordinates."""
    for i, row in enumerate(matrix):
        for j, value in enumerate(row):
            if value == target:
                return i, j  # Found it, return coordinates
    return None  # Not found

# Test the patterns
test_numbers = [5, 3, 8, -2, 1, -7, 4]
pos, val = find_first_negative(test_numbers)
if pos is not None:
    print(f"First negative: {val} at position {pos}")

test_data = ['a', 'b', 'c', 'd', 'STOP', 'e', 'f']
result1 = process_until_condition(test_data, stop_value='STOP')
print(f"Result 1: {result1}")

result2 = process_until_condition(test_data, max_items=3)
print(f"Result 2: {result2}")

# Test matrix search
test_matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

coord = find_in_matrix(test_matrix, 5)
if coord:
    print(f"Found 5 at row {coord[0]}, column {coord[1]}")
```

### **Common Pitfalls and Solutions**

#### **Pitfall 1: Modifying List While Iterating**
```python
# WRONG: This can skip items or cause errors
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)  # Dangerous!

# CORRECT: Iterate over copy or use different approach
numbers = [1, 2, 3, 4, 5]

# Solution 1: Iterate over copy
for num in numbers[:]:  # numbers[:] creates a copy
    if num % 2 == 0:
        numbers.remove(num)

# Solution 2: Build new list
numbers = [1, 2, 3, 4, 5]
numbers = [num for num in numbers if num % 2 != 0]

# Solution 3: Use reverse iteration with indexes
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers) - 1, -1, -1):
    if numbers[i] % 2 == 0:
        del numbers[i]
```

#### **Pitfall 2: Wrong Loop Variable Scope**
```python
# Problem: Loop variable persists after loop
for i in range(3):
    print(f"Loop iteration {i}")
print(f"After loop, i = {i}")  # i is still 2!

# Solution: Use more descriptive names and be aware
for iteration in range(3):
    print(f"Loop iteration {iteration}")
# 'iteration' still exists here but name makes it clearer
```

#### **Pitfall 3: Incorrect use of Loop else**
```python
# WRONG: else runs when you might not expect
for x in []:  # Empty sequence
    print("This never runs")
else:
    print("This runs because no break occurred")

# Understanding: else runs if loop completes normally
# (even if body never executed)
```

### **Advanced Applications**

#### **Combination and Permutation Generator**
```python
def generate_combinations(items, r):
    """Generate all combinations of r items from the list."""
    if r == 0:
        yield []
        return
    
    for i in range(len(items)):
        for combo in generate_combinations(items[i+1:], r-1):
            yield [items[i]] + combo

# Example usage
letters = ['A', 'B', 'C', 'D']
print("Combinations of 2 letters:")
for combo in generate_combinations(letters, 2):
    print(combo)
```

#### **State Machine Implementation**
```python
def simple_parser(text):
    """Simple state machine parser example."""
    state = 'NORMAL'
    result = []
    i = 0
    
    while i < len(text):
        char = text[i]
        
        if state == 'NORMAL':
            if char == '"':
                state = 'IN_STRING'
                result.append('STRING_START')
            elif char == ' ':
                pass  # Skip spaces
            else:
                result.append(f'CHAR:{char}')
                
        elif state == 'IN_STRING':
            if char == '"':
                state = 'NORMAL'
                result.append('STRING_END')
            else:
                result.append(f'STR_CHAR:{char}')
        
        i += 1
    
    return result

# Test the parser
test_input = 'hello "world of code" end'
tokens = simple_parser(test_input)
for token in tokens:
    print(token)
```

### **Performance Tips and Tricks**

#### **Tip 1: Use Built-ins When Possible**
```python
# Slower: Manual sum calculation
numbers = range(1000000)
total = 0
for num in numbers:
    total += num

# Faster: Built-in sum function
total = sum(range(1000000))

# Slower: Manual max finding
max_val = numbers[0]
for num in numbers[1:]:
    if num > max_val:
        max_val = num

# Faster: Built-in max function
max_val = max(numbers)
```

#### **Tip 2: Choose Right Loop Type**
```python
# For simple iteration: use for
items = ['a', 'b', 'c', 'd']

# Good
for item in items:
    process(item)

# Less good (unnecessary complexity)
i = 0
while i < len(items):
    process(items[i])
    i += 1

# For complex conditions: while might be better
while complex_condition_check() and other_condition():
    do_something()
```

---

## **Chapter Review Questions**

### **Conceptual Questions**
1. What's the difference between `break` and `continue`?
2. When does a loop's `else` clause execute?
3. Why might you choose `for` over `while` for sequence iteration?
4. What happens when `zip` gets sequences of different lengths?
5. How does `enumerate` differ from `range(len(sequence))`?

### **Practical Exercises**
1. Write a function to find the longest word in a sentence
2. Create a program that prints a multiplication table using nested loops
3. Implement a simple guessing game using `while` and `break`
4. Write code to transpose a matrix using `zip`
5. Create a function that counts word frequencies in text

### **Debugging Challenges**
1. Fix code that tries to modify a list while iterating over it
2. Correct a loop that should stop at first match but continues
3. Debug nested loops where `break` doesn't work as expected

---

## **Next Chapter Preview**

The next chapter (Chapter 14) will cover:
- **List Comprehensions**: Concise syntax for creating lists
- **Iteration Protocol**: How Python's iteration actually works
- **Generator Expressions**: Memory-efficient iterations
- **Advanced Iteration Tools**: More sophisticated looping constructs

These concepts build directly on the loop foundations covered here, providing more Pythonic and efficient ways to process data.
