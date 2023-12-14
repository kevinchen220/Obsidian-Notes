---
dg-publish: true
---
# Aggregation

> [!tldr] Map relationship set R that is aggregated to new table R
> * Tabular representation of aggregation of R = Tabular representation for relationship R
##### Relationship set involving aggregation of R is like an entity set whose primary key is the primary key of the table for R

### Example
![[Pasted image 20231212161539.png]]
**EnrolledIn constraints:**
* `foreign key ( StudentNum ) references Student`
* `foreign key ( CourseNum ) references Course`

**CourseAccount constraints:**
* `foreign key ( UserdId ) references Account`
* `foreign key ( StudentNum, CourseNum ) references EnrolledIn`



