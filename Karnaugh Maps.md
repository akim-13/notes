---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Boolean Logic and Circuits]]"
presentations:
  - W10_L02_P01
  - W11_L01_P01
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

- It is possible to make a Karnaugh map for a formula in which some inputs do not have to be considered, either because they cannot arise or their corresponding output is not needed. Such inputs are called **"Don't cares"**.
    - "Don't cares" are **denoted with "x"** in the corresponding square of the Karnaugh map.
    - When grouping and simplifying, **each "x" can be treated as a 1 or a 0**, whichever leads to the simplest expression.

- An example of a situation with "don't care" inputs is a **seven-segment display** that uses *BCD*:

    ![[Attachments/Pasted image 20240207142158.png]]
    - It is driven by **binary coded decimal (BCD)**^[TODO: Link to W5 "Data representation".] to allow a separate set of combinational logic to turn on or off each segment to create the digit display. The digits $0-9$ can be represented using *4-bit patterns* or *Boolean formulae* over $A, B, C, D$, where $A$ is the most significant bit and $D$ is the least significant bit.

        ![[Attachments/Pasted image 20240207142919.png]]
        - If $ABCD = 0000$, the display should light the **digit 0** (segments a, b, c, d, e, f) 
        - If $ABCD = 0001$, the display should light the **digit 1** (segments b, c) 
        - If $ABCD = 0010$, the display should light the **digit 2** (segments a, b, d, e, g) 
        - ...                                                        
        - If $ABCD = 1001$, the display should light the **digit 9** (segments a, b, c, f, g) 
        - If $ABCD = 1010$ to $1111$, the inputs are ignored, i.e. they are the **"don't cares"**.
    - The **truth table** for each input and output is:

        ![[Attachments/Pasted image 20240207143539.png]]

    1. **Make a Karnaugh map for a segment (output)**. For example, the map for output "a" is:

        ![[Attachments/Pasted image 20240207144153.png]]
    2. Read off the resulting **formula**: $a = A + C + BD + B'D'$.
    3. Implement it as a **circuit**:

        ![[Attachments/Pasted image 20240207144545.png]]
    4. **Repeat** the steps $1-3$ for each segment.
