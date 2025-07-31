# Chapter 2: How Python Runs Programs

## Introduction

This chapter explores **program execution** - how you launch code and how Python runs it. We'll study the Python interpreter's execution process from an abstract perspective before diving into practical implementation details.

### Key Focus Areas
- Python interpreter fundamentals
- Program execution models
- Internal execution flow
- Implementation variations
- Performance implications

---

## 1. The Python Interpreter

### What is an Interpreter?

**Definition**: An interpreter is a program that executes other programs. When you write Python code, the Python interpreter reads and carries out the instructions.

**Role**: The interpreter serves as a **layer of logic** between your code and the computer hardware.

### Python Installation Components

When Python is installed, it generates several components:

1. **Interpreter** (core component)
2. **Support library** (standard library)
3. **Additional tools** (depending on installation)

### Forms of the Python Interpreter

The interpreter can take different forms:
- **Executable program** (most common)
- **Set of libraries** linked into another program
- **Different implementations**: C program (CPython), Java classes (Jython), etc.

**Important**: Regardless of form, all Python code must be run by this interpreter.

---

## 2. Program Execution: Two Perspectives

### The Programmer's View

#### Simple Python Program Structure

A Python program is fundamentally a **text file containing Python statements**.

**Example 2-1: script0.py**
```python
print('hello world')
print(2 ** 100)
```

**Components Explained**:
- **Two print statements**
- **String output**: `'hello world'` (text in quotes)
- **Numeric expression**: `2 ** 100` (2 to the power of 100)
- **Output stream**: Results display in GUI or window where file runs

#### File Conventions

- **Extension**: Python files use `.py` extension
- **Requirement**: Technically required only for imported files
- **Best Practice**: Use `.py` for all Python files for consistency

#### Execution Process

1. **Create** the file with any text editor
2. **Tell Python to execute** the file
3. **Execution means**: Run all statements from top to bottom, one after another

#### Expected Output
```
hello world
1267650600228229401496703205376
```

#### Command Line Example
```bash
C:\Users\me\code> py script0.py
hello world
1267650600228229401496703205376
```

### Python's Internal View

#### What Happens "Under the Hood"

When you instruct Python to run your script, several steps occur before code execution:

1. **Compilation** to bytecode
2. **Routing** to virtual machine

This process applies to the most common Python version (CPython).

---

## 3. Internal Execution Process

### Step 1: Bytecode Compilation

#### What is Bytecode?

**Definition**: Bytecode is a lower-level, platform-independent representation of your source code.

**Process**:
- Python translates each source statement into bytecode instructions
- Decomposition into individual steps
- **Purpose**: Speed execution (bytecode runs much faster than original source)

#### Bytecode File Storage

**Automatic Saving**:
- Files saved with `.pyc` extension
- `.pyc` = `.py` source, compiled
- **Location**: `__pycache__` subdirectory
- **Naming**: Includes Python version (e.g., `script0.cpython-312.pyc`)

**When Bytecode is Saved**:
- **NOT saved**: Single file execution (like our example)
- **Saved**: All but topmost file in multifile programs
- **Requirement**: Python must have write access

#### Bytecode Optimization Logic

**Startup Speed Optimization**:
Python loads `.pyc` files and skips compilation when:
- Bytecode is present
- Source code unchanged since last save
- Same Python version created the bytecode

**Automatic Recompilation Triggers**:

1. **Source Changes**:
   - Python saves timestamp and size in bytecode file
   - Compares with source when loading
   - Recompiles if source was modified

2. **Python Version Changes**:
   - Version suffix added to bytecode filenames
   - Different Python versions generate separate bytecode

**Fallback Behavior**:
- If bytecode can't be written: program still works
- Bytecode generated in memory and discarded on exit

#### Import Optimization Details

**Key Points**:
- Bytecode is primarily an **import optimization**
- Saved only for **imported files**, not top-level scripts
- Each file imported only **once per program run**
- **Interactive prompt**: Bytecode never saved

### Step 2: Python Virtual Machine (PVM)

#### What is the PVM?

**Definition**: The Python Virtual Machine is the runtime engine that executes bytecode.

**Reality Check**: 
- Not a separate program
- No separate installation needed
- Just a **big code loop** that iterates through bytecode instructions
- **Final step** of the "Python interpreter"

#### PVM Operation

**Process**:
1. Receives compiled bytecode
2. Iterates through instructions one by one
3. Carries out operations
4. **Always present** as part of Python system

