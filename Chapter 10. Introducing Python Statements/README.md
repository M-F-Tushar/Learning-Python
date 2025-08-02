# Chapter 10: Introducing Python Statements

## Overview
This chapter introduces Python's fundamental statement forms and syntax rules. Statements are the code we write to tell Python what our programs should do - they specify the actions and logic that make up a program.

---

## 1. The Python Conceptual Hierarchy

Understanding how Python code is organized:

1. **Programs** are composed of modules
2. **Modules** contain statements  
3. **Statements** contain expressions
4. **Expressions** create and process objects

**Key Points:**
- Statements code the larger logic of program operation
- Expressions are embedded within statements
- Statements create objects and direct how expressions process them
- All statements exist within modules

---

## 2. Python's Complete Statement Set

| Statement | Role | Example |
|-----------|------|---------|
| **Assignment** | Creating references | `a, b = 'python', 3.12` |
| **Calls/expressions** | Running functions | `log.write('app crash')` |
| **print** | Printing objects | `print(hack, code, file=log)` |
| **if/elif/else** | Selecting actions | `if 'python' in text: read(text)` |
| **match/case** | Multiway selections | `match edition: case 6: print(2024)` |
| **for/else** | Iteration | `for x in myiterable: print(x)` |
| **while/else** | General loops | `while x := file.readline(): print(x)` |
| **pass** | Empty placeholder | `if 'python' not in text: pass` |
| **break** | Loop exit | `while True: if exittest(): break` |
| **continue** | Loop continue | `while True: if skiptest(): continue` |
| **def** | Functions/methods | `def f(a, b, c=2, *more): print(a + b + c)` |
| **return** | Function results | `def f(a, b, c=2, *more): return a + b + c` |
| **yield** | Generator functions | `def gen(n): for i in n: yield i*2` |
| **global** | Namespaces | `x = 1; def function(): global x; x = 2` |
| **nonlocal** | Namespaces | `def outer(): x = 1; def inner(): nonlocal x; x = 2` |
| **async** | Coroutine designator | `async def consumer(a, b): await producer()` |
| **await** | Coroutine transfer | `await asyncio.sleep(1)` |
| **import** | Module access | `import sys` |
| **from** | Attribute access | `from sys import stdin as f` |
| **class** | Building objects | `class Subclass(Superclass): classAttr = []` |
| **try/except/finally** | Exception handling | `try: action() except: print('action error')` |
| **raise** | Triggering exceptions | `raise EndSearch(location)` |
| **assert** | Debugging checks | `assert X > Y, 'X too small'` |
| **with** | Context managers | `with open('data') as file: process(file)` |
| **del** | Deleting references | `del data[k]; del obj.attr` |
| **type** | Type hinting alias | `type vector = list[float]` |

### Important Notes:
- **Assignment** comes in many forms (basic, sequence, augmented)
- **print** is actually a built-in function, not a reserved word
- **yield** and **await** are expressions, not statements (but often used as statement expressions)
- Most statement words are reserved and cannot be used as variables
- Some newer statements use "soft" reserved words (match, case, type)

---

## 3. Python vs C-like Languages: Syntax Comparison

### What C-like Languages Require:
```c
// C/C++/Java style
if (x > y) {
    x = 1;
    y = 2;
}
```

### Python Equivalent:
```python
# Python style
if x > y:
    x = 1
    y = 2
```

---

## 4. What Python Adds: The Colon

**Rule:** All compound statements follow this pattern:
```python
Header line:
    Nested statement block
```

**Example:**
```python
if x > y:        # Header line with colon
    x = 1        # Nested block
    y = 2        # Same indentation level
```

**Common Mistake:** Forgetting the colon
```python
>>> if x        # Missing colon - ERROR!
  File "<stdin>", line 1
    if x
       ^
SyntaxError: expected ':'
```

---

## 5. What Python Removes

### 5.1 Parentheses Are Optional

**C-style (required):**
```c
if (x < y)
```

**Python style (optional):**
```python
if x < y        # Preferred - no parentheses
if (x < y)      # Valid but not Pythonic
```

### 5.2 No Semicolons Required

**C-style:**
```c
x = 1;
```

**Python style:**
```python
x = 1          # No semicolon needed
x = 1;         # Valid but not Pythonic
```

**Rule:** End of line = end of statement

### 5.3 Indentation Defines Blocks

**C-style:**
```c
if (x > y) {
    x = 1;
    y = 2;
}
```

**Python style:**
```python
if x > y:
    x = 1      # Same indentation
    y = 2      # Same indentation
```

**Key Rules:**
- All statements in a block must be indented the same distance
- Python doesn't care how much you indent (spaces or tabs)
- Different blocks can have different indentation amounts
- Consistency within each block is required

---

## 6. Why Indentation Syntax?

