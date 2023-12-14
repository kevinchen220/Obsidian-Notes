---
dg-publish: true
---
# Boyce-Codd Normal Form
Schema $R$ is in **BCNF** with respect to a set of [[functional dependencies]] $F$ if and only if whenever $(X→Y)\in F^+$ where $XY \subseteq R$ then at least one of the following hold:
1. $X→Y$ is trivial ($Y\in X$)
2. $X$ is a [[Keys#superkey|superkey]] of $R$

Database schema $\langle p=\{R_1, …, R_n\}, F\rangle$ is in **BCNF** if each relation schema $R_i$ is in BCNF with respect to $F$

## Algorithm
```
function computeBCNF(R, F)
begin
    Result := {R};
    while some Ri ∈ Result and (X -> Y) ∈ F+
            violate the BCNF condition do begin
        Replace Ri by Ri - (Y - X);
        Add X ∪ Y to Result;
    end;
    return Result;
end
```

#### Correctness Theorem for ComputeBCNF
Function `ComputeBCNF(R,F)` returns a [[lossless-join]] decomposition of $R$ for which each table in the decomposition is in BCNF with respect to $F$


> [!tip] Computing lossless-join BCNF decomposition
> **No efficient procedure exists**
> * Results depend on sequence of FDs used to decompose relations
> * It is possible no lossless join [[dependency preserving]] BCNF decomposition exists
> 
> Consider $R=\{A,B,C\}$ and $F=\{AB→C, C→B\}$
> * $R$ is not in BCNF with respect to $F$
> * $AB→C$ will be an inter-relational FD in any decomposition of $R$


