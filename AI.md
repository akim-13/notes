---
tags: cm12001, cs
links: 
presentations: W7
---
# AI
## Terminology
- **Agent** — an entity that makes decisions or performs actions based on its surroundings and objectives.
- **Rational agent** — an agent acting in a way that will achieve the *best outcome*, or in situations of uncertainty, the *best expected outcome*.
- **Search problem** is a situation where an agent chooses a series of *actions* to take it from an *initial state* to a specified *goal state*.
- A search problem can have one or multiple *solutions* and **optimal solutions**, i.e. the best possible solution according to a specified criterion or set of criteria.

    ![[Attachments/Pasted image 20231129195636.png]]

- A **state** is a specific configuration or condition of the system/problem at a particular point in time. It represents a snapshot of all relevant information needed to describe the system at that moment. For example, in a chess game, a state would represent the positions of all the pieces on the chessboard at any given turn.
- An **action** (or **transition**) is the means by which the system moves from one state to another.
- **State space** — the set of all possible states that the system or problem can be in. It represents the entire landscape or universe of possible configurations, i.e. the *search problem itself*. The above example can be simplified as the following state space:

    ![[Attachments/Pasted image 20231129200754.png]]

- **Search tree** represents the carrying out of a search of the state space.
    - In the search tree, the **children** of each node are the states reachable in exactly one action.
    - As the searched tree gets explored, the **explored states** (*in purple*) and the **frontier** (available states, *in green*) change.

        ![[Attachments/Pasted image 20231129201440.png]]

- **Graphs** are defined by a collection of *vertices* (points) and *edges* (lines).
    - Graphs can be **weighted** or **unweighted**, and **directed** or **undirected**.

- A **tree** is a special type of graph with the following properties:
    - Every node except the root node has **exactly one parent node**.
    - It is **acyclic** — no node can be its own ancestor, which means there are no cycles or loops.

## Search Algorithms
- A search algorithm is called **complete** if it is guaranteed to find a solution (assuming one exists).
- A search algorithm is called **optimal** if it is guaranteed to find an optimal solution.
- **Time Complexity** is normally measured in terms of the number of nodes generated during the search.
- **Space complexity** is normally measured in terms of the maximum number of nodes stored in memory.
- Time and complexity of a tree-searching algorithm can be specified using the **branching factor** ($b$), **maximum depth** ($m$) and **depth of the shallowest goal node** ($d$).

    ![[Attachments/Pasted image 20231129211135.png]]

### Uninformed search
- **Uninformed search** (or **blind search**) is a class of algorithms for searching through a problem's state space without any domain-specific knowledge other than the problem definition itself. These algorithms only know whether a state is a goal state and how to generate successor states.
- A **breadth-first search (BFS)** explores the shallowest state in the frontier.

    ![[Attachments/Pasted image 20231129210716.png]]

- A **depth-first search (DFS)** explores the deepest state in the frontier.

    ![[Attachments/Pasted image 20231129210858.png]]

- An **iterative deepening search (IDS)** is a depth first search, but only up to a certain depth, $D$. If the search at depth $D$ finishes without finding a goal state, $D$ is incremented.

    ![[Attachments/Pasted image 20231129215650.png]]

- **Comparison** of uninformed searches:[^comparison]

    |                  | Breadth-first       | Depth-first         | Iterative Deepening |
    |------------------|---------------------|---------------------|---------------------|
    | Complete?        | Yes                 | Yes                 | Yes                 |
    | Optimal?         | Yes                 | No                  | Yes                 |
    | Time Complexity  | $O\left(b^d\right)$ | $O\left(b^m\right)$ | $O\left(b^d\right)$ |
    | Space Complexity | $O\left(b^d\right)$ | $O\left(bm\right)$  | $O\left(bd\right)$  |

[^comparison]: ChatGPT's explanation of each property (has not been sanity-checked):
    - **BFS**
        - **Complete?**: Yes, BFS is complete, which means it will always find a solution if one exists, as it systematically explores each level of the tree before moving to the next.
        - **Optimal?**: Yes, when the path cost is a non-decreasing function of the depth of the node. BFS is optimal because it always finds the shallowest (least-cost) solution first.
        - **Time Complexity**: $O(b^d)$, where $b$ is the branching factor, and $d$ is the depth of the shallowest solution. This is because BFS must explore all nodes at each level of the tree before finding the solution.
        - **Space Complexity**: $O(b^d)$, as it needs to store all the nodes at the current level to find their successors.
    - **DFS:**
        - **Complete?**: Yes, DFS is complete in finite spaces, but in infinite spaces or trees with infinite branches, it may get trapped in one part of the tree.
        - **Optimal?**: No, because DFS might find a deeper solution even if a shallower one exists.
        - **Time Complexity**: $O(b^m)$, with $m$ as the maximum depth of the tree. This is because DFS continues to explore to the deepest level before backtracking.
        - **Space Complexity**: $O(bm)$, which is less than BFS, as it only needs to store a single path from the root to a leaf node, along with unexplored sibling nodes for each node on the path.
    - **IDS:**
        - **Complete?**: Yes, it combines the depth-first exploration of space with the level-by-level exploration of BFS.
        - **Optimal?**: Yes, it finds the shallowest solution first, similar to BFS.
        - **Time Complexity**: $O(b^d)$, which may seem counter-intuitive since it revisits nodes. However, the number of nodes revisited is a small fraction of the total number of nodes, so the overall time complexity is the same as BFS.
        - **Space Complexity**: $O(bd)$, which is much better than BFS, as it stores only a single depth-limited path at a time, similar to DFS.
