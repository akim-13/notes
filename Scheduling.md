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
