# PThread CV API
```C
// Init with specific attributes
int pthread_cond_init(pthread_cond_t *c, ...);
// Automatically unlock m and sleep until c is signaled
// Then re-acquire m and resume executing
int pthread_cond_wait(pthread_cond_t *c, pthread_mutex_t *m);
// Wake one or all threads waiting on c
int pthread_cond_signal(pthread_cond_t *c);
int pthread_cond_broadcast(pthread_cond_t *c);
```

See also [[PThead Mutex API]]