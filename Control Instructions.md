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
    - The following shows the **most common** conditional jump/branch instructions **names**.

        ![[Attachments/Pasted image 20231128215159.png]]

    - Conditional branches can utilize one-bit **flags** or **condition-codes**, which are automatically set by the CPU as a result of executing an instruction:

        ![[Attachments/Pasted image 20231128220606.png]]

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

- A **subroutine** is a set of instructions designed to perform a specific task. It has many names, depending on the context and programming language: a procedure, a function (in C), a routine, a method (in Java) or a subprogram. 

- A usual **subroutine operation** is as follows: 
    - A block of instructions for performing the task is placed in the memory and the subroutine is called by branching to the starting location of the block.
    - When the block of instructions is completed, the subroutine returns to the point at which it was called.
    - This behaviour can be implemented using the **LIFO stack** (Last In First Out)

        ![[Attachments/Pasted image 20231128221812.png]]

- The following is an **example use of subroutines**:

    ![[Attachments/Pasted image 20231128222110.png]]
    ![[Attachments/Pasted image 20231128222241.png]]

    - In this example, there is a main program starting at location 4000. This program includes a call to procedure Proc1, starting at location 4500. 
    - When this call instruction is encountered, the processor suspends execution of the main program and begins execution of Proc1 by fetching the next instruction from location 4500. 
    - Within Proc1, there are two calls to Proc2 at location 4800. In each case, the execution of Proc1 is suspended and Proc2 is executed. 
    - The RETURN statement causes the processor to go back to the calling program and continue execution at the instruction after the corresponding CALL instruction. This behavior is illustrated with arrows on (b).
    - When the processor executes a call, it places the return address on the stack. When it executes a return, it uses the address on the stack. 

