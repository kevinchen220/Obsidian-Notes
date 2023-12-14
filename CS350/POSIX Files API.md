---
dg-publish: true
---
# POSIX Files API
## POSIX functions for working with files include
* `open`
	* returns a **file descriptor**
		* used to identify files
		* passed to other functions
* `read`
	* copies data from file to process’s [[Address Space]]
* `write`
	* copies data from process’s [[Address Space]] into a file
* `lseek`
	* specifies where to point at in the file
	* non-sequential reading and writing
* `close`
	* invalidates a **file descriptor**
[[OS Kernel]] tracks which file descriptors are valid for which process

> [!tip] Standard file descriptors open by default
> * 0 for stdin
> * 1 for stdout
> * 2 for stderr

`stdio` library in C works on top of these functions
* `fopen`, `fscanf`, …

## Manipulating File Descriptors
### dup2
```c
int dup2(int oldfd, int newfd);
```
- ### Makes `newfd` an exact copy of `oldfd`
* Closes what was originally in `newfd` if it was a valid FD
* Both will share same offset
	* `lseek` affects both
> [!example]
> ```C
> fd = open(infile, O_RDONLY);
> dup2(fd,0);
> ```
> the `infile` is opened and is set to `stdin`
> * reading from `stdin` now reads from `infile`
### fcntl (file control)
```C
int fcntl(int fd, F_SETFD, int val);
```
* ### Sets the `close-on-exec` flag
	* if `val=1`, `execvp` will **close** the file **FD**
	* if `val=0`, `execvp` will **leave open** the file **FD**
	* if `execvp` was unsuccessful, **FD** is left open
### Pipes
```C
int pipe(int fds[2]);
```
* ### Returns two file descriptors in `fds[0]` and `fds[1]`
* Output of `fds[1]` becomes input of `fds[0]`
	* `fds[1] | fds[0]`

> [!example]-
> ```c
> 1 void doexec (void) {
> 2   while (outcmd) {
> 3   int pipefds[2]; pipe(pipefds);
> 4   switch (fork()) {
> 5     case -1: // error
> 6       perror("fork"); exit(1);
> 7     case 0: // child writes to the pipe
> 8       dup2(pipefds[1], 1); //stdout is pipe input
> 9       close(pipefds[0]); close(pipefds[1]);
> 10     outcmd = NULL;
> 11     break;
> 12   default: // parent reads from the pipe
> 13     dup2(pipefds[0], 0); // stdin is pipe output
> 14     close(pipefds[0]); close(pipefds[1]);
> 15     parse_input(&av, &outcmd, outcmd);
> 16     break;
> 17   }
> 18 }
> ```
