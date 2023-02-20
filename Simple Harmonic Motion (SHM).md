# Simple Harmonic Motion (SHM)

* **Simple Harmonic Motion (SHM)** is a type of [[./Harmonic Motion.md | harmonic motion]] in which the acceleration of a particle $P$ is always towards a fixed point $O$ on the line of motion of $P$. SHM can be modeled by an [[./Second-order Differential Equations (SDEs).md|SDE]] of the form:
$$
\begin{flalign}
    \boxed{\drv{d^2 x}{dt^2} + \omega^2 x = 0 \iff \ddot x = -\omega^2 x} \tag{1}
\end{flalign}
$$
Notice that the number of dots above $\ddot x$ represent the order of the derivative of $x$ with respect to time, i.e. if $x$ is the displacement of $P$, then $\dot x = \drv{dx}{dt} = v$ and $\ddot x = \drv{d^2 x}{dt^2} = a$. Furthermore, $\boxed{\ddot x = v\drv{dv}{dx}}$, since $\ddot x = \drv{dv}{dt} = \drv{dv}{dx} \drv{dx}{dt} = v \drv{dv}{dx}$.

This general form can be derived by considering the motion of a horizontal elastic spring $S$. If $S$ (at rest) is pulled from the point $O$ to the point $A$, then $OA$ will represent the displacement of $S$. According to the *Hooke's law*, $T = kx$, where $T$ is the tension and $k$ is a positive constant. The *Newton's second law* states that $\sum F = m \ddot x$, therefore $-kx = m \ddot x \iff \ddot x = -\frac{k}{m}x$. Since both $k$ and $m$ are positive, the ratio can be denoted as $\omega^2$, giving us the general form of SHM (1).

Consider the general solution of (1):
$$
\begin{flalign}
    & \text{Auxiliary equation: } m^2 + \omega^2 = 0 \iff m = \pm i \omega &\\
    & x(t) = a \cos{\omega t} + b \sin{\omega t} &\\
    & x(0) = a \implies \text{ let } a = A &\\
    & \dot x(t) = -A \omega \sin{\omega t} + b \omega \cos{\omega t} &\\
    & \dot x(0) = 0 \text{ (starting from rest) } \implies b = 0 &\\
    & x(t) = \cos{\omega t} &
\end{flalign}
$$

* An **alternative form** of the SHM equation is:
$$
\begin{flalign}
    \boxed{x = A \cos{\omega t}}
\end{flalign}
$$
where $A$ is the **amplitude** — the maximum displacement from the origin. Moreover, the **period** of the motion ($T$) is the time the particle takes to complete one oscillation, i.e. when the angle $\omega T = 2 \pi$:
$$
\begin{flalign}
    \boxed{T = \frac{2\pi}{\omega} = 2\pi \sqrt{\frac{m}{k}}}
\end{flalign}
$$

