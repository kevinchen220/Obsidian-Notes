---
dg-publish: true
tags: CS370
---
# Search
>[!tldr] Searching
>* Often not given an algorithm to solve a problem
>	* Only specification of **what is a solution**
>	* We have to **search** for a solution
>* We can do so by exploring a **directed graph** that represents the **state space** of our problem
>* Sometimes the graph is literal
>	* Nodes may represent actual locations in space
>	* Edges represent the distance between them
>* Sometimes the graph is implicit
>	* Nodes represent **states**
>	* Edges represent **state transitions**

## Directed Graphs
* A **graph** consists of a set $N$ of **nodes** and a set $A$ of ordered pairs of nodes, called **arcs** or **edges**
* Node $n_2$ is a **neighbor** of $n_1$ if there is an arc from $n_1$ to $n_2$
* A **path** is a sequence of nodes $n_0, n_1, \cdots, n_k$ such that $(n_{i-1}, n_i) \in A$
* Often there is a **cost** associated with arcs and the cost of a paths is the sum of the costs of the arcs in the path
## A Search Problem
>[!important] Definition
>* A **search problem** is defined by:
>* * A set of **states**
>* An **initial state**
>* **Goal states**
>	* a boolean function which tells whether a given state is a goal state
>* A **successor/neighbor function**
>	* an action which takes us from one state to other states
>* A **cost** associated with each action
>
>A solution to the problem is a path from the start state to a goal state
>* optionally with the smallest cost

### Graph Searching
![[Pasted image 20250415103900.png]]
Generic search algorithm:
* Given a graph, start nodes, and goal nodes, **incrementally explore paths** from the start nodes
* Maintain a **frontier** of paths from the start node that have been explored
* As search proceeds, the frontier **expands** into the unexplored nodes until a goal node is encountered
* The way in which the frontier is expanded defines the **search strategy**
### Graph Search Algorithm
![[Pasted image 20250415103943.png]]
* We assume that after the search algorithm returns an answer, it can be asked for more answers and the **procedure continues**
* The **neighbors** define the graph structure
* Which value is **selected** from the frontier and how the new values are **added** to the frontier at each stage defines the **search strategy**
* Goal defines what is a **solution**
## Uniformed (blind) Search
### Depth-First Search
* DFS treats the frontier as a **stack**
* It always selects the **last element** added to the frontier
#### Cycle Checking
* A searcher can **prune** a path that ends in a node **already on the path**
* We will assume that this check can be done via hashing in constant time
#### Implementation of DFS
> [!tldr]- DFS with Cycle Check
> ![[Pasted image 20250415104452.png]]

> [!tldr]- Recursive Implementation of DFS
> ![[Pasted image 20250415104522.png]]

#### Properties of DFS
##### Useful Quantities
* **b** is the branching factor
* **m** is the maximum depth of the search tree
* **d** is the depth of the shallowest goal node
##### Properties
* **Space Complexity:** size of frontier in worst case
	* $O(bm)$
* **Time Complexity:** number of nodes visited in worst case
	* $O(b^m)$
* **Completeness:** does it find a solution when one exists?
	* No, will get stuck in an infinite path
* **Optimality:** if solution found, is it the one with the least cost?
	* No, it pays no attention to the costs and makes no guarantee on the solution’s quality
#### When should we use DFS?
**Useful when:**
* Space is restricted
* Many solutions exist, perhaps with long paths
**DFS is a poor method when:**
* There are infinite paths
* Solutions are shallow
* There are multiple paths to a node
### Breadth-First Search
* BFS treats the frontier as a **queue**
* It always selects the **earliest** element added to the frontier
#### Multiple-Path Pruning
**Prune** a path to node $n$ that **if any previously-found path terminates in $n$**
* **subsumes a cycle check** because the current path is a path to the node
* Need to **store all nodes** it has found paths to
* Want to **guarantee that an optimal solution** can still be found
#### Implementation
>[!tldr]- BFS with Multiple-Path Pruning
>![[Pasted image 20250415105544.png]]

#### Properties of DFS
##### Properties
* **Space Complexity:** size of frontier in worst case
	* $O(b^d)$
* **Time Complexity:** number of nodes visited in worst case
	* $O(b^d)$
* **Completeness:** does it find a solution when one exists?
	* Yes, explores the tree level by level until it finds a goal
* **Optimality:** if solution found, is it the one with the least cost?
	* No, guaranteed to find the shallowest goal node
#### When should we use BFS
**Useful when:**
* Space is not a concern
* We would like a solution with the fewest arcs
**Poor method when:**
* All the solution are deep in the tree
* The problem is large and the graph is dynamically generated
### Iterative-Deepening Search
**Combine the best of BFS and DFS**
* For every depth limit, perform DFS until the depth limit is reached
#### Properties
##### Properties
* **Space Complexity:** size of frontier in worst case
	* $O(bd)$
	* similar to DFS
* **Time Complexity:** number of nodes visited in worst case
	* $O(b^d)$
	* Same as BFS
* **Completeness:** does it find a solution when one exists?
	* Yes, explores the tree level by level until it finds a goal
	* Same as BFS
