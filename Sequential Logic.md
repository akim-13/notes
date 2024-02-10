---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Boolean Logic and Circuits]]"
presentations:
  - W11_L03_P01
---
# Sequential Logic
- The **flip-flop** is the simplest form of sequential circuit. The **three properties** of flip-flops are:
    1. It is a **bistable device** — it exists in one of two states and, in the absence of input, remains in that state. This property allows the flip-flop to function as a *1-bit memory*.
    2. The flip-flops have **two outputs**, which are *always* **complements** of each other (generally labeled $Q$ and $Q'$).
    3. Has a **clock** component to synchronize inputs.

## SR Latch

- The **SR latch** (or the **Set-Reset latch**) is a flip-flop without the clock. It has:
    1. **Two inputs**: $S$ (Set) and $R$ (Reset).
    2. **Two outputs**: $Q$ and $Q'$, where $Q$ is the output value we are interested in, i.e. the "value" of the bit if this circuit were act as a 1-bit memory.
    3. **Two [[./Boolean Logic and Circuits.md | NOR gates]]** connected in a feedback way.

        ![[Attachments/Pasted image 20240210144940.png]]

- The **SR latch works as follows**:
    1. Consider an **initial state**:

        ![[Attachments/Pasted image 20240210145622.png]]
    2. The **Set** operation:

        ![[Attachments/Pasted image 20240210145721.png]]
    3. The **Reset** operation:

        ![[Attachments/Pasted image 20240210145828.png]]
    4. When **Set and Reset** are applied **simultaneously** the output becomes *inconsistent* (both $Q$ and $Q'$ equal to 0). Therefore $S = 1$ and $R = 1$ inputs **are not allowed**.

- The SR latch can also be defined using a **characteristic table** which shows the next state or states of a sequential circuit as a function of current states and inputs:

    ![[Attachments/Pasted image 20240210151243.png]]

- The **inverted SR latch** is implemented using [[./Boolean Logic and Circuits.md | NAND gates]]. It *Sets* when $S = 0$, *Resets* when $R = 0$, and the disallowed inputs are $S = R = 0$:

    ![[Attachments/Pasted image 20240210154151.png]]

- There are **two problems** with the SR latch:
    1. There are **disallowed inputs** ($S = R = 1$), which lead to inconsistent behaviour.
        - **Solution:** avoid states that cause such behaviour by adding gates to control the inputs.
    2. It is **asynchronous** — there is a delay before a logic gate responds to an input. This means that two separate gates *cannot switch simultaneously*. Furthermore, in circuits with several sequential components, output states may depend on the order in which changes to inputs occur, or the moment the circuit is tested.

        ![[Attachments/Pasted image 20240210152828.png]]
        ![[Attachments/Pasted image 20240210152903.png]]
        - **Solution:** use a *clock input* to enable/disable transitions (see *SR flip-flop* next).

## Types of Flip-Flops
- There are **three types of flip-flops**:
    1. **SR flip-flop** (also known as **clocked SR flip-flop** or **gated SR latch**) — an extension of the SR latch that responds to inputs *only when the clock signal is present*, rather than at any time.

        ![[Attachments/Pasted image 20240210181915.png]]
        ![[Attachments/Pasted image 20240210184443.png]]
        - However, the SR flip-flop still has the issue of **disallowed inputs** being passed to it.
    2. **D flip-flop**^[The **D** stands for *Data* or *Delay.*] — by using an inverter, the nonclock inputs to the two AND gates are guaranteed to be the opposite of each other, hence *solving the problem of disallowed inputs.*

        ![[Attachments/Pasted image 20240210182358.png]]
        - It is also referred to as the **data flip-flop** because it is, in effect, *storage for one bit of data*. The output of the D flip-flop is always equal to the most recent value applied to the input. Hence, it remembers and produces the last input.
        - Moreover, it may be referred to as the **delay flip-flop**, because it delays a 0 or 1 applied to its input for a single clock pulse. 
    3. The **JK flip-flop** (or the **universal flip-flop**^[It may be referred to as **universal** because it can act both as the *SR flip-flop* and the *D flip-flop.*]) makes use of the restricted (1, 1) inputs in order to *toggle* the output state of the flip-flop.

        ![[Attachments/Pasted image 20240210184036.png]]
