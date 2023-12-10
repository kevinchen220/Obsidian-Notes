> [!tldr] Manages a list of sleeping threads
> Used by [[Mutex]], [[Semaphores]], [[Condition Variables]]
### lock
```c
void WaitChannel_Lock(WaitChannel *wc);
```
* Lock waitchannel for sleep and wake operations
### sleep
```c
void WaitChannel_Sleep(WaitChanne; *wc);
```
* Puts calling thread to sleep
* Causes [[Context Switch]]
### wake
```c
void WaitChannel_Wake(WaitChannel *wc);
```
* Unblocks one thread sleeping on the wait channel
### wakeall
```c
void WaitChannel_WakeAll(WaitChannel *wc);
```
* Unblocks all threads sleeping on the wait channel

