# Chapter 3: How You Run Programs

## Overview
This chapter covers all major ways to execute Python code, from interactive sessions to file execution. It's essential for understanding Python's execution model and setting up your development environment.

**Key Learning Objectives:**
- Master different ways to run Python code
- Understand interactive vs. file-based programming
- Learn module import concepts
- Set up proper development environment
- Practice debugging techniques

---

## 1. Installing Python

### Platform-Specific Installation
- **Windows & macOS**: Download self-installing executable from python.org
- **Linux/WSL**: Usually pre-installed, or install from distribution repositories
- **Mobile (Android/iOS)**: Install Python app from app store
- **Unix systems**: Often compile from source

### Checking Existing Installation
Before installing, check if Python is already present:
- **Windows**: Look in Start menu
- **All platforms**: Run Python command in terminal (covered in next section)

**Important**: This book uses **Python 3.12**, so choose the closest version available.

---

## 2. Interactive Code (REPL)

### 2.1 Starting an Interactive REPL

**REPL** = Read-Eval-Print Loop - the interactive Python command line

#### Platform-Specific Commands:
```bash
# Windows
$ py

# macOS/Linux/Android
$ python3

# Alternative (works almost everywhere)
$ python3
```

**Example Session:**
```python
$ python3
Python 3.12.3 (main, Apr 9 2024, 14:05:25)
Type "help", "copyright", "credits" or "license"
>>> print('Hello world!')
Hello world!
>>> print(2 ** 8)
256
>>> ^D  # Ctrl+D to exit (Ctrl+Z on Windows)
```

#### Exit Commands:
- **Unix/macOS/Linux/Android**: `Ctrl+D`
- **Windows**: `Ctrl+Z` (then Enter)

### 2.2 Setting Up Code Folders

**Recommended Directory Structure:**
```
your-code-folder/
├── Chapter03/
│   ├── script1.py
│   ├── module1.py
│   └── ...
├── Chapter04/
│   └── ...
└── ...
```

**Why This Matters:**
- Avoids filename collisions
- Simplifies import behavior
- Keeps work organized
- Required for book examples to work properly

#### Creating Folders:
```bash
# Command line (Windows & Unix)
mkdir LP6E
cd LP6E
mkdir Chapter03
cd Chapter03

# Or use your system's file explorer
```

### 2.3 REPL Conventions and Prompts

