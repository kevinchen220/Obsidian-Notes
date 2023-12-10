# Performance of File Systems
### FS is dominated by number of FS accesses
* A lotttt slower than most computer operations

> [!tip] Transfer time is only a small part of the total access time
> access time = **seek time** + **rotational delay** + transfer time
> * 1 sector = 5ms + 4ms + 5$\mu$s = 9ms
> * 50 sectors = 5ms + 4ms + .25ms = 9.25ms
> 
> Can get 50x more data for only 3% overhead


