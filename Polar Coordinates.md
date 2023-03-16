---
tags: Math, Math/Pure
---
%%
links:
%%
# Polar Coordinates
* **Polar coordinate system** is a 2D coordinate system in which each point on a plane is determined by a distance from a reference point (*origin*) and an angle from a reference direction (*initial line*). 

* A point $P(x, y)$ in **cartesian coordinates** can be represented as $P(r,\theta)$ in **polar coordinates**, where $r$ is the distance from the origin and $\theta$ is the angle from the initial line. Notice that $P(x,y) \iff y = f(x)$, whereas $P(r, \theta) \iff r = f(\theta)$.

* To **convert** between the coordinate systems use:
    1. Cartesian to polar $P(x, y) \rightarrow P(r, \theta)$
    $$
    \begin{flalign}
        &\begin{cases}
            r = \sqrt{x^2 + y^2} \\
            \theta = \arctan{\frac{y}{x}}
        &\end{cases}
        &
    \end{flalign}
    $$

    2. Polar to cartesian $P(r, \theta) \rightarrow P(x, y)$
    $$
    \begin{flalign}
        &\begin{cases}
           x = r \cos{\theta} \\
           y = r \sin{\theta}
        &\end{cases}
        &
    \end{flalign}
    $$

* **Standard curves** in polar coordinates:
    1. Circle with radius $a$ and centre $O$
    $$
    \begin{flalign}
        r = a
    \end{flalign}
    $$
    ![[Attachments/Pasted image 20230316200057.png]]
    2. Spiral
    $$
    \begin{flalign}
        r = a\theta
    \end{flalign}
    $$
    ![[Attachments/Pasted image 20230316201448.png]]

Cartesian coordinates may be inconvenient in some situations. For instance, the equation of a circle $x^2 + y^2 = r^2 \iff y = \pm \sqrt{r^2 - x^2}$ is not a function, since there could be more than one value of $x$ for a given value of $y$ (see the orange line below).

![[Attachments/Pasted image 20230316190051.png]]
