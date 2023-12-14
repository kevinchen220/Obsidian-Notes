---
dg-publish: true
---
# Logical Schema and Query Tuning
## Schema Tuning

> [!NOTE] It may be necessary to make changes to the conceptual database design and tune queries
> **Goals**
> * Avoid expensive operations in query execution
> 	* Joins
> * Retrieving related data in fewer operations
> 
> **Techniques**
> * Choosing an alternative normalization or weaker [[normal form]]
> * [[Co-Clustering Indices|Co-clustering]] relations and denormalization
> * Vertically and horizontally partitioning data and materialized views
> * Avoiding concurrency hot-spots

### Tuning Conceptual Schema
##### Re-Normalization
Consider alternative BCNF decompositions that better fit the queries in the workload
* Speeds up simple updates
	* Less change anomalies
* Speeds up simple queries
	* Smaller tables
* Slows down complex queries
	* More joins
* Slows down complex updates
	* If they involve complex queries

##### Denormalization
Consider merging relational schemata to intentionally increase redundancy
* Redundancy increases update overhead due to change anomalies
* Redundancy decreases query overhead

#### Partitioning

> [!warning] Very large tables can be a source of performance bottlenecks

Splitting a table into multiple for the purpose of reducing I/O cost or lock contention
##### Horizontal Partitioning
* Each partition has all the original columns and a subset of the original rows
* Tuples are assigned to a partition based upon a usually natural criteria
* Often used to separate operational from archival data
##### Vertical Partitioning
* Each partition has a subset of the original columns and all the original rows
* Typically used to separate frequently-used columns from each other or from infrequently-used columns

> [!warning] Changes to the physical or conceptual schemas impacts all queries and updates in the workload

## Tuning Queries

> [!info] Sometimes desirable to target performance of specific queries or applications

 * Sorting is expensive 
	* Avoid unnecessary uses of `ORDER BY`, `DISTINCT`, `GROUP BY` 
* May be necessary to replace subqueries with joins
* May be necessary to replace correlated subqueries with uncorrelated subqueries
* Use vendor-supplied tools to examine generated plans
	* Update and/or create statistics if poor plans are due to poor cost estimation

## Tuning Applications
#### Minimize communication costs
1. Return the fewest columns and rows necessary
2. Update multiple rows with a WHERE clause rather than a cursor

#### Minimize lock contention and hot-spots
1. Delay updates as long as possible
2. Delay operations on hot-spots as long as possible
3. Shorten or split transactions as much as possible
4. Perform insertions/updates/deletions in batches
5. Consider lower isolation levels
