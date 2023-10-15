---
tags:
  - cm12003
  - CS
  - programming
links: "[[Haskell]]"
---
# Haskell Constructors & Pattern Matching
- [[Haskell Lists#^a73fd4| Nil ([]) and Cons (:)]]
- **Pairs constructor** is `(,)`:
    ```haskell
    vectorAdd :: (Float,Float) -> (Float,Float) -> (Float,Float)
    vectorAdd (x1,y1) (x2,y2) = (x1+x2, y1+y2)
    ```

- Each constructor has a pattern that allows for **pattern-matching**:
    - In the following example the patterns are nil (`[]`) and cons (`x:xs`), where `x` is a **variable** that is matched with the *first element of the input list*, and `xs` is matched with the rest of the list.
    ```haskell
    isEmpty :: [a] -> Bool
    isEmpty [] = True
    isEmpty (x:xs) = False
    ```
    - The **order** matters: top patterns are matched first.

    - **Wildcards** (`_`) are used in pattern-matching when the matched parameter will not be used (or to match the rest of the patterns like in `isEmpty`):
    ```haskell
    head (x:_) = x
    tail (_:xs) = xs

    -- Alternative isEmpty implementation:
    isEmpty :: [a] -> Bool
    isEmpty [] = True
    isEmpty _ = False
    ```
    - It is also possible to pattern-match **`True`, `False` and integers**:
    ```haskell
    not :: Bool -> Bool
    not True = False
    not False = True

    factorial :: Int -> Int
    factorial 0 = 1
    factorial 1 = 1
    factorial n = n * factorial (n-1)
    ```
