# PThead Mutex API
```c
// Init
int pthread_mutex_init(pthread_mutex_t *m, pthread_mutexattr_t attr);
// Destroy
int pthread_mutex_destroy(pthread_mutex_t *m);
// Acquire mutex
int pthread_mutex_lock(pthread_mutex_t *m);
// Attempt to acquire, 0 if successfull, otherwise -1
int pthread_mutex_trylock(pthread_mutex_t *m);
// Release a mutex
int pthread_mutex_unlock(pthread_mutex_t *m);
```
