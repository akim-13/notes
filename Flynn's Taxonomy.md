---
tags:
  - cm12003
  - CS
links:
  - "[[Computer Systems Architectures]]"
---
# Flynn's Taxonomy^[**Taxonomy** is a classification or organization scheme.]
|                                         | **<u>S</u>ingle <u>D</u>ata Stream** | **<u>M</u>ultiple <u>D</u>ata Streams** |
|-----------------------------------------|--------------------------------------|-----------------------------------------|
| **<u>S</u>ingle <u>I</u>nstruction**    | SISD                                 | MISD                                    |
| **<u>M</u>ultiple <u>I</u>nstructions** | SIMD                                 | MIMD                                    |

- **SISD** (Single Instruction, Single Data) is an example of a uniprocessor architecture, for instance classical [[./Harvard Architecture.md | Harvard]] or [[./Von Neumann Architecture.md | Von Neumann]] architectures.

    ![[Attachments/Pasted image 20231029212924.png]]^[**PU** stands for Processing Unit.]

- **SIMD** (Single Instruction, Multiple Data) allows to execute the same instructions in different memory positions (i.e. different data values).

    ![[Attachments/Pasted image 20231029213428.png]]
    ![[Attachments/Pasted image 20231029213448.png]]
    - It is most suited to apply a **basic operation** to a **large dataset**. For instance, processing of *graphics* (e.g. single greyscale filter instruction applied to all pixels of an image), *sound* (e.g. autotuning a song), etc. Moreover, the GPUs (e.g. in Xbox) use SIMD for the same reason.

- **MISD** (Multiple Instructions, Single Data) allows to perform different operations on the same data.

    ![[Attachments/Pasted image 20231029214753.png]]
    ![[Attachments/Pasted image 20231029214823.png]]^[It does not have to be the same instruction like `load`. It can be, for example, P1: `load A(1)`, P2: `store A(1)`, Pn: `move A(1)`. (Actually I'm not sure, check later.)]
    - It is frequently used for **fault-tolerant computing**, for example in space shuttles, where errors are unacceptable. It creates redundancy by processing the same data with multiple instruction streams (i.e. different algorithms) to ensure that if one fails, the other will be able to back it up. Furthermore, it allows for error detection and correction by noticing and preventing discrepancies in results of calculations.

- **MIMD** (Multiple Instructions, Multiple Data) allows multiple processors to function asynchronously and independently.

    ![[Attachments/Pasted image 20231029220046.png]]
    ![[Attachments/Pasted image 20231029220053.png]]
    - This architecture is used in modern multi-core processors.
