### Creating processes

#### fork
```c
// Returns new Process ID in parent
// Returns 0 in child
int fork(void);
```
* #### Create a process that is an exact copy of the current one
* Called once returned twice
> [!question] Why `fork`?
> * Most calls to `fork` are followed by `execve`
> 	* could combine into one `spawn` [[System Calls|system call]]
> 	* ==load and execute new child process==
> * Occasionally useful to fork one process
> 	* For webservers, parallelism
> 	* Create one process per core
> * **Simplicity**
> 	* no arguments needed

#### waitpid
```C
int waitpid(int pid, int *status, int options);
```
* #### Attempt to get exit status of child
* `pid`: process ID of child
* `status`: will contain exit value or signal if crashed
* `options`: 
	* 0 -> wait for child to terminate
	* WNOHANG -> do not wait for terminate
* Returns process ID or -1 on error

### Deleting Processes
#### exit
```c
void exit(int status);
```
* #### have the current process exit
* `status`: shows up in encoded format if [[#Creating processes#waitpid|waitpid]] is called
* status of 0 is success, non-zero is error

#### Kill
```c
int kill(int pid, int sig);
```
* #### Sends signal `sig` to `pid`

> [!faq] A signal is a software [[Interrupts|interrupt]]
> * **SIGTERM** is most common
> 	* kills process by default
> 	* applications can catch to do clean up
> * **SIGKILL** is stronger
> 	* kill process always

### Running Programs
#### execve
```c
int execve (char *prog, char **argv, char **envp)
```
* #### Replaces the current running program with a new one `prog`
* `prog`: full pathname of the program to run
* `argv`: argument vector that is passed to `main` of `prog`
* `envp`: environment variables

> [!tip] Execve is usually called through wrapper functions
> ```c
> int execvp(char *prog, char **argv);
> ```
> * searches `PATH` for `prog`
> * then runs execve
> ```c
> int execlp(char *prog, char *arg, …);
> ```
> * `lp` stands for list parameters
> * list arguments one at a time
> 	* end with `NULL`
