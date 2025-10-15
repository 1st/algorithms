# 02 · How Computers Execute Code

Understanding what happens between your editor and the CPU clarifies why certain algorithms shine—and why some fail in practice. This chapter traces the path from high-level source code to instructions a processor can execute.

## Learning objectives
- Describe the hardware components involved when a program runs (CPU, memory, storage, I/O)
- Explain the roles of compilation, interpretation, and virtual machines
- Identify performance considerations introduced by language runtimes and operating systems

## Layers of execution
- **Hardware:** the CPU fetches instructions from memory, executes arithmetic/logic operations, and coordinates with caches and storage.
- **Operating system:** schedules processes/threads, manages memory, handles system calls (file I/O, networking).
- **Language runtime:** optional layer providing garbage collection, JIT compilation, or standard libraries (e.g., Python interpreter, JVM).
- **Your program:** algorithms and data structures expressed in a high-level language.

Each layer adds helpful abstractions while hiding details that might impact performance.

## Compilation vs. interpretation
- **Compiled languages** (C, Rust) translate source code into machine instructions ahead of time. Result: fast startup, optimised binaries; cost: longer build times.
- **Interpreted languages** (CPython) execute source line by line, decoding statements at runtime. Result: fast iteration, dynamic introspection; cost: extra overhead per operation.
- **Hybrid models** use bytecode + virtual machines (Java, JavaScript, Python via `.pyc`). Just-In-Time (JIT) compilers detect hot paths and optimise them on the fly.

### Example: Python execution pipeline

```python
def is_even(value: int) -> bool:
    return value & 1 == 0

print(is_even(42))
```

1. **Parsing:** CPython tokenises and builds an Abstract Syntax Tree (AST).
2. **Bytecode emission:** the AST compiles to stack-based bytecode stored in `.pyc`.
3. **Interpreter loop:** the Python Virtual Machine (PVM) dispatches each bytecode instruction, implemented in C.
4. **System call:** `print` eventually invokes OS-level write operations to display text.

Understanding this ladder explains why loop-heavy Python code benefits from vectorised libraries (NumPy) or C extensions—they skip repeated interpreter overhead.

## Memory and caches
- CPUs operate fastest on data in **registers** and **L1/L2 caches**; fetching from RAM is slower, disk slower still.
- **Locality of reference** (accessing neighbouring memory) boosts cache hits—algorithms that scan contiguous arrays often outperform pointer-heavy structures.
- **Garbage-collected languages** may pause execution to reclaim memory; design data structures to minimise unnecessary allocations during critical loops.

## Interview checkpoints
- State relevant runtime characteristics when comparing algorithms (e.g., cache-friendly array vs. pointer-based list).
- Mention how language choices influence complexity constants, especially in micro-optimisation questions.
- Recognise when to propose lower-level optimisations (C extensions, memoisation, concurrency) and when they are premature.

## Further practice
- Inspect bytecode with `python -m dis` to reinforce the compilation steps.
- Profile a Python script using `timeit` or `cProfile` to see interpreter overhead firsthand.
- Continue to [03 · Complexity Basics](03-complexity-basics.md) to quantify how these layers influence algorithmic cost.
