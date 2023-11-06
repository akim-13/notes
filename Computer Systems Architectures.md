---
tags:
  - cm12002
  - CS
links:
---
# Computer Systems Architectures

- Classically **uniprocessor^[Uniprocessor architectures are characterised  by having one ALU.] architectures** include:
    - [[Von Neumann Architecture]]
    - [[Harvard Architecture]]
- **Multiprocessor** (or **parallel**) **architectures** are potentially faster but harder to understand, control and predict.
    - There is no single dominant parallel architecture, but a set of alternatives that depend upon different **types of parallelisms** (either on *task* or *data* level) described by the [[Flynn's Taxonomy]].
    - There is a limit on how much a process can be parallelized described by the **[[Amdahl's Law]]**.
- There are different types of **[[Memory Architectures | memory architectures]]** — shared and distributed.

# Unsorted
## Shared Memory MIMD
- **Shared memory MIMD** is becoming dominant in general purpose computing, due to the diminishing returns on building larger/faster uniprocessors.
- **Multi-core processors** — multiple CPUs on the same chip — are now standard. 
    - They are typically used for **multitasking**.
    - However, it can be **challenging to design software** that effectively utilises multithreading capabilities.
