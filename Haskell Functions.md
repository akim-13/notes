---
tags:
  - cm12003
  - CS
  - programming
links:
  - "[[Haskell]]"
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
    ^753913
    ```haskell
    func_hyp x y = sqrt(func_square x + func_square y)
    ---
    > func_hyp 3 4
    5
    ```
    - See [[Haskell Types#^839334| type declaration]] for functions with multiple arguments.
    - Note that Haskell treats all curried function as if they had **one argument**. This is because function applications **associate left**[^associate]:
        ```haskell
        fun x y z == ((fun x) y) z
        ```
        Here the function `fun` is [[Haskell Functions#^partial-app | partially applied]] to `x`, and a [[Haskell Functions#^9c4c29 | higher-order]] function is returned. It is then partially applied to `y`, which returns another higher-order function, which is finally applied to `z`. This process is called **currying**.
        ^currying

[^associate]: "Associates" refers to the order in which operations or function applications are grouped, i.e. "associates left" means they apply from left to right.

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
    ^9c4c29
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

- A function can be **partially applied**, i.e. take fewer arguments than it is supposed to. This is possible due to [[Haskell Functions#^currying | currying]].
	^partial-app
    ```haskell
    max     :: Int -> Int -> Int
    max 3   ::          Int -> Int
    max 3 5 ::                Int
    ---
    ghci> map (max 3) [1..5]
    [3,3,3,4,5]
    ```
    See [[Haskell Standard Functions#^map | map]].
    - **Sections** are partially applied infix operators, written in parenthesis:
        ```haskell
         (<)   :: Int -> Int -> Bool
        (3 <)  ::        Int -> Bool
        (< 5)  :: Int ->        Bool
        3 < 5  ::               Bool
        ---
        ghci> [-4 .. 4]
        [-4,-3,-2,-1,0,1,2,3,4]

        ghci> map (max 0) it
        [0,0,0,0,0,1,2,3,4]

        ghci> map (3*) it
        [0,0,0,0,0,3,6,9,12]

        ghci> map (<=5) it
        [True,True,True,True,True,True,False,False,False]

        ghci> map (map (+3)) [[1,2],[],[3,4,5],[6]]
        [[4,5],[],[6,7,8],[9]]
        ```
    - Partial application can also be used in **function definition**:
        ```haskell
        addOne :: [Int] -> [Int]
        addOne = map (+1)

        squareAll :: [Int] -> [Int]
        squareAll = map square
            where
                square x = x*x

        reverseAll :: [String] -> [String]
        reverseAll = map reverse
        ```
