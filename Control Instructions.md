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
- **Conditional branch/jump** — the branch is made (update program counter to equal address specified in operand) only if a certain condition is met. Otherwise, the next instruction in sequence is executed (increment program counter as usual). ^branch-def
    - The following shows the **most common** conditional jump/branch instructions **names**.

        ![[Attachments/Pasted image 20231128215159.png]]

    - Conditional branches can utilize one-bit **flags** or **condition-codes**, which are automatically set by the CPU as a result of executing an instruction:

        ![[Attachments/Pasted image 20231128220606.png]]

- **Unconditional branch/jump** — the branch is always taken. 

- The following **example** shows how an unconditional and a conditional branch can be used to create a repeating loop of instructions. The instructions in locations 202 through 210 will be executed repeatedly until the result of subtracting `Y` from `X` is 0. Note that a branch can be either *forward* (an instruction with a higher address) or *backward* (lower address). ^branch-eg

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
  // Assuming R1 = i, R2 = j, R3 = h
  // Load registers with the values of i and j (this step is implied)
              CMP R1, R2       // Compare R1 and R2
              BNE DoElse       // Branch to DoElse if R1 is not equal to R2
              ADD R3, R1, R2   // If equal, perform R3 = R1 + R2
              B SkipElse       // Unconditional branch to SkipElse
    DoElse:   SUB R3, R1, R2   // If not equal, perform R3 = R1 - R2
    SkipElse: ...              // Continue with the rest of the program
	// Note that DoElse is just a label, not a subroutine.
    ```
    Where `JNE` means "jump if not equal" (conditional branch) and `JMP` is an unconditional branch.

- A **subroutine** is a set of instructions designed to perform a specific task. It has many names, depending on the context and programming language: a procedure, a function (in C), a routine, a method (in Java) or a subprogram. 
	- Sometimes a subroutine is said to be **different from a function** in that it does not return any values. However, in some contexts these two terms are used interchangeably.

- A usual **subroutine operation** is as follows: 
    - A block of instructions for performing a task is placed in memory and a subroutine is called by branching to the starting location of the block.
    - When the block of instructions is completed, the subroutine returns to the point at which it was called.
    - This behaviour can be implemented using the **LIFO stack** (Last In First Out):

        ![[Attachments/Pasted image 20231128221812.png]]

- A **call stack** is used in order to *return to the right point in the program* after executing a branch/subroutine. Furthermore, it allows to *nest subroutines calls* to any depth (provided there is enough memory).
    - Normally, **stack starts** at *high address* in memory and grows from higher addresses to lower ones.^[It is designed this way for historical and architectural reasons, but mainly becuase the **heap** (used for dynamically allocated memory) grows upwards from a lower memory address. Having the stack grow downwards from the top of memory ensures that both the heap and the stack have as much space as possible to expand without colliding.]
    - A stack consists of a **block of successive memory locations** storing its contents, and a special [[Registers | CPU register]] called the **stack pointer (SP)**, which stores the address of the "top" of the stack.
    - To **push** a value onto the stack, *decrement* the address (see the first bullet point) in the stack pointer and store it there. 
    - To **pop** a value from the stack, *dereference* (get the content of) the address stored in the stack pointer, which is then *incremented* by one.
    - To **call** a subroutine, the contents of the program counter are pushed onto the stack and the PC is reset to the starting address of the subroutine.
    - To **return**, the program counter is reset to the value popped from the stack.
    - A portion of the stack dedicated to a single function call is called a **stack frame**.  It includes various elements necessary for the function's execution and return, including:
        - The **return address** (the contents of the PC right before they are changed to the address of the subroutine).
        - **Argument variables** passed to the subroutine.
        - Space to store function's **local variables** (in high level languages).
        - Saved **copies of registers** that need to be preserved across function calls.

- The following is an **example use of subroutines**:

    ![[Attachments/Pasted image 20231128222110.png]]
    ![[Attachments/Pasted image 20231128222241.png]]

    - In this example, there is a main program starting at location 4000. This program includes a call to procedure Proc1, starting at location 4500. 
    - When this call instruction is encountered, the processor suspends execution of the main program and begins execution of Proc1 by fetching the next instruction from location 4500. 
    - Within Proc1, there are two calls to Proc2 at location 4800. In each case, the execution of Proc1 is suspended and Proc2 is executed. 
    - The RETURN statement causes the processor to go back to the calling program and continue execution at the instruction after the corresponding CALL instruction. This behavior is illustrated with arrows on (b).
    - When the processor executes a call, it places the return address on the stack. When it executes a return, it uses the address on the stack. 

