---
dg-publish: true
---
# Greedy
## Greedy Strategy based on the following principles
1. choose a “progress measure”
2. preprocess input accordingly
3. make next decision based on what is **best** given *current* partial solution
4. **Main idea**: Must show greedy is always *no worse* than any other optimal solution
	* Usually can prove this by being able to transform any optimal solution into the greedy one without losing anything
#### Optimal Substructure
A problem has optimal substructure if any optimal solution contains optimal solutions to the subproblem