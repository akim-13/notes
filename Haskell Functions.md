---
tags:
  - cm12003
  - CS
  - programming
links: "[[Haskell]]"
---
# Haskell Functions
- Functions with **one argument**:
    ```haskell
    func_square x = x * x
    ---
    > func_square 6
    36
    ```

- **WARNING:** Do not name functions with default names, e.g. `max`, since it will cause `Ambigious occurence` error:
    ```sh
    <interactive>:4:1: error:
        Ambiguous occurrence ‘max’
        It could refer to
           either ‘Prelude.max’,
                  imported from ‘Prelude’ at basics.hs:1:1
                  (and originally defined in ‘GHC.Classes’)
               or ‘Main.max’, defined at basics.hs:21:1
    ```

- Functions with **multiple arguments** are called **curried**^[Named after the logician Haskell B. Curry]:
    ```haskell
    func_hyp x y = sqrt(func_square x + func_square y)
    ---
    > func_hyp 3 4
    5
    ```
    See [[Haskell Types#^839334| type declaration]] for functions with multiple arguments.
 ^753913
- Funtctions with **paired arguments**:
    ```haskell
    func_hyp (x, y) = sqrt(func_square x + func_square y)
    ---
    > func_hyp (3, 4)
    5
    ```
    A **pair** (or a **tuple**) is just a value that can be manipulated, for example, as such:
    ```haskell
    vectorAdd (x1, y1) (x2, y2) = (x1+x2, y1+y2)
    vector1 = (1.2, 1.7)
    vector2 = (3.7, 0.9)
    --
    > vectorAdd vector1 vector2
    (4.9,2.6)
    ```

- A function is **higher-order** if one of its arguments is itself a function.
    ```haskell
    iter :: Int -> (a -> a) -> a -> a
    iter i func arg
        | i <= 0    = arg
        | otherwise = iter (i-1) func (func arg)
    ---
    > iter 3 (*3) 1
    27
    ```
    - This applies function `func` `i` times starting from `arg`.
    - This is they key feature of **functional programming**, hence there are no `for` loops in Haskell, since everything can be done through recursion.

- **Value** is a function with 0 arguments.
    ```haskell
    value      = 28       -- a function in 0 arguments
    function x = 28 + x   -- a function in 1 argument
    ```

- A function is **polymorphic** if it can have more than one type.
    ```haskell
    ghci> "Baren" ++ "dregt"      ghci> [1,2,3] ++ [4,5,6]
    "Barendregt"                   [1,2,3,4,5,6]
    ```
    There are **two types of polymorphism**:
    -  **Parametric** - uses [[Haskell Types#^71112e | type variables]] to define to define function that work with any type.
	```haskell
	id :: a -> a id x = x
	```
    - **Ad-hoc** - uses type classes to implement explicit definition for separate types.
	```haskell
	 -- The built-in function + can operate on the following types:
	(+) :: Num a => a -> a -> a
	(+) :: Int -> Int -> Int
	(+) :: Integer -> Integer -> Integer
	(+) :: Float -> Float -> Fload
	```