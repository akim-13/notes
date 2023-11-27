---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W08_L01_P02
---
# Control Instructions
- **Control instructions** are used to branch to a different set of instructions depending on the decision made.
- Reasons why **control instructions are required**:
    - It is essential to be able to **execute** each instruction **more than once**.
    - Virtually all programs involve some **decision making**.
    - It helps if there are mechanisms for **breaking the task up into smaller pieces** that can be worked on one at a time.
- Control instructions can **alter the contents of the PC** in order to *jump* (a.k.a. *branch*) to another instruction or execute a *subroutine*.
- **Conditional branch/jump** — the branch is made (update program counter to equal address specified in operand) only if a certain condition is met. Otherwise, the next instruction in sequence is executed (increment program counter as usual).
- **Unconditional branch/jump** — the branch is always taken.
- The following **example** shows how an unconditional and a conditional branch can be used to create a repeating loop of instructions. The instructions in locations 202 through 210 will be executed repeatedly until the result of subtracting `Y` from `X` is 0. Note that a branch can be either *forward* (an instruction with a higher address) or *backward* (lower address).

    ![[Attachments/Pasted image 20231127222848.png]]

- Comparing C with pseudo-Assembly:
    ```c
    if (i == j)
        h = i + j;
    else
        h = i - j;
    ...
    ```
    ```armasm
              Load registers (R1 = i; R2 = j; R3 = h;) 
              CMP R1,R2
              JNE DoElse
              ADD R1,R2
              MOVE R3,R1
              JMP SkipElse
    DoElse:   SUB R1,R2
              MOVE R3,R1
    SkipElse: ...
    ```
    Where `JNE` means "jump if not equal" (conditional branch) and `JMP` is an unconditional branch.

<!-- STOPPED ON SLIDE 11 -->
