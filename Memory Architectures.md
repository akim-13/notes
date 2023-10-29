---
tags: cm12002, CS
links: "[[Computer Systems Architectures]]"
---
# Memory Architectures
- There are **two types** of memory architectures — either *shared* or *distributed*.
- In **shared memory** each processor has access to the same memory space.

    ![[Attachments/Pasted image 20231029222028.png]]
    - **Effectively** utilizes memory space.
    - However, it also lead to **memory-to-CPU bottlenecks**.
    ***TODO: LOOK UP CACHE COHERENCE*** 
    - **Cache coherence** becomes a problem.

- In **distributed memory** each processor has its own data store (memory).

    ![[Attachments/Pasted image 20231029222038.png]]
