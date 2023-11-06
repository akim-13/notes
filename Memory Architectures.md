---
tags: cm12002, CS
links: "[[Computer Systems Architectures]]"
---
# Memory Architectures
- There are **two main types** of memory architectures — either *shared* or *distributed*.
- In **shared memory** each processor has access to the same memory space.

    ![[Attachments/Pasted image 20231029222028.png]]
    ![[Attachments/Pasted image 20231030134810.png]]
    - **Effectively** utilizes memory space.
    - However, it also lead to **memory-to-CPU bottlenecks**, i.e. the CPUs start to process data faster than it can be retrieved from memory.
    - **Cache coherence** becomes a problem, i.e. if each CPU has it's own cache, then inconsistencies may arise. 
         - For example:
            1. *CPU1* reads a value from the shared memory and stores it in its cache.
            2. *CPU2* then reads the same value from the shared memory into its cache.
            3. *CPU1* modifies its cached value.
            4. *CPU2*, unaware of the modification made by *CPU1*, might continue to work with the old value it cached earlier, leading to inconsistency.
        - This problem is solved by **coherence protocols**^[More about this later in the unit.].
    - Typically **does not scale well** due to the aforementioned issues.

- In **distributed memory** each processor has its own data store (memory).

    ![[Attachments/Pasted image 20231029222038.png]]
    ![[Attachments/Pasted image 20231030134910.png]]
    - Easy to **scale up** the number of parallel processors.
    - However, the processors **communicate indirectly**, which is inefficient.
    - **Distributing** (before computation), and then **reassembling** the data (after computation) **is non-trivial**.

***<span style="color:red">TODO: ASK IF FURTHER INFO IS REQUIRED FOR THESE COMPROMISE SOLUTIONS.</span>***
- There are also **compromise solutions**, which utilize different elements of the main types:
    - **Virtual shared memory** — distributed memroy which "seems" shared to the CPUs. 
    - **Non-Uniform Memory Access (NUMA)** — shared memory which has parts which are faster for each CPU.
