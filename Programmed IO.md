---
tags:
  - cs
  - cm12002
links:
  - "[[Computer Systems Architectures]]"
  - "[[IO]]"
presentations:
  - W09_L02_P01
---
# Programmed IO
- **Programmed IO** is a method of data transfer between the CPU and external devices, where the data transfer is managed by explicit instructions (or *programs*, hence the name) executed by the CPU, requiring the CPU to actively control and monitor the entire I/O process.

- The simplest and most general **way to deal with IO** is:
    1. A stored *instruction is fetched* to the IR in the CPU and turns out, upon decoding, to be an IO operation.
    2. An instruction from the control unit to the IO control unit causes the *IO control unit to send signals to the device* to set it into action.
    3. Data will need to be transferred to the device (a write) or from the device (a read). An obvious place to put this data is in a *data register*.

        ![[Attachments/Pasted image 20231203140625.png]]

    - Since there may be **several external devices**, the IO instruction must contain the following three parts:
        1. An IO **[[./Fetch-Decode-Execute (FDE) Cycle.md#^motorola | opcode]]**.
        2. The **direction** of transfer (read/write).
        3. The **address** of the device.

    - IO data placed on a common **IO data bus**, whereas the address is placed on a common **IO address bus**.
        - The main **advantages** of using a common IO data bus are *simplicity* and *flexibility* — a single I/O control system with a single connection to the CPU.
        - The **disadvantages** are the *cost of building* a shared bus and the possibility of ***contention*** — a situation when multiple devices try to communicate over the bus simultaneously. ^contention
    - It is assumed that each device has its own **data register** or **buffer** that holds data passing into or out of the device. This also allows the device to **identify its own address**.

- **Memory mapped IO** refers to an architecture where external devices are mapped into the same address space as the program's memory, allowing the CPU to interact with these devices using standard memory instructions.^[As opposed to addressing a limited number of locations, depending on how many address lines of the bus there are (e.g. 24 lines means $2^{24}$ possible locations).]

    ![[Attachments/Pasted image 20231204090808.png]]

    - With this arrangement, the IO data is transmitted along the *data lines* of the bus; device and store addresses along the *address lines*; and read/write information along the *control lines*.
    - **Advantages** of this method are:
        1. Simplified IO control means the **CPU is freed** for other uses.
        2. **No special IO instructions** are needed in the machine's instruction set, akin to the [[./CISC vs RISC.md | RISC]] philosophy.
    - **Disadvantages** are:
        1. **Less storage**, since address space is used for devices.
        2. IO devices are in **[[./IO.md#^contention | contention]]** with the store for the same bus.
        3. Programs may be **harder to understand**, as IO and storage can be confused.

- A **major problem** with programmed IO is that IO device operation often involves some sort of *electro-mechanical process*, e.g. depressing keys on a keyboard, or waiting for a magnetic disc to spin into the correct position for data to be transferred to or from a specific place on the disc surface. 
    - This is inherently much slower that the electronic transfer of data within a CPU, leading to **IO timing problems**, such as waste of resources (since CPU may be idle while waiting), performance bottlenecks, difficulty in synchronisation, etc.

- The IO timing problem can be helped with **device flags** — a one-bit register on each device, where `1` indicates that the device is *idle/ready* for an IO action, whereas `0` means that it is currently *busy*. Device operation can therefore be controlled by testing the device status flag and not starting an IO transfer until the device is ready.
    1. When an IO transfer is **started**, the device status flag is unset to the `0` state *by the CPU* to indicate that the device is busy doing a transfer.
    2. When the transfer is **complete** the *device itself* sets the device status flag to `1`, to indicate that the transfer is complete and that the device is idle.

- There are two **protocols** for programmed IO transfer using device flags:
    1. **Busy waiting** — if the device flag is `1` (idle) then reset it and transfer data, if it is `0` (busy) then test the flag again.

        ![[Attachments/Pasted image 20231204100741.png]]
        ```
        load next data to send to I/O device x;
        initiate I/O device x;
        test I/O device x’s status flag;
        if flag not set, 
            repeat last instruction (test).  /* wait */
        write data to device
        ```
    2. **Polling** — if the device flag is `1` then reset it and transfer data, if it is `0` then *perform another task* for a fixed time, then repeat the test.
        ```
        load next data to send to I/O device x;
        initiate I/O device x;
        test I/O device x’s status flag;
        if flag not set, 
            Do something else for a while, and go to previous step (test).
        write data to device
        ```
        - Polling allows the CPU to get on with background computations, however it has the following **disadvantages**:
            - **Unresponsiveness**: if the device flag becomes idle just after being polled, then transfer must wait until the next poll.
            - **Multiple devices**: a fast device might need to do IO at the same time as a slow device.
            - **Complexity**: polling is a more difficult programming task in terms of implementation.
