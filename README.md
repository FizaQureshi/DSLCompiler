# DSL to C++ Compiler with LLVM Analysis

## Overview

This project implements a compiler for a simplified Domain Specific Language (DSL) that translates source programs into valid C++ code. The compiler is built using **Flex**, **Bison**, and **C++**, and includes support for lexical analysis, parsing, Abstract Syntax Tree (AST) generation, semantic validation, code generation, and LLVM-based program analysis.

The project was developed as part of compiler engineering and LLVM training to understand the complete compilation pipeline from source code parsing to intermediate representation analysis.

---

# Features

### Lexical Analysis

* Implemented using **Flex**
* Tokenizes:

  * Keywords
  * Identifiers
  * Numeric literals
  * Boolean literals
  * Operators
  * Delimiters

### Syntax Analysis

* Implemented using **Bison**
* Validates DSL grammar
* Reports syntax errors
* Builds Abstract Syntax Tree (AST)

### AST Construction

Supports:

* Variable declarations
* Assignments
* Arithmetic expressions
* Boolean expressions
* Unary operations
* Return statements

### Code Generation

Generates equivalent C++ code for valid DSL programs.

Supported translations:

* Integer variables
* Boolean variables
* Arithmetic operations
* Relational operators
* Logical operators
* Return statements

### LLVM Analysis

LLVM tools are used to:

* Generate LLVM IR
* Inspect control flow
* Visualize Control Flow Graphs (CFG)
* Understand compiler optimizations

---

# Project Architecture

```text
DSL Source
    │
    ▼
Flex Scanner
    │
    ▼
Bison Parser
    │
    ▼
Abstract Syntax Tree (AST)
    │
    ▼
Code Generator
    │
    ▼
Generated C++ Code
    │
    ▼
LLVM IR
    │
    ▼
CFG Analysis & Visualization
```

---

# Project Structure

```text
DSLCompiler/
│
├── src/
│   ├── main.cpp
│   ├── ast.h
│   ├── generator.cpp
│   └── generator.h
│
├── parser/
│   ├── parser.y
│   └── scanner.l
│
├── samples/
│   ├── test.dsl
│   ├── test1.dsl
│   ├── test2.dsl
│   ├── test3.dsl
│   ├── test4.dsl
│   ├── test5.dsl
│   └── test6.dsl
│
├── build/
│
│
└── CMakeLists.txt
```

---

# DSL Grammar Overview

## Variable Declaration

```dsl
int a;
uint b;
bool flag;
```

## Assignment

```dsl
a = 10;
b = a + 5;
```

## Arithmetic Expressions

```dsl
x = a + b;
x = a - b;
x = a * b;
x = a / b;
```

## Boolean Expressions

```dsl
flag = a > b;
flag = a == b;
flag = a != b;
```

## Logical Expressions

```dsl
flag = (a > b) && (b > c);
```

## Return Statement

```dsl
return x;
```

---

# AST Design

The compiler constructs an Abstract Syntax Tree representing the parsed program.

Core node types:

### Expressions

```cpp
Expr
├── NumberExpr
├── VariableExpr
├── BinaryExpr
├── BoolExpr
└── UnaryExpr
```

### Statements

```cpp
Statement
├── VariableDecl
├── AssignmentStmt
└── ReturnStmt
```

---

# Building the Project

## Prerequisites

* CMake
* Ninja
* GCC/G++
* Flex
* Bison
* LLVM

### Verify Installation

```bash
g++ --version
flex --version
bison --version
cmake --version
ninja --version
llvm-dis --version
opt --version
```

---

## Configure Build

```bash
mkdir build
cd build

cmake -G Ninja ..
```

---

## Compile

```bash
ninja
```

Expected output:

```text
[100%] Built target dsl_to_cpp
```

---

# Running the Compiler

Execute:

```bash
./dsl_to_cpp.exe ../samples/test.dsl
```

Example output:

```text
Starting parser...
Valid Contract!
Variables: 2
```

---

# Example DSL Program

## Input

```dsl
contract Test {

    int a;
    int b;

    a = 10;
    b = a + 5;

    return b;
}
```

## Generated C++

```cpp
#include <iostream>

int main() {

    int a;
    int b;

    a = 10;
    b = a + 5;

    return b;
}
```

---

# LLVM Training

## Generate LLVM IR

```bash
clang++ -S -emit-llvm output.cpp -o output.ll
```

Generated:

```text
output.ll
```

---

## View LLVM IR

```bash
llvm-dis output.bc
```

or

```bash
cat output.ll
```

---

## Analyze CFG

Generate Control Flow Graph:

```bash
opt -passes=dot-cfg -disable-output output.ll
```

Output:

```text
._Z3sumi.dot
```

---

## Visualize CFG

Convert DOT file:

```bash
dot -Tpng ._Z3sumi.dot -o cfg.png
```

Result:

```text
cfg.png
```

This graph shows:

* Basic blocks
* Conditional branches
* Loop structures
* Program control flow

---

# Sample LLVM Concepts Explored

### Basic Blocks

A sequence of instructions with:

* Single entry point
* Single exit point

### Control Flow Graph (CFG)

Represents:

```text
Nodes  → Basic Blocks
Edges  → Control Flow Transfers
```

Used by LLVM for:

* Dead code elimination
* Loop optimization
* Constant propagation
* Branch simplification

### Intermediate Representation (IR)

LLVM IR acts as a platform-independent representation between source code and machine code.

Example:

```llvm
%1 = add i32 %a, %b
ret i32 %1
```

---

# Learning Outcomes

Through this project:

* Built a compiler frontend using Flex and Bison
* Designed and implemented an AST
* Generated valid C++ code from DSL programs
* Learned parser construction techniques
* Explored LLVM Intermediate Representation (IR)
* Visualized Control Flow Graphs (CFG)
* Understood compiler optimization foundations
* Gained practical experience with compiler toolchains

---

# Technologies Used

* C++
* Flex
* Bison
* CMake
* Ninja
* LLVM
* Graphviz

---

# Author

Developed as part of Compiler Construction and LLVM Training, focusing on DSL parsing, AST generation, C++ code generation, and LLVM-based program analysis.