#### Execution Flow Diagram

```
Source Code (.py) → Bytecode Compilation → Bytecode (.pyc) → Python Virtual Machine (PVM) → Program Output
```

**Note**: All this complexity is deliberately hidden from Python programmers.

---

## 4. Performance and Development Implications

### Performance Characteristics

#### Compared to Compiled Languages (C/C++)

**Differences**:
- **No build step**: Code runs immediately after writing
- **Not machine code**: Bytecode is Python-specific, not CPU instructions
- **Speed trade-off**: PVM must interpret bytecode vs. direct CPU execution

**Result**: Python runs at speeds between traditional compiled and interpreted languages.

#### Why Bytecode Instead of Machine Code?

**Development Speed vs. Execution Speed Trade-off**:

**Traditional Languages (C)**:
- Constrain code to accommodate CPU expectations
- Translate to machine code ahead of time
- **Result**: Fast execution, slow development

**Python Approach**:
- Easy-to-use language design
- PVM intermediary runs bytecode on CPU
- **Result**: Faster development, acceptable execution speed

### Development Implications

#### Unified Environment

**Key Feature**: No distinction between development and execution environments.

**Benefits**:
- **Rapid development cycle**: No precompile and link steps
- **Dynamic flavor**: Programs can construct and execute other Python programs at runtime
- **Runtime flexibility**: Code can be changed on the fly

#### Runtime Features

**Everything Happens at Runtime**:
- Function creation
- Class creation  
- Module linkage
- **Dynamic programming**: More flexible than static languages

**Built-in Dynamic Execution**:
- `eval()`: Execute strings containing Python expressions
- `exec()`: Execute strings containing Python statements

---

## 5. Execution Model Variations

### Python Implementation Alternatives

The standard execution model is not a language requirement - it's just the most common implementation. Multiple Python implementations exist:

#### CPython: The Standard

**Description**: Original, standard, and reference implementation
**Name Origin**: Coded in portable ANSI C
**Usage**: 
- Default Python from python.org
- Most Linux distributions
- Smartphone Python apps (Android/iOS)
- **Most common implementation**

#### Alternative Implementations

**Jython: Python for Java**
- **Target**: Java programming language integration
- **Implementation**: Java classes compile Python to Java bytecode
- **Execution**: Java Virtual Machine (JVM)
- **Files**: Still use `.py` files
- **Status**: Currently implements Python 2.X, working toward 3.X

**IronPython: Python for .NET**
- **Target**: Microsoft .NET Framework integration
- **Implementation**: Coded in C#
- **Compatibility**: Works with Mono open source equivalent
- **Benefit**: Accessibility to/from other .NET languages

**Stackless: Python for Concurrency**
- **Focus**: Enhanced concurrency support
- **Feature**: Doesn't save state on C language call stack
- **Benefits**: 
  - Easier porting to small-stack architectures
  - Efficient multiprocessing options
- **Example**: EVE Online game uses Stackless for massively parallel tasks

**PyPy: JIT Compiler for Speed**
- **Innovation**: Just-in-time (JIT) compiler for normal Python code
- **Process**: Translates bytecode portions to machine code during execution
- **Intelligence**: Tracks data types to create type-specific machine code
- **Benefits**: 
  - Programs run faster as they execute
  - Potentially less memory usage

**Numba: JIT Compiler for Numeric Speed**
- **Focus**: Numerically oriented code optimization
- **Method**: "@" decorators direct the compiler
- **Specialization**: Works well with NumPy arrays and math-oriented loops
- **Features**: Supports code parallelization for scientific programming

**Shed Skin: AOT Compiler**
- **Type**: Ahead-of-time (AOT) compiler
- **Process**: Translates Python code to C++, then to machine code
- **Output**: Standalone programs or extension modules
- **Limitation**: Restricted Python subset with implicit static typing

**Cython: Python/C Hybrid**
- **Concept**: Combines Python code with C function calls and type declarations
- **Compilation**: AOT-compiled to C code using Python/C API
- **Uses**: 
  - Wrapping external C libraries
  - Performance-critical system components

**MicroPython: Constrained Environments**
- **Focus**: Efficiency in limited environments
- **Implementation**: Limited CPython dialect with small standard library subset
- **Targets**: Microcontrollers, WebAssembly for browsers

#### Choosing an Implementation

**Recommendation**: Use standard CPython unless you have specific needs.

