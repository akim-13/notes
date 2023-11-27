---
tags:
  - cm12002
  - cs
links:
  - "[[Fetch-Decode-Execute (FDE) Cycle]]"
  - "[[Computer Systems Architectures]]"
presentations:
  - W08_L01_P02
---
# Operand Addressing Modes
- **Immediate** mode — the given value is used itself. For example in the [[./Fetch-Decode-Execute (FDE) Cycle.md#^motorola | MC68000 architecture]], it is indicated with `#`.
- **Direct** mode — the value of the given address is used (a *pointer*). ^f0bcc6
- **Indirect** mode — the operand is a location of store (or a register) which contains not data, but another address, where the true operand will be found (a *pointer to a pointer*). Typically indicated by placing the operand in parentheses, e.g. `ADD ($101E), D2` (in this case, add `D2` with the content of the content of memory addressed by `$101E`)

    ![[Attachments/Pasted image 20231127191934.png]]

- **The fastest mode** is the *immediate* one, since it does not access memory. The more memory the mode accesses, the slower it is, hence the next fastest is the *direct*, followed by the *indirect*.

- The **less common addressing modes**^[Non-assessable.] (depending on the processor) are: 
    - Indirect with displacement
    - Indirect with post-increment
    - Indirect with pre-decrement
    - Indirect with index
    - For PC (program counter)
        - PC with displacement
        - PC with index
