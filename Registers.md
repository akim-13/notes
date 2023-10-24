---
tags:
  - cm12002
  - CS
links:
---
# Registers
- **Registers** are rapid access data stores on the CPU that store values used in ongoing computations.

    ![[Attachments/Pasted image 20231024223614.png]]
- **For example**, for a computation like `a + b`, `a` would go to one register, `b` to another, then the ALU would add two values together and store the result in either these two or a different register.
    ```armasm
    LOAD R1, A       ; Load value A into Register1
    LOAD R2, B       ; Load value B into Register2
    ADD R1, R2, R3   ; Add the values in Register1 and Register2, store result in Register3
    ```
- They provide **the fastest possible access** to the CPU, even faster than [[./Cache.md | L1 cache]].
- **Modern Programming languages** do not have direct access to registers, with the exception of assembly and inline assembly in C.