**Important: What NOT to Type:**
- `$` - System prompt (don't type this)
- `>>>` - Python prompt (don't type this)  
- `...` - Continuation prompt (don't type this)
- `#` comments - Optional (these are explanatory)

**Example of What You Actually Type:**
```python
>>> language = 'Python'    # You type: language = 'Python'
'Python'
>>> 2 ** 8                 # You type: 2 ** 8  
256
```

### 2.4 Running Code Interactively

#### Basic Examples:
```python
>>> print('Hello world!')
Hello world!
>>> print(2 ** 8)
256
>>> language = 'Python'
>>> language
'Python'
>>> 2 ** 8
256
```

**Key Points:**
- Each line executes immediately when you press Enter
- Results are displayed automatically (no need for `print` for expressions)
- Variables are created by assignment (`=`)
- REPL shows expression results automatically

#### String Operations Example:
```python
>>> 'Hack!' * 8
'Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!'
```
This demonstrates string repetition - `*` means repeat for strings.

#### Error Handling Example:
```python
>>> X
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'X' is not defined
```

**Learning Point**: Variables must be assigned before use. Python gives helpful error messages.

#### Module Import Example:
```python
>>> sys.ps1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'sys' is not defined. Did you forget to import 'sys'?

>>> import os
>>> os.getcwd()
'/Users/me/code'
```

### 2.5 Why Use Interactive Mode?

#### For Learning:
- Immediate feedback
- Quick experimentation
- Safe environment (hard to break anything)
- Perfect for testing small code snippets

#### For Testing:
- Test functions and modules interactively
- Import your own modules and test them
- Explore library functions
- Debug code components

---

## 3. Program Files (Scripts and Modules)

### 3.1 Creating Your First Script

**Example 3-1: script1.py**
```python
# A first Python script
import sys                 # Load a library module
print(sys.platform)        # Show platform name
print(2 ** 100)           # Raise 2 to a power
x = 'Hack!'
print(x * 8)              # String repetition
```

**Explanation of Each Line:**
1. `# A first Python script` - Comment (ignored by Python)
2. `import sys` - Loads the sys module for system information
3. `print(sys.platform)` - Shows what system you're on ('win32', 'darwin', 'linux')
4. `print(2 ** 100)` - Demonstrates large integer calculation
5. `x = 'Hack!'` - Creates a variable and assigns a string
6. `print(x * 8)` - Shows string repetition

**File Naming Rules:**
- Use `.py` extension for Python files
- Required for files you want to import
- Helps editors provide syntax highlighting
- Enables tap-to-run on some systems

### 3.2 Running Files with Command Lines

**Basic Execution:**
```bash
$ python3 script1.py
darwin
1267650600228229401496703205376
Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!
```

**Important Requirements:**
- Run from same directory as the script file
- Use system prompt (`$`), not Python prompt (`>>>`)
- Python must be in your PATH (usually automatic)

#### Command Variations:

**Output Redirection (save output to file):**
```bash
$ python3 script1.py > saveit.txt
```

**Windows Shortcut (filename associations):**
```bash
$ script1.py  # Automatically runs with Python
```

**Full Path Examples:**
```bash
# If Python not in PATH (macOS example)
$ /usr/local/bin/python3 /Users/me/code/script1.py

# Windows PowerShell with different directories
PS C:\Users\me\code> py D:\temp\script1.py
```

### 3.3 Alternative Ways to Run Files

#### File Icon Clicks
- **Windows**: Double-click in File Explorer (requires Python association)
- **macOS**: Right-click → Open With → Python Launcher
- **Linux**: Requires executable permission and `#!` line
- **Mobile**: Tap filename in file explorer (app-dependent)

**Limitation**: Output window closes immediately - use `input()` to pause:
```python
print("Hello World!")
input("Press Enter to exit...")  # Keeps window open
```

#### The IDLE GUI

**Starting IDLE:**
- **Windows**: Python → IDLE from Start menu
- **macOS**: Applications → Python → IDLE
- **Linux**: Command line or applications menu
- **Any platform**: `python3 -m idlelib.idle`

**IDLE Features:**
- **Shell window**: Interactive REPL with command recall
- **Edit windows**: For writing and editing code files
- **Run menu**: Execute scripts directly
- **Debug menu**: Built-in debugger
- **Auto-completion**: Tab completion and help balloons

**Running Files in IDLE:**
1. Open file: File → Open
2. Run file: Run → Run Module (F5)
3. Output appears in Shell window

**IDLE Advantages:**
- Beginner-friendly GUI
- Cross-platform consistency
- Integrated debugging
- Syntax highlighting

**IDLE Limitations:**
- Less flexible than command lines
- Additional learning curve
- May not suit advanced development needs

---

## 4. Running Code in Code (Imports and Modules)

### 4.1 Understanding Modules

**Key Concepts:**
- Every `.py` file is a module
- Modules can be imported by other modules
- Importing runs the code in the imported file
- Programs are typically collections of modules

### 4.2 Import Examples

**Basic Import (using script1.py):**
```python
$ python3
>>> import script1
darwin
1267650600228229401496703205376
Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!
```

**Important**: Run this in the directory containing `script1.py`

**Imports Run Only Once:**
```python
>>> import script1     # Runs the code
>>> import script1     # Does nothing (already imported)
```

### 4.3 Reloading Modules

**When You Need to Reload:**
- Modified the source file
- Want to run updated version
- Working in same REPL session

**How to Reload:**
```python
>>> from importlib import reload
>>> reload(script1)
darwin
1267650600228229401496703205376
Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!
<module 'script1' from '/Users/me/Code/script1.py'>
```

**Reload Requirements:**
- Module must be successfully imported first
- Use parentheses: `reload(modulename)`
- Returns module object (that's the extra output line)

### 4.4 Module Attributes

**Example 3-2: myfile.py**
```python
title = 'Learning Python, 6th Edition'
```

**Accessing Attributes - Method 1 (import):**
```python
>>> import myfile        # Loads module
>>> myfile.title        # Access attribute with dot notation
'Learning Python, 6th Edition'
```

**Accessing Attributes - Method 2 (from):**
```python
>>> from myfile import title  # Copy name directly
>>> title                     # Use as simple variable
'Learning Python, 6th Edition'
```

**Difference Between import and from:**
- `import`: Creates module namespace, access with `module.attribute`
- `from`: Copies names directly, access as simple variables

**Example 3-3: threenames.py**
```python
a = 'PC'           # Define three attributes
b = 'Phone'        # Exported to other files
c = 'Tablet'

print(a, b, c)     # Also used as variables within this file
```

**Running as Script:**
```bash
$ python3 threenames.py
PC Phone Tablet
```

**Using as Module:**
```python
>>> import threenames       # Grab the whole module
PC Phone Tablet
>>> threenames.b, threenames.c
('Phone', 'Tablet')

>>> from threenames import b, c  # Copy specific names
>>> b, c
('Phone', 'Tablet')
```

### 4.5 The exec Built-in

**Alternative to Import:**
```python
>>> exec(open('script1.py').read())
darwin
1267650600228229401496703205376
Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!
```

**How exec Works:**
1. `open('script1.py')` - Opens the file
2. `.read()` - Reads entire file content as string
3. `exec()` - Compiles and runs the code

**exec vs import:**
- **exec**: Runs code each time, no reload needed
- **import**: Module namespace, reload required for changes
- **exec**: Can overwrite existing variables (dangerous)
- **import**: Safe namespace separation

**Name Collision Example:**
```python
>>> x = 999
>>> exec(open('script1.py').read())
# ... output ...
>>> x                    # x was overwritten by script1.py!
'Hack!'
```

### 4.6 Command-Line Launchers

**Using os.system:**
```python
>>> import os
>>> os.system('python3 script1.py')
darwin
1267650600228229401496703205376
Hack!Hack!Hack!Hack!Hack!Hack!Hack!Hack!
0
```

The `0` return value means success.

**Other Options:**
- `os.popen()` - Returns file object to read output
- `subprocess.run()` - More control over process execution

**Caution**: These tools can run any system command - use carefully!

---

## 5. Other Launch Options

### 5.1 Mobile Apps
- Platform-specific interfaces
- May use button taps instead of command lines
- Similar to IDE environments
- See Appendix A for platform-specific details

### 5.2 WebAssembly (Pyodide)
- Runs Python in web browsers
- No local installation required
- Limited by browser sandbox
- Slower than native Python
- Good for demos and learning, less suitable for development

### 5.3 Jupyter Notebooks
- Web-based coding environment
- Popular in scientific computing
- Interactive cells with immediate feedback
- Not covered in detail (specialized tool)

### 5.4 Alternative IDEs
**Popular Options:**
- PyCharm (professional)
- VSCode (lightweight, extensible)
- Wing IDE (Python-focused)
- Spyder (scientific)
- PyScripter (Windows)

**Recommendation**: Start with IDLE or command line before trying advanced IDEs.

---

## 6. Which Option Should You Use?

### For Beginners:
1. **IDLE GUI** - User-friendly, hides complexity
2. **Command line + text editor** - Simple, powerful, educational

### For Experienced Programmers:
- Text editor + system console
- Command lines for full control
- IDE of choice based on needs

### General Principle:
**Use whatever environment makes you most productive**, but understand the fundamentals first.

---

## 7. Test Your Knowledge: Quiz

### Questions:

1. **How can you start a Python interactive interpreter session (REPL)?**

2. **Where do you type a system command line to launch a script file?**

3. **Name four or more ways to run the code saved in a script file.**

4. **What pitfall is related to clicking file icons on Windows and Linux?**

5. **Why might you need to reload a module?**

6. **How do you run a script from within the IDLE GUI?**

7. **How are modules, attributes, and namespaces related?**

### Detailed Answers:

1. **Starting REPL:**
   - Type `py` (Windows) or `python3` (everywhere else) at system prompt
   - Launch IDLE (Shell window is a REPL)
   - Use IDE-specific REPL interfaces
   - Mobile apps provide REPL through their interfaces

2. **System Command Line:**
   - Windows: Command Prompt or PowerShell
   - macOS/Linux: Terminal
   - Android: Termux app
   - **Important**: Use system prompt (`$`), NOT Python prompt (`>>>`)

3. **Ways to Run Script Files:**
   - System command lines: `python3 script.py`
   - File icon clicks (double-click)
   - Import/reload: `import script`
   - exec function: `exec(open('script.py').read())`
   - IDE Run menus (IDLE: Run → Run Module)
   - Mobile app interfaces
   - Web notebooks (Jupyter)
   - OS module tools: `os.system('python3 script.py')`

4. **Icon Click Pitfall:**
   - Output window closes immediately after program ends
   - Can't see results of print statements
   - Error messages disappear before you can read them
   - **Solution**: Add `input("Press Enter...")` to pause before exit

5. **Why Reload Modules:**
   - Python imports modules only once per session
   - If you modify source code, need to reload to see changes
   - Alternative: Restart Python session
   - exec() doesn't need reloading (runs fresh each time)

6. **Running in IDLE:**
   - Open file: File → Open or File → New File
   - Run file: Run → Run Module (or F5)
   - Output appears in Shell window
   - Can also use Run → Run... Customized for command-line arguments

7. **Modules, Attributes, and Namespaces:**
   - **Module**: Each .py file is automatically a module
   - **Namespace**: Collection of names (variables) in a module
   - **Attributes**: Names assigned at module's top level
   - **Access**: Use dot notation (`module.attribute`) or `from` import
   - **Purpose**: Avoid name collisions, organize code, enable reuse

---

## 8. Practical Exercises

### Exercise 1: Environment Setup
**Goal:** Verify your Python installation works correctly.

**Task:**
```python
# At the system prompt:
$ python3
>>> 'Hello World!'
'Hello World!'
>>> exit()
```

**What you're testing:**
- Python is properly installed
- Interactive mode works
- Basic string handling functions

### Exercise 2: First Script
**Goal:** Create and run your first Python script file.

**Step 1 - Create module1.py:**
```python
print('Hello module world!')
```

**Step 2 - Run it multiple ways:**
```bash
# Command line
$ python3 module1.py

# In IDLE: File → Open → Run → Run Module

# Icon click (double-click the file)

# Import method
$ python3
>>> import module1
Hello module world!

# Exec method
>>> exec(open('module1.py').read())
Hello module world!
```

**Expected Output:** `Hello module world!`

### Exercise 3: Import Experiments
**Goal:** Understand how imports work and module search paths.

**Step 1 - Basic Import:**
```python
>>> import module1    # Should work if in same directory
Hello module world!
```

**Step 2 - Move File Test:**
1. Move `module1.py` to different directory
2. Try importing from original directory
3. **Expected:** Import will fail (file not found)
4. **Learning Point:** Imports search current directory first

**Step 3 - Bytecode Discovery:**
Look for `__pycache__` directory - contains compiled `.pyc` files.

### Exercise 4: Platform Scripts
**Goal:** Create executable scripts (Unix/Linux/macOS).

**Create script1.py:**
```python
#!/usr/bin/env python3
print('Hello executable world!')
```

**Make executable and run:**
```bash
$ chmod +x script1.py    # Make executable
$ ./script1.py           # Run directly
Hello executable world!
```

**Windows Alternative:**
```cmd
C:\> script1.py    # Should work with Python association
```

### Exercise 5: Error Exploration
**Goal:** Learn about Python's error handling.

**Try these in REPL:**
```python
>>> 2 ** 500    # Large number calculation
# Shows Python handles big integers automatically

>>> 1 / 0       # Division by zero
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero

>>> undefined_variable
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'undefined_variable' is not defined
```

**Learning Points:**
- Python provides detailed error messages
- Errors don't crash the system
- Error messages include line numbers and error types

### Exercise 6: Circular References
**Goal:** Explore Python's object handling.

**Try this:**
```python
>>> L = [1, 2]      # Create a list
>>> L.append(L)     # Add the list to itself
>>> L               # Print the list
[1, 2, [...]]
```

**Explanation:**
- `[...]` represents the circular reference
- Python detects and handles circular references gracefully
- This prevents infinite recursion in printing

### Exercise 7: Documentation Exploration
**Goal:** Familiarize yourself with Python documentation.

**Tasks:**
1. Visit python.org/doc
2. Browse the Library Reference
3. Look up the `print()` function
4. Try the `help()` function in REPL:
   ```python
   >>> help(print)
   ```
5. Explore PyPI (Python Package Index) at pypi.org

**Time Investment:** Spend at least 5 minutes browsing to get familiar with structure.

---

## 9. Debugging Python Code

### 9.1 Debugging Strategies (Ranked by Simplicity)

#### Level 1: Do Nothing (Read Error Messages)
```python
>>> x = y + 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'y' is not defined
```

**Learning:** Python error messages are usually clear and helpful. Read them carefully!

#### Level 2: Print Statements
```python
def problematic_function(x, y):
    print(f"Debug: x={x}, y={y}")    # Debug beacon
    result = x / y
    print(f"Debug: result={result}") # Check intermediate values
    return result
```

**Advantages:**
- Quick and simple
- Works everywhere
- Immediate feedback
- Most common debugging method

#### Level 3: Logging Module
```python
import logging
logging.basicConfig(level=logging.DEBUG)

def function_with_logging(x, y):
    logging.debug(f"Called with x={x}, y={y}")
    result = x / y
    logging.debug(f"Calculated result={result}")
    return result
```

**Advantages:**
- More professional than print
- Can control output levels
- Better for larger programs

#### Level 4: IDLE Debugger
**How to use:**
1. Open file in IDLE
2. Debug → Debugger (enable)
3. Set breakpoints (right-click in editor)
4. Run → Run Module
5. Step through code with debugger controls

#### Level 5: Command-Line Debugger (pdb)
```python
import pdb

def buggy_function(x, y):
    pdb.set_trace()    # Breakpoint
    result = x / y
    return result

# Or run entire script in debugger:
# python3 -m pdb myscript.py
```

**pdb Commands:**
- `n` (next line)
- `s` (step into)
- `c` (continue)
- `l` (list current code)
- `p variable_name` (print variable)
- `h` (help)

#### Level 6: Interactive Mode After Errors
```bash
$ python3 -i script.py    # Drops to REPL after script ends
```

**Use case:** Script crashes, and you want to examine variable states.

#### Level 7: Exception Handling (Advanced)
```python
try:
    risky_operation()
except ValueError as e:
    print(f"Caught error: {e}")
    # Handle or investigate the error
```

### 9.2 Debugging Best Practices

1. **Start Simple:** Read the error message first
2. **Add Beacons:** Use print statements liberally while learning
3. **Test Small Pieces:** Use REPL to test functions in isolation
4. **Keep Code Simple:** Complex code is harder to debug
5. **Use Meaningful Variable Names:** Makes debugging easier

---

## 10. Chapter Summary

### Key Concepts Mastered:

1. **Interactive Programming (REPL):**
   - Starting Python interactive sessions
   - Using REPL for learning and testing
   - Understanding prompts and conventions

2. **File-Based Programming:**
   - Creating and running script files
   - Understanding modules vs scripts
   - Using proper file naming conventions

3. **Multiple Execution Methods:**
   - Command-line execution
   - Icon clicking
   - IDE environments (IDLE)
   - Import/reload mechanisms
   - exec() function

4. **Module System Basics:**
   - Import vs from statements
   - Module attributes and namespaces
   - Reloading changed modules

5. **Development Environment Setup:**
   - Proper directory structure
   - Path considerations
   - Platform differences

6. **Debugging Fundamentals:**
   - Reading error messages
   - Using print statements
   - Basic debugging strategies

### Skills You Should Now Have:

- ✅ Can start Python interactive sessions
- ✅ Can create and run Python script files
- ✅ Understand the difference between system and Python prompts
- ✅ Can import modules and understand basic module concepts
- ✅ Know multiple ways to execute Python code
- ✅ Can set up proper development directory structure
- ✅ Can interpret basic Python error messages
- ✅ Ready to start learning Python language features

### What's Next:

Chapter 4 will dive into Python's core data types - the building blocks of all Python programs. You'll learn about numbers, strings, lists, dictionaries, and other fundamental objects that make up Python code.

The foundation you've built in this chapter - knowing how to run code and work with files and modules - will be essential as you start writing more complex Python programs.
