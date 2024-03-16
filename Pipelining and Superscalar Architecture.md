---
tags:
  - cm12002
  - cs
links:
  - "[[Computer Systems Architectures]]"
presentations: W09_L01_P01
---
# Pipelining and Superscalar Architecture
- A **CPU architecture** can be:
    - *Pipelined*.
    - *Superscalar*.
    - *Both* pipelined and superscalar.
    - *Neither* pipelined or superscalar.

- Some of the metrics used when evaluating the **performance of a CPU** are:
    - **Latency** — the time it takes to complete a single task or operation. 
    - **Throughput** — the number of tasks or operations a CPU can process in a given unit of time. Both pipelining and superscalar architecture focus on this aspect of performance. ^throughput

- **Pipelining** is a technique used to increase the *throughput* of the processor by allowing multiple instructions to be processed simultaneously in different stages of their execution.

- Consider the following version of the [[./Fetch-Decode-Execute (FDE) Cycle.md | FDE cycle]]: Fetch, Decode, Fetch (operands), Execute, Store. In this case, the execution of multiple instructions **utilizing pipelining** would look as follows:

    ![[Attachments/Pasted image 20231202130002.png]]

    This approach is similar to an assembly line on a factory, e.g. building a car.

- However, there are **issues with pipelining**:
    - **[[./Control Instructions.md#^branch-eg | Branches]]** break the pipeline, since the CPU has to guess whether to branch or not. If it guesses incorrectly, it has to flush and reload the process, hence wasting time. This problem can be minimized by:
        - Trying to **avoid branches** in code.
        - **Predictive decoding** — sophisticated algorithms the CPU uses in order to guess which branch will be taken.
        - Creating **multiple pipelines** — one for each possible branch.
    - **Dependencies** create instruction conflicts, e.g. instruction `STORE D5, 1000` might be dependent on the instruction `ADD D1, D5`, therefore it must come afterwards.
    - **Unequal stage times** and **load delays** may occur, since, for example, *fetch* is slower than *decode* or *execute* (it might need to access the memory). This stalls the pipeline, when one stage takes too long. Meaning in the ideal situation, the *latency* of each stage would be constant.

- **Superscalar architecture** refers to a design in CPUs where multiple instructions are executed in parallel during a single clock cycle. Similar to pipelining, it increases the throughput of a CPU.
    - It can also be referred to as a form of **instruction level parallelism** in which instructions are executed in parallel if they are recognized by the CPU as *not data dependent*.
    - The **key feature** of this architecture is the of use **redundant functional units** in the processor, i.e. multiple instances of the same type of a functional unit, such as multiple ALUs, bit shifters or multipliers (within a single CPU core).

- Pipelined and superscalar architectures **combined**:

    ![[Attachments/Pasted image 20231202134321.png]]
