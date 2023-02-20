# L'Hopital's Rule
* **L'Hopital's rule** states that if the limit of a ratio is indeterminate of 
the form $\frac{0}{0}$ or $\frac{\infty}{\infty}$, then:
$$ \boxed{\lim_{x \to a} \frac{f(x)}{g(x)} = \lim_{x \to a} \frac{f'(x)}{g'(x)}} $$ 

* If $\lim_{x \to a} f(x)$ exists, then:
$$ \boxed{\lim_{x \to a} e^{f(x)} = e^{\lim_{x \to a} f(x)}} $$ 

---

**Q:** Find $\lim_{x \to 0} x\ln{x}$
**A:** 
$$
\begin{align}
    \lim_{x \to 0} \frac{\ln{x}}{\frac{1}{x}} = \lim_{x \to 0} \frac{\frac{1}{x}}{-\frac{1}{x^{2}}} = 
    \lim_{x \to 0} -x = 0
\end{align}
$$
*Answer:* 0

---

**Q:** Find $\lim_{x \to \infty} \frac{x^{2} + e^{4x}}{2x - e^{x}}$
**A:** The given ratio is not intdeterminate of the required form, since $\lim_{x \to \infty} 2x - e^{x}$
is unknown, therefore L'Hopital's rule is not applicable yet.
$$
\begin{align}
    \lim_{x \to \infty} \frac{\frac{1}{x}(x^{2} + e^{4x})}{\frac{1}{x}(2x - e^{x})} =
    \lim_{x \to \infty} \frac{x + \frac{e^{4x}}{x}}{2 - \frac{e^{x}}{x}} = L
\end{align}
$$

Consider the unkown limits of ratios separately:
$$
\begin{align}
    &l_1 = \lim_{x \to \infty} \frac{e^{4x}}{x} \overset{\text{L'Hopital}}{=}
    \lim_{x \to \infty} 4e^{4x} = \infty \\
    &l_2 = \lim_{x \to \infty} \frac{e^{x}}{x} \overset{\text{L'Hopital}}{=}
    \lim_{x \to \infty} e^{x} = \infty \\
    &L = \lim_{x \to \infty} \frac{x + l_1}{2 - l_2} =
    \lim_{x \to \infty} \frac{\infty}{\infty} \xRightarrow[]{\text{L'Hopital}}
    \dots 
\end{align}
$$

---

**Q:** Find $\lim_{y \to 0^{+}} \cos^{\frac{1}{y^{2}}}{2y}$
**A:**
$$
\begin{align}
    \lim_{y \to 0^{+}} e^{\frac{1}{y^{2}}\ln{(\cos{2y})}} =
    e^{\lim_{y \to 0^{+}}\frac{\ln{(\cos{2y})}}{y^{2}}} =
    e^{\lim_{y \to 0^{+}} \frac{-\frac{\sin{2y}}{\cos{2y}}}{2y}} =
    e^{\lim_{y \to 0^{+}} \frac{-\tan{2y}}{2y}} =
    e^{\lim_{y \to 0^{+}} \frac{-2(1 + \cancelto{0}{\tan^{2}{2y}})}{1}} =
    e^{-2}
\end{align}
$$
 
*Answer:* $e^{-2}$