### Benefits:
1. **Forces readable code** - Visual structure matches logical structure
2. **Prevents common errors** - No ambiguous else clauses
3. **Eliminates style wars** - No debates about brace placement
4. **WYSIWYG principle** - Code looks like it behaves

### Example of C Ambiguity:
```c
// Which if does the else belong to?
if (x)
    if (y)
        statement1;
else
    statement2;    // Actually belongs to inner if!
```

### Python Clarity:
```python
# Visual alignment shows logical structure
if x:
    if y:
        statement1
else:
    statement2     # Clearly belongs to outer if
```

### Indentation Error Example:
```python
>>> if True:
...     a = 1
...   b = 2        # Wrong indentation!
  File "<stdin>", line 3
    b = 2
    ^
IndentationError: unindent does not match any outer indentation level
```

---

## 7. Special Cases and Flexibility

### 7.1 Multiple Statements Per Line

**Rule:** Use semicolons as separators
```python
a = 1; b = 2; print(a + b)    # Three statements on one line
```

**Limitation:** Only simple statements, not compound ones
```python
# Valid
x = 1; y = 2; print(x + y)

# Invalid - compound statements need their own lines
if x > 0; print(x)    # ERROR!
```

### 7.2 Line Continuation

**Method 1: Bracketed pairs (preferred)**
```python
# Lists
mylist = [1111,    # Continuation lines
          2222,    # Any code in (), [], {}
          3333]

# Expressions  
X = (A + B +
     C + D)

# Compound statements
if (A == 1 and
    B == 2 and
    C == 3):
    print('hack' * 3)
```

**Method 2: Backslash (discouraged)**
```python
X = A + B + \
    C + D          # Error-prone, avoid this
```

**Why backslash is discouraged:**
- Hard to notice and maintain
- No spaces or comments allowed after backslash
- Brittle - easy to break accidentally

### 7.3 Single-line Compound Statements

**Rule:** Body can appear after colon on same line
```python
if x > y: print(x)                    # Single-line if
while x > 0: x -= 1                   # Single-line while
for i in range(5): print(i)           # Single-line for
```

**Limitations:**
- Only simple statements in body
- No nested compound statements
- else clauses must be on separate lines

---

## 8. Interactive Loop Examples

### 8.1 Basic Interactive Loop

```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    print(reply.upper())
```

**Components explained:**
- `while True:` - Infinite loop (True is always true)
- `input('Enter text:')` - Gets user input, returns string
- `if reply == 'stop': break` - Single-line if with break
- `break` - Exits the loop immediately
- `print(reply.upper())` - Converts to uppercase and prints

**Sample run:**
```
Enter text:python
PYTHON
Enter text:312
312
Enter text:stop
```

**Alternative using := operator (Python 3.8+):**
```python
while (reply := input('Enter text:')) != 'stop':
    print(reply.upper())
```

### 8.2 Math on User Inputs

**Problem:** Input is always a string
```python
>>> reply = '40'
>>> reply ** 2
TypeError: unsupported operand type(s) for ** or pow(): 'str' and 'int'
```

**Solution:** Convert to integer
```python
>>> int(reply) ** 2
1600
```

**Complete script:**
```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    print(int(reply) ** 2)
print('Bye')
```

**Sample run:**
```
Enter text:2
4
Enter text:40
1600
Enter text:stop
Bye
```

### 8.3 Handling Invalid Input - Method 1: Testing

**Problem:** Non-numeric input causes errors
```python
Enter text:xxx
ValueError: invalid literal for int() with base 10: 'xxx'
```

**Solution:** Test input first
```python
>>> S = '40'
>>> T = 'xxx'
>>> S.isdigit(), T.isdigit()
(True, False)
```

**Complete script with error checking:**
```python
while True:
    reply = input('Enter text:')
    if reply == 'stop':
        break
    elif not reply.isdigit():
        print('Bad!' * 8)
    else:
        print(int(reply) ** 2)
print('Bye')
```

**Structure analysis:**
- `if reply == 'stop':` - Check for exit condition
- `elif not reply.isdigit():` - Check for invalid input  
- `else:` - Process valid input
- All parts at same indentation level = single if statement
- Entire if block indented under while = part of loop

**Sample run:**
```
Enter text:5
25
Enter text:xxx
Bad!Bad!Bad!Bad!Bad!Bad!Bad!Bad!
Enter text:10
100
Enter text:stop
Bye
```

### 8.4 Handling Invalid Input - Method 2: Exception Handling

**Philosophy:** Try the operation, handle errors if they occur

```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    try:
        num = int(reply)
    except:
        print('Bad!' * 8)
    else:
        print(num ** 2)
print('Bye')
```

**try statement structure:**
- `try:` - Main block (attempt this code)
- `except:` - Exception handler (run if error occurs)
- `else:` - Success block (run if no error)
- All keywords at same indentation = single try statement

**Even more concise version:**
```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    try:
        print(int(reply) ** 2)
    except:
        print('Bad!' * 8)
print('Bye')
```

