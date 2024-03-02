---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Operating Systems (OSs)]]"
  - "[[History of OSs]]"
presentations:
  - W22_S3-4
---
# Scheduling
- **Scheduling** is the process of assigning system resources, such as processor time and memory, to various tasks or jobs in a way that optimizes the overall performance and efficiency of the system.

- Initially, it was done **by hand**, and then it got **automated by the monitor**.^[See [[History of OSs]].]

- **Early scheduling algorithms** were *very simple*, e.g., keep running the same program until it is done.
    - Some programmers would write their programs to **take advantage of deficiencies** in the scheduling algorithm, sometimes to the point of starving other programs of any CPU time at all.

- A scheduling algorithm **should not be overcomplicated** because the more time is spent scheduling the programs, the less time is spent actually running them. 
    - Therefore, scheduling algorithms should be **fast but fair**.

- **Preemptive[^preemptive] scheduling** (or just **preemption**) is a type of scheduling that implements a *timer* and employs *interrupts*.
    - The **timer** can be set to send interrupts regularly after an appropriate period of time has elapsed in order to control unresponsive programs.
    - When the **interrupt** is taken, the interrupt service routine jumps to the OS and so it can decide what to do next, including:
        1. **Resume** running the interrupted program.
        2. **Kill** the interrupted program.
        3. **Switch** to another program.
    - This approach enabled **timesharing** — several programs share the available CPU time, and so appear to be running simultaneously to the user.
    - It also allowed for the use of **terminals** — historically, hardware devices consisting of a keyboard and a display screen. The users could now interact directly with the computer, not just via job submission.[^term]

[^preemptive]: **Preemptive** refers to taking action before a potential issue or situation occurs, with the intention of preventing an undesirable outcome or securing an advantage. It involves proactive measures to address or mitigate risks before they have a chance to manifest.

[^term]: The slides:
    > A program can sit and wait (i.e., not be scheduled to run by the OS) until the user hits a key on the terminal. When a key is hit, an interrupt happens, the OS takes over, schedules and runs the appropriate program to deal with the keystroke.
