# Chain Rule
* The **chain rule** allows to differentiate composite functions, such as $y = f(g(x))$:
$$ \frac{\mathrm{d}y}{\mathrm{d}x} = \frac{\mathrm{d}f}{\mathrm{d}g} \frac{\mathrm{d}g}{\mathrm{d}x} \tag{1} $$ 

* It is also applicable for **any number of functions** nested inside each other, for example if $y = f(g(u(v(x))))$, then:
$$ 
\frac{\mathrm dy}{\mathrm dx} = 
\frac{\mathrm df}{\mathrm dg} 
\frac{\mathrm dg}{\mathrm du} 
\frac{\mathrm du}{\mathrm dv}
\frac{\mathrm dv}{\mathrm dx} \tag{2}
$$

It might be useful to think that the chain rule works by canceling out the derivative symbols, e.g. for (2):
$$ 
\frac{\mathrm dy}{\mathrm dx} = 
\frac{\mathrm df}{\cancel{\mathrm dg}} 
\frac{\cancel{\mathrm dg}}{\cancel{\mathrm du}} 
\frac{\cancel{\mathrm du}}{\cancel{\mathrm dv}}
\frac{\cancel{\mathrm dv}}{\mathrm dx} = \frac{\mathrm df}{\mathrm dx}
$$
While the derivatives behave like fractions most of the time, it just happens to be so. In reality it is just a notation and they are not actual fractions. This fact is most evident with partial derivatives, since $\frac{\partial y}{\partial x} = xy \centernot{\iff} \frac{1}{y} \partial y = x \partial x$^[Expression on the right is nonesense.].

---

**Q1:** Find the derivative of $y = \sin{x^{2}}$
**A:** Let $u = g(x) = x^{2}$, then $y = f(g(x)) = f(u) = \sin{u}$
$$
\begin{align}
    \frac{\mathrm dy}{\mathrm dx} &= \frac{\mathrm df}{\mathrm du} \frac{\mathrm du}{\mathrm dx} \\
    &= (\cos{u})(2x) \\
    &= (\cos{x^{2}})(2x)
\end{align}

$$
*Answer:* $y' = 2x \cos{x^2}$
