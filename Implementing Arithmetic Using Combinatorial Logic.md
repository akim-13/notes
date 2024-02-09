---
tags:
  - cm12002
  - CS
links: 
presentations:
  - W11_L02_P01
---
# Implementing Arithmetic Using Combinatorial Logic
## Addition and Subtraction
- A **half-adder** add 2 one-bit binary numbers. They have:
    1. **Two inputs** ($A, B$).
    2. **Two outputs** (The *sum* of $A$ and $B$ and the *carry*).

    ![[Attachments/Pasted image 20240209134120.png]]
    - Notice that the truth tables of "Sum" and "Carry" correspond to the truth tables of XOR and AND, hence the **[[./Boolean Logic and Circuits.md | circuit]] implementation**.

- A **full-adder** also adds 2 one-bit binary numbers, however they are called *full* because they have one more input:
    1. **Three inputs** ($A, B$ and $C_{\text{in}}$, i.e. the *input carry*).
    2. **Two outputs** (The *sum* of $A$ and $B$, and the *carry*).

    - The circuit is implemented by writing the "Sum" and "$C_{\text{out}}$" outputs as a [[./Standard Sum of Products (SofP).md | SofP]]:

        ![[Attachments/Pasted image 20240209135517.png]]

    - However, the above expressions and **circuits can be [[./Boolean Logic and Circuits.md | simplified]]** using the [[./Logical Connectives.md | XOR connectives]] :

         ![[Attachments/Pasted image 20240209140144.png]]

    - It is possible to add two *n*-bit binary numbers by **chaining together *n* full-adders**:

        ![[Attachments/Pasted image 20240209140612.png]]
        - For instance, if $1011$ is the first number and $0010$ is the second (unsigned), then:
        $$ A_0 = 1, B_0 = 0, C_{\text{in}} = 0 \implies S_0 = 1, C_0 = 0 $$
        $$ A_1 = 1, B_1 = 1, C_{\text{in}} = 0 \implies S_1 = 0, C_1 = 1 $$
        $$ A_2 = 0, B_2 = 0, C_{\text{in}} = 1 \implies S_2 = 1, C_2 = 0 $$
        $$ A_3 = 1, B_3 = 0, C_{\text{in}} = 0 \implies S_3 = 1, C_3 = 0 $$
            Which is equivalent to:
        $$ 
            \begin{align*}
              &\phantom{+}\tiny \ \ \  1\phantom{1} \\
              &\ \ \ 1011 \\
            + &\ \ \ 0010 \\
            \hline
              &\ \ \ 1101
            \end{align*}
        $$

- A **subtractor** is a modified full-adder, since $A-B = A+(-B)$. Therefore, all $B$'s are converted to $(-B)$'s using 2's complement^[TODO: Link to W5.] by:
    1. Taking 1's complement using [[./Boolean Logic and Circuits.md | inverters]];
    2. Setting the initial $C_{\text{in}} = 1$ in order to add one bit.

        ![[Attachments/Pasted image 20240209193007.png]]

- An **adder-subtractor** can both add and subtract depending on the *switch mode* (SM) using full-adders and [[./Boolean Logic and Circuits.md | XOR gates]]. When SM $= 0$ addition is performed, when SM $= 1$ — subtraction.

    ![[Attachments/Pasted image 20240209193454.png]]


- A **guard bit** is used in order to **detect overflow** when adding two *signed*^[When adding two **unsigned** numbers just check whether there is a carry after the addition of the most significant bits (see "Overflow signal" in the *chained full-adders* picture). **TODO: Link to W5 "Data Representation."**] binary numbers. It is an additional bit which:
    1. **Is a copy of the MSB** (Most Significant Bit, i.e. the sign bit).
    2. **Is prepended** to the most significant bit.
    3. **Lengthens the internal representation** of the numbers, i.e. arithmetic is now performed internally on an *(n+1)*-bit long operand, instead of an *n*-bit operand.
    4. **Signals an arithmetic overflow** if after adding two *(n+1)*-bit numbers the MSB is different from the second MSB.

        ![[Attachments/Pasted image 20240209191451.png]]



## Multiplication and Shifts
- Note that *positive* binary numbers can be multiplied using **long-division**:^[TODO: So what actually? How's it implemented using combinatorial logic?]

    ![[Attachments/Pasted image 20240209194751.png]]

- **Shifts** can move bit patterns either *left* or *right*, by one or more places.

- There are **three kinds of shifts**:
    1. **Logical shift** — bits moved out are lost and zeroes fill the vacated positions:

        ![[Attachments/Pasted image 20240209202256.png]]
        - *n*-place logical **left-shift** corresponds to **multiplication by $2^n$** on unsigned binary.
            
            ![[Attachments/Pasted image 20240209195556.png]]
        - *n*-place logical **left-right** corresponds to **division by $2^n$** on unsigned binary (*always rounds down!*).

            ![[Attachments/Pasted image 20240209200509.png]]

    2. **Arithmetic right shift**^[Arithmetic *left* shift is the same as the logical left shift.] — similar to the logical right shift, except that *copies of the sign bit are propagated* into the vacated bit positions:
        ![[Attachments/Pasted image 20240209202218.png]]
        ![[Attachments/Pasted image 20240209201505.png]]

        - Note that the **remainder cannot be negative**.

    3. **Circular shift** (or **rotation**) — bits moved out of one end of a register are moved in at the opposite end of the register:

        ![[Attachments/Pasted image 20240209201842.png]]

## Bitwise Logical Operations
- [[./Logical Connectives.md | Logical operations]] can be implemented on bit patterns, as well as single bits:

    ![[Attachments/Pasted image 20240209202916.png]]
    The above table is related to [[./C Basics.md | C basics]].
- Note that bitwise operations are typically **parallel**[^parallel], and therefore *fast*.

[^parallel]: ChatGPT: 
    >In a CPU, bitwise operations like AND, OR, XOR, and NOT are inherently **parallel** because they are applied simultaneously to all the bit pairs in the operands. This means that for an 8-bit operand, for example, all 8 bitwise operations are performed at the same time, rather than sequentially. This is made possible by the architecture of the processor, which has the circuitry to perform these operations across all bits of the operand in a single CPU cycle.
