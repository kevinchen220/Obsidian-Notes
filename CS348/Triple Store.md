---
dg-publish: true
---
# Triple Store
```sql
create view TRIPLE as ( <query> )
```
Schema `TRIPLE/(subject, property, object)`
##### ER Diagram Modification
* Turn all entity sets into regular entity sets
* Add an `OID` attribute to be the primary key for each entity set

`<query>` - union of queries `QTi` over each of the other tables `Ti`
* `Ti` schema `Ti/(OID, A1, ..., An)`

```sql
Qti = 
(select OID as subject, 'in' as property, 'Ti' as object from Ti)
    union
(select OID as subject, 'A1' as property, A1 as object from Ti)
    union
    ...
    union
(select OID as subject, 'An' as property, An as object from Ti)  
```

> [!NOTE] 
> * Data in `TRIPLE` replicates data in all other tables
> 	* All queries over a triple store schema have equivalent formulations that only mention TRIPLE
> * A relational schema with single `TRIPLE` table can replicate any relational database
> 	* Never requires revision
> * Replacing `OID` with `URI` roughly obtains a RDF encoding of data
> 	* Resource Description Framework (RDF)
> * Graphical Data Models
> 	* Each column `subject` or `object` as a graph node and each tuple in `TRIPLE` as a labelled graph edge


