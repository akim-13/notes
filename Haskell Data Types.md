---
tags: cm12003, cs, programming
links: "[[Haskell]]"
---
# Haskell Data Types
- A **data type** is defined using the `data` keyword and represents a kind of value that a variable can hold. It consists of a:
    - **Type constructor** (the name of a data type) — used in type declarations. The terms "type constructor" and "data type" are often used interchangeably.
    - **Data constructor(s)** — used to create instances of the data type. Usually, when referring to "constructors" in the context of data types, this terms is implied.
        - It is possible to define **as many constructors as needed** by separating them with `|`:
            ```haskell
            data Weekday = Monday   | Tuesday  | Wednesday |
                           Thursday | Friday   | Saturday  | Sunday
            ```
            However, only one constructor can be used when creating values of the data type.
        - Constructors can take in **parameters**, i.e. act like **functions**. When there is only one data constructor that takes in arguments, it is encouraged to name it the same as the type constructor:
            ```haskell
            -- Two data constructors (`Cricle` and `Rectangle`) 
            -- with arguments (`Float`).
            data Shape = Circle Float | Rectangle Float Float

            -- One data constructor (second `Fraction`) with arguments 
            -- (`Integer`s) named after the type class (first `Fraction`).
            data Fraction = Fraction Integer Integer
            ```
            ^fraction
            - The data constructor `Fraction` allows us to **build** fractions, i.e. create values of the `Fraction` data type[^rational]:
                ^build-fraction
                ```haskell
                build_fraction :: Integer -> Integer -> Fraction
                build_fraction n d 
                    | d == 0    = error "Denominator cannot be equal to 0."
                    | d < 0     = Fraction ((-n) `div` x) ((-d) `div` x)
                    | otherwise =  Fraction (n `div` x) (d `div` x)
                        where x = gcd n d -- Normalizing.
                ```
            - Custom data constructors with arguments can be **[[Haskell Constructors & Pattern Matching | pattern matched]]**. For the `Fraction` constructor the pattern would be `Fraction n d`:
                ```haskell
                sum_fractions :: Fraction -> Fraction -> Fraction
                sum_fractions (Fraction n1 d1) (Fraction n2 d2) = fraction (n1*n2 + n2*d1) (d1*d2)
                ```
            - The **type** of the *data constructor* `Fraction` (i.e. the second `Fraction` in the data type definition) is:
                ```haskell
                Fraction :: Integer -> Integer -> Fraction
                ```
            - Constructors can be defined for **infix operators** using `:`:
                ```haskell
                data Expr = Num Int
                    | Expr :+ Expr
                    | Expr :- Expr
                    | Expr :* Expr
                    deriving Show
                ---
                ghci> Num 3 :+ (Num 5 :- (Num 4 :* Num 2)) 
                Num 3 :+ (Num 5 :- (Num 4 :* Num 2))
                ```
                This is an [[#^inductive-data-types | inductive data type]] and a type of [[Haskell Trees#^cc80ee | tree]]. ^be153e

    - For example, the internal **definition of the Booleans** is:
        ```haskell
        data Bool = False | True
        ```
        Where `Bool` is the *data type* and `True`, `False` are the *constructors*.

- Data types can be **parameterized**, using type variables. The parameters in this case must be specified both after the type and the data constructors:
    ```haskell
    data Pair a b = Pair a b
    ```
    This data type is equivalent to the built-in tuple of two element `(a,b)`.

- **Built-in data types** include:
    - **Tuple** (`(a,b)`) — a fixed-size collection of elements.
        - The **number of elements** in a tuple can range from 2 to 15, e.g. `(a, b, c, d, e)` is also a tuple.
        - There is also a **zero-tuple**: `()`.
    - **`Maybe`** allows to write *partial function*^[A **partial function** is a function that is not defined for all possible inputs of its domain. Not to confuse with partial definition of a function.]:
        ```haskell
        data Maybe a = Nothing | Just a

        divide :: Int -> Int -> Maybe Int
        divide n 0 = Nothing
        divide n m = Just (div n m)
        ```
        Using `Maybe` instead of throwing errors gives safer code.
    - **`Either`** is typically used for error messages, i.e. either return a value (e.g. `Right x`) or an error message (e.g. `Left "<error message>"`):
        ```haskell
        data Either a b = Left a | Right b

        at :: [a] -> Int -> Either String a
        at xs i 
            | i < 0      = Left "at: negative index"
            | otherwise  = atPos xs i
            where
                atPos []     _ = Left "at: index too large"
                atPos (x:_)  0 = Right x
                atPos (_:xs) n = atPos xs (n-1)
        ```
        Note that this is just an example, in practice `Either` can be used for anything else, not only error messages.

- Data type declarations can be **inductive** (a.k.a **recursive**):
    ^inductive-data-types
    ```haskell
    data MyList a = MyNil | MyCons a (MyList a)
    ```
    This is conceptually equivalent to the built-in list:
    ```haskell
    -- Note that since : and [] are built-in operators, 
    -- the following is not a valid syntax.
    data [a] = [] | a :
    ```
    And it can be used in the same way as a list:
    ```haskell
    append :: List a -> List a -> List a
    append Nil         ys = ys
    append (Cons x xs) ys = Cons x (append xs ys)
    ```
    - Inductive data types can be used to define data types such as lists (as demonstrated above), **[[Haskell Trees | trees]]** and others.

- The **`deriving`** keyword automatically generates instances of certain standard type classes (e.g. `Eq`, `Ord`), providing default implementations of the methods defined by those type classes:
    ```haskell
    data Color = Red | Green | Blue 
        deriving (Eq, Show, Ord)
    ```
    - For **`Eq`**, the default `(==)` tests if all data are equal.
    - For **`Ord`**, the default `(<=)` tests data one by one. **The derived ordering is based on the order in which the constructors are defined**, so `Red < Green`, `Green < Blue`, etc.
    - For **`Show`**, the default `show` method generates a string representation of the data type's value.
    - However, **unexpected behaviour** may arise (see the [[#^build-fraction | build_fraction example]]):
        ```haskell
         data Fraction = Fraction Integer Integer
            deriving (Eq, Ord, Show)
        ---
        ghci> x = build_fraction 1 2 ; y = build_fraction 1 3
        ghci> x == y
        False
        ghci> x <= y
        True  -- Incorrect result.        
        ghci> x
        Fraction 1 2
        ```
        This can be fixed by using the `instance` keyword.

- The **`instance`** keyword allows to create specific implementations of type class methods for a given data type (see the [[#^fraction | Fraction example]]):
    ```haskell
    instance Ord Fraction where
    Fraction n1 d1 <= Fraction n2 d2 = (d1*n2 <= d2*n1)

    instance Show Fraction where
    show (Fraction n d) = show n ++ " % " ++ show d
    ---
    ghci> x = fraction 1 2 ; y = fraction 1 3
    ghci> x <= y
    False
    ghci> x
    1 % 2
    ```

[^rational]: The `Fraction` data type is built-in as `Rational`, which is accessible through the `Data.Ratio` module:
    ```haskell
    ghci> :m Data.Ratio
    ghci> x = 1 % 2
    ghci> y = 1 % 3
    ghci> x == y
    False
    ghci> x <= y
    False
    ghci> x + y
    5 % 6
    ```
