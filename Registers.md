---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W19_L01_P01
---
# Registers
- **Registers** are rapid access data stores in the CPU that store values used in ongoing computations.

    ![[Attachments/Pasted image 20231024223614.png]]
- **For example**, for a computation like `a + b`, `a` would go to one register, `b` to another, then the ALU would add two values together and store the result in either of these two registers, or a different one.
    ```armasm
    LOAD R1, A       ; Load value A into Register1
    LOAD R2, B       ; Load value B into Register2
    ADD R1, R2, R3   ; Add the values in Register1 and Register2, store result in Register3
    ```
- Registers provide **the fastest possible access** to the CPU, even faster than [[./Cache.md | L1 cache]].
- **Modern Programming languages** do not have direct access to registers, with the exception of assembly and inline assembly in C.
- There are **two types of registers**:
    1. **Parallel registers:** 

        ![[Attachments/Pasted image 20240211153107.png]]
        - Consists of a set of 1-bit memories that can be read or written **simultaneously**.
        - Used to **store data**.
        - In the example above, the **1-bit memories are** implemented using **[[./Sequential Logic.md | D flip-flops]]**.
        - The **clock** is used to synchronize the simultaneous reading/writing and to ensure that it happens in unison with other components of the system.
        - The **load** control signal indicates when the data should be read or written.
        - The data is **read/written** only when **both clock and load** signals are **active**.

    2. **Shift registers**:

        ![[Attachments/Pasted image 20240211163215.png]] 
        - Accepts and/or transfers information **serially**, i.e. they move data either inside the register or to another location **bit by bit**.
        - The above diagram shows a **5-bit shift register** constructed from **[[./Sequential Logic.md#Types of Flip-Flops| D flip-flops]]**.
        - With each clock pulse^[Clock pulses can be controled, although it is not shown in the diagram.] a **[[./Implementing Arithmetic Using Combinatorial Logic.md#^logical | logical right shift]]** is performed, i.e. the data is shifted to the right one position and the rightmost bit is transferred out.
        - Notice that if *Serial out* is connected to *Serial in*, a **[[./Implementing Arithmetic Using Combinatorial Logic.md#^circular | circular shift]]** would be performed instead.

