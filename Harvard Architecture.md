---
tags: cs, cm12002
links: 
---
# Harvard Architecture (HA)
- **The HA** is an architeture with *separate* stores for data and instructions. 

    ![[Attachments/Pasted image 20231024140229.png]]

- It allows the CPU to acess instructions and data **simultaneously** resulting in better performance.
- It is **useful for**:
    - **Embedded applications**, e.g. *microcontrollers*[^microcontr] and *signal processors* (e.g., data from sensors) with instructions stored in ROM.
    - **Parallel fetching** of code and data in sophisticated processors. 

[^microcontr]:**Microcontroller:** a small computer on a single integrated circuit containing a processor core, memory, and programmable input/output peripherals (basically one device with ALU, control unit, I/O, memory). Typically designed for embedded application.

    ![[Attachments/Pasted image 20231024141539.png]]

- The **first computer to use** the HA was *The Harvard Mark I* in 1944.
- The HA can be modified into a **HA/[[./Von Neumann Architecture.md | vNA]] hybrid** by introducing separate caching for code and data to increase efficiency. *(How?)*
