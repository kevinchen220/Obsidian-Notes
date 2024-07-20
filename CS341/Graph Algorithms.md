---
dg-publish: true
---
# Graph Algorithms
### Undirected Graphs
[[BFS]]
* Finds shortest path
* Can be used to detect graph is bipartite
* Shortest paths encoded int he BFS tree
* Non-tree edges in adjacent layers
[[DFS]]
* Parenthesis lemma:
	* Start and finish time intervals are either disjoint, or one contains the other
* Non-tree edges in DFS tree must be back edges
* Checks for cut vertices or cut edges
### Directed Graphs
* BFS still gives shortest paths from source
* BFS and DFS trees have less structure
	* Parenthesis lemma still holds for DFS tree
* Directed Acyclic Graphs
	* [[Topological sort]]
* Any directed graphs is a DAG of strongly connected components
* Linear time algorithm to find all SCCs!
### Minimum Spanning Trees
[[Greedy]] for the rescue!
* [[Boruvka’s Algorithm]]
	1. Pick cheapest edge from a vertex, and contract it
	2. Recurse on contracted graph
* Cut property:
	* Given any cut $(S, \bar{S})$, there is an MST containing edge with smallest weight across cut
* [[Prim’s Algorithm]]
	1. Start from a arbitrary vertex and grow connected component one vertex at a time
* [[Kruskal’s Algorithm]]
	1. Consider edges from cheapest to most expensive, add edge to solution so long as it does not create a cycle
	2. needs UNION-FIND for that last step
All of the above can be assumed to run in $O(m \log n)$ time
### Shortest Paths
* **Single-source, all weights non-negative**: [[Dijkstra’s Algorithm]]
	* Start from source, and build shortest paths by adding one vertex at a time
	* Runtime $O((m+n) \log n)$
* **Single-source, arbitrary weights**: [[Bellman-Ford Algorithm]]
	* Cannot do greedy because of negative weights
	* [[Dynamic Programming|DP]] to the rescue
	* Subproblems $D[v,i] := $ captures shortest $s$ → $v$ distance using at most $i$ edges
	* Runtime $O(mn)$
* **All-pars shortest-paths, (arbitrary weights, no negative cycles)**: [[Floyd-Warshall Algorithm]]
	* Subproblems: $D[u,v,k] :=$ shortest $u$ → $v$ path using only $\{1, .. , k\}$ as intermediate vertices
	* Runtime $O(n^3)$
### Max-Flow & Min-Cut
Let $G(V, E, C)$ be an undirected graph, with capacity (weight) function $C: E → R_{\geq 0}$ two special vertices $s,t\in V$
* **Flows**: $f: E→ R_{\geq 0}$ satisfying:
	1. Capacity: $f(e) \leq c(e)$ for all $e \in E$
	2. Conservation: $f_{in}(u) = f_{out}(u)$ for all $u \in V \backslash \{s,t\}$
	3. Value: $f_{out}(s) - f_{in}(s)$
* **Flow decomposition theorem**
	* Any integral flow $f: E→ N$ of value $r$ can be decomposed into paths $P_1, …, P_r$ cand cycles $C_1, …, C_m$ such that each $e \in E$ appears in exactly $f(e)$ of the paths and cycles
* **Cuts**
	* A cut is a partition of the vertices into two sets $(S, V \backslash S)$
		* Capacity of a cut: $C_{out}(S)$ is the total capacity *coming out* of $S$
* **Max-Flow Min-Cut Theorem**
	* The value of the maximum flow equals the minimum capacity of a cut
* **Ford-Fulkerson**
	* Keep finding $s$→$t$ paths in [[residual graph]], when there is none, found a max-flow and a min-cut
