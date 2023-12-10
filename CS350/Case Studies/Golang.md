### Go routines

> [!tldr] Very light-weight [[User Thread|user-level threads]]
> * 100KiB go routines vs. 2MiB OS thread
> * stack starts small and grows as needed
> * [[Context Switch]] is a function call rather than a [[System Calls|system call]]

* Go routines run on top of [[POSIX Threads API#Approach 3 User threads on kernel threads (n m)|kernel threads]]
	* One [[Kernel Thread]] per processor core
* Every logical core is owned by a [[Kernel Thread]] when running
* Convert blocking system calls
	* convert to non-blocking by yielding the core
	* poll using kernel event API `poll`, `epoll`, `kqueue` to check whether an event has happened

### Go channels

> [!example]
> ```go
> func worker(done chan bool) {
>   // Notify the main routine
>   done <- true
> }
> 
> func main() {
>   // Create a channel to notify us
>   done := make(chan bool, 1)
>   // Create go routine
>   go worker(done)
>   // Block until we receive a message
>   next() // <- start executing here when worker is done done
> }
> ```

