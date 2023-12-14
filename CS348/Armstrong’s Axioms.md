---
dg-publish: true
---
# Armstrong’s Axioms

> [!tldr] Infer [[functional dependencies]] from other functional dependencies

> [!NOTE] 
> **Sound**: Anything derived from $F$ is in $F^+$
> **Complete**: Anything in $F^+$ can be derived

1. **Reflexivity**: If $Y \subseteq X$ holds then $X→Y$ holds
2. **Augmentation**: If $X→Y$ holds then $XZ→YZ$ holds
3. **Transitivity**: If $X→Y$ and $Y→Z$ holds then $X→Z$ holds

### Additional rules
4. **Union**: If $X→Y$ and $X→Z$ holds then $X→YZ$ holds
5. **Decomposition**: If $X→YZ$ holds then $X→Y$ holds

