---
tags:
  - cm12002
  - CS
---
%%
links:
%%
# Von Neumann Architecture (vNA)
- **The vNA** is a computer architecture based on a 1945 description by John von Neumann that combines instruction and data stores.
- The **first computer to implement** the vNA was *The Manchester Baby* in 1940s.
- The vNA **components** are: 
    1. **ALU** (Arithmetic Logic Unit) processes the data.
    2. **Control Unit** (CU) is used to:
        - Determine the operation to be performed.
        - Select the correct opeands and make them available at the right time.
        - Perform the operation on the operands by supplying the correct control data to the ALU.
        - Determine the next operation to be performed.
    3. **Memory** stores *both data and instructions* - the **main feature** of the vNA.
    4. **External mass storage**.
    5. **I/O mechanisms**.
    6. **Busses**, i.e. connections between components.
- The **CPU** is a combination of the CU and ALU.

    ![[Attachments/Pasted image 20231012095028.png]]
- The **von Neumann bottleneck** (a.k.a the **memory wall**) is the main limitation of the vNA. It occurs when the CPU is continually forced to wait for needed data or instructions to be transferred to or from memory via the shared bus (due to the transfer speed not being fast enough).
    - Since CPU speed and memory size have increased much faster than the throughput between them, the bottleneck has become more of a problem, a problem whose severity increases with every newer generation of CPU.
    - This issue can be **solved** either by incorporating an *alternative architecture* with distributed storage (e.g. [[./Harvard Architecture.md | the Harvard architecture]]) or by *minimising use of main memory* (e.g. by using [[./Cache.md | cache]] or [[./Registers.md | registers]]).

