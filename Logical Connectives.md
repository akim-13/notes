---
tags:
  - Math
  - Math/Pure
  - cm12004
  - cm12002
links:
  - "[[Propositional Calculus]]"
Presentation:
  - W10_L01_P01
---
# Logical Connectives
- The **number of possible logical connectives** between two variables is *16*, since there are 4 possible combinations of True and False, every one of which can yield 2 outcomes -- True or False, hence $2^4=16$.

- **Conjunction** ($\wedge$) is the logical *and*.

    | X | Y | X $\wedge$ Y |
    |---|---|--------------|
    | T | T |       T      |
    | T | F |       F      |
    | F | T |       F      |
    | F | F |       F      |

    - *Other notations* include: $X.Y, XY, X\&Y$.
    - Logical AND has the following **properties:**
        - **Associativity**: $(A.B).C = A.(B.C)$
        - **Commutativity**: $A.B = B.A$
        - 1 is the **Identity**: $A.1 = A$
        - **Absorption**: $A.A = A$
        - 0 is an **Annihilator**: $A.0 = 0$

- **Disjunction** ($\vee$) is the logical *inclusive or*. 

    | X | Y | X $\vee$ Y   |
    |---|---|--------------|
    | T | T |       T      |
    | T | F |       T      |
    | F | T |       T      |
    | F | F |       F      |

    - *Other notations* include: $X+Y, X|Y$
    - For example, $(2 + 2 = 5) \vee ($ snow is white $)$ evaluates to true.
    - When "or" is used in mathematical or programming contexts, it is assumed to be a disjunction by default.
    - Logical OR has the following properties:
        - **Associativity**: $(A+B)+C = A+(B+C)$
        - **Commutativity**: $A+B = B+A$
        - 0 is the **Identity**: $A+0 = A$
        - **Absorption**: $A+A = A$
        - 1 is an **Annihilator**: $A+1 = 1$
        - **Distributivity**: $A.(B + C) = A.B + A.C$ and $A + (B.C) = (A + B).(A +C)$

- **XOR** is the logical *exclusive or*.

    | $X$ | $Y$ | $X$ *XOR* $Y$   |
    |---|---|--------------|
    | T | T |       F      |
    | T | F |       T      |
    | F | T |       T      |
    | F | F |       F      |

    For example, one might be male or (XOR) female, but not both at the same time.
- **Implication** ($\rightarrow$) is the logical *if — then*.

    | X | Y | X $\rightarrow$ Y   |
    |---|---|---------------------|
    | T | T |       T             |
    | T | F |       F             |
    | F | T |       T             |
    | F | F |       T             |

    - If $X \rightarrow Y$, then $X$ is called the **assumption** of the implication, while $Y$ is called its **consequence**.
    - $F \rightarrow T$ and $F \rightarrow F$ both evaluate to $T$, since if the initial assumption in an argument is incorrect, then it does not matter what follows, i.e. it will always be possible to arrive to the desired outcome — $T$.

- **Negation** ($\neg$) is the logical *not*.

    | X | $\neg$ X |
    |---|----------|
    | T | F        |
    | F | T        |

    - *Other notations* include: $\bar X, X', !X$.
    - Negation has the **involutive property**: $\neg\neg X = X$.
- See also [De Morgan's laws](https://en.wikipedia.org/wiki/De_Morgan%27s_laws).