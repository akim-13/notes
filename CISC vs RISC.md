---
tags:
  - CS
  - cm12002
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W08_L02_P01
---
# CISC vs RISC
| Feature                       | CISC (Complex Instruction Set Computer)                                            | RISC (Reduced Instruction Set Computer)                                              |
|:-------------------------------:|:--------------------------------------------------:|:---------------------------------------------------:|
| Instruction Complexity        | More powerful instructions                       | Simpler instructions                              |
| Decoding Complexity           | More complicated to decode instructions          | Simple decoding                                   |
| Memory Access                 | Arithmetic instructions also perform memory accesses (e.g. see [[Operand Addressing Modes]]) | Arithmetic instructions only use registers (load/store architecture) |
| Registers (see memory access) | Less registers                                    | More registers                                    |
| Instruction Execution         | Varies (multiple cycles per instruction possible) | Uniform (typically one clock cycle per instruction) |
| Code Length                   | Completes a task in fewer lines of assembly code | More lines of code, therefore more memory needed to store instructions |
| Memory for Instructions       | Not a lot of memory needed to store instructions | More memory needed to store assembly level instructions |
| Work for Compiler             | -                                                | Compiler needs to perform more work to convert high-level language code into RISC instruction statements |
| General-Purpose Registers     | Fewer because decoding instructions require more transistors | -                                                 |
| Usage                         | Computers, consoles, laptops, etc.                | Mainly in devices that have to save power (phones, tablets, etc.)
| Examples | Intel, AMD, [[./Fetch-Decode-Execute (FDE) Cycle.md#^motorola\|Motorola MC68000]], etc. | ARM, MIPS, PowerPC, etc.
