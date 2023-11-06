---
tags:
  - cm12003
  - CS
  - programming
links: "[[Haskell]]"
---
# Haskell Conditionals
- Conditionals evaluate to either constant: `True` or `False`.
- All **boolean expressions** are standard. There is a function `not` and operator "not equals to" is `/=`.
- **Guards (`|`)** give multiple cases for a function:
    ```haskell
    absolute n
        | n < 0     = -n
        | otherwise = n
    ```
    The first guard to evaluate to `True` determines function's return value. There can be any number of guards. `otherwise` is another way to write `True`.

- Guards are the same as **`if`-`then`-`else` structure**:
	^if-then-else
    ```haskell
        power_if_then_else a b = 
        if b == 0 then 
            1 
        else if b < 0 then 
            error "Power cannot be negative!" 
        else 
            a * power_if_then_else a (b-1)
    ``` 
    is the same as:

    ```haskell
        power_guards a b
            | b == 0 = 1
            | b < 0 = error "Power cannot be negative!"
            | otherwise = a * power_guards a (b-1)
    ```
