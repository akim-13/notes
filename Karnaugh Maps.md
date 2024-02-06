---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Boolean Logic and Circuits]]"
presentations:
  - W10_L02_P01
---
# Karnaugh Maps
- **Karnaugh Maps** (also called **Veitch diagrams, Karnaugh/Veitch diagrams, Carroll diagrams**) is a method to simplify Boolean algebra expressions of up to 4 variables.^[It does work with more variables, but it is not very convenient, hence it is usually not worth it.] It reduces the need for extensive calculations by taking advantage of humans’ pattern-recognition capability.

- **In order to represent a Boolean formula** on a Karnaugh map, it has to be represented as a [[./Standard Sum of Products (SofP).md | SofP]].

- For the combinations of **2, 3 and 4 variables**, the Karnaugh maps are represented with **4, 8 and 16 regions** respectively:
    - **2 variables** example: $F = AB' + A'B$

        ![[Attachments/Pasted image 20240206124242.png]]

    - **3 variables** example: $F = A'BC' + A'BC + ABC'$

        ![[Attachments/Pasted image 20240206124349.png]]

    - **4 variables** example: $F = A'B'CD + AB'C'D + ABC'D'$

        ![[Attachments/Pasted image 20240206124502.png]]

- **The order of 00, 01, 11 and 10 is important.** Starting from 00, the next binary number is constructed using [Gray code](https://en.wikipedia.org/wiki/Gray_code)^[TODO: Link to week 5 "Data representation".], i.e. only one bit changes.

- Any adjacent squares of 1s represent a **grouping**. For example, a *grouping of 2* squares (see below) shows that the corresponding product terms differ in only one variable (the variable and its negation). Notice that in such case the value of this variable does not affect the resulting value of the formula, hence it can be *eliminated*:

    ![[Attachments/Pasted image 20240206131125.png]]

    - **Adjacency** can be extended to include **wrapping around the edge**:

        ![[Attachments/Pasted image 20240206131226.png]]

    - **To eliminate variables** from a grouping, write down the product of variables that do *not* change.
    - Examples of **a group of 4** adjacent squares:

        ![[Attachments/Pasted image 20240206131511.png]]

    - Examples of **a group of 8** adjacent squares:

        ![[Attachments/Pasted image 20240206131534.png]]

    - Notice that **the larger the grouping, the more variables can be eliminated**.
