---
tags:
  - Math
  - Math/Pure
  - cm12004
links:
  - "[[Propositional Calculus]]"
---
# Boolean Formulae
- **Boolean formula** is a string of symbols from the set $\{X_1,\dots, X_n, \wedge, \vee, \rightarrow, \neg, (, ) \}$, which is organized as follows:
    1. Symbols $X_1,\dots,X_n$ are variables.
    2. Any variable $X_i, (1 \leq i \leq n)$ is a Boolean formula.
    3. If $F$ and $G$ are two Boolean formulae, then expressions $(F \wedge G), (F \vee G), (F \rightarrow G)$ and $\neg F$ are Boolean formulae.

- The most external parenthesis in a Boolean formula may be omitted.
- Any Boolean formula can be evaluated to either True or False if specific values are given.
- A Boolean formula $F$ with variables $X_1,\dots,X_n$ is called **identically true** or **tautology** if for any assignment of True/False values to variables the value of $F$ is True.
    - The definition of an **identically false** Boolean formula is analogues, however it is **not** called a tautology.
    - $X \vee \neg X$ is a famous tautology called *tertium non datur* (a third is not given).
    - Another example of tautology is $((\neg X \rightarrow Y) \wedge (\neg X \rightarrow \neg Y)) \rightarrow X \equiv \text{True}$.
