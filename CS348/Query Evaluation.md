---
dg-publish: true
tags:
  - cs348
  - unit
---
# Query Evaluation
## Overview
1. Parsing, view expansion, and type and authorization checking of $Q$
2. Translation of $Q$ to a formulation $E_Q$ in [[relational algebra]]
3. Optimization of $E_Q$
	1. Generates an efficient query plan $P_Q$ from $E_Q$
	2. Uses statistical metadata about the database instance
4. Execution of query plan $P_Q$ 
	1. Uses access methods to access stored relations
	2. Uses physical relational operators to combine relations

##### Considerations
* How relations are stored and physically represented
* Choice of physical relational operators to answer complex queries
* How intermediate results are managed

#### [[Two-Tier Architecture]]

## [[Relational Algebra]]

## [[Query Optimization]]
## [[Cost Estimation]]
