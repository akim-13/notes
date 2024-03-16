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
# OS Scheduling
- **Scheduling** is the process of assigning system resources, such as processor time and memory, to various tasks or jobs in a way that optimizes the overall performance and efficiency of the system.

- Initially, it was done **by hand**, and then it got **automated by the monitor**.^[See [[History of OSs]].]

- There are different **[[./CPU Scheduling Algorithms.md | scheduling algorithms]]**, including:
    1. Run Until Completion (**FIFO**).
    2. Shortest Job First (**SJF**).
    3. **Run Until Completion With Cooperative Multitasking**.
    4. **Preemptive Round Robin**.
    5. **Round Robin**.
    6. Shortest Remaining Time (**SRT**).
    7. Least Completed Next (**LCN**).
    8. Highest Response Ratio Next (**HRRN)**.
    9. Multilevel Feedback Queueing (**MFQ**).

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

- Scheduling is an *extremely difficult problem* because there are a lot of **problems to be accounted for**:
    1. Try to give each process its **fair share of CPU** time.
    2. **No starvation** of any process.
    3. Try to make interactive processes **respond in human timescales**.
    4. Try to give as much computation time as possible to **compute-heavy processes**.
    5. Ensuring **critical real-time processes** are dealt with before it is too late.
    6. Try to service **peripherals** in a timely way.
    7. Understanding the various **requirements of hardware**: mice and printers are slow; networks and disks are medium; memory is fast.
    8. Try to **distribute work** amongst multiple devices; e.g, CPUs, disks and networks.
    9. Try to make behaviour **predictable**: do not allow for wildly erratic behaviour.
    10. Try to **degrade gracefully** under heavy load.

- Measurements used to **quantify the available resources** include:
    - **CPU cycles** used.
    - **Memory** used.
    - **Disk** used.
    - **Network** used.

- The outcome of utilization of [[./System Resources.md | system resources]] can be measured, for example, using:
    - **[[./Pipelining and Superscalar Architecture.md#^throughput | Throughput]]**; more or fewer jobs finished in a given time.
    - **Turnaround**: the total time taken from the submission of a task to the completion of the process, encompassing all stages of processing.
    - **Response time**: interactive response is snappy or sluggish.
    - **Meeting real-time deadlines**; some data must be dealt with now or the system will crash.
    - **Money**; e.g. being given money to get this data ready in the next hour.

- **Initially**, all the above **measurements were collected to figure out how much money to charge** the user.
    - Although **today it is** not the main concern of most people (the main one is making the best use of the computer), it is still **important for cloud services** like Amazon, Google and Microsoft that sell time on their machine. They charge based on *disk storage*, *data input and output* and *compute (CPU) used*.
