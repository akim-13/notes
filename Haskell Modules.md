---
tags: cm12003, cs, programming
links: "[[Haskell]]"
---
# Haskell Modules
- **Modules** are Haskell's function libraries, many of which are pre-installed.
- More modules can be found on **Hackage**: [hackage.haskell.org](https://hackage.haskell.org).
- To **import** a module use the `import` keyword at the top of the file, or `:m` in ghci:
    ```haskell
    Import Data.Ratio
    x = 1 % 2
    y = 1 % 3
    ---
    ghci> :m Data.Ratio  -- Not need if already imported in the file.
    ghci> x + y
    5 % 6
    ```
- Example modules:
    - `Data.List`: more list functions.
    - `Data.Char`: functions for characters and strings.
    - `Data.Ratio`: rational numbers.
    - `System.Random`: (pseudo)-random number generators.