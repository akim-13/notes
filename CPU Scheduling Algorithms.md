---
tags:
  - cm12002
  - CS
links:
  - "[[Operating Systems (OSs)]]"
  - "[[Computer Systems Architectures]]"
  - "[[OS Scheduling]]"
presentations:
  - W23_S6
  - W23_S7
---
# CPU Scheduling Algorithms
- **Early scheduling algorithms** were *very simple*, e.g., keep running the same program until it is done.
    - Some programmers would write their programs to **take advantage of deficiencies** in the scheduling algorithm, sometimes to the point of starving other programs of any CPU time at all.

- A scheduling algorithm **should not be overcomplicated** because the more time is spent scheduling the programs, the less time is spent actually running them. 
    - Therefore, scheduling algorithms should be **fast but fair**.

## Run Until Completion (FIFO)
- **Non-preemptive batch**, as on pre-OS machines^[See [[History of OSs]].].
- Good for **large amounts of computation**.
- **No overheads of multitasking**.
- **Poor interaction with other hardware**; can’t process while printing (recall [[./History of OSs.md#^spooling | spooling]])
- **No interactivity**, i.e. it does not allow for user interaction or input while tasks are being processed.
- The **modern usage** is that it is the basis for jobs on **large supercomputers**.

## Shortest Job First
- **Non-preemptive**, prioritizes tasks with the shortest time-to-completion.
- **No multitasking**, leading to **good throughput**.
- Similar behavior to **FIFO** on average.
- **Long jobs suffer** and might get starved.
- **Difficult to estimate time-to-completion**, so reliant on the job description for this information.

## Run Until Completion With Cooperative Multitasking
- **Non-preemptive** with **weak multitasking** capabilities.
- Utilizes round-robin or similar to choose another task on relinquish.
- **Poor interactivity**. 
- Easy for a process to **starve** other processes.
- **Hard to write "good citizen" programs**.
- **Was used on millions of PCs** for a long time.

## Preemptive Round Robin
- Gives each process in turn a **fixed time slice**.
- **Multitasking**. 
- Gives **interactive processes** the same time as compute processes.
- **No starvation**.
- **Better interactivity** than cooperative systems.
- But still **not really good for either interactive or real-time**; may have to wait a long time for a slice of time.

## Round Robin
- More **suited to systems where all the processes are fairly similar**; e.g., dedicated appliances like network routers that have to decide how to share network capacity fairly.

## Shortest Remaining Time (SRT)
- Time slice pick next process by the estimate of the **shortest time remaining**; **preemptive**.
- **Good for short jobs**.
- **Good throughput**.
- **Long jobs still can be starved**.
- Still **hard to make estimates of times**.

## Least Completed Next
- The process that has consumed the **least amount of CPU time next**.
- All processes make **equal progress** in terms of CPU time.
- **Interactive processes get good attention** as they use relatively little CPU.
- **Long jobs can be starved** by lots of small jobs.

## Highest Response Ratio Next
- A **variant of SRT**, where we take the time a process has been waiting since its last time slice into account.
$$ \text{Dynamic priority} = \frac{\text{Time so far in the system}}{\text{CPU used so far}} $$

- A process executes **repeated time slices** until its **priority drops** below that of another process.
- Tries to **avoid starvation**, so long jobs will eventually get a slice.
- **New jobs get immediate attention** as CPU time is near 0.
- But now **critical shorter jobs might not finish** in time as they could get scheduled after a long-waiting job.
- This **needs frequent re-evaluation of priorities** to get good behaviour, which implies small time slices, and so **lots of scheduling overhead**.
