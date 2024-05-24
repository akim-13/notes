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


## Table of Definitions
| Term/Notion | Definition | Revised |
|-------------|------------|:-------:|
| Frontier | <details><summary></summary>The collection of all states that have been generated but have not yet been explored</details> | <input type="checkbox" /> |
| Complete search algorithm | <details><summary></summary>A search algorithm is called complete if it is guaranteed to find a solution (assuming one exists).</details> | <input type="checkbox" /> |
| Optimal search algorithm | <details><summary></summary>An algorithm is optimal if it guarantees to find the best solution according to the given cost function.</details> | <input type="checkbox" /> |
| Optimal solution | <details><summary></summary>An optimal solution refers to the best possible solution to a problem according to a specified criterion, usually minimizing or maximizing some cost function.</details> | <input type="checkbox" /> |
| Optimally efficient solution | <details><summary></summary>An optimally efficient solution refers to the efficiency of the algorithm used to find the solution, focusing on minimizing computational resources like time or memory (the solution itself might not necessarily be optimal).</details> | <input type="checkbox" /> |
| All properties of BFS, DFS and IDS | <details><summary></summary>See the completeness/optimality/time/space complexity table.</details> | <input type="checkbox" /> |
| Admissible heuristic | <details><summary></summary>A heuristic is admissible if it never overestimates the cost to reach the goal state.</details> | <input type="checkbox" /> |
| Consistent heuristic | <details><summary></summary>$h(n) \leq c + h(n')$</details> |<input type="checkbox" /> |
| A* is optimal when | <details><summary></summary>it uses an admissible heuristic.</details> | <input type="checkbox" /> |
| A* is optimally efficient when | <details><summary></summary>it uses a consistent heuristic.</details> | <input type="checkbox" /> |
| A* space complexity type | <details><summary></summary>Exponential</details> |<input type="checkbox" /> |
| Elements of the formal definition of CSPs | <details><summary></summary>1. A set of variables<br>2. A set of domains specifying the values each variable can take<br>3. A set of constraints that specifies the values that the variables are allowed to have collectively</details> | <input type="checkbox" /> |
| State | <details><summary></summary>A state is an assignment of values to all or some of the variables.</details> | <input type="checkbox" /> |
| Complete and partial states | <details><summary></summary>A state is called complete if it assigns all the variables, and partial if not.</details> | <input type="checkbox" /> |
| Consistent state | <details><summary></summary>A state is called consistent if it does not violate the constraints.</details> | <input type="checkbox" /> |
| Solution (CSP context) | <details><summary></summary>A solution is a state which is complete and consistent.</details> | <input type="checkbox" /> |
| MRV heuristic | <details><summary></summary>"One option is to choose the variable with the fewest legal values..."</details> | <input type="checkbox" /> |
| LCV heuristic| <details><summary></summary>The Least Constraining Value heuristic tells us that we should select the value which constrains the fewest other values.</details> | <input type="checkbox" /> |
| Utility function | <details><summary></summary>A function that assigns values to final states.</details> | <input type="checkbox" /> |
| Atomic sentence | <details><summary></summary>A logically irreducible statement which can be either true or false.</details> | <input type="checkbox" /> |
| Model | <details><summary></summary>A full assignment of truth values to atomic sentences.</details> | <input type="checkbox" /> |
| $\alpha \models \beta$| <details><summary></summary>We write $\alpha \models \beta$ (entails) if in every model in which $\alpha$ is true, $\beta$ is also true.</details> | <input type="checkbox" /> |
| $KB$ | <details><summary></summary>We can summarize the information we know about the world in a set of sentences (facts, rules, etc). This set is known as a Knowledge Base abbreviated $KB$.</details> | <input type="checkbox" /> |
| $KB \models \alpha$| <details><summary></summary>We write $KB \models \alpha$ if every possible model where every sentence in the knowledge base is true, then $\alpha$ is true</details> | <input type="checkbox" /> |
| Model checking | <details><summary></summary>It is used to determine if $KB \models \alpha$ by checking all possible worlds in which all the sentences in $KB$ are true (i.e. there are no contradictions). If $\alpha$ is true in all of them, then $KB \models \alpha$.</details> | <input type="checkbox" /> |
| $KB \vdash_i \alpha$ | <details><summary></summary>$\alpha$ is derived from the $KB$ using a given algorithm $i$.</details> | <input type="checkbox" /> |
| An algorithm $i$ is called sound | <details><summary></summary>If $KB \vdash_i \alpha$ always means that $KB \models \alpha$.</details> | <input type="checkbox" /> |
| An algorithm $i$ is called complete | <details><summary></summary>If $KB \models \alpha$ always means that $KB \vdash_i \alpha$.</details> | <input type="checkbox" /> |
| Soundness, completeness and complexity of model checking | <details><summary></summary>Sound, complete, exponential — there are $2^n$ models if we have $n$ atomic sentences.</details> | <input type="checkbox" /> |
| Proof system | <details><summary></summary>a set of inference rules.</details> |<input type="checkbox" /> |
| CNF | <details><summary></summary>Conjunctive Normal Form — conjunction of disjunctions of literals.</details> | <input type="checkbox" /> |
| Resolution inference rule | <details><summary></summary>$\frac{A_1 \lor A_2 \lor \ldots \lor A_n \lor B \quad \neg B \lor C_1 \lor C_2 \lor \ldots \lor C_m}{A_1 \lor A_2 \lor \ldots \lor A_n \lor C_1 \lor C_2 \lor \ldots \lor C_m}$</details> | <input type="checkbox" /> |
| Resolution proof is sound and complete when | <details><summary></summary>All sentences are in CNF.</details> | <input type="checkbox" /> |
| Modus Ponens | <details><summary></summary>$\frac{P \rightarrow Q \quad P}{Q}$</details> |<input type="checkbox" /> |
| Contraposition | <details><summary></summary>$(P \rightarrow Q) \equiv (\neg Q \rightarrow \neg P)$</details> | <input type="checkbox" /> |
| Biconditional elimination | <details><summary></summary>$(P \leftrightarrow Q) \equiv ((P \rightarrow Q) \land (Q \rightarrow P))$</details> | <input type="checkbox" /> |
| Outcome a.k.a. ...| <details><summary></summary>Realization is a possible result of a single trial.</details> | <input type="checkbox" /> |
| Sample space | <details><summary></summary>The set of all possible outcomes</details> |<input type="checkbox" /> |
| Event | <details><summary></summary>A subset of the sample space, i.e. a set of one or more outcomes from the sample space.</details> | <input type="checkbox" /> |
| Probability of an event | <details><summary></summary>The sum of the probabilities of each of the outcomes in the sample space where the event holds.</details> | <input type="checkbox" /> |
| Product rule for probability | <details><summary></summary>$P(X_1, X_2, X_3) = P(X_1) \cdot P(X_2 \mid X_1) \cdot P(X_3 \mid X_1, X_2)$</details> | <input type="checkbox" /> |
| Product rule for probability for independent variables | <details><summary></summary>$P(X_1, X_2, X_3) = P(X_1) \cdot P(X_2) \cdot P(X_3)$</details> | <input type="checkbox" /> |
| Marginalization (sum rule) | <details><summary></summary>$p(X) = \sum_Y p(X,Y) = \sum_Y p(X \mid Y)p(Y)$</details> | <input type="checkbox" /> |
| Bayes' rule | <details><summary></summary>$P(X \mid Y) = \frac{P(Y \mid X) \cdot P(X)}{P(Y)}$</details> | <input type="checkbox" /> |
| Markov property | <details><summary></summary>Systems with the Markov Property are “memoryless” – knowing how a particular state was arrived adds no information to what will happen next.</details> | <input type="checkbox" /> |
| MDP | <details><summary></summary>A Markov Decision Process consists of:<br>- A set of **states**: $\{s_0, s_1, \ldots\}$<br>- A set of **actions** $A(s)$ from each state $s$: $\{a_{s1}, a_{s2}, \ldots\}$<br>- A **transition model** – a transition probability for each set of action and state: $p(s_{t+1} \mid s_t, a_t)$<br>- A **reward** for each transition: $r(s_{t+1}, s_t, a_t)$</details> | <input type="checkbox" /> |
| Discounted return | <details><summary></summary>$G_t = r_{t+1} + \gamma r_{t+2} + \gamma^2 r_{t+3} + \gamma^3 r_{t+4} + \cdots = \sum_{k=0}^{\infty} \gamma^k r_{t+k+1}$</details> | <input type="checkbox" /> |
| Objective function for an MDP policy (and what to do with it)| <details><summary></summary>discounted return, maximize</details> | <input type="checkbox" /> |
| State-value function | <details><summary></summary>$V^\pi(s) = \mathbb{E}_\pi [G_t \mid S_t = s]$</details> | <input type="checkbox" /> |
| The Bellman equation | <details><summary></summary>$V^\pi(s) = \sum_a \pi(a \mid s) \sum_{r, s'} p(r, s' \mid a, s) \cdot \left( r + \gamma V^\pi(s') \right)$</details> | <input type="checkbox" /> |
| The Bellman optimality equation| <details><summary></summary>$V^*(s) = \max_a \sum_{r, s'} p(r, s' \mid a, s) \left( r + \gamma V^*(s') \right)$</details> | <input type="checkbox" /> |
| Fundamental assumptions in ML | <details><summary></summary>1. Similar Feature Values and Similar Outputs —  If two observations have similar feature values (e.g., length of tail, weight, length of ears), it is assumed that their outputs will also be similar or the same (e.g., the type of animal).<br>2. Smoothness —  if observations are close in the input space (i.e., their features are similar), their outputs will also be close in the output space</details> | <input type="checkbox" /> |
| Reasons for bias in supervised learning | <details><summary></summary>Bias in society, relying on prior beliefs, unbalanced datasets.</details> | <input type="checkbox" /> |
| Supervised learning | <details><summary></summary>compare observations/inputs against each other to try to separate them in terms of the target – our aim is to distinguish between different inputs such that this helps to distinguish between targets.</details> | <input type="checkbox" /> |
| Unsupervised learning | <details><summary></summary>we do not have labels or do not care about the labels. We wish to gain insights into what is described in the dataset. We wish to gain understanding of the phenomenon</details> | <input type="checkbox" /> |