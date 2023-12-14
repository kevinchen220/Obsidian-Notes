---
dg-publish: true
---
# Coarse-grained locking

> [!tldr] One [[Mutex|lock]] for entire data structure

> [!example] 
> ```c
> /* Coarse-grained Locking */
> mutex_t m;
> mutex_lock(&m); /* a single lock for the whole hash table */
> struct list_head *pos = hash_tbl[hash(key)];
> /* walk list and find entry */
> mutex_unlock(&m);
> ```

> [!NOTE] Makes most sense when data structure is not used often
> * Less locks → less space, less complexity