* **Optimality:** if solution found, is it the one with the least cost?
	* No, guaranteed to find the shallowest goal node
	* Same as BFS
### Lowest-Cost-First Search
Sometimes there are **costs** associated with arcs
* The cost of a path is the **sum of the costs** of its arcs
At each stage, **LCFS** selects a path on the frontier with lowest cost
* The frontier is a **priority queue** ordered by path cost
* It finds a **least-cost path** to a goal node
* When arc costs are **equal** $\implies$ BFS
* Still **uniformed/blind search** (does not take the goal into account)
##### Properties
* **Space Complexity:** size of frontier in worst case
	* Exponential
* **Time Complexity:** number of nodes visited in worst case
	* Exponential
* **Completeness:** does it find a solution when one exists?
	* Yes, if branching factor is finite and cost of each edge is **strictly positive**
* **Optimality:** if solution found, is it the one with the least cost?
	* Yes, if branching factor is finite and cost of each edge is **strictly positive**
### Dijkstra’s Algorithm
Variant of LCFS with a kind of multiple-path pruning
* Like LCFS, frontier is stored in **priority queue**, sorted by cost
* For every node in the graph, we keep track of the **lowest cost to reach it** so far
* If we find a lower cost path to a node, we update that value
	* May require re-sorting the priority queue
* An example of **dynamic programming** because it trades space (store value for each node) for time (find the shortest path faster)
## Heuristic Search
**Idea:** don’t ignore the goal when selecting paths
* Often there is extra knowledge that can be used to guide the search: **heuristic**
$h(n)$ is an **estimate** of the cost of the **shortest path** from node $n$ to a goal node
* uses only **readily obtainable** information about a node
* computing the heuristic must be **much easier** than solving the problem
* $h$ can be **extended** to paths: $h(n_0, n_1, \cdots, n_k) = h(n_k)$
* $h(n)$ is an **underestimate** if there is no path from $n$ to a goal that has path length less than $h(n)$
> [!example] Example Heuristic Functions
> * If the nodes are points on a Euclidean plane and the cost is the distance, we can use the **straight-line distance** from $n$ to the closest goal as the value of $h(n)$
> * If the nodes are locations and cost is **time**, we can use the distance to a goal divided by the maximum speed
> * If nodes are locations on a grid and cost is distance, we can use the **Manhattan distance**
> 	* distance by taking horizontal and vertical moves only
### Greedy Best-First Search
**Idea:** select the path whose end is **closest to a goal** according to the **heuristic** function
* **Best-first search** selects a path on the frontier with **minimal $h$-value**
* It treats the frontier as a **priority queue** ordered by $h$
#### Implementation
>[!tldr]- Best-First Search with Multiple Path Pruning
>![[Pasted image 20250415123923.png]]
#### Properties
* **Space and Time complexities**
	* Both exponential
* **Completeness and Optimality**
	* No, GBFS is not complete
		* It could be stuck in a cycle
	* No, GBFS is not optimal
		* It may return a sub-optimal path first
### Heuristic Depth-First Search
**Idea:** Do a **DFS**, but add paths to the stack **ordered according to $h$**
* **Locally** does a best-first search, but aggressively pursues the **best looking** path
	* Even if it ends up being worse than one higher up
* Same properties as regular depth-first search
* Is often **used in practice**
#### Implementation
>[!tldr]- Heuristic Depth-First Search
>![[Pasted image 20250415124401.png]]

### A* Search
Uses both path **cost and heuristic** values
* $cost(p)$: the cost of path $p$
* $h(p)$ estimates the cost from the end of $p$ to a goal
* Let $f(p) = cost(p) + h(p)$; $f(p)$ estimates the **total path cost** of going from a start node to a goal via $p$
![[Pasted image 20250415125028.png]]
A* is a **mix** of **lowest-cost-first** and **best-first search**
* It treats the frontier as a **priority queue ordered by $f(p)$**
* It always selects the node on the frontier with the **lowest estimated distance** from the start to a goal node constrained to go via the node
#### Admissibility of A*
If there is a solution, A* always finds an **optimal solution** - the **first** to a goal selected - if
* The branching factor is **finite**
* Arc costs are **bounded above zero**
* $h(n)$ is a **lower bound** on the length of the shortest path from $n$ to a goal node
>[!important] Admissible heuristics never overestimate the cost to the goal
##### Proof
> [!tldr]- Why is A* with admissible h optimal?
> ![[Pasted image 20250415161520.png]]
#### Implementation
> [!tldr]- A* Implementation
> ![[Pasted image 20250415161630.png]]
#### Properties
**Space and Time Complexities**
* Both are exponential
**Completeness and Optimality**
* Yes and Yes
	* assuming the heuristic function is admissible, the branching factor is finite, and arc costs are bounded above zero
##### Optimally Efficient
Among all optimal algorithms that start from the same start node and use the same heuristic, A* expands the fewest nodes
* No algorithm with the same information can do better
* A* expands the minimum number of nodes to find the optimal solution
* Intuition for proof:
	* any algorithm that does not expand all nodes with $f(n) < cost(s,g)$ run the risk of missing the optimal solution
