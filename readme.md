**Fluent Python**
# Python Execution Model – Notes

## Background

Hi everyone. My main motive for this repo is to keep notes of my understanding of Python. I chose *Fluent Python* because it is more than just learning syntax—it focuses on how Python actually works under the hood and the design philosophy behind it.

First, let's understand how Python executes code.

---

# 🧠 Big Picture: How Python Executes Code

When you run a Python program, it does **NOT** directly convert your code into machine code.

Instead, it goes through multiple stages:

```text
Python Code (.py)
   ↓
Parsing (Syntax Check)
   ↓
AST (Structure)
   ↓
Bytecode Compilation
   ↓
Execution by Python Virtual Machine (PVM)
```

---

# ⚙️ Stage 1 & 2: Parsing (Syntax & Structure)

### What happens:

* Python reads your code as text
* Checks if it follows valid syntax rules
* Converts it into a structured format called an **AST (Abstract Syntax Tree)**

### Where rules come from:

* Defined in `.gram` files (grammar rules)
* These are converted into C code and compiled into the interpreter

### Errors here:

* `SyntaxError`
* `IndentationError`

👉 If code fails here, execution **stops immediately**

---

# 🔧 Stage 3: Bytecode Compilation

### What happens:

* AST is converted into **bytecode**
* Bytecode is a low-level, Python-specific instruction set

### Example:

```python
x = 2 + 3
```

Becomes:

```text
LOAD_CONST 2
LOAD_CONST 3
BINARY_ADD
STORE_NAME x
```

### Key Points:

* Bytecode is **NOT machine code**
* It is **platform-independent**
* Stored in `.pyc` files (optional caching)

---

# 🔥 Stage 4: Execution (Python Virtual Machine)

### What is PVM?

The **Python Virtual Machine (PVM)** is:

* A loop inside the interpreter
* Executes bytecode instructions one by one

### How it works:

```text
Read instruction → Execute → Move to next
```

### Stack-based execution:

```text
LOAD_CONST 2   → [2]
LOAD_CONST 3   → [2, 3]
BINARY_ADD     → [5]
STORE_NAME x   → []
```

---

# 🧩 Role of Interpreter

The Python interpreter is:

* A **compiled machine code program**
* Written in C
* Stored inside `python.exe`

It includes:

* Parser
* Compiler (to bytecode)
* PVM (execution engine)

---

# ⚠️ Important Clarifications

### ❌ Python code is NOT converted to C

### ❌ Bytecode is NOT converted to machine code at runtime

### ✅ Instead:

* Interpreter already contains machine code
* It **reads bytecode and executes it directly**

---

# 🧠 Compiler vs Interpreter (Clear Understanding)

### Compiler:

* Translates code **before execution**
* Example: C → Machine Code

### Interpreter:

* Executes code **step-by-step at runtime**

### Python:

* Uses **both**

  * Compiles → Bytecode
  * Interprets → Executes bytecode

---

# 💥 When Do Errors Occur?

### Parsing Stage:

* Syntax errors

### Execution Stage:

* `KeyError`
* `ValueError`
* `TypeError`

👉 These happen because of **actual runtime values**, not syntax

---

# 🖥️ Role of Operating System

* Interpreter runs as machine code on CPU
* OS is only involved when needed:

  * File operations
  * Input/output
  * Memory access

👉 Interpreter does NOT send machine code to OS
👉 It only makes **system calls when required**

---

# 🏗️ Inside python.exe (Final Mental Model)

```text
python.exe (machine code)
│
├── Parser
│     → Syntax & AST
│
├── Compiler
│     → Bytecode
│
└── PVM (Interpreter Loop)
      → Executes bytecode
```

---

# 📚 What Fluent Python Focuses On

This book does NOT focus heavily on parsing or bytecode.

Instead, it focuses on:

### 🔹 Object Model

* Everything in Python is an object

### 🔹 Special Methods

* `__len__`
* `__getitem__`
* `__iter__`

### 🔹 Behavior Over Types

* Python cares about what objects **can do**, not what they are

### 🔹 Data Model

* How objects interact during execution

👉 In short:

* This README explains **how Python runs**
* The book explains **what happens during execution**

---

# 🎯 Final Mental Model

> Python code is parsed into structure, compiled into bytecode, and executed by a virtual machine inside the interpreter, which is itself a compiled machine code program.

---

# 🚀 Conclusion

Understanding this pipeline helps in:

* Debugging errors
* Writing efficient Python code
* Understanding advanced concepts in *Fluent Python*

---

(If you made it this far, congratulations—you now understand Python better than most people who just “run scripts.”)
