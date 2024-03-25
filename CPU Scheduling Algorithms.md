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
  - W24_S7
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

## Multilevel Feedback Queue (MFQ)
![[Attachments/Pasted image 20240323175417.png]]

- Can be used when there are **no estimates of run times**.
- There are multiple FIFO run queues, `RQ0, RQ1, ... RQn`, with `RQ0` the **highest priority**, `RQn`, the **lowest**.
- Queues are processed in **FIFO fashion**, in priority order;
    - So `RQ1` does not get a look-in until `RQ0` has emptied;
    - And `RQ2` does not get a look-in until `RQ1` has emptied, and so on.
- If a **process appears in a higher queue**, we go back to that higher queue.
- Each process is allocated a **quantum** of time (a timeslice).
- A **new process** is admitted to the end (last) of `RQ0`.
- When the running **process has used its quantum of time**, it is interrupted and placed at the end of the next lower queue: **demoted**.
- If the running **process relinquishes voluntarily** before the end of the quantum, it gets placed back at the end of the same queue.
- If it **blocks for I/O**, it will be promoted and placed at the end of the next higher queue (when ready to run).
- **Demoted processes** in `RQn` get placed back at the end of `RQn`.
- Similarly **blocking processes** in `RQ0` get placed back at the end of `RQ0`.
    - This gives newer, **shorter processes priority over older**, longer ones.
- **I/O processes tend to rise**, getting more priority.
- **Compute processes tend to sink**, getting less.
    - Old processes tend to starve with this, so a variant doubles the quantum for each level: `RQ0` gets 1, `RQ1` gets 2, `RQ2` gets 4, and so on.
    - So compute intensive processes get a big bite, whenever they get a chance, at the potential cost of responsiveness to a new process.
- Another **advantage of MFQ** is that it does not need to do any arithmetic: it just moves processes between queues.
- MFQ was used in **Windows NT** and **UNIX derivatives**.

## Traditional UNIX scheduling
- The following algorithm was used in **older UNIX derivatives**, **nowadays** it is much **more sophisticated**.
- Everything is based on **timer interrupts every 1/60th second**.
- A priority is computed from the CPU use of each process
    $$ \text{Priority} = \text{Base priority} + \frac{\text{CPU time used}}{2} $$
    - The $\frac{1}{2}$ was a quirk of implementation and is not important.
- A process with the **smallest priority value is chosen next**. Thus — mostly — a process that has used less CPU.
- The **base priority** depends on whether this is a system process or a user process, with user priority being lower (i.e., with a larger value).
- Processes of the **same priority** are treated **round robin**.
- Note that this is actually very similar in effect to MFQ where a priority of n corresponds to `RQn`.
- The CPU use of a process is recorded and halved every second: this **decays the influence of CPU usage over time** and makes the **priority based on recent behaviour**.
    - This algorithm gives **more attention to processes that have used less CPU recently**, e.g., interactive and I/O processes.
    $$ \text{Priority} = \text{Base priority} + \frac{\text{Decayed CPU time used}}{2} $$
- Processes can choose to be **nice**. 
    - Generally, **−20 ≤ nice ≤ 19**, but only certain users (administrators) can use negative nices.
        $$ \text{Priority} = \text{Base priority} + \frac{\text{Decayed CPU time used}}{2} + \text{nice}$$
    - A process that has nice −20 can really **jam up the system**.
    - Nice also enables a **purchased priority**.
- There are a few **problems with this algorithm**:
    - The **priorities were recomputed once per second**, all in a single pass, taking a significant chunk of time (on old machines).
    - It **does not respond quickly** enough to dynamic changes in the system;
    - And **does not scale** to large numbers of processes;
    - So this **is not used in modern systems**, where many 100s of processes is common.

## Fair Share Scheduling
- Modern machines can support **many users simultaneously**, therefore if user A has 9 processes and user B just 1, the resources have to be allocated in a fair way.
- **Fair share scheduling** is where each user (or group or other collective entity) gets a fair share, rather than each process.
- Recall Unix processes are collected in groups in a tree: a **process group**, so:
    $$ \text{Priority} = \text{Base priority} + \frac{\text{CPU time used by process}}{2} + \frac{\text{CPU time used by process group}}{2} + \text{nice}$$

- However, **modern Unix derivatives** use much better, and much more complicated, scheduling algorithms than this.
    - They can afford to be more complicated as **CPUs are now much faster**.

