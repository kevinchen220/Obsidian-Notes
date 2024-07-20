---
dg-publish: true
---
# BFS
### Initialization
```
array vistied[v] = 0 for all v in V
queue Q = empty
array p[v] = NULL for all v in V
array l[v] = infinity for all v in V
```
### Start
```
ENQUEUE(Q, s)
visited[s] = 1
l[s] = 0
```
### While $Q \neq \emptyset$
```
u = DEQUEUE(Q)
for each neighbor v of u:
	if visited[v] = 0:
		ENQUEUE(Q, v)
		visited[v] = 1
		p[v] = u
		l[v] = l[u] + 1
```

