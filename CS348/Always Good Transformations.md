---
dg-publish: true
---
# Always Good Transformations
#### Push selections:
$\sigma_{\varphi}(E_1 \bowtie_{\theta}E_2) = \sigma_{\varphi}(E_1) \bowtie_{\theta}E_2$
* for $\varphi$ involving columns of $E_1$ only
#### Push projections:
$\pi_{V}(E_1 \bowtie_{\theta}E_2) = \pi_{V}(\pi_{V_1}(E_1) \bowtie_{\theta}\pi_{V_2}(E_2))$
* where $V_1$ is the set of all columns of $R$ involved in $\theta$ and $V$ 
* Similarly for $V_2$
#### Replace products by joins:
$\sigma_{\varphi}(R \times S) = R \bowtie_{\theta}S$

**These rewrites also reduce the space of plans to search**
