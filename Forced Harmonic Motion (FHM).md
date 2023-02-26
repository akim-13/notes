---
tags: Math, Math/applied
---
# Forced Harmonic Motion (FHM)
* **Forced Harmonic Motion (FHM)** occurs when a particle is subject to [[./Damped Harmonic Motion (DHM).md|DHM]] and is forced to oscillate with a frequency other than in natural one. It can be modeled by a [[./Non-homogeneous SDEs.md|non-homogeneous SDE]]:
$$
\begin{flalign}
    \boxed{\drv{d^2 x}{dt^2} + k\drv{dx}{dt} + \omega^2 x = f(t)}
\end{flalign}
$$
where $k$ and $\omega^2$ are positive constants.

The image below shows the displacement of a particle *(purple)*, when an external harmonic force *(grey)* is applied to the particle that already oscillates with a natural frequency.

![[./Attachments/fhm.png]]
![[./Attachments/fhm.gif|center]]
