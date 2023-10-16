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
        - Examples:
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
