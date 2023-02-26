---
tags: Math, Math/Pure
---
# Homogeneous SDEs

* A **homogeneous SDE** is an [[./Second-order Differential Equations (SDEs).md|SDE]] of the form:
$$ f(y'', y', y) = 0 $$ 

* A **linear homogeneous SDE** has the following form:
$$
a\frac{\mathrm{d}^{2}y}{\mathrm{d}x^{2}} +
b\frac{\mathrm{d}y}{\mathrm{d}x} + cy = 0,\ \text{where constants } a, b, c \in
\mathbb{R} \tag{1}
$$ 

To find a general solution of a linear homogeneous SDE, let us assume that 
$y = Ae^{\alpha x} + Be^{\beta x}$ is a solution, where $A$ and $B$ are arbitrary constants, and $\alpha$ and $\beta$ 
are constants to be determined. By substituting $y, y', y''$ into (1) and simplifying we get: ^408c5f
$$ 
Ae^{\alpha x}(a \alpha^{2} + b \alpha + c) + 
Be^{\beta x }(a \beta^{2} + b \beta + c) = 0 \tag{2}
$$ 
This implies that in order for $\alpha$ and $\beta$ to satisfy (2), and consequently (1), they have to be the solutions of the **auxiliary equation** of the form:
$$ am^{2} + bm + c = 0 \tag{3} $$^auxiliary-equation

* **To find the general solution** of a linear homogeneous SDE (1), first find 
the discriminant ($\Delta$) of the auxiliary equation (3) that has roots $\alpha$ and $\beta$, and then if:
    1) $\Delta > 0$ ($\alpha, \beta \in \mathbb{R}, \alpha \neq \beta$):
        $\qquad \boxed{y = Ae^{\alpha x} + Be^{\beta x}}$
    2) $\Delta = 0$ ($\alpha, \beta \in \mathbb{R}, \alpha = \beta$):
        $\qquad \boxed{y = (A + Bx)e^{\alpha x}}$
    3) $\Delta < 0$ ($\alpha, \beta \in \mathbb{C} \text{ and } \alpha = z = p + qi,\ \beta = z^{*} = p - qi$):
        $\qquad \boxed{y = e^{px}(A \cos{qx} + B \sin{qx})}$
where $A$ and $B$ are arbitrary constants. ^solve-homogeneous-sde

---

**Q:** Find the particular solution of $y'' - y' - 6y = 0$ given that if $x = 0$, then 
$y = 0$ and $y' = -1$.
**A:** The auxiliary equation is $m^{2} - m - 6 = 0 \implies \Delta = 25 > 0
\implies m_1 = -2, m_2 = 3$

$$
\begin{align}
    y &= Ae^{3x} + Be^{-2x} \tag{1}\\
    y' &= 3Ae^{3x} - 2B^{-2x} \tag{2}
\end{align}
$$

After substitutin the given values into (1) and (2) respectively we get:

$$
\begin{cases}
    A + B  = 0 \\
    3A - 2B = -1 
\end{cases}
\iff
\begin{cases}
    A = -\frac{1}{5} \\
    B = \frac{1}{5}
\end{cases}
$$

*Answer:* $y = -\frac{1}{5}e^{3x} + \frac{1}{5}e^{-2x}$
