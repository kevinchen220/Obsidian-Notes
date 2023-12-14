---
dg-publish: true
---
# Relational Algebra

> [!info] Consists of a set of operations on the universe $U$ of finite relations over an underlying universe of values D of a database instance DB

### $(U; R_0, ..., R_k, \times, \sigma, \pi, \bigcup, -, elim, c_1, c_2, ...)$
* Constants
	* $R_i$ - Relation name
		* One for each relation name in a signature $p$
	* $c_i$ - Constant
		* One for each constant in $D$ 
* Unary Operations
	* $\sigma$ - Selection
		* Removes rows
	* $\pi$ - Duplicate preserving projection
		* Removes columns
	* elim - Duplicate elimination
* Binary Operations
	* $\times$ - Cross product
	* $\cup$ - Multiset union
	* $-$ - Multiset difference

## [[Query]]
## [[Semantics]]
## [[Expressiveness]]
## [[Implementation]]
## [[Relation Names]]