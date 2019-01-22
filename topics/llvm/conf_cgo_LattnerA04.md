# LLVM: A Compilation Framework for Lifelong Program Analysis & Transformation.

- CGO 2004
- [dblp](https://dblp.uni-trier.de/rec/html/conf/cgo/LattnerA04)

## Summary
This paper presents LLVM and compilation framework for lifelong program ananlysis and transformation.

Lifelong:

- link-time: interprocedural optimizations
- install time: machine-dependent optimizations
- runtime: dynamic optimization
- idle-time (between runs): profile guided optimizations

Contributions:

- A low-level, language-independent type system
- Instructions for performing type conversions and low-level address arithmetic
- Two low-level exception-handling instructions
- A simple, low-level memory model distinguishing heap, stack, global data, and code memory regions

Instructions:

- load and store
- most opcodes in LLVM are overloaded
- three-address form
- explicit phi instruction (SSA form)
- cast
- getelementptr
- alloca: allocates memory in the stack frame, automatically de-allocated on return from the function
- invoke and unwind (exception handling)

LLVM makes the Control Flow Graph (CFG) of every function explicit in the representation. A function is a set of basic blocks, and each basic block is a sequence of LLVM instructions, ending in exactly one terminator instruction.

Applications:

- DGE (aggressive Dead global variable and function Elimination)
- DAE (an aggressive Dead Argument Elimination)
- Data Structure Analysis (DSA)
- Automatic Pool Allocation: analyze and transform programs in terms of their logical data structures
- SAFECode: A safe low-level representation and execution environment
- LLVM as an intermediate representation for binary- to-binary transformations.
- a compiler back-end to support a hardware-based trace cache and optimization system

### Good

### Bad

language-specific optimizations must be performed in the front-end before generating LLVM code

### What would you do next

### Questions

More on runtime and idle-time analysis?
