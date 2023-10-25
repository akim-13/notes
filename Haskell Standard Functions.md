---
tags:
  - cm12003
  - CS
  - programming
links:
  - "[[Haskell]]"
  - "[[Haskell Functions]]"
---
# Haskell Standard Functions
- A useful resource for **finding standard functions** is https://hoogle.haskell.org/. When unsure if a standard function that does X exists, search for its type, e.g. `(a -> Bool) -> [a] -> [a]` to find `filter`.

- **`map`** generalises a common pattern of *applying* a given function *to every element* of the list[^map-eg]:
    ^map
    ```haskell
    map :: (a -> b) -> [a] -> [b]
    map f []     = []
    map f (x:xs) = f x : map f xs
    ---
    ghci> [1..5]
    [1,2,3,4,5]

    ghci> map even it
    [False,True,False,True,False]

    ghci> map show it
    ["False","True","False","True","False"]

    ghci> map length it
    [5,4,5,4,5]
    ``` 
    - Map and **recursion** can do strange things:
         ```haskell
        counter :: [Int]
        counter = 0 : map (+1) counter
        --- 
        ghci> counter
        ==   0 : map (+1) counter
        ==   0 : map (+1) (0 : map (+1) counter)
        ==   0 : 1 : map (+1) (map (+1) counter)
        ==   0 : 1 : map (+1) (map (+1) (0 : map (+1) counter))
        ==   0 : 1 : map (+1) (1 : map (+1) (map (+1) counter))
        ==   0 : 1 : 2 : map (+1) (map (+1) (map (+1) counter)) 
        ...
        [1,2,3,4,5,...]
        ```

- **`filter`** allows to *select or remove* items, which meet a given condition, from a list[^filter-eg]:
    ```haskell
    filter :: (a -> Bool) -> [a] -> [a]
    filter p [] = []
    filter p (x:xs)
        | p x        = x : filter p xs
        | otherwise =      filter p xs
    ```
    The argument `p` is the *predicate* or *property*. Elements `x` that make `p x` `True` are kept, and the others are discarded.
    - Examples:
        ```haskell
        evens :: [Int] -> [Int]
        evens xs = filter even xs

        positives :: [Int] -> [Int]
        positives xs = filter (1<=) xs

        -- Or partially with applied definitions:
        evens :: [Int] -> [Int]
        evens = filter even

        positives :: [Int] -> [Int]
        positives = filter (1<=)
        ```

- **`zip`** *creates* a list of *pairs* of corresponding elements from two lists:
    ```haskell
    zip :: [a] -> [b] -> [(a,b)]
    zip [] _          = []
    zip _ []          = []
    zip (x:xs) (y:ys) = (x,y) : zip xs ys
    ---
    ghci> zip [1,2,3] [4,5,6]
    [(1,4),(2,5),(3,6)]

    ghci> zip "Hello" "Hi"
    [('H','H'),('e','i')]
    ```
    - **`zipWith`** *applies a given function* to every pair of elements from two lists:
        ```haskell
        zipWith :: (a -> b -> c) -> [a] -> [b] -> [c]
        zipWith _ [] _          = []
        zipWith _ _ []          = []
        zipWith f (x:xs) (y:ys) = f x y : zipWith f xs ys
        ```
        - **Examples**:
        ```haskell
        -- For [x1,x2,x3,...] we want to test:
        -- x1 <= x2 &&
        -- x2 <= x3 &&
        -- x3 <= x4 &&
        -- ...
        -- to check if the list is in order.

        ordered :: Ord a => [a] -> Bool
        ordered xs = and (zipWith (<=) xs (tail xs))
        ```
        ```haskell
        fibonacci :: [Int]
        fibonacci = makeFibonacci 1 1
            where
                makeFibonacci n m = n : makeFibonacci m (n+m)
         
        -- Since the first row plus the second row gives the third row:
        --            fibonacci  =   1 : 1 : 2 : 3 : 5 : 8 : ...
        --       tail fibonacci  =   1 : 2 : 3 : 5 : 8 : ...
        -- tail (tail fibonacci) =   2 : 3 : 5 : 8 : ...
        -- the above can be written as:
        fibonacci = 1 : 1 : zipWith (+) fibonacci (tail fibonacci)
        ```

