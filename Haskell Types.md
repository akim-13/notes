---
tags:
  - cm12003
  - programming
  - CS
links: "[[Haskell]]"
---
# Haskell Types
- Everything has a **type** in Haskell.

- **Type declaration** is of the form `function :: Type`.
 ^a50e06
- **[[Haskell Functions#^753913|Curried functions]]** have a type of the form `Type_1 -> Type_2 -> ... -> Type_n -> Type_r`, where the first argument has type `Type_1`, the second `Type_2`, etc., and the return value has the type `Type_r`.
 ^839334
- Types may contain **variables**, which stand in for any type:
    ```haskell
    ifthenelse :: Bool -> type1 -> type1 -> type1
    ifthenelse b x y
        | b = x
        | otherwise = y
    ```
    ^71112e
    - **WARNING:** `x` and `y` can have any type but it must be the same for both variables. The logic is as follows: `x` can be any type, so create a variable (`type1`). The function may return `x` if `b` is `True`, therefore the return value is also `type1`. Consequently, when `y` is returned it must have the same type as the return value, i.e. also `type1`.
    - **Variable names** start with lowercase, whereas **type constants** start with uppercase. 
    - **The difference between variables and constants** is that the value of the latter is known at compile time, while the former can change at runtime. 

- **Type class** is a collection of types. It allows to constrain a type variable to certain types using the following syntax structure:
    ```haskell
    Func :: TypeClass var => var -> ...
    ```

- Some of the **built-in type classes** are:
    - `Eq`: values can be tested for *equality*. Key function:
        ```haskell
        (==) :: Eq a => a -> a -> Bool
        ```
        Additional functions: `/=`.
    - `Ord`: values are *ordered*. Key function:
        ```haskell
        (<) :: Ord a => a -> a -> Bool
        ```
        Additional functions: `<=`, `>`, `>=`, `max`, etc.
    - `Num`: values represent *numbers*. Key functions:
        ```haskell
        (+) :: Num a => a -> a -> a
        (*) :: Num a => a -> a -> a
        (-) :: Num a => a -> a -> a
        ```
    - `Show`: values can be displayed as *strings*. Key function:
        ```haskell
        show :: Show a => a -> String
        ```
