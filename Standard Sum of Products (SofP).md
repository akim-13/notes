---
tags:
  - cm12002
  - CS
  - Math
links:
  - "[[Computer Systems Architectures]]"
presentations:
  - W10_L01_P02
---
# Standard Sum of Products (SofP)
- A **standard Sum of Products (SofP)** of a [[./Boolean Formulae.md | Boolean formula]] is a series of terms joined by *OR* operations, in which each term contains a combination of **all** variables joined by *AND* operations:^[See [[./Logical Connectives.md | logical connectives]] for OR and AND.] 

    $$ A + B \cdot C = A \cdot B \cdot C + A \cdot B \cdot C’ + A \cdot B’ \cdot C + A \cdot B’ \cdot C’ + A’ \cdot B \cdot C $$

- **Theorem:** every Boolean expression over $n$ variables can be represented as a SofP. This can be achieved either by using:
    1. **Algebra:**

        ![[Attachments/Pasted image 20240202183511.png]]

    2. Or **truth tables** — for each row of the truth table with value 1, form the product of all literals with value 1, then form the sum of all these products:

        ![[Attachments/Pasted image 20240202183806.png]]