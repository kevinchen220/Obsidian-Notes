# Functional Dependencies
Let $R$ be a $k$-ary relation $R/(A_1, … , A_k)$ where $l(i) = A_i, 1 \leq i \leq k$ and let $X, Y$ be subsets of $\{A_1, … , A_k\}$
A **functional dependency** over the attributes of $R$ is $X \rightarrow Y$, $Y$ depends on $X$
* We say that set of attributes **X** functionally determines the set of attributes **Y** in $R$
* Usually forms a relation schema with its set of attributes

> [!example]
> ![[Pasted image 20231212123130.png]]
> Employee SIN numbers functionally determine employee names
> * SIN → EName
> 
> Project numbers functionally determines project names and locations
> * PNum → PName, PLoc
> 
> Project locations and the number of hours functionally determine allowances
> * PLoc, Hours → Allowance

> [!question] What functional dependencies should hold as a consequence of the primary key of EmpProj?
> **SIN, PNum → SIN, PNum, Hours, EName, PName, PLoc, Allowance**

## [[Logical Consequence]]





