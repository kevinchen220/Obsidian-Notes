---
dg-publish: true
---
# Third Normal Form
Schema $R$ is in **3NF** with respect to a set of functional dependencies $F$ if and only if whenever $(X→Y)\in F^+) and $XY\subseteq R$ then one of the following holds:
1. $X→Y$ is trivial
2. $X$ is a [[Keys#superkey|superkey]] of $R$
3. Each attribute of $Y-X$ is contained in a candidate key of $R$

Database schema $\langle p=\{R_1, …, R_n\}, F\rangle$ is in **3NF** if each relation schema $R_i$ is in 3NF with respect to $F$

> [!NOTE] [[Boyce-Codd Normal Form|BCNF]] implies 3NF
> $R = \{A, B, C\}$ is in 3NF with respect to $F = \{AB→ C, C→B\}$

> [!tip] [[Lossless-Join]] and [[Dependency Preserving]] decomposition into 3NF relation schemata always exists

#### Compute 3NF Decomposition
Assume $R$ is a set of attributes and $F$ a set of FDs over $R$
* We will need the [[minimal cover]]
```
function Compute3NF(R, F)
begin
    Result := ∅;
    G := minimal cover for F;
    for each (X -> Y) ∈ G do
        Result := Result ∪ {XY};
    if there is no Ri ∈ Result such that
        Ri contains a candidate key for R then begin
            compute a candidate key K for R;
            Result := Result ∪ {K};
    end;
    return Result;
end
```
1. Add all FDs in minimal cover as decompositions
2. Then add a candidate key decomposition if there doesn’t exists one

##### Correctness Theorem
Compute3NF($R,F$) returns a lossless-join decomposition of $R$ that is also dependency preserving and for which each table in the decomposition is in 3NF with respect to $F$


