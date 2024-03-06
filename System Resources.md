---
tags:
  - cm12002
  - CS
links:
  - "[[Operating Systems (OSs)]]"
  - "[[Computer Systems Architectures]]"
presentations:
  - W21_L01_P02
---
# System Resources
- A **system resource** is any physical or virtual component of limited availability within a computer system. 
- There are **two types of resources**:
    - **Hardware** — all connected devices and internal system components, e.g. the CPU, memory, printer.
    - **Software** — virtual entities and services that the OS provides and manages, such as file handles, network sockets, and [[OS Processes | processes]].[^resources] 

[^resources]: ChatGPT:
    > For example, a file handle allows a program to read or write to a specific file, and each handle is a resource because the operating system can only manage a finite number of them simultaneously. Network sockets enable network communication, and they are limited by the operating system's capacity to handle connections. Processes are instances of running programs, and they are considered resources because they require and consume system memory and CPU time.]

- Resources have to be **managed** by the OS because:
    1. They are **limited**: Most computers are constrained either by *size* (e.g., mobile phones with limited memory) or by *efficiency in* terms of *energy consumption* (e.g., supercomputers that are expensive to operate).
    2. They need **protection**:
        - **Security** — protecting programs and data from corruption by other programs, whether accidental or intentional.
        - **Authorization** — restricting resource access to approved programs or users.
        - **Safety** — warning users before they perform potentially harmful actions, like deleting files.
    3. They must satisfy performance and operational **criteria**, such as:
        - **Responsiveness**: Ensuring programs react quickly to user input or process incoming network packets promptly.
        - **Real-time performance**: Handling certain tasks within a strict time frame, which is critical for applications like video streaming.
