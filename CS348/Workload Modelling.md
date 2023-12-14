---
dg-publish: true
---
# Workload Modelling
## Workload Description
* **Critical queries** and their frequency
* **Critical updates** and their frequency
* **Desired performance goal** for each query or update

#### Query
* Which relations are accessed
* Which attributes are retrieved
* Which attributes occur in selection/join conditions
* How selective are query conditions

#### Update
* The type of update and relations/attributes affected
* Which attributes occur in selection/join conditions
* How selective are query conditions

#### Performance Goals
* Reducing the time needed to compute answers to a query
* Transaction throughput for transactions entailing updates

> [!warning] **Core Issues:** How can a DBA group
> 1. Make queries run faster 
> 	* Data structures, clustering, replication
> 2. Make updates run faster
> 	* Locality of data items
> 3. Minimize congestion due to concurrency


