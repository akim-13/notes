---
tags: Math, Math/Pure, cm12004
links: "[[Propositional Calculus]]"
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

- **Disjunction** ($\vee$) is the logical *inclusive or*. 

    | X | Y | X $\vee$ Y   |
    |---|---|--------------|
    | T | T |       T      |
    | T | F |       T      |
    | F | T |       T      |
    | F | F |       F      |

    - For example, $(2 + 2 = 5) \vee ($ snow is white $)$ evaluates to true.
    - When "or" is used in mathematical or programming contexts, it is assumed to be a disjunction by default.

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