---
tags:
  - cm12002
  - CS
links:
---
# Computer Systems Architectures

- Classically **uniprocessor^[Uniprocessor architectures are characterised  by having one ALU.] architectures** include:
    - [[Von Neumann Architecture]]
    - [[Harvard Architecture]]
- **Multiprocessor** (or **parallel**) **architectures** are potentially faster but harder to understand, control and predict.
    - There is no single dominant parallel architecture, but a set of alternatives that depend upon different **types of parallelisms** (either on *task* or *data* level) described by the [[Flynn's Taxonomy]].
    - There is a limit on how much a process can be parallelized described by the **[[Amdahl's Law]]**.
- There are different types of **[[Memory Architectures | memory architectures]]** — shared and distributed.

# Unsorted
## Shared Memory MIMD
- **Shared memory MIMD** is becoming dominant in general purpose computing, due to the diminishing returns on building larger/faster uniprocessors.
- **Multi-core processors** — multiple CPUs on the same chip — are now standard. 
    - They are typically used for **multitasking**.
    - However, it can be **challenging to design software** that effectively utilises multithreading capabilities.

## Data Representation
- A **numeration system** is a writing system for expressing numbers.
- The **radix** (or the **base**) determines the number of unique digits, including zero, that a numeration system uses to represent numbers. 
- To **convert a number in base $n$ to decimal**, sum up the products of each digit and $n$ to the power of its position, starting with 0, from left to right. For example:
$$ 134_8 = 1 \times 8^2 + 3 \times 8^1 + 4 \times 8^0 = 92_{10} $$

- To **convert decimal to binary**, divide the given number by two^[If the number is odd, first subtract one and then divide it by two.], recording each remainder. Then write down the remainders starting from the bottom; this is the result. For example, converting 167 to binary:

    | DEC  | BIN |
    | ---- | --- |
    | 167  | 1   |
    | 83   | 1   |
    | 41   | 1   |
    | 20   | 0   |
    | 10   | 0   |
    | 5    | 1   |
    | 2    | 0   |
    | 1    | 1   |
    | 0    | 0   |

    Starting from the bottom and omitting the preceding zero, the result is $167_{10} = 10100111_2$.

- For reference, the **first 16 binary and hexadecimal numbers** are:

| HEX  | DEC     | BIN|
|------|---------| --------|
| 1    | 1       | 0001    |
| 2    | 2       | 0010    |
| 3    | 3       | 0011    |
| 4    | 4       | 0100    |
| 5    | 5       | 0101    |
| 6    | 6       | 0110    |
| 7    | 7       | 0111    |
| 8    | 8       | 1000    |
| 9    | 9       | 1001    |
| A    | 10      | 1010    |
| B    | 11      | 1011    |
| C    | 12      | 1100    |
| D    | 13      | 1101    |
| E    | 14      | 1110    |
| F    | 15      | 1111    |
| 10   | 16      | 10000   |

- For reference, the **first 16 powers of 2** are:
$$
\begin{align*}
2^1 & = 2 \\
2^2 & = 4 \\
2^3 & = 8 \\
2^4 & = 16 \\
2^5 & = 32 \\
2^6 & = 64 \\
2^7 & = 128 \\
2^8 & = 256 \\
2^9 & = 512 \\
2^{10} & = 1024 \\
2^{11} & = 2048 \\
2^{12} & = 4096 \\
2^{13} & = 8192 \\
2^{14} & = 16384 \\
2^{15} & = 32768 \\
2^{16} &= 65536
\end{align*}
$$
