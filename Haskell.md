---
tags:
  - cm12003
  - programming
  - CS
---
# Haskell
## Topics
- [[Haskell Functions | Functions]]     
- [[Haskell Conditionals | Conditionals]]
- [[Haskell Types | Types]]
- [[Haskell Lists | Lists]]
- [[Haskell Constructors & Pattern Matching | Constructors & Pattern Matching]]
## Examples
- [[Haskell Sorting Algorithms | Sorting Algorithm]]

## Unsorted

### Lazy Evaluation
- **Lazy evaluation** means that expressions are only evaluated when their values are needed. This, for instance, allows for creating and working with "infinite" lists like `[1..]`.

```haskell
isEmpty1 :: [a] -> Bool
isEmpty1 [] = True
isEmpty1 (x:xs) = False

isEmpty2 :: [a] -> Bool
isEmpty2 xs = length xs == 0
---
ghci> isEmpty1 [1..]
False

ghci> isEmpty2 [1..]
... (does not terminate)
```

```haskell
fibonacci :: [Int]
fibonacci = makeFibonacci 1 1

-- Does not have a recursion-terminating condition.
makeFibonacci :: Int -> Int -> [Int]
makeFibonacci n m = n : makeFibonacci m (n+m)
---
ghci> take 17 fibonacci
[1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,1597]
```

### Where clause
- The **`where` clause** allows to *localize* functions and variables (as opposed to leaving them global)
    ```haskell
    fibonacci :: [Int]
    fibonacci = makeFibonacci 1 1
        where
            makeFibonacci :: Int -> Int -> [Int]
            makeFibonacci n m = n : makeFibonacci m (n+m)
    ```

- It is also useful for naming **intermediate calculations** that are used in multiple places:
    ```haskell
    average :: [Int] -> Int
    average xs
        | count == 0 = error "Can't average no numbers"
        | otherwise = total `div` count 
        where
            total = sum xs
            count = length xs
    ```

### Map Function
- The **`map` function** generalizes a common pattern[^examples] of applying a given function to *every element* of the list:
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

[^examples]: Some examples of this pattern include:
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
