# Cost of Retrieval
$R$ has the signature MARK/(studnum, course, assignnum, mark)

$E$ is the query
$\pi_{\#1, \#4}(\sigma_{\#2=\#7}(\sigma_{\#1=\#6}(\sigma_{\#4>\#5}(MARK \times 90) \times 100) \times PHYS))$
```sql
select studnum, mark from MARK
where course = 'PHYS' and studnum = 100 and mark > 90
```
##### Physical design for MARK
1. Btree primary index on course
	* `MARK-PINDEX/(RID-P, studnum, course, assignnum, mark)`
2. Btree secondary index on studnum
	* `MARK-SINDEX/(RID-S, studnum, RID-P)`

##### Statistical metadata
1. |MARK| = 10000
2. $b$(MARK-PINDEX) = 50
3. distinct(MARK, studnum) = 500 (number of different students)
4. distinct(MARK, course) = 100 (number of different courses)
5. distinct(MARK, mark) = 100 (number of different marks)

##### Strategy 1: Use Primary Index
Query plan
$\pi_{\#2, \#5}(\sigma_{\#2=\#7}(\sigma_{\#5>\#6}(\sigma_{\#3='PHYS'}(MARK-PINDEX) \times 90) \times 100))$
* Assuming uniform distribution of tuples over the course, there are about |MARK| / 100 = 100 tuples with **course = PHYS**
* Searching MARK-PINDEX Btree has a cost of 2
* Retrieving the 100 matching tuples adds a cost of 100/$b$(MARK-INDEX) data blocks
* Total cost is 2 + 100 / 50 = 4 block reads


> [!tip] Selection of $N$ tuples from relation $R$ using a clustered primary key has cost $2 + N/b(R)$

> [!tip] Searching Btree has cost 2
> Whether its for primary or secondary index

##### Strategy 2: Use Secondary Index
Query Plan:
$\pi_{\#5, \#8}(\sigma_{\#6=\#10}(\sigma_{\#8>\#9}((\sigma_{\#2=100}(MARK-SINDEX) \times_{\sigma_{\#1=\#3l}}(MARK-PINDEX))\times 90) \times PHYS))$

> [!info] Nested index join
> $\#3l$ refers to column 3 of the left argument of the nested cross product operator $\times$

* Assuming uniform distribution of tuples over student numbers there will be about |MARK|/500 = 20 
* Searching MARK-SINDEX Btree has a cost of 2
	* Not clustered index so we assume each matching record in Btree is on a separate data block **(Pessimistic)**
	* 20 blocks will need to be read
* Total cost is 22 block reads

> [!tip] Selection of $N$ tuples from relation $R$ using an unclustered secondary index has a cost of 2+$N$

##### Strategy 3: Scan Primary Index
Query Plan:
$\pi_{\#2, \#5}(\sigma_{\#2=\#8}(\sigma_{\#5>\#7}(\sigma_{\#3=\#6}(MARK-PINDEX \times PHYS) \times 90) \times 100))$
* 10000/50 = 200 MARK-INDEX Btree data pages
* Total cost is 200 block reads

> [!tip] Selection of $N$ tuples from relation $R$ by an exhaustive scan of its primary index has a cost of $|R|/b(R)$
