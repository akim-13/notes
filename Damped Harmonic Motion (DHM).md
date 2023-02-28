---
tags: Math, Math/Applied, Math/Pure
---
%%
links: [[Differential Equations]]
%%
# Damped Harmonic Motion (DHM)

* **Damped Harmonic Motion (DHM)** is [[./Simple Harmonic Motion (SHM).md|SHM]] with a **damping force** added to it, i.e. the force proportional to the velocity of the particle:
$$
\begin{flalign}
    \boxed{\drv{d^2 x}{dt^2} + k\drv{dx}{dt} + \omega^2 x = 0 \iff 
    \ddot x + k \dot x + \omega^2 x = 0} \tag{1}
\end{flalign}
$$
where $k$ and $\omega^2$ are positive constants. This equation is also an example of a [[./Homogeneous SDEs.md|homogeneous SDE]].

* There are **3 types of damping** determined by the discriminant ($\Delta$) of the [[./Homogeneous SDEs.md#^auxiliary-equation|auxiliary equation]] of (1):
    1. **Heavy damping** ($\Delta > 0$) — no oscillation
    ![[./Attachments/heavy_damping.png]]
    2. **Critical damping** ($\Delta = 0$) — no oscilation
    ![[./Attachments/critical_damping.png]]
    3. **Light damping** ($\Delta < 0$) — exponentially decreasing oscillation
    ![[./Attachments/light_damping.png]]
