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

### Where Clause
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

### Sieve of Eratosthenes
We know that prime numbers are those which are indivisible, except in trivial ways.

Here’s a test for indivisibility:

indivisible :: Int -> Int -> Bool
indivisible x y = mod y x /= 0

We can filter for indivisibility:

ghci> filter (indivisible 2) [1..]
[1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,
41,43,45,47,49,51,53,55,57,59,61,63,65,67,69,71,73,75,77,
79,81,83,85,87,89,91,93,95,97,99,101,103,105,107,109,111,
113,115,117,119,121,123,125,127,129...

ghci> filter (indivisible 3) (filter (indivisible 2) [1..])
[1,5,7,11,13,17,19,23,25,29,31,35,37,41,43,47,49,53,55,59,
61,65,67,71,73,77,79,83,85,89,91,95,97,101,103,107,109,113,
115,119,121,125,127,131,133,137,139,143,145,149,151,155,157,
161,163,167,169,173,175,179,181,185,187,191,193...

This idea lets us write a version of the Sieve of Eratosthenes algorithm for finding primes.

- • Start with the list [2..]
    
- • The first number is prime (2).
    
- • Filter the tail to leave the numbers not divisible by 2
    
- • The next number is prime (3).
    
- • Filter the tail to leave the numbers not divisible by 3
    
- • …

sieve :: [Int] -> [Int]
sieve (x:xs) = x : sieve (filter (indivisible x) xs)

primes :: [Int]
primes = sieve [2..]