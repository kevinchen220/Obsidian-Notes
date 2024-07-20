---
dg-publish: true
---
# Dynamic Programming
Sometimes when trying [[divide and conquer]] approach, we are only able to divide in a way which makes us perform “exhaustive search”
* Bad divide and conquer

However, in several situations, it turns out that a *small set* of particular subproblems appear *several times* in our recurrence 

Instead of recomputing the subproblems, we can:
1. Solve them once
2. Save them to memory
3. If we need them again, we already precomputed them
#### DP template
1. Identify small set of subproblems
2. Devise proper recursion
3. Show bottom-up approach correctly compute the subproblems