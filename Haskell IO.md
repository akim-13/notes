---
tags: cm12003, programming, CS
links: "[[Haskell]]"
---
# Haskell IO
- Some **standard IO functions** are:
    ```haskell
    putStr :: String -> IO ()
    putStr s -- Prints `s` to standard output.

    putStrLn :: String -> IO ()
    putStrLn s -- Same, then starts new line.

    print :: String -> IO ()
    print s -- Short for `putStrLn (show s)`.

    writeFile :: String -> String -> IO ()
    writeFile f s -- Opens a file `f` and writes `s` to it.

    getLine :: IO String
    s <- getLine -- Reads `s` from standard input.

    readFile :: String -> IO String
    s <- readFile f -- Opens a file `f` and reads contents to `s`.

	read :: String -> a
	read s :: a -- Convert `s` to a given type `a`.
    ```

    - These function have **two components**:
        1. An **IO action** — reading from / writing to the file system, standard IO, etc.
        2. A **return value** — e.g. the contents of the file being read, or the user’s input.

    - Expressions such as `putStr` that carry out an IO action (output text on the screen) **do not produce a useful value**, however they still return the empty tuple `()` (similar to `void` in Java or C). 

- Most of the time, the IO actions are done inside a **`do`-block**:
    ```haskell
    do_block = do
        exprIO        -- IO expression, drop return value.
        x <- exprIO   -- IO expression bound to x.
        let x = expr  -- Bind expression to x.
        return expr   -- Return value for the do_block.
    ```
    - The lines are executed **in order**.
    - Each line is either:
        - An **IO expression** whose *return value is thrown away*:
            ```haskell
            putStr "hello"
            ```
        - An **IO expression** whose *return value is bound to a variable*:
            ```haskell
            x <- readFile "hello.txt"
            ```
        - A **let-expression** that binds a non-IO expression to a variable:
            ```haskell
            let x = take 10 fibonacci
            ```

    - A do-block is **itself an IO expression**:
        ^do-is-io
        - *IO action*: the combination of the actions in the block.
        - *Return value*: that of the last line in the block (i.e. the last line *must* be an IO expression).

    - In a do-block, the lines must have the **types**:
        ```haskell
        do_block :: IO a
        do_block = do
            exprIO       :: IO b  -- `b` may be the same as `a`.
            x <- exprIO  :: IO b  -- then x :: b.
            let x = expr          -- not an expression, no type.
            return expr  :: IO a  -- where expr :: a.
        ```

- The **`return` function** takes a non-IO value and wraps it into an IO type, thus providing an explicit return value:
    ```haskell
    return :: a -> IO a
    ```
    - For example:
        ```haskell
        hitme = do
            putStrLn "Ninety-nine what?"
            x <- getLine
            return (99,x)
        ```
        - *IO action*: output `Ninety-nine what?`, then read input line as `x`.
        - *Return value*: the pair `(99,x)`.
    - Importantly, `return` is **not a keyword**, i.e. it does not cause the function to exit or return in the traditional sense (e.g. like the `return` keyword in Python).

- It is possible to write **recursive IO expressions**:
    ```haskell
    countdown n = do
        print n
        if n == 0 then do
            putStrLn "Liftoff!"
        else do
            countdown (n-1)
    ```
    - **Guards cannot be used** inside a `do`-block, therefore [[Haskell Conditionals#^if-then-else | if-then-else structure]] is used instead.
    - The recursion is possible since `do` is [[#^do-is-io | itself an IO expression]].

- To **accumulate return values**, the following recursive structure may be used:
    ```haskell
    getList = do
        putStr "Who's on the list?"
        x <- getLine
        if x == "Nobody" then 
            return ()
        else do
            putStrLn (x ++ " is on the list.")
            xs <- getList
            return (x:xs)
	---
	ghci> getList
	Who's on the list? You
	You is on the list.
	
	Who's on the list? Me
	Me is on the list.
	
	Who's on the list? Us
	Us is on the list.
	
	Who's on the list? Them
	Them is on the list.
	
	Who's on the list? Nobody
	["You","Me","Us","Them"]
    ```
