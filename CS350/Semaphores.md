---
dg-publish: true
---
# Semaphores
> [!tldr] Lock with multiple states

## init
```c
int sem_init(sem_t *s, ..., unsigned int n);
```
* Initialize a semaphore with `n`
## wait
```c
sem_wait(sem_t *s);
```
* **If semaphore value `n` is greater than 0, decrement it**
* Otherwise, wait until `n > 0`, then decrement it
## signal
```c
sem_signal(sem_t *s);
```
* Increment `n` by 1

## Implementation
### wait
```c
Semaphore_Wait(Semaphore *sem) {
  Spinlock_Lock(&sem->sem_lock);
  while (sem->sem_count == 0) {
    /* Locking the wchan prevents a race on sleep */
    WaitChannel_Lock(sem->sem_wchan);
    /* Release spinlock before sleeping */
    Spinlock_Unlock(&sem->sem_lock);
    /* Wait channel protected by it’s own lock */
    WaitChannel_Sleep(sem->sem_wchan);
    /* Recheck condition, no locks held */
    Spinlock_Lock(&sem->sem_lock);
  }
  sem->sem_count--;
  Spinlock_Unlock(&sem->sem_lock);
}
```
### signal
```c
Semaphore_Post(Semaphore *sem) {
  Spinlock_Lock(&sem->sem_lock);
  sem->sem_count++;
  WaitChannel_Wake(sem->sem_wchan);
  Spinlock_Unlock(&sem->sem_lock);
}
```