### Constructing an Admissible Heuristic
1. **Define a relaxed problem** by simplifying or removing constraints on the original problem
2. **Solve the relaxed problem** without search
3. The cost of the optimal solution to the relaxed problem is an **admissible heuristic** for the original problem
#### Desirable heuristic properties
* We want a heuristic to be admissible
	* A* is optimal
* We want a heuristic to have higher values
	* The close $h$ is to $h^*$, the more accurate $h$ is
* Prefer a heuristic that is very different for different states
	* $h$ should help us choose among different paths
	* If $h$ is close to constant, it’s not useful
#### Dominating Heuristic
>[!tldr] Definition
>Given heuristics $h_1(n)$ and $h_2(n)$, $h_2(n)$ dominates $h_1(n)$ if 
>* $\forall n(h_2(n)\geq h_1(n))$
>* $\exists n(h_2(n)>h_1(n))$

>[!important] Theorem
>If $h_2(n)$ dominates $h_1(n)$, $A^*$ using $h_2$ will never expand more nodes than $A^*$ using $h_1$
### Multiple-Path Pruning & Optimal Solutions
>[!faq] What if a subsequent path to $n$ is shorter than the first path to $n$?
>* **Remove** all paths from the frontier that use the longer path
>* **Change** the initial segment of the paths on the frontier to use the shorter path
>* **Ensure this doesn’t happen:** make sure that the shortest path to a node is found first
>	* lowest-cost-first-search

### Multiple-Path Pruning & A*
Suppose path $p$ to $n$ was selected, but there is a shorter path to $n$; and suppose this shorter path is via path $p’$ on the frontier. Suppose path $p’$ ends at node $n’$.
* $cost(p)+h(n)\leq cost(p’) + h(n’)$ because $p$ was selected before $p’$
* $cost(p’)+cost(n’, n) < cost(p)$ because the path to $n$ via $p’$ is shorter (by assumption)
$$cost(n',n)<cost(p) - cost(p') \leq h(n')-h(n)$$
You can ensure this doesn’t occur by letting $h(n’)-h(n) \leq cost(n’,n)$
### Monotone Restriction
Heuristic function $h$ satisfies the **monotone restriction** if $h(m)-h(n) \leq cost(m, n)$ for every arc $(m,n)$
* **Monotone** heuristic functions are also called **consistent**
* $h(m)-h(n)$ is the heuristic estimate of the path cost from $m$ to $n$
* The heuristic estimate of the path cost is **always less than** the actual cost
* If $h$ satisfies the monotone restriction, $A^*$ with multiple path pruning **always finds the shortest path** to a goal
#### Monotonicity and Admissibility
This is a strengthening of the admissibility criterion
* Monotonicity is like Admissibility but between **any two nodes**
	* Note: admissibility is between any node to goal
### Summary
![[Pasted image 20250415165350.png]]
## Adversarial Search
### Minimax
For **competitive, two-person, zero-sum** games
* Try to find the **best option** for you on nodes that you control (MAX nodes)
* Assumer competitor will take the **worst option** for you on nodes you do not control (MIN nodes)
* Recursively search to leaf nodes to find the **state evaluations**, and percolate values upward through the tree
#### Implementation
>[!tldr]- Minimax
>![[Pasted image 20250415165627.png]]

#### Minimax in larger games
Searching all the way to every leaf node is impossibly costly in larger games (e.g. chess)
* **Alpha-beta pruning** is a method that allows us to ignore portions of the search tree without losing optimality
	* It is useful in practical application, but does not change worst-case performance (exponential)
* We can also stop search early by evaluating **non-leaf** nodes via **heuristics**
	* Can no longer guarantee optimal play
	* Can set a fixed maximum depth for the search tree
### Higher Level Strategies
The following methods are not full algorithms per se, but can be  used to form a strategy for search at a higher level
#### Direction of Search
The definition of searching is **symmetric:**
* find path from start nodes to goal node or from goal node to start nodes
**Forward branching factor:**
* Number of arcs out of a node
**Backward branching factor:** 
* Number of arcs into a node
Search complexity is $b^n$, so we should use the direction where the branching factor is smaller
> [!caution] sometimes where graph is dynamically constructed, you may not be able to construct the backwards graph
#### Bidirectional Search
You can search backward from the goal and forward form the start **simultaneously**
* This wins as $2b^{k/2} << b^k$
	* This **can result** in an exponential saving in time and space
* The main problem is making sure the **frontiers meet**
* This is often used with one **breadth-first** method that builds a set of location that can lead to the goal
	* In the other direction another method can be used to find a path to these intersecting locations
#### Island Driven Search
**Idea:** find a set of **islands** between $s$ and $g$
$$s \rightarrow i_1 \rightarrow i_2 \rightarrow \cdots \rightarrow i_{m-1} \rightarrow g$$
There are $m$ **smaller problems** rather than 1 big problem
* This can win as $mb^{k/m} << b^k$
* The problem is to **identify the islands** that the path must pass through
	* It is **difficult to guarantee optimality**