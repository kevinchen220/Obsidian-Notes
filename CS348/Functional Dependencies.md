# Functional Dependencies
Let $R$ be a $k$-ary relation $R/(A_1, … , A_k)$ where $l(i) = A_i, 1 \leq i \leq k$ and let $X, Y$ be subsets of $\{A_1, … , A_k\}$
A **functional dependency** over the [[attributes]] of $R$ is $X \rightarrow Y$, $Y$ depends on $X$
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
#### Algorithm
Assume $R$ is a set of attributes, $X$ a subset of $R$, and $F$ a set of FDs over $R$
```
function ComputeX+(X, F)
begin
    X+ := X;
    while true do
        if there exists (Y -> Z) ∈ F such that
            1. Y ⊆ X+
            2. Z ⊈ X+
        then X+ := X+ ∪ Z
        else exit;
    return X+;
end
```
**Correctness Theorem:** $(X→Y)\in F^+$ if and only if $Y \subseteq ComputeX^+(X,F)$
## [[Armstrong’s Axioms]]

## [[Keys]]
**Superkey theorem for functional dependencies:** 
$X$ is a superkey of a relation with schema $R$ if and only if $R \subseteq ComputeX^+(X,F)$
