---
tags: cm12002, cs
links: "[[Computer Systems Architectures]]"
---
# Fetch-Decode-Execute (FDE) Cycle

- **FDE Cycle** — the cycle that the CPU follows from boot-up until the computer has shut down in order to process instructions. 
    - **Fetch phase** — bringing the instruction from store to the instruction register. This phase is **the same for all instructions**.
    - **Decoding phase** — the binary instruction are translated into a set of signals by the instruction decoder to control other parts of the CPU to perform the required operation.
    - **Execution phase** — accessing the operands (if any) and carrying out the operation. This and previous phases **vary from instruction to instruction**.

- The following **example** demonstrates how a **load instruction** might be carried out:
    - **Fetch**:
        1. Contents of the PC are placed in the MA (**PC→MA**), setting the store location of the next instruction.
        2. Contents of the cell whose address is in MA are placed in the MB (**STORE→MB**). This gets the contents of the cell.
        3. Contents of the MB are placed in the IR (**MB→IR**). The instruction is now ready for decoding.
        4. **Increment PC** so that the next instruction in sequence will be accessed next.
        ![[Attachments/Pasted image 20231121142923.png]]
        ![[Attachments/Pasted image 20231121143406.png]][^legend]
        - Notice that **PC and IR do not access the memory directly** primarily to avoid memory access conflicts. 
    - **Decode**: instructions are decoded by the instruction decoder inside the CPU (not on the diagram).
    - **Execute**:
        1. **Increment MA** to point at the next address in memory.
        2. Contents of the cell whose address is in MA are placed in the MB (**MA→MB**).
        3. Contents of MB are placed in the data register (**MB→Rn**)
        ![[Attachments/Pasted image 20231121144750.png]]

- **Another example** shows how to execute an instruction that specifies *adding the contents of a cell at a specific location to the data register R0*. It is assumed that the fetch phase has already happened.

    ![[Attachments/Pasted image 20231121145455.png]]

- **Real world example**: *the Motorola MC68000 architecture*. Let us consider an addition operation that adds the 16-bit contents of a specified location to one of the eight data registers of this machine (register 5 in this example) — `ADD $1202, D5`, where `$` denotes that the following number is hexadecimal. ^motorola
    - The instruction is stored in 4 bytes — 2 byte control word and 2 byte extension word.
    1. **Control word**: [`1101`] [`101`] [`001`] [`111000`] (`$DA78` in HEX), where each part represents (in order):
        1. **Opcode** (Operation Code) — the instruction (`ADD` here). 
        2. **Operand** — any object that can be manipulated by opcode. In this example the `D5` data register is the *first operand*. 3 bits are used to be able to represent $2^3 = 8$ registers.
        3. **The size** of the data that the instruction operates on. This size determines how many bits of the data registers or memory the instruction will process. This operation size is critical because it tells the CPU how to interpret the data it's working with, ensuring that the correct amount of data is read from or written to the registers or memory. The possible values for the size are:
        ![[Attachments/Pasted image 20231121163158.png]]
        Where a byte is 8 bits, a word is 16 bits and longword is 32 bits. So `001` in this architecture means "add words to register".
        4. Additional information.
    2. **Extension word** includes more additional information. In this case it points to an address, however it could also store a value, depending on the addressing mode (more on that later): `0001001000000010` = `$1202`. This is the *second operand*.

        ![[Attachments/Pasted image 20231127183335.png]]
    - Store and I/O devices are connected to the CPU via a single electronic “pathway”, or **bus**, that contains lines for *addresses*, *data* and *control* signals:

        ![[Attachments/Pasted image 20231127183923.png]]

    - The CPU also contains:
        - A 16-bit **IR** for the instruction's control word
        - Four **temporary registers** (`Tn`) for the instruction's extension words, of which there could be a maximum of four.

            ![[Attachments/Pasted image 20231127184529.png]]

    - The **FDE cycle**. Note that (X) is used to denote the contents of X and we take it that (PC) is `$100` to start:
        1. **Fetch** phase:
            - (PC) → placed on the address lines of the bus [`$100`];
            - (PC) + 2 → PC [`$102`];
            - Read signal is placed on the control lines of bus;
            - Begin read from store, placing data on the data lines of bus [`$DA78`];
            - Data lines on bus → IR [`$DA78`];
        2. **Decode** phase:
            - (IR) → decode logic in CPU.
        3. **Execute** phase:
            - (PC) → placed on the address lines of bus [`$102`];
            - (PC) + 2 → PC [`$104`];
            - Read signal is placed on the control lines of bus;
            - Begin read from store, placing data on the data lines of bus [`$1202`];
            - Data lines on bus → T1 [`$1202`];
            - (T1) → placed on the address lines of bus [`$1202`];
            - Read signal is placed on the control lines of bus;
            - Begin read from store, placing data on the data lines of bus [contents of location `$1202`];
            - Add the contents of the data lines of bus to the lowest order 16 bits of the 32-bit data register 5 in the ALU.
            - At the end of this operation the (PC) points to the next instruction, whose control word should be found in location `$104`.


[^legend]:
    - **PC**: Program Counter.
    - **IR**: Instruction Register.
    - **Rn**: Data Register n.
    - **MB**: Memory Buffer.
    - **MA**: Memory Address.
