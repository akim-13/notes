---
tags:
  - cm12003
  - CS
  - programming
links:
  - "[[Haskell]]"
---
# Haskell Lazy Evaluation

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
- **WARNING**: Haskell's evaluation is lazy but not smart, so for example the following expression will *not* terminate:
    ```haskell
    ghci> (map (*2) . filter (<= 10)) [1..]
    ...
    ```
    See [[Haskell Standard Functions | standard functions]] and [[Haskell Functions#^func-comp | function composition]].