- **`foldr`** replaces `:` in a list with a given function `f`, and the last element (`[]`) with a given unit value `u`:[^foldr-eg]
    ```haskell
    foldr :: (a -> b -> b) -> b -> [a] -> b
    foldr f u []     = u
    foldr f u (x:xs) = f x (foldr f u xs)
    -- E.g.
    xs           =   x1  :  (x2  :  (x3  :  ...  : (xn  : [ ]))...
    foldr f u xs =   x1 `f` (x2 `f` (x3 `f` ... `f`(xn `f` u ))...
    ```
    - **Examples**:
        ```haskell
        -- Partially applied, i.e. `sum` is waiting for a list input,
        -- which will also be appended to `foldr` as a 3rd argument.
        sum     = foldr (+) 0
        product = foldr (*) 1

        -- An intuitive solution for `length` might be `foldr (+1) 0`.
        -- However, to see why it doesn't work, and how it should work,
        -- replace `f` in the example above with appropriate function,
        -- starting from the innermost layer.
        length = foldr f 0
            where f _ n = n+1

        or :: [Bool] -> Bool
        or = foldr (||) True

        concat :: [[a]] -> [a]
        concat = foldr (++) []

        -- Appends xs to ys.
        append :: [a] -> [a] -> [a]
        append xs ys = foldr (:) ys xs

        -- ?
        reverse = foldr snoc []
            where snoc x = foldr (:) [x]

        member :: Eq a => a -> [a] -> Bool
        member x = foldr f False
            where f y b = x == y || b

        -- Think about these:
        concatmap :: (a -> [b]) -> [a] -> [b]
        concatmap f = foldr g []
            where g x ys = f x ++ ys

        unZip :: [(a,b)] -> ([a],[b])
        unZip = foldr f ([],[])
            where f (x,y) (xs,ys) = (x:xs,y:ys)
        ```

    - The `r` in `foldr` stands for "right", because it starts folding from the right. Correspondingly, there is also **`foldl`**.
    - **`foldr1`** uses the last element as the basis of the fold instead of the unit case `u`:
    ```haskell
    foldr1 :: (a -> a -> a) -> [a] -> a
    foldr1 f (x1  :  (x2  :  (x3  :  ...  : [xn] ))) ==
              x1 `f` (x2 `f` (x3 `f` ... `f` xn  ))
    -- E.g.
    product = foldr (*)
    ```


[^map-eg]: Some examples of this pattern include:
    ```haskell
    addOne :: [Int] -> [Int]
    addOne []     = []
    addOne (x:xs) = (x+1) : addOne xs

    squareAll :: [Int] -> [Int]
    squareAll []     = []
    squareAll (x:xs) = (x*x) : squareAll xs

    reverseAll :: [String] -> [String]
    reverseAll []     = []
    reverseAll (x:xs) = reverse x : reverseAll xs
    ```

[^filter-eg]: Common pattern generalised by `filter`:
    ```haskell
    evens :: [Int] -> [Int]
    evens [] = []
    evens (x:xs)
        | even x    = x : evens xs
        | otherwise =     evens xs

    positives :: [Int] -> [Int]
    positives [] = []
    positives (x:xs)
        | x >= 1    = x : positives xs
        | otherwise =     positives xs
    ```

[^foldr-eg]: Common pattern generalized by `foldr`:
    ```haskell
    sum :: Num a => [a] -> a
    sum []     = 0
    sum (x:xs) = x + sum xs

    product :: Num a => [a] -> a
    product []     = 1
    product (x:xs) = x * product xs

    length :: [a] -> Int
    length []     = 0
    length (_:xs) = 1 + length xs
    ```
