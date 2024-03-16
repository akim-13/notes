---
tags:
  - cm12002
  - CS
links:
  - "[[Operating Systems (OSs)]]"
presentations:
  - W23_S5
---
# OS Processes
- **Process** (or **task**, **job**) — the *executable code*, *its data* and the *associated information* the [[./Operating Systems (OSs).md | OS]] needs to run it.

- Computer programs can be **structured in three ways**:
    1. **Structure by process**: a single program might use more than one process to perform its tasks. Each process is a completely separate execution environment, with its own memory space, which helps in isolating tasks for better security and stability. 
        - Programs are **rarely structured by process**, with the **exception of web-browsers**, which use different processes for different tabs to prevent one tab accessing the information of another.
    2. **Multithreading**: one process that uses multiple threads of execution, i.e. individual sequences of executed instructions.
        - This is a **more common approach** since threads share the same memory and resources of their parent process, making them quicker to create and switch between compared to processes. 
    3. **Hybrid**: multiple processes that utilize multithreading. *Non-assessable.*

- The OS has to [[OS Scheduling| schedule]] and [[./OS Memory Protection.md | protect]] processes. Therefore, it has to **keep track of a lot of information** about each process, including:
    - Where in memory its **code** is.
    - Where in memory its **data** is.
    - What **permissions** it has on those parts of memory ([[./OS Memory Protection.md#MMU | MMU flags]]).
    - How much **time** it is **allocated**.
    - How much **time** it has **used**.
    - The CPU's **PC** (so that the process can resume execution from the correct place) and **[[./Registers.md | registers]]** (to restore the state of the process).
    - **User identifier**.
    - A **priority**.
    - **Statistics** like memory and CPU used
    - The scheduling **state** (see below).

- The collection of data a process needs is called the **process control block**, or **PCB**. The above list is an example of a PCB.
    - **When a process is interrupted**, all data is stored in the PCB in order to later be retrieved when the process gets scheduled to run again.

- A process can be in one of several **states**. In a simplified model, the **five main states** are:
    1. **New**: A process that has just been created. The OS does the following in this state:
        - Allocate and create **PCB** structure.
        - **Find** a free **PID**.
        - Determine and allocate the necessary **resources** (in particular memory).
        - Determine the initial **priority** of the process.
        - Insert PCB into the relevant **kernel list of PCBs** — a data structure maintained by the OS's kernel that contains the PCBs of all processes.
    2. **Running**: It is currently executing on the CPU.
    3. **Ready**: It is ready to run, but not currently running as some other process is currently using the CPU.
    4. **Blocked**: Can’t run right now as it is waiting for some event or resource to become available. E.g., waiting for a block of data to arrive from the disk.
    5. **Exit**: A process that has finished. Some tidying up is usually needed after a process ends, such as closing files or reclaiming memory or other resources it used. *Happens once per process.*

- The OS will have **sets of processes in each state**, so the scheduling decision is making the choice of which process to move between which states.
    - **In real OSs**, these **sets use more sophisticated datastructes** instead of simple lists, e.g. a *pair of lists*, one for real-time processes and the other for non-real-time; or a *tree*, which allows for easy manipulation of whole bunches of (usually related) processes in a simple way. For instance, tress are used in UNIX systems:

        ![[Attachments/Pasted image 20240306195315.png]]

- There is a **standard finite state machine** that describes the allowed transitions between states:

    ![[Attachments/Pasted image 20240306195625.png]]

- An **example of a typical transition** is:
    1. The OS decides to **schedule** a process **on the ready list**;
    2. The process is **dispatched**, i.e., the OS marks its state as running and starts executing it (it jumps and then [[./OS Memory Protection.md#Rings and Privilege Elevation | drops privilege]]);
    3. The process **may** choose to voluntarily suspend itself: **relinquish** (e.g., a clock program displaying the time might suspend itself for a minute);
    4. Or an **interrupt may arise**, e.g., from a packet arriving on the network card, or a key being hit on the keyboard.
    5. Or a **timer interrupt may arise**. In any of these three cases the OS moves the process to the Ready state.
    6. Or the running **process may need some resource** the OS must supply (e.g., for disk access) so it does a syscall and must wait until the resource is ready (e.g., the disk returns some data); the OS moves it to *Blocked*.
    7. **In the case of a blocked process**, perhaps data has returned from the disk and the process can wake up and become *Ready* again. Note that the process won’t necessarily start running immediately, it is just ready to run when it gets its chance.

- **Example processes** under Linux:

    ![[Attachments/Pasted image 20240306201434.png]]

    - `User`: the user who owns the process.
    - `PID`: process identifier. An integer that uniquely identifies this process.
    - `PPID`: parent PID. The PID of the process that started this process. This allows processes to be grouped in trees. Process number 1 is the parent of all processes.
    - `PRI`: priority. In Linux, priorities are integers, larger indicates less important.
    - `CPU, MEM, TIME`: how much of these resources this process is using.
    - `STAT`: current status:
        - `S`: sleeping: like blocked (interruptible sleep; waiting for an event like a timer or other interrupt).
        - `D`: disk wait (uninterruptible sleep; waiting for requested I/O).
        - `R`: running or ready to run.
        - `s`: session leader.
        - `+`: foreground process group.
        - `l`: multithreaded.
        - Note that it is hard to catch new and exiting processes.

- Most **processes are** created (**forked**/**spawned**) by other processes (of course, only the OS can actually create processes). For example:
    1. A process decides it **wants to start another process**. E.g., a GUI process as a response to a user clicking on an icon;
    2. It calls the OS kernel (**syscall**), telling it what process it want to start (e.g., “start the browser program”);
    3. **OS can now create a new process** according to the specifications given;
    4. New process can now be **scheduled**.
    5. However, the **OS can choose not to create the new process** if some policy says not to, or there is not enough memory, or some other reason. In that case, the originating process usually gets a message back from the OS (via the value returned from the syscall) explaining the problem.
