---
dg-publish: true
---
# Co-Clustering Indices

> [!tldr] Two indices are **co-clustered** if the data pages for the indices are in common
> * Records encoding tuples in the indices are interleaved within the same data pages
> * Useful when (1,N) relationships exist between the records for the two indices

Can speed up joins
Sequential scans of either relation become slower

### Search
Ordered indices allow more general subqueries to be evaluated efficiently
##### Range Queries
Btrees can help evaluating a query with the form
```sql
select * from <table>
where <attribute> >= <constant>
```
* If the search key of a Btree is on `<attribute>`, it can be used to efficiently locate tuples where `<attribute> = <constant>`
* Remaining records that qualify are obtained by scanning the remaining data pages

##### Multi-attribute Search Keys
It is usually possible to create an index on several attributes of the same relation

Assume relation name `PROM/(pnum, lname, fname, dept)`
→ Secondary index now defined as follows
```sql
create view PROF-SECONDARY
as (select lname, fname, rid from PROF-PRIMARY)
materialized as BTREE with search key (lname, fname)
```
* Records are organized first by `lname`
* Tuples with a common surname are organized `fname`

Order in which attributes appear in the search key is important

> [!info] Multi-Attribute Indices
> `PROF-SECONDARY` index is useful for the following queries
> ```sql
> select * from PROF where lname = 'Smith'
> select * from PROF and lname = 'Smith' and fname = 'John'
> ```
> Very useful for these queries
> ```sql
> -- Number of data pages storing secondary index can be less
>select fname from PROF where lname = 'Smith'
> -- No need to go to primary index
> select fname, lname from PROF
> ```
> Unlikely to be useful for
> ```sql
> select * from PROF where fname = 'John'
> -- Need primary index
> ```


