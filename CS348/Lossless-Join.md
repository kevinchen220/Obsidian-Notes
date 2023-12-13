# Lossless-Join

> [!tldr] No loss of information in comparison to the original schema before decomposition

### Example
![[Pasted image 20231213115033.png]]![[Pasted image 20231213115036.png]]
```sql
-- Natural Join
select distinct Student, Assignment, Group, x.Mark as Mark
from SGM x, AM y
where x.Mark = y.Mark
```
![[Pasted image 20231213115348.png]]
##### **Spurious Tuples:** Computes extra tuples
Decomposition {$R_1, R_2$} of $R$ is a **lossless-join** if for any instance of $R$ the natural join of 
$R_1$ and $R_2$ has no spurious tuples

**Theorem:** Decomposition $\{R_1, R_2\}$ of $R$ is a **lossless-join** decomposition if and only if the common attributes of $R_1$ and $R_2$ form a [[Keys#Superkey|superkey]] for either schema
