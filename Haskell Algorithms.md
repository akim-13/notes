---
tags: cm12003, cs, programming
links: "[[Haskell]]"
---
# Haskell Algorithms
## Sorting
### Merge Sort
```haskell
merge :: Ord a => [a] -> [a] -> [a]
merge xs [] = xs
merge [] ys = ys
merge (x:xs) (y:ys)
    | x <  y    = x : merge    xs (y:ys)
    | x == y    = x : merge    xs    ys
    | otherwise = y : merge (x:xs)   ys

msort :: Ord a => [a] -> [a]
msort []  = []
msort [x] = [x]
msort xs  = merge (msort (take n xs)) (msort (drop n xs))
  where
    n = div (length xs) 2
```

### Insertion Sort
```haskell
insert :: Ord a => a -> [a] -> [a]
insert x []     = [x]
insert x (y:ys)
    | x <= y    = x : y : ys
    | otherwise = y : insert x ys

isort :: Ord a => [a] -> [a]
isort []     = []
isort (x:xs) = insert x (isort xs)
```

## Sieve of Eratosthenes
- This is one of the most famous algorithms for **finding prime numbers**:
    ```haskell
    indivisible :: Int -> Int -> Bool
    indivisible x y = y `mod` x /= 0

    sieve :: [Int] -> [Int]
    sieve (x:xs) = x : sieve (filter (indivisible x) xs)

    primes :: [Int]
    primes = sieve [2..]
    ---
    ghci> take 10 primes
    [2,3,5,7,11,13,17,19,23,29]
    ```

- The algorithm works as follows:
    1. Start with the list `[2..]`.
    2. The first number is prime (`2`).
    3. Filter the tail to leave the numbers not divisible by 2:
        ```haskell
        ghci> filter (indivisible 2) [2..]
        [3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,
        41,43,45,47,49,51,53,55,57,59,61,63,65,67,69,71,73,75,77,
        79,81,83,85,87,89,91,93,95,97,99,101,103,105,107,109,111,
        113,115,117,119,121,123,125,127,129...
        ```
    4. The next number is prime (`3`).
    5. Filter the tail to leave the numbers not divisible by 3:
        ```haskell
        ghci> filter (indivisible 3) (filter (indivisible 2) [2..])
        [5,7,11,13,17,19,23,25,29,31,35,37,41,43,47,49,53,55,59,
        61,65,67,71,73,77,79,83,85,89,91,95,97,101,103,107,109,113,
        115,119,121,125,127,131,133,137,139,143,145,149,151,155,157,
        161,163,167,169,173,175,179,181,185,187,191,193...
        ```
    6. …
