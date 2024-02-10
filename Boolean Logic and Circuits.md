---
tags:
  - cm12002
  - CS
  - Math
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W10_L01_P01
  - W10_L02_P01
---
# Boolean Logic and Circuits
- There are **two kinds of logic/circuits**:
    1. **Combinational** (or **combinatorial**) — logic circuits that combine their inputs in a way that is:
        - *Static* — they do not change over time.
        - *Deterministic* — for each combination of inputs there is a single output.

        They are used to efficiently implement "timeless" operations such as **logic** and **arithmetic**.

    2. **[[Sequential Logic | Sequential]]** — logic circuits that incorporate feedback from their outputs. Hence, they are: 
        - *Dynamic* — they change over time.
        - *Potentially (!) non-deterministic* — they may have several possible outputs for a single given input. 

        They are used to  implement "stateful" operations such as **control circuits** and **memory cells**.
- A **Logic gate** is a basic building block of digital circuits that performs a [[./Logical Connectives.md | logical operation]] on one or more binary inputs and produces a single binary output. 

    ![[Attachments/Pasted image 20240202175413.png]]

- A **circuit** is multiple logic gates connected together:

    ![[Attachments/Pasted image 20240202175953.png]]

    - Circuits can be represented using [[./Boolean Formulae.md | Boolean formulae]]. For instance, the above example is equivalent to: $P = (A + B)C'$.

- There are **two ways** of ensuring that two formulas are **equivalent**:
    - **Equational reasoning** (by *algebra*) — use a series of known laws or axioms to get from one formula to the other by algebraic manipulation.
    - **Semantic reasoning** or **model checking** (by *truth table*) — verify that the two formulas have the same output value for each possible input combination.

- In order to **build a circuit based on a Boolean formula**, first the formula should be *simplified* as much as possible in order to use *the least number of gates*.

- **To simplify a Boolean formula**, the following procedure may be used:
    1. Write it in the form of a **[[./Standard Sum of Products (SofP).md | SofP]]**;
    2. Plot the product terms on a **[[Karnaugh Maps]]**;
    3. **Find** the *smallest* number of the *biggest* valid **groupings** that will encompass all of the marked squares (1s) of the Karnaugh map;
    4. **Eliminate variables** from each grouping;
    5. Write down **the sum of resulting products**;
    6. **Factorise** if possible.

    - For example, simplify the following formula or determine that it is already in the simplest form:
        $$ F = A + BC $$
        1. Write it down as a **SofP**:
        $$ F = ABC + ABC' + AB'C + AB'C' + A'BC $$
        2. The **Karnaugh map** is:

            ![[Attachments/Pasted image 20240206142235.png]]
        3. Find the **groupings**.
        4. The **groupings are simplified** to $A$ and $BC$, as shown above.
        5. $F = A + BC$, i.e. the initial formula is indeed **the simplest form** of this Boolean function.
