# Relation Names
### Indexing
#### Standard Physical Design
Defines the following for each relation name $R$
1. Primary index for $R$ materializing its extension as a concrete data structure
2. Zero or more secondary indices for $R$ materializing projections of the primary index for $R$ as concrete data structures

→ Materialization of a relation adds an additional **record identifier (RID)** attribute to the relation
→ Secondary Indices usually include the RID attribute of the primary index in their projection of $R$

#### Index Scan $\sigma_{\varphi}(\langle index\rangle)$
* $\varphi$ - Condition supplies search values for the underlying data structure

Assuming $k$ = Cnum($\langle$index$\rangle$) and $\varphi$ is the condition $\#i = c$ then an index scan is equivalent to $\pi_{\#1,...,\#k}(\sigma_{\#i=\#k+1}(\langle index \rangle \times c))$

#### Primary Indices
Btree index PROF-PRIMARY on pnum
![[Pasted image 20231213194851.png]]
#### Secondary Indices
Btree index PROF-SECONDARY on lname
![[Pasted image 20231213194923.png]]