### 8.5 Supporting Floating-Point Numbers

**Problem:** `isdigit()` only works for integers
**Solution:** Use try/except with `float()`

```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    try:
        print(float(reply) ** 2)
    except:
        print('Bad!' * 8)
print('Bye')
```

**Sample run:**
```
Enter text:50
2500.0
Enter text:40.5
1640.25
Enter text:1.23E-100
1.5129e-200
Enter text:hack
Bad!Bad!Bad!Bad!Bad!Bad!Bad!Bad!
Enter text:stop
Bye
```

**Why this approach is better:**
- No `isfloat()` method exists
- Floating-point syntax is complex (scientific notation, etc.)
- Exception handling is more general and robust

### 8.6 Advanced: Using eval() for Any Expression

**Powerful but dangerous approach:**
```python
while True:
    reply = input('Enter text:')
    if reply == 'stop': break
    try:
        print(eval(reply))  # Can evaluate any Python expression
    except:
        print('Bad!' * 8)
print('Bye')
```

**Sample run:**
```
Enter text:2 ** 100
1267650600228229401496703205376
Enter text:3 + 4 * 5
23
Enter text:stop
Bye
```

**Security warning:** `eval()` can execute arbitrary code - only use with trusted input!

### 8.7 Three-Level Nesting Example

**Adding magnitude-based branching:**
```python
while True:
    reply = input('Enter text:')
    if reply == 'stop':
        break
    elif not reply.isdigit():
        print('Bad!' * 8)
    else:
        num = int(reply)
        if num < 20:           # Nested if statement
            print('low')
        else:
            print(num ** 2)
print('Bye')
```

**Nesting structure:**
- **Level 1:** while loop
- **Level 2:** if/elif/else statement  
- **Level 3:** inner if/else statement

**Sample run:**
```
Enter text:19
low
Enter text:20
400
Enter text:hack
Bad!Bad!Bad!Bad!Bad!Bad!Bad!Bad!
Enter text:stop
Bye
```

---

## 9. Key Programming Concepts Demonstrated

### 9.1 Statement Nesting
- Statements can be nested to any depth
- Indentation level determines nesting structure
- Inner statements inherit the context of outer statements

### 9.2 Error Handling Approaches
1. **Preventive (LBYL - Look Before You Leap):**
   - Test conditions before performing operations
   - Use methods like `isdigit()`, `isalpha()`, etc.
   
2. **Reactive (EAFP - Easier to Ask for Forgiveness than Permission):**
   - Attempt operation and handle exceptions
   - Use try/except blocks
   - More Pythonic for complex validations

### 9.3 Loop Control
- **Infinite loops:** `while True:`
- **Conditional exit:** `if condition: break`
- **Input validation:** Multiple approaches available
- **Graceful termination:** Exit messages and cleanup

### 9.4 User Interface Patterns
- **Prompt-response loops:** Common in command-line applications
- **Input validation:** Essential for robust programs  
- **Error messages:** User-friendly feedback for invalid input
- **Exit strategies:** Clear ways for users to quit

---

## 10. Best Practices Summary

### Syntax Style:
1. **Use colons** after compound statement headers
2. **Avoid unnecessary parentheses** around conditions  
3. **Don't use semicolons** at line ends
4. **Use consistent indentation** (4 spaces recommended)
5. **Keep statements on separate lines** for readability

### Error Handling:
1. **Use try/except** for complex validations
2. **Provide helpful error messages** to users
3. **Validate user input** before processing
4. **Plan exit strategies** for interactive programs

### Code Organization:
1. **Indent consistently** within blocks
2. **Use meaningful variable names**
3. **Keep nesting levels reasonable** (avoid deep nesting)
4. **Comment complex logic** when necessary

---

## 11. Common Beginner Mistakes

### Syntax Errors:
```python
# Missing colon
if x > y        # ERROR: expected ':'
    print(x)

# Inconsistent indentation  
if x > y:
    print(x)    # 4 spaces
  print(y)      # 2 spaces - ERROR!

# Wrong nesting
if x > y:
print(x)        # Not indented - not in if block!
```

### Logic Errors:
```python
# Infinite loop (forgot break condition)
while True:
    reply = input('Enter text:')
    print(reply.upper())
    # Missing: if reply == 'stop': break

# Wrong exception handling
try:
    result = int(input('Number: '))
    print(result)
except:
    print('Error')
    # This catches ALL exceptions, even KeyboardInterrupt!
```

### Best Practice Violations:
```python
# Not Pythonic
if (x > y):     # Unnecessary parentheses
    x = 1;      # Unnecessary semicolon

# Better
if x > y:
    x = 1
```

---

This chapter provides the foundation for understanding Python's statement syntax and structure. The examples progress from simple concepts to practical interactive programs, demonstrating how proper syntax enables clear, readable, and maintainable code.
