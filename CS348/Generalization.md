# Generalization

> [!tip] Treat generalization of $n$ [[entity sets]] as $n$ [[specialization|specializations]]
> * Additional constraints for coverage or disjointedness

## Example
![[Pasted image 20231212173542.png]]
**Constraints**
* Truck `foreign key ( LicenseNum ) references Vehicle`
* Car `foreign key ( LicenseNum ) references Vehicle`

**Assertion**
* Vehicle license numbers are also truck or car license numbers
* Truck license numbers are disjoint from car license numbers


