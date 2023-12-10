# Sequential Consistency

> [!tldr] Result of the execution is as if all operations were executed in some order
> Operations of each processor occured in the order of the prgram

## Two requirements
1. Maintaining **program order** on individual processors
2. Ensuring **write atomicity**
	* If any processor reads the result of the write, all subsequent reads will be the same

## Limitations
### Hardware optimizations
* Complicates write buffers
* Can’t reorder overlapping write operations
* Complicates non-blocking reads
	* Cannot prefetch data
* Makes [[Cache Coherence]] more expensive
	* Must delay write completion until invalidation and update of old write
### Compiler optimizations
* **Code motion**
	* Moving code around to improve performance
	* e.g. load-use hazard
* **Loop blocking**
	* Rearrange loops for better cache performance
		* keep inner loop completely in cache
* **Software pipelining**
	* Move instructions across iterations of a loop

> [!example] 
> ```c
> for (i = 0; i<N; i += 2) {
>   f(i);
>   f(i+1);
>   g(i);
>   g(i+1);
}
> ```
