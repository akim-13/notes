---
tags: Math, Math/Pure, Math/Applied
---
# First-order Differential Equations (FDEs)
* **First-order differential equation (FDE)** is a [[Differential Equations.md|differential equation]] of the form $f(y, \frac{dy}{dx}) = g(x)$.

* FDE of the form $\frac{\mathrm{d}y}{\mathrm{d}x} = f(x)g(y)$ is solved by **separating the variables**:
$$
\begin{align}
    \int \frac{1}{g(y)} \,\mathrm{d}y = \int f(x) \,\mathrm{d}x 
\end{align}
$$

* **To solve an FDE** of the form $\frac{dy}{dx} + P(x)y = Q(x)$, multiply both sides by the **integrating factor** $f(x) = e^{\int P(x) \,\mathrm{d}x }  \,$:

$$
\begin{align}
    \frac{dy}{dx} + P(x)y &= Q(x) \quad \biggr| \times f(x) \\
    f(x)y' + f(x)P(x)y &= Q(x)f(x) \\
    f(x)y' +f'(x)y &= Q(x)f(x) \\
    \frac{\mathrm{d}}{\mathrm{d}x} \left( f(x)y \right) &= Q(x)f(x) \tag*{The product rule} \\
    y = \frac{1}{f(x)} \int & Q(x)f(x) \,\mathrm{d}x
\end{align}
$$

Since the integrating factor $f(x)$ can be anything, it is always chosen to be $e^{\int P(x) \,\mathrm{d}x }$ in order to get an expression for the product rule: 

$$
\begin{align}
    f'(x) &= f(x)P(x) \\
    \frac{f'(x)}{f(x)} &= P(x) \\
    \frac{\mathrm{d}}{\mathrm{d}x} \left( \ln{f(x)} \right) &= P(x) \\
    e^{\ln{f(x)}} &= e^{\int P(x) \,\mathrm{d}x } \\
    f(x) &= e^{\int P(x) \,\mathrm{d}x }
\end{align}
$$

* If $x$ and $y$ cannot be separated to get the required form, a **substitution** may be used (see **Q2**).

* FDEs can be used to **model kinematics problems**. If $s(t)$ is the *displacement* of the particle at time $t$, then:
$$
\begin{flalign}
    & v = \drv{ds}{dt} &\\
    & a = \drv{dv}{dt} = \drv{d^2 s}{dt^2}
\end{flalign}
$$
where $v$ and $a$ is *velocity* and *acceleration* respectively.

* Two linear FDEs connected by two dependent variables (e.g. the rate of change of $x$ and $y$ — the populations of foxes and rabbits), and one independent variable (e.g. time $t$) are called **coupled**: 
$$
\begin{flalign}
    &\begin{cases}
        \drv{dx}{dt} = ax + by + f(t) \\
        \drv{dy}{dt} = cx + dy + g(t)
    \end{cases}
    &
\end{flalign}
$$
Such system of simlutaneous equations is **solved by eliminating one of the dependent variables** to form an [[./Second-order Differential Equations (SDEs).md|SDE]]. Additionally, note that if $f(t)$ and $g(t)$ are both $0$, the system is said to be *homogeneous*.

---

**Q1:** Solve $\frac{\mathrm{d}y}{\mathrm{d}x} + \frac{3}{x}y = 
\frac{\cos{x}}{x^{3}}$ in terms of $x$.

**A:** Integrating factor $=e^{\int \frac{3}{x} \,\mathrm{d}x} = e^{3\ln{x}}
= x^{3}$

$$
\begin{align}
    \frac{\mathrm{d}y}{\mathrm{d}x} + \frac{3}{x}y &= \frac{\cos{x}}{x^{3}} 
    \quad \biggr| \times x^{3} \\
    x^{3}\frac{\mathrm{d}y}{\mathrm{d}x} + 3x^{2}y &= \cos{x} \\
    \frac{\mathrm{d}}{\mathrm{d}x} \left( x^{3}y \right) &= \cos{x} \tag*{The product rule} \\
    x^{3}y &= \int \cos{x} \,\mathrm{d}x \\
    x^{3}y &= \sin{x} + c \\
\end{align}
$$

*Answer:* $y = \frac{\sin{x}}{x^{3}} + \frac{c}{x^{3}}$

---

**Q2:** Solve $\frac{\mathrm{d}y}{\mathrm{d}x} - \frac{y}{x} = \frac{y^{2}}{x^{2}}$ in terms of $x$.
**A:** Let $z = \frac{y}{x} \iff y = xz$
$z$ is a function of $x$ because $z = \frac{y}{x} = \frac{f(x)}{x} = z(x)
\implies \frac{\mathrm{d}y}{\mathrm{d}x} = z + x\frac{\mathrm{d}z}{\mathrm{d}x}$
$$
\begin{align}
    z + x \frac{\mathrm{d}z}{\mathrm{d}x} - z &= z^{2} \tag*{Substitution}\\
    x \frac{\mathrm{d}z}{\mathrm{d}x} &= z^{2} \tag*{The product rule} \\
    \int \frac{1}{z^{2}} \,\mathrm{d}z &= \int \frac{1}{x} \,\mathrm{d}x \\
    -\frac{1}{z} &= \ln{x} + c \\
    z &= \frac{1}{-c-\ln{x}} \\
    &=  \frac{1}{k - \ln{x}}\\
    y &= xz =\frac{x}{k - \ln{x}}
\end{align}
$$

*Answer:* $y = \frac{x}{k - \ln{x}}$
