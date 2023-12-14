---
dg-publish: true
---
# Specialization

> [!tldr] Treat entity set which is a specialization of one or more other [[entity sets]] as a [[weak entity sets|weak entity set]]
> * Empty discriminator set
> * Existence dependent on each of the other entity sets

## Example
![[Pasted image 20231212170725.png]]
**Graduate constraints:**
* `foreign key ( StudentNumber ) references Student`
* `foreign key ( ProfessorName ) references Professor

**Degree constraints:**
* `foreign key ( StudentNumber ) references Graduate`



