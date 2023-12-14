---
dg-publish: true
---
# Join Order Selection
Joins are associative so $R\bowtie S \bowtie T \bowtie U$ are equivalent to
1. $((R\bowtie S) \bowtie T) \bowtie U$
2. $(R\bowtie S) \bowtie (T \bowtie U)$
3. $R\bowtie (S \bowtie (T \bowtie U))$

→ Try to minimize the intermediate result
Need to decide which of the subexpressions is evaluated first
* Try to join with filtered one first

> [!warning] Cost of nested loop join is not symmetric
