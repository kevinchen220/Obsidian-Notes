---
dg-publish: true
---
# MCS Lock
> [!tldr] Improved [[Spinlock]]
> * Less traffic
> * More fair

## Structure
```C
typedef struct qnode {
	struct qnode *next;
	bool locked;
} qnode;
```
Each processor has a `qnode` structure in local memory
* `next` can point to another `qnode` not in local memory
**While waiting, spin on local `locked` flag**

## The lock
```C
typedef qnode *lock;
```
Point to a list of processors holding or waiting to hold the MSC lock
* When `lock` is null, then it is available
* When a thread tries to acquire a lock, it will ad itself to the list

## Implementation
### MCS Acquire
```C
1 acquire(lock *L, qnode *I) {
2   I->next = NULL;
3   qnode *predecessor = I;
4   XCHG(predecessor, *L); /* atomic swap */
5   if (predecessor != NULL) {
6     I->locked = true;
7     predecessor->next = I;
8     while (I->locked)
9     /* spin */;
10   }
11 }
```
### MCS Release
```c
1. release(lock *L, qnode *I) {
2.   if (!I->next)
3.     if (CAS(*L, I, NULL)) /* atomic compare-and-swap */
4.     return;
5.   while (!I->next)
6.     /* spin */;
7.  I->next->locked = false;
8. }
```
