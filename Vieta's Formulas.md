---
tags: Math, Math/Pure
---
%%
links:
%%
# Vieta's Formulas
- **Vieta's formulas** relate the coefficients of a polynomial to sums and products of its roots.

- If the roots of a polynomial are denoted by greek letters, then:
    1) $ax^2 + bx + c = 0$
        - $\alpha + \beta = -\frac{b}{a}$
        - $\alpha\beta = \frac{c}{a}$
    2) $ax^3 + bx^2 + cx + d = 0$
        - $\sum \alpha = \alpha + \beta + \gamma = -\frac{b}{a}$
        - $\sum \alpha\beta = \alpha\beta + \beta\gamma + \gamma\alpha = \frac{c}{a}$
        - $\alpha\beta\gamma = -\frac{d}{a}$
    3) $ax^4 + bx^3 + cx^2 + dx + e = 0$
        - $\sum \alpha = \alpha + \beta + \gamma + \delta = -\frac{b}{a}$ 
        - $\sum \alpha\beta = \alpha\beta + \alpha\gamma + \alpha\delta + \beta\gamma + \beta\delta + \gamma\delta = \frac{c}{a}$
        - $\sum \alpha\beta\gamma = \alpha\beta\gamma + \alpha\beta\delta + \alpha\gamma\delta + \beta\gamma\delta = -\frac{d}{a}$
        - $\alpha\beta\gamma\delta = \frac{e}{a}$

    Notice the pattern of alternating signs: the even terms change sign to the opposite one (e.g. $-\frac{b}{a}$ and $-\frac{d}{a}$), whereas the odd terms do not (e.g. $\frac{c}{a}$ and $\frac{e}{a}$).

- Given a polynomial and a **linear transformation** of its roots (e.g. $\alpha \rightarrow A\alpha+B$), it is possible to find a corresponding polynomial that has the transformed roots (see **Q1**).

---

**Q1:** The quartic equation $x^4 - 3x^3 + 15x + 1 = 0$ has roots $\alpha, \beta, \gamma$ and $\delta$. Find the equation with roots $(2\alpha + 1), (2\beta + 1), (2\gamma + 1)$ and $(2\delta + 1)$.^[C1.66 E9]
**A:** Let $w = 2x + 1 \iff x = \frac{w - 1}{2}$
$$
\begin{flalign}
    & \text{Substituting in the original equation:} \\
    & \(\frac{w - 1}{2}\)^4 - 3\(\frac{w - 1}{2}\)^3 + 15\(\frac{w - 1}{2}\) + 1 = 0 \\
    & \text{Expanding and simplifying:} \\
    & w^4 -10w^3 + 24w^2 + 98w - 97 = 0
    &
\end{flalign}
$$

*Answer:* $w^4 -10w^3 + 24w^2 + 98w - 97 = 0$
