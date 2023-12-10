# Fine-grained locking

> [!tldr] Create a [[Mutex|lock]] for each entry of a datastructure

> [!example] 
> ```c
> /* Fine-grained Locking */
> mutex_t bucket[1024]; /* a separate lock for each linked list */
> int index = hash(key);
> mutex_lock(&bucket[index]);
> struct list_head *pos = hash_tbl[index];
> /* walk list and find entry */
> mutex_unlock(&bucket[index]);
> ```

> [!NOTE] Use when data structure is used often
> * maximizing concurrency and performance

See also [[Coarse-grained locking]]