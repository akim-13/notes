---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[History of OSs]]"
  - "[[Operating Systems (OSs)]]"
presentations:
  - W22_S4
---
# OS Modes and Rings
- **OS modes and rings** aim to solve the issue of programs being able to access parts of memory that they are not supposed to access.
    - Since every memory access has to be checked, the mechanism must be *fast* and *unobtrusive*, necessitating support on **both hardware and software levels**.

## OS Modes
- **OS mode** is a *software-level* control that dictates the level of privileges a running process has within the OS environment.

- There are generally^[Some systems may incorporate more than two OS modes.] **two OS modes/types of operations**:
    1. **Unprivileged mode** (also called **user mode**) allows for operations *any program can execute*, e.g. arithmetic operations, loads, stores, jumps and so on.
    2. **Privileged mode** (also called **kernel mode**) is reserved only for programs that require elevated privileges. It includes operations such as accessing the peripherals, rebooting the machine, etc.

## Rings and Privilege Elevation
- **Ring** is a *hardware-level* mechanism that enforces access control to critical system resources by categorizing operations into different privilege levels.
    - The **rings** typically **range** from 0 to 3, where 0 is the *most privileged* (**kernel**) level and 3 is the *least privileged* (**user**) level.

        ![[Attachments/Pasted image 20240302123740.png]]
    - Whilst not part of the standard rings architecture, there are also **negative rings**, e.g. -1, -2 and -3[^rings], which have even more control over hardware than the OS kernel. For instance, the latest Intel and AMD architectures use Ring -1 for *OS virtualisation*^[**OS virtualization** refers to the creation of multiple isolated virtual OS environments on a single physical hardware system, enabling different OS instances to run simultaneously and independently.].

[^rings]: ChatGPT:
    > - **Ring -2** is often associated with System Management Mode (SMM), a special operating mode used by the CPU for system-level functions like power management, hardware control, and other proprietary OEM functions. SMM operates at a level of privilege higher than the OS kernel, allowing it to execute code transparently to the operating system.
    > - **Ring -3** is related to the Intel Management Engine (ME) or similar technologies, which operate at a level below the operating system, providing out-of-band management features, remote administration capabilities, and other low-level control functionalities over the computer system, even when the system is powered off or the OS is non-functional.

- Note that **privilege is a state of the processor, not the program**. It is common to say "a privileged program", however what is actually meant is "a program running with the CPU in privileged mode".

- A **system trap** is a mechanism that *interrupts* the normal execution flow of a program if the program requires OS's attention, for example, in cases when it needs elevated privileges or encounters an error.

- A **system call** (or the **syscall instruction**) is a programmed request from a user program to the OS to perform a specific operation that requires elevated privileges.

- ** *All* privileged operations are performed on behalf of the OS**. 

    ![[Attachments/Pasted image 20240302143154.png]]
    - **User programs can never run their code in privileged mode** because the syscall instruction is *tied by the hardware* to always jumps to the same place in the OS.
    - Forcing access to hardware through the OS **ensures system security and resource efficiency** by centralizing control and oversight over hardware interactions.

## MMU
- The **Memory Management Unit** (**MMU**) is a special piece of hardware that contains a table of *flags* (usually 1-bit) that say whether the currently running (user mode) program can read or write a given area of memory.

    ![[Attachments/Pasted image 20240302153345.png]]
    - The memory is divided into **pages** — continuous areas of memory. A popular page size is 4096 bytes or 4 KB.
    - The OS gives each process its own **page table**, which maps *virtual addresses* (used by the process) to *physical addresses* (actual locations in memory). 
    - **When a process is created** or a new memory region is allocated to it, **the OS sets** the appropriate **flags in the page table** entries for that process's pages.
    - So each page has its corresponding flags. Some **examples of flags** include:
        1. *Readable:* 1 means this area of memory is readable, 0 means it is not.
        2. *Writable*.
        3. *Executable*.
    - Whenever **a process tries to access memory**, the **MMU checks the flags** for the corresponding page in the current page table.
    - **_Every_ access to memory is checked by the MMU** before it is allowed: this means the hardware that does this check has to be *very fast*.
    - **When the OS switches** from running one process to another, it changes the active page table to that of the next process to run, which takes up a lot of CPU cycles, i.e. _switching is a relatively slow operation._

## Example
- The following is **an example of a user program requesting elevated privileges with memory access** provided by ChatGPT:
    1. **User Program Initiates a System Call**
        - **Software Level (OS modes)**: A user-mode program requires a privileged operation, such as writing to a protected file. It cannot directly execute this operation due to its unprivileged status.
        - **Action**: The program invokes a system call to request this operation from the operating system.
    2. **System Call Triggers CPU Mode Switch**
        - **Hardware Level (Rings)**: The system call instruction signals the CPU to switch from user mode (Ring 3) to kernel mode (Ring 0), enabling the OS to perform privileged operations. This transition is enforced by the CPU's architecture.
    3. **Operating System Validates the Request**
        - **Software Level (OS modes)**: Now in kernel mode, the OS evaluates the request from the user program. It checks permissions and decides whether the requested operation is allowed.
    4. **MMU Configures Memory Access**
        - **Hardware Level (MMU)**: If the operation involves accessing specific memory areas (e.g., for reading or writing to a file), the OS configures the MMU to allow access to these areas. The MMU's page tables and flags are set accordingly to ensure that only the current operation can access the required memory, maintaining protection for other memory areas.
    5. **Operation Execution**
        - **Software and Hardware Levels**: The OS executes the requested operation, utilizing its kernel-mode privileges. This might involve direct interaction with hardware, managed through the CPU and MMU based on the permissions and settings configured in the previous steps.
    6. **Returning to User Mode**
        - **Hardware Level (Rings)**: After completing the privileged operation, the CPU switches back from kernel mode (Ring 0) to user mode (Ring 3), resuming the execution of the user program.
        - **Software Level (OS modes)**: The OS returns control to the user program, possibly providing the results of the operation (e.g., success or failure status).
    7. **MMU Reverts Memory Access Permissions**
        - **Hardware Level (MMU)**: If any temporary changes were made to memory access permissions for the operation, the MMU's configuration is reverted to ensure that the user program continues running with standard, restricted access to system resources.
