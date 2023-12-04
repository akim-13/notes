---
tags:
  - cm12002
  - cs
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W09_L02_P01
---
# IO
- **Input/Output (IO)** is any transfer of information beyond the CPU and main memory (RAM).

- **External devices** (or **peripheral devices**) provide a means of exchanging data between the computer's external environment and the computer itself.
    - They attach to the computer through a link to an **IO module** —  a hardware component in a computer system that acts as an intermediary between the CPU and the peripheral devices
    - There are three **categories** of external devices:
        1. **Human readable** — used for communication with the computer user, e.g. monitors, printers, etc.
        2. **Machine readable** — used for communication with other equipment, e.g. disks, sensors, actuators, etc.
        3. **Communication** — used for communicating with remote devices such as a terminal, other machine readable devices, or another computer.

- The major **functions for an IO module** fall into the following categories:
    - **Error Detection** — detects and reports transmission errors.
    - **Control and Timing** — coordinates the flow of traffic between internal resources and external devices.
    - **Processor Communication** — involves command decoding, data, status reporting, address recognition.
    - **Device Communication** — involves commands, status information, and data.
    - **Data Buffering** — performs the needed buffering operation to balance device and memory speeds.

- There are three **techniques for IO operations**:
    1. [[Programmed IO]]
    2. Interrupt-driven IO
    3. Direct Memory Access (DMA)