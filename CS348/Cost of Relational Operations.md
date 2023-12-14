---
dg-publish: true
---
# Cost of Relational Operations
**Selection:** cost($\sigma_{\varphi}(E)$) = (1 + $\epsilon_{\varphi}$)cost($E$)
**Nested loop join:** cost($R\times S$) = cost($R$) + ($|R|/b$)cost($S$)
**Nested index join:** cost($R\times \sigma_{\varphi}(S)$) = cost($R$) + $d_s + |R|$
* Btree depth $d_s$
**Soft-merge join:** cost($R\bowtie_{\varphi}S$) = cost(sort($R$)) + cost(sort($S$))
* cost(sort($E$)) = cost($E$) + $(|E|/b)\log (|E|/b)$
