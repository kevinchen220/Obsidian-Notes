---
dg-publish: true
---
# Relationship Sets
#### If general cardinality constraint (1, 1) for a component entity set E
→ Add following columns to table E:
1. [[Attributes]] of the relationship set
2. primary key attributes of remaining component [[entity sets]]
#### Otherwise make a new table $R$ for relationship $R$
1. attributes of the relationship set
2. primary key attributes of each component entity set
##### Primary key determined as follows
* General cardinality constraint (0,1) for component entity set E?
	* Use primary key attributes for E
* Otherwise choose primary key attributes of each component entity

![[Pasted image 20231212151755.png]]
**Constraints:**
* `foreign key ( HomeTeamName ) references Team`
* `foreign key ( VisitorTeamName ) references Team
* `foreign key ( LocName ) references Location