---
tags: cm12003, programming, cs
links: "[[Haskell]]"
---
# Haskell Trees
- **Tree** — abstract data type that simulates a hierarchical tree structure. It consists of:

    ![[Attachments/Pasted image 20231111125556.png]] 
    1. **Root**: The topmost node in the tree, which has no parent.
    2. **Edge**: The connection between one node to another.
    3. **Child**: A node that has a parent node.
    4. **Parent**: A node that has an edge to one or more nodes.
    5. **Leaf**: A node that has no children.
    6. **Subtree**: A tree entirely contained within another tree.
    7. **Height**: The length of the longest path to a leaf.
    8. **Depth**: The length of the path to its root.

- Trees can be used to represent a **file system**, where each node is either a file or a directory, which can contain more directories (see [[Haskell Data Types#^inductive-data-types| inductive data types]]):
    ```haskell
    data Folder = Folder [File] [Folder]
    ```

- **Arithmetic expressions**, such as $3 + (5 - (4 \times 2))$, can be thought of as trees:

    ![[Attachments/Pasted image 20231111133453.png]] ^cc80ee
	
    See the implementation [[Haskell Data Types#^be153e | here]].

- **Binary tree** — a tree in which each node has at most two children.

    ![[Attachments/Pasted image 20231111125434.png]]
    - An **integer binary tree** can be implemented in Haskell using an [[Haskell Data Types#^inductive-data-types| inductive data type]]:
        ```haskell
        data IntTree = Empty | Node Int IntTree IntTree
            deriving Show
        ---
        ghci> x = Node 1 (Node 0 Empty Empty) (Node 5 Empty Empty)
        ghci> print x
        Node 1 (Node 0 Empty Empty) (Node 5 Empty Empty)
        ```
        ![[Attachments/Pasted image 20231111130450.png]]
        - Examples of functions that implement **recursion over trees**:
        ```haskell
        size :: IntTree -> Int
        size Empty = 0
        size (Node x left right) = 1 + size left + size right

        total :: IntTree -> Int
        total Empty = 0
        total (Node x left right) = x + total left + total right

        treemap :: (Int -> Int) -> IntTree -> IntTree
        treemap f Empty = Empty
        treemap f (Node x left right) = Node (f x) (treemap f left) (treemap f right)
        ```
        Applying `treemap (*2)` to the following tree:
        ![[Attachments/Pasted image 20231111140202.png]]
        will result in:
        ![[Attachments/Pasted image 20231111140212.png]]
    - The above `IntTree` data type can be generalized to store any type:
        ```haskell
        data Tree a = Leaf | Branch a (Tree a) (Tree a)
            deriving Show
        ```
    - A binary tree is **ordered** if every value in a left subtree is smaller than the node’s value, and every integer in a right subtree is larger than the node’s value.
        - The following function allows to **insert an element** into an ordered tree:
            ```haskell
            insertT :: Int -> IntTree -> IntTree
            insertT x Empty = Node x Empty Empty
            insertT x (Node y left right)
                | x <= y    = Node y (insertT x left) right
                | otherwise = Node y left (insertT x right)
            ```
        - It is possible to **sort a list** using trees:
            ```haskell
            -- Build an ordered tree from a list.
            build :: [Int] -> IntTree
            build []     = Empty
            build (x:xs) = insertT x (build xs)
            -- Alternatively, using folding:
            build = foldr insertT Empty

            -- Flatten a tree into a list.
            flatten :: IntTree -> [Int]
            flatten Empty = []
            flatten (Node x left right) =
            flatten left ++ [x] ++ flatten right

            -- First build an ordered tree and then flatten it.
            treeSort :: [Int] -> [Int]
            treeSort = flatten . build
            ---
            ghci> build [1,3,6,4,2]
            Node2 (Node 1 Empty Empty) (Node 4 (Node 3 Empty Empty) (Node 6 Empty Empty))
            
            ghci> flatten Node2 (Node 1 Empty Empty) (Node 4 (Node 3 Empty Empty) (Node 6 Empty Empty))
            [1,2,3,4,5,6]

            ghci> treeSort [1,6,2,5,3,4] 
            [1,2,3,4,5,6]
            ```
            This is very similar to the [[./Haskell Algorithms.md#Insertion Sort | insertion sort]] algorithm. However, on average this algorithm is faster — $O(n \log{n})$, compared to $O(n^2)$ for insertion sort.

            See also [[Haskell Standard Functions#^foldr | folding]] and [[Haskell Functions#^func-comp | function composition]].

