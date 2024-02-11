---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W19_L01_P01
---
# Counters
- A **counter** is a [[./Registers.md | register]] that can be incremented by 1.
- **After** the **maximum** is achieved, next increment **sets counter to 0**.
- Register of *n* [[./Sequential Logic.md | flip-flops]] can count up to $2^n - 1$. For example, with 4 bits (i.e. 4 flip-flops) the counter starts at 0 and resets after reaching $2^4 - 1 = 15$.
- One example of a counter is the **PC (Program Counter)**.
- There are **two types of counters**:
    1. **Asynchronous** (also known as the **ripple counter**) — the change that occurs to increment the counter starts at one end and *“ripples”*  through to the other end. For example, a *4-bit up counter* that uses edge-triggered^[**Edge-triggered** means that the state changes with the *falling* edge of the clock pulse.] [[./Sequential Logic.md#Types of Flip-Flops| J-K flip-flops]]:^[There is no explanation of how it works in the book, however Fabio linked a [video](http://goo.gl/YsrsGF), which may or may not help.]

        ![[Attachments/Pasted image 20240211180030.png]]
        - However, the **problem with ripple counters** is that the delay is proportional to the length of the counter.
    2. **Synchronous** counters change all flip-flops of the counter at the same time. For example, a *3-bit synchronous counter* using three [[./Sequential Logic.md#Types of Flip-Flops| J-K flip-flops]]:

        ![[Attachments/Pasted image 20240211180832.png]]
        ![[Attachments/Pasted image 20240211181322.png]]
        ![[Attachments/Pasted image 20240211181247.png]]
        ![[Attachments/Pasted image 20240211181357.png]]

