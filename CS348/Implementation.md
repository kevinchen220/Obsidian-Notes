---
dg-publish: true
---
# Implementation

> [!info] Multiset semantics of RA enables implementations of its operators

Implementation for an RA operator provides a **cursor for OPEN/FETCH/CLOSE** interface
1. Implements the cursor interface to produce answers
2. Uses the same interface to get answers from its children

Providing at least one physical implementation for this protocol for each operator enables evaluating RA queries

#### Example implementation of selection
```c
// select_{#i=#j}(Child)
    OPERATOR child;
    int i,j;

public:
    OPERATOR selection(OPERATOR c, int i0, int j0)
                { child = c; i = i0; j = j0; };
    void open () { child.open(); };
    tuple fetch() { tuple t = child.fetch();
                      if (t==NULL || t.attr(i) = t.attr(j))
                          return tu;
                      return this.fetch();
                  };
    void close() { child.close(); }
// fully pipelined since it requires a constant space overhead 
```
* **Constant:**
	* First fetch returns the constant
	* Next fetch fails
* **Cross product:**
	* Simple nested loops algorithm
* **Duplicate preserving projection:**
	* Eliminate unwanted attributes from each tuple
* **Multiset union:**
	* Simple concatenation
* **Multiset difference (alternative semantics):**
	* Nested loops algorithm that checks for a tuple in the inner loop 
* **Relation name:**
	* Simple file scan of the primary index for the relation
* **Duplication elimination:**
	* Remember tuples that have  been returned


> [!tip] Plans are inefficient and efficiency can be improved
> * Use concrete (disk based) data structures for efficient searching
> 	* Choose a [[B Trees]] for the primary index
> * Use better algorithms to implement the operators based on SORTING or HASHING
> * Rewrite the RA expression to an equivalent expression enabling a more efficient implementation
> 	* Remove unnecessary operations such as duplicate elimination
> 	* Apply always good transformations
> 	* Perform cost-based join order selection
> 	* Introduce STORE operations using memory to factor computation of common subexpressions
