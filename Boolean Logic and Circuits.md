---
tags:
  - cm12002
  - CS
  - Math
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W10_L01_P01
---
# Boolean Logic and Circuits
- There are **two kinds of circuits**:
    1. **Combinational** (or **combinatorial**) — logic circuits that combine their inputs in a way that is:
        - *Static* — they do not change over time.
        - *Deterministic* — for each combination of inputs there is a single output.

        They are used to implement "timeless" operations such as **logic** and **arithmetic**.

    2. **Sequential** — logic circuits that incorporate feedback from their outputs. Hence, they are: 
        - *Dynamic* — they change over time.
        - *Potentially (!) non-deterministic* — they may have several possible outputs for a single given input. 

        They are used to  implement "stateful" operations such as **control circuits** and **memory cells**.
- A **Logic gate** is a basic building block of digital circuits that performs a [[./Logical Connectives.md | logical operation]] on one or more binary inputs and produces a single binary output. 

    ![[Attachments/Pasted image 20240202175413.png]]

- A **circuit** is multiple logic gates connected together.

    ![[Attachments/Pasted image 20240202175953.png]]

    - Circuits can be represented using [[./Boolean Formulae.md | Boolean formulae]]. For instance, the above example is equivalent to: $P = (A + B) . C'$.

- There are **two ways** of ensuring that two formulas are **equivalent**:
    - **Equational reasoning** (by *algebra*) — use a series of known laws or axioms to get from one formula to the other by algebraic manipulation.
    - **Semantic reasoning** or **model checking** (by *truth table*) — verify that the two formulas have the same output value for each possible input combination.
