---
tags:
  - cm12003
  - CS
  - programming
links: "[[Haskell]]"
---

# Haskell Lists
- A **list** is a sequence of elements of the same type.
- If the **elements** have **type** `a`, the list has type `[a]`:
    ```haskell
    [1,2,3,4,5] :: [Int]
    [True,False] :: [Bool]
    ['a','b','c'] :: [Char]
    ["Brouwer","Heyting","De Bruijn","Dijkstra"] :: [String]
    [ [3], [1,8], [], [4,5,6] ] :: [[Int]]
    ```
- A **`String`** is just a list of characters: 
    ```haskell
    "abc" :: String  ==  ["a","b","c"] :: [Char]
    ```
- Lists are **defined using** two **constructors**:
    - `[]` (**nil**) - the empty list.
    - `x:xs` (**cons**) - put a "head" element `x` on top of a "tail" list `xs`. Importantly, it does *not* work the other way around.
    ```haskell
    ghci> 1 : [2,3]             ghci> 1 : 2 : 3 : []
    [1,2,3]                     [1,2,3]
    
    ghci> 'a' : "bcd"           ghci> 1 : 2 : 3 : [4,5]
    "abcd"                      [1,2,3,4,5]

    ghci> 1 : (2 : (3 : [] ))   ghci> ((1 : 2) : 3) : []
    [1,2,3]                     * error ...
    ```
 ^a73fd4
- The notation `[1,2,3]` is **syntactic sugar** for the internal definition: `1 : 2 : 3 : []`.
- Lists can be **built** recursively using nil and cons as functions:
    ```haskell
    countdown :: Int -> [Int]
    countdown x
    | x <= 0    = []
    | otherwise = x : countdown (x-1)
    --
    ghci> countdown 5   ghci> countdown (-13)
    [5,4,3,2,1]         []
    ```
- **Examples** of recursively built lists with pattern-matching:
    ```haskell
    -- Sum integers in a list
    total :: [Int] -> Int
    total [] = 0
    total (first_element:the_rest) = first_element + total the_rest
    -----
    -- Every following line outputs 6.
    ghci> total [1..3]
    6
    ghci> total (1 : [2,3]) -- Matching (x:xs) pattern
    ghci> 1 + total [2,3]
    ghci> 1 + total (2 : [3])
    ghci> 1 + 2 + total ([3])
    ghci> 1 + 2 + total (3 : [])
    ghci> 1 + 2 + 3 + total []
    ghci> 1 + 2 + 3 + 0
	```
 
	```haskell
    -- Add an element to the end of a list
    snoc :: Int -> [Int] -> [Int]
    snoc x [] = [x]
    snoc x (y:ys) = y : snoc x ys
    -----
    -- Every following line outputs [1,2,3,4].
    ghci> snoc 4 [1,2,3]
    [1,2,3,4]
    ghci> snoc 4 (1 : [2,3])
    ghci> 1 : snoc 4 ([2,3])
    ghci> 1 : snoc 4 (2 : [3])
    ghci> 1 : 2 : snoc 4 ([3])
    ghci> 1 : 2 : snoc 4 (3 : [])
    ghci> 1 : 2 : 3 : snoc 4 []
    ghci> 1 : 2 : 3 : [4]
	```
 
	```haskell
    -- Reverse a list, inefficiently.
    rev :: [Int] -> [Int]
    rev [] = []
    rev (x:xs) = snoc x (rev xs)
    ```
