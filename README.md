# tinyL Custom Compiler
### Developed by: Amy Margolina

This repository contains a complete compiler and virtual machine toolchain for the **tinyL** programming language.

The toolchain includes:

- A **recursive-descent compiler** (`Compiler.c`) that parses tinyL programs and generates RISC-style instructions.
- A **RISC virtual machine interpreter** (`Interpreter.c`) that executes the generated instruction list.
- Instruction utilities (`Instr.h`, `InstrUtils.c/h`) for reading, printing, and managing instructions.
- Error/debug helpers (`Utils.c/h`).
- A Makefile for building the compiler and interpreter.
- Sample `.tinyL` programs located in the `tests/` folder.

---

## tinyL Language Overview

**tinyL** is a minimal prefix-notation programming language where every token is a single character.  
Whitespace is ignored, and all programs must end with the `!` symbol.

### Example tinyL Program

    a=+2*35;%a!

This program assigns a computed value to `a` and then prints it.

---

## tinyL Grammar Specification

The tinyL compiler is built around an LL(1) recursive-descent parser.  
The full grammar implemented in `Compiler.c` is shown below:

```text
<program>   ::= <stmt_list> !
<stmt_list> ::= <stmt> <morestmts>
<morestmts> ::= ; <stmt_list> | ε
<stmt>      ::= <assign> | <read> | <print>

<assign>    ::= <variable> = <expr>
<read>      ::= ? <variable>
<print>     ::= % <variable>

<expr>      ::= + <expr> <expr>
              | - <expr> <expr>
              | * <expr> <expr>
              | & <expr> <expr>
              | | <expr> <expr>
              | <variable>
              | <digit>

<variable>  ::= a | b | c | d | e | f
<digit>     ::= 0–9
```

---

## Project Structure

This repository contains the full tinyL compiler toolchain.  
Only **`Compiler.c`** and part of **`InstrUtils.c`** were implemented by me; the remaining files were provided.

    Compiler.c        → full tinyL compiler implementation (written by me)
    Interpreter.c     → provided RISC-style virtual machine
    Instr.h           → instruction format definitions
    InstrUtils.c/h    → instruction creation and printing utilities
    Utils.c/h         → error, debug, helper utilities
    Makefile          → builds compiler and interpreter
    tests/*.tinyL     → sample tinyL programs for testing

---

## Building the Project

To compile the tinyL compiler and interpreter:

    make

This produces two executables:

- **compiler** — implemented in `Compiler.c`
- **interpreter** — virtual machine that executes the instructions

Example output:

    gcc -o compiler Compiler.c InstrUtils.c Utils.c
    gcc -o interpreter Interpreter.c InstrUtils.c Utils.c

---

## Compiling a tinyL Program

To compile a tinyL program:

    ./compiler tests/comp01.tinyL

This generates:

    tinyL.out

---

## Running a Compiled tinyL Program

To run it:

    ./interpreter tinyL.out

If the program uses input (`?a`):

    tinyL>> enter value for "a":

---

## Cleaning the Build

    make clean

---

## Skills Demonstrated

- Recursive-descent parsing
- Low-level code generation into a RISC-style instruction set
- Linked list manipulation
- Understanding source → IR → virtual machine execution
- C systems programming (memory, I/O)
