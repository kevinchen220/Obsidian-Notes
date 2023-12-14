---
dg-publish: true
---
# Semantics

> [!info] Semantics of Eval($E$, DB) is given by appeal to range restricted relational calculus with multiset semantics

Answers($Q$, DB) - denotes the answers to RC query $Q$ over DB
1. $S_i$ is a table with arity Cnum($E_i$) and extension Eval($E_i$, DB)
2. $\bar{x}=x_1, …, x_n$ 

For $R_i/n \in \rho$
1. **Relation name:** Eval($R_i$, DB) = Answers$(\{(\bar{x})|R_i(\bar{x})\}, DB)$ where Cnum($R_i$) = $n$
2. **Constant:** Eval($c$) = Answers($\{(x)|x=c\}$, DB) where Cnum($R_i$) = 1
3. **Selection:** Eval($\sigma_{\#i=\#j}(E_1)$, DB) = Answers($\{(\bar{x})|S_1(\bar{x})\land (x_i=x_j)\}$, DB) where Cnum($\sigma_{\#i=\#j}(E_1)$) = Cnum($E_1$)
4. **Projection:** Eval($\pi_{\#i_1, ..., \#i_m}(E_1)$) = Answers($\{(x_{i_1},…,x_{i_m})|\exists x_{i_{m+1}},…, x_{i_n}\}$, DB) where Cnum($\pi_{\#i_1, ..., \#i_m}(E_1)$) = m
5. **Duplicate elimination:** Eval(elim $E_1$, DB) = Answers($\{(\bar{x})$|elim $S_1(\bar{x}) \}$, DB) where Cnum(elim $E_1$) = Cnum($E_1$)
6. **Cross product:** Eval($E_1 \times E_2$, DB) = Answers($\{(\bar{x}, \bar{y})|S_1(\bar{x})\land S_2(\bar{y})\}, DB$) where Cnum($E_1 \times E_2$) = Cnum($E_1$) + Cnum($E_2$)
7. **Multiset Union:** Eval($E_1 \cup E_2$, DB) = Answers($\{(\bar{x})|S_1(\bar{x}) \lor S_2(\bar{x})\}$, DB) where Cnum($E_1 \cup E_2$) = Cnum($E_1$)
8. **Multiset Difference: (Except all)** Eval ($E_1 - E_2$, DB) = Answers($\{(\bar{x})|S_1(\bar{x}) \land \neg S_2(\bar{x}) \}$, DB) where Cnum(E_1 - E_2) = Cnum($E_1$)
9. **Multiset Difference: (Alternative not exists)** Eval ($E_1 - E_2$, DB) = Answers($\{(\bar{x})|S_1(\bar{x}) \land \neg (S_1(\bar{x}) \land  S_2(\bar{x})) \}$, DB) where Cnum(E_1 - E_2) = Cnum($E_1$)


> [!tip] Multiset difference with alternative semantics can be used when translating subqueries in SQL conditions


