---
tags: cm12002, CS, Math
links: "[[Computer Systems Architectures]]"
---
# Amdahl's Law
- **Amdahl's law** states that if for a given computational task, $p$ is the proportion of that task that *can be parallelized*^[Meaning that $1-p$ is the proportion of that task that is inherently sequential.], then the *maximum speedup* obtainable using $N$ *parallel processors* equals to:
    $$ \boxed{\frac{1}{(1-p) + \frac{p}{N}}} $$
    ![[Attachments/Pasted image 20231031142035.png]]

- **For example**, if $90\%$ of a process can be parallelized, then running it on a quad-core processor gives speedup that at most equals to:
    $$ \frac{1}{(1-0.9) + \frac{0.9}{4}} = 3.08 \text{ (3 s.f.)} $$
