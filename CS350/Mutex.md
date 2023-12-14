---
dg-publish: true
---
# Mutex
> [!tldr] If mutexes used correctly, should be indistinguishable from [[Sequential Consistency]]

## All global data should be protected by a mutex!
* Accessed by more than one thread
* At least one write
* Don’t need to lock during initialization

> [!NOTE] Mutexes busy wait
> Constantly trying to acquire mutex
> * inefficient

## [[PThead Mutex API]]
