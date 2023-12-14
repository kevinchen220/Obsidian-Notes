---
dg-publish: true
---
# Physical Database Design
## Materialized Views
```sql
CREATE VIEW <name> [AS] (<query>)
MATERIALIZED [AS <data_structure>]
```

**Example:** PNUM/(pnum, lname, dept)
1. Btree primary index on `pnum` called `PROF-PRIMARY` 
```sql
create view PROF-PRIMARY as (select * from PROF)
materialized as BTREE with search key (pnum)
```
2. Btree secondary index `lname` called `PROF-SECONDARY`
```sql
create view PROF-SECONDARY
as (select lname, rid from PROF-PRIMARY)
materialized as BTREE with search key (lname)
```

### Data Structure
`<data_structure>`
* ISAM or VSAM file
* Unsorted heap file
* Hash file
* R trees
* Array

> [!info] Workloads exist and are common that favour any of these
> * Navigational applications and R trees
> * OLAP workloads, main memory arrays, and heap files

> [!info] Records encoding tuples in an index can also be co-clustered with records encoding tuples for another index

### [[Co-Clustering Indices]]
### [[Beyond Standard Physical Design]]
### Query Optimizations
see also [[Query Optimization]] for [[Relational Algebra]]
##### View Based Query Rewriting Problem
Given a query $Q$ and a physical database design consisting of a set of arbitrary materialized views $\{V_1, … V_n\}$, find the most efficient query plan $P$ equivalent to $Q$ that uses only views $V_i$

**Theorem:** View based query rewriting is undecidable
* Even when $Q$ and each $V_i$ is a conjunctive query and any plan $P$ equivalent to $Q$ is acceptable
#### Query Plan Tools
Tool to enable one to investigate what plan is chose for a query and what the estimated cost is
* DB2 `db2expln` and `dynexpln`
**Example:** Invoking tools on bibliography query
```sql
select name from author, wrote where aid = author
```
![[Pasted image 20231214111938.png]]
#### Index Advising Tools
Tool to advise on a standard physical design given a workload description
* DB2 `db2advis`

![[Pasted image 20231214112025.png]]

## Guidelines
* Don’t index unless the performance increase outweighs the update overhead
* Attributes mentioned in WHERE clauses are candidates for each index search keys
* Multi-attribute search keys should be considered when
	* A WHERE clause contains several conditions
	* It enables index-only plans
* Choose indexes that benefit as many queries as possible
* Each relation can have at most one primary index so it should be chosen wisely
	* Target important queries that would benefit the most
		* Range queries benefit the most from clustering
		* Join queries benefit the most from [[co-clustering indices|co-clustering]]
	* [[Co-Clustering Indices#Multi-attribute Search Keys|multi-attribute index]] that enabled an index-only plan does not benefit from being clustered
