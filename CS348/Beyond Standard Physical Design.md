---
dg-publish: true
---
# Beyond Standard Physical Design
### Join Indices
Supports materialized view defined by a conjunctive query on more than one primary index

> [!info] In standard physical design, a secondary index is a materialized view on a primary index

*Join index for the bibliography database*
```sql
create view AUTHOR-BOOK as (
    select author-rid, book-rid
    from AUTHOR-PRIMARY, WROTE-PRIMARY, BOOK-PRIMARY
    where aid = author and publication = pubid )
materialized as heap file
```
### Arbitrary Materialized Views
Supports a materialized view defined by an arbitrary SQL query
