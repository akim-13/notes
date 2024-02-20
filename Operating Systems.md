---
tags:
  - CS
  - cm12002
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W21_L01_P02
---
# Operating Systems
- An **operating system** (also an **OS**, the **kernel** or **monitor**) is a program which essentially:
    1. **Manages [[./System Resources.md|system resources]]**.
    2. Provides an **API** (Application Programming Interface) for developers to build software applications. It allows for:
        - **Portability:** a program written on one machine could be run on another without or with minimal modification.
        - **Ease of use:** simplifies programming by abstracting the complexity of hardware from developers.
        - **Better performance:** optimizes the usage of system resources, potentially leading to more efficient execution of applications.

- Other **important function of an OS** include:
    1. Coordinating **application execution** 
    2. Ensuring system **security**.
    3. Managing **file systems** 
    4. **Handling errors** for stable performance.

- Importantly, **the (G)UI is *not* part of the OS**, but just another program that *uses the OS*.

    ![[Attachments/Pasted image 20240220214445.png]]
    - There was a time when some **OS vendors tried to tie the GUI into the OS** to gain *speed* and *commercial advantage*. However, it is considered to be a *poor design* and should be avoided because, for instance, bugs in the GUI would cause the OS to crash and take out the entire machine. Moreover, it was a *security risk*.
