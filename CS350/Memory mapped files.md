
> [!tldr] Memory objects can exist between heap and stack using `mmap` [[System Calls|system call]]

![[Pasted image 20231209182652.png]]
```c
void *mmap(void *addr, size_t len, int prot, int flags, int fd, off_t offset);
```
* Treat a file as if it were memory
* Map the file specified by `fd` to the virtual address `adr` 
	* Changes are backed up to the file
* `prot`
	* specifies the protection of region
* `flags`
	* `MAP_SHARED`
		* Modifications seen by everyone
	* `MAP_PRIVATE`
		* Modifications are private
	* `MAP_ANON`
		* Anonymous memory