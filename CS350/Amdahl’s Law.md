# Amdahl’s Law
> [!tldr] Efficiency gains when using multiple cores
> $$T(n) = T(1)(B+\frac{1}{n}(1-B))$$
> * $T(1)$: the time one core takes to complete the task
> * $B$: fraction of the job that must be serial
> * $n$: number of cores

 Suppose $n$ were infinity!
 * unlimited limit on parallel speedup

> [!warning] Synchronization increases the serial section size

