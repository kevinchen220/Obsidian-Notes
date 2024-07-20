---
dg-publish: true
---
# Divide and Conquer
## Structure of Divide and Conquer
#### Divide
* Given instance $I$, construct smaller instances $I_1, …, I_a$ (subproblems)
	* Ideally want $|I_j|$ small compared to $|I|$.
#### Conquer
* Recursively solve instances $I_1, … I_a$ obtaining solutions $S_1, …, S_a$
#### Combine
* Solutions $S_1, …, S_a$ → solution $S$ to instance $I$
### Recursion for running time
$$T(I) = T(I_1) + \cdots + T(I_a) + \text{time to combine}$$