**CPython Advantages**:
- Reference implementation (most complete)
- Most up-to-date
- Most robust
- Widest compatibility

### Standalone Executables

#### Purpose

Convert Python programs into **self-contained executables** (frozen binaries) that run without Python installation.

#### How They Work

**Bundle Contents**:
- Program bytecode
- PVM (interpreter)
- Python support files and libraries
- **Result**: Single executable file

**Examples**:
- Windows: `.exe` files
- macOS: `.app` files  
- Android: `.apk` or `.aab` files

#### Available Tools

**Platform-Specific**:
- **py2exe**: Windows standalones
- **py2app**: macOS standalones

**Cross-Platform**:
- **PyInstaller**: Windows, macOS, Linux
- **cx_freeze**: Windows, macOS, Linux

**Mobile**:
- **Buildozer**: Android and iOS apps
- **Briefcase**: Android and iOS apps

#### Important Characteristics

**Performance**: Same speed as original source (still runs bytecode through VM)
**Size**: Not small (contains PVM) but acceptable by current standards
**Distribution**: No Python installation required on target machine
**Security**: Bytecode not easily viewed

---

## 6. Future Possibilities

### Runtime Model Evolution

The current execution model is an **implementation artifact**, not a language requirement.

### Potential Changes

**AOT Compiler Possibility**:
- Could translate unrestricted Python to machine code
- **Likelihood**: Seems unlikely after 30+ years without one
- **Challenge**: Would break Python's flexibility and simplicity

**JIT Compiler Trends**:
- Appearing in many Python implementations
- May become more common in CPython

### CPython JIT Development

**Version 3.13 Features**:
- **Experimental JIT compiler** (similar to PyPy)
- Translates bytecode to machine code during execution
- **Initial state**: Negligible speed boost, disabled by default
- **Future potential**: May be enabled by default if significant performance gains achieved

**Trade-off Consideration**:
Adding type constraints for static compilation would break:
- Flexibility
- Conciseness  
- Simplicity
- Spirit of Python coding

---

## 7. Test Your Knowledge

### Quiz Questions

1. **What is the Python interpreter?**

2. **What is source code?**

3. **What is bytecode?**

4. **What is the PVM?**

5. **What is machine code?**

6. **Name two or more variations on Python's standard execution model.**

7. **How are CPython, Jython, and IronPython different?**

8. **What are PyPy, Shed Skin, and Cython?**

### Quiz Answers

1. **Python Interpreter Answer**:
   The Python interpreter is a program that runs Python programs you write. It intermediates between your Python instructions and CPU machine code instructions.

2. **Source Code Answer**:
   Source code consists of the statements you write for your program. It's text in files with names normally ending in `.py` extension.

3. **Bytecode Answer**:
   Bytecode is the lower-level form of your program after Python compiles it. Python automatically stores bytecode in `.pyc` files when possible and recreates it when needed.

4. **PVM Answer**:
   The PVM (Python Virtual Machine) is the runtime engine of Python that interprets your compiled bytecode.

5. **Machine Code Answer**:
   Machine code contains the low-level instructions of the underlying CPU. Since every program ultimately runs as machine code, Python code must be translated by software layers like the PVM interpreter, or JIT/AOT compilers.

6. **Execution Model Variations**:
   Examples include:
   - Numba (JIT compiler for numeric code)
   - Shed Skin (AOT compiler)
   - Standalone executables (frozen binaries)
   - Alternative implementations (Jython, IronPython, PyPy)

7. **Implementation Differences**:
   - **CPython**: Standard and reference implementation
   - **Jython**: Processes Python programs for Java environments
   - **IronPython**: Processes Python programs for .NET environments
   - All are alternative compilers for Python with different target environments

8. **Speed-Focused Implementations**:
   - **PyPy**: Reimplementation targeting speed using JIT compiler with runtime type information
   - **Shed Skin**: AOT compiler that translates restricted Python subset to C++ for full machine code compilation
   - **Cython**: Python/C hybrid language that compiles to machine-code extensions for CPython

---

## Key Takeaways

1. **Python execution involves two main steps**: compilation to bytecode and execution by the PVM
2. **Bytecode optimization**: Automatic caching speeds up subsequent program runs
3. **Development efficiency**: No separate build step enables rapid development cycles
4. **Multiple implementations**: Different Python implementations serve different needs
5. **Performance trade-offs**: Python prioritizes development speed and flexibility over raw execution speed
6. **Future evolution**: The execution model continues to evolve with new optimization techniques
