---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Operating Systems (OSs)]]"
  - "[[OS Scheduling]]"
presentations:
  - W24_S7
  - W24_S8
---
# Deadlock
- A set of processes $D$ is **deadlocked** if both of the following conditions are met:
    1. Each process $P_i$ in $D$ is blocked on some event $E_i$;
    2. Event $E_i$ can only be caused by some process in $D$.

- A **deadlock can occur only if** both of the conditions are met:
    - There is **more than one [[./System Resources.md | resource ]]**;
    - There is **more than one [[./OS Processes.md | process]]**.^[It could technically happen with just one process, but that would be quite dumb programming to request for a resource you already have]

- Furthermore, deadlock is only possible if necessary **Coffman Conditions** are met:
    1. **Mutual exclusion**: only one process can use a resource at a time.
    2. **Hold-and-wait**: a process continues to hold a resource while waiting for other resources.
    3. **No preemption**: no resource can forcibly be removed from a process holding it.
    4. **Circular Wait**: there is a circular chain of processes where each holds a resource that is needed by the next in the circle.
    - If only conditions 1—3 are met, a deadlock is **possible**.
    - For a deadlock to **actually happen**, condition 4 must be met, which is equivalent to the formal definition above.

- **Example of a deadlock** in the OS:
    - Process P1 wants to copy some data from disk D1 to disk D2, while process P2 wants to copy some data from disk D2 to disk D1.
    1. Initially P1 is running and makes a request for access to D2;
    2. The OS takes over and gives P1 exclusive access to D2;
    3. The OS decides to run P2 (not a smart OS);
    4. P2 runs and makes a request for access to D1;
    5. The OS takes over and gives P2 exclusive access to D1;
    6. The OS decides to run P1
    7. P1 runs and makes a request for access to D1
    8. The OS takes over and notices P2 has locked D1, so P1 must wait until P2 has finished with it; P1 moves to state blocked
    9. The OS decides to run P2: it can’t run P1 as it is blocked
    10. P2 runs and makes a request for access to D2
    11. The OS takes over and notices P1 has locked D2, so P2 must wait until P1 has finished with it; P2 moves to state blocked
    12. Now both P1 and P2 are blocked and the OS can’t run either process!
        - P1 can’t run until D1 is free, but D1 won’t be free until P2 runs.
        - P2 can’t run until D2 is free, but D2 won’t be free until P1 runs.
        - Hence, a deadlock.
