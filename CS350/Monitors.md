---
dg-publish: true
---
# Monitors
> [!tldr] Class where only one procedure runs at a time

Possibly less error prone than [[Mutex]], but also less flexible
```c
monitor monitor-name {
	// Shared varaible declarations

	procedure P1(...) {...}
	...
	procedure Pn(...) {...}

	Initialization code(...) {...}
}
```


> [!NOTE] Implementation
> ![[Pasted image 20231207222052.png]]
> - Queue of threads waiting to get in
> 	- Might be protected by [[Spinlock]]
> - Queues insides are associated with conditions
> 	- implements CV
