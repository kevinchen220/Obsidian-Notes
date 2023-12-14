---
dg-publish: true
---
# Views

> [!tip] Sometimes [[entity sets]] can be mapped to views instead of tables

## [[Specialization]]
An entity set E that is a specialization of one parent entity set and satisfies:
1. Only typing [[Attributes]] declared
2. No foreign key constraints reference E
3. All entity sets that are specializations of E are mapped to views

**Need to add a new two-valued typing attribute `is-E`**
* Combine with E’s existing typing attributes to the parent entity set to enable a view definition for the mapping of E

## [[Generalization]]
Generalization entity set E of two or more child entity sets
* No foreign key constraints that reference E
* All attributes on E are defined on each child entity set to enable a view definition for the mapping of E

![[Pasted image 20231212182428.png]]
```sql
create view Vehicle as (
	( select LicenseNum, MakeAndModel, Price from Truck )
	union
	( select LicenseNum, MakeAndModel, Price from Car )
)
